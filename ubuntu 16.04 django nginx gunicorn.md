# ubuntu 16.04 django nginx gunicorn.md 구성

### 디렉토리 구성
```
home
-vagrant
 -workspace
  -Kice_CMS (확실치는 않음)
  -ai_api (내가 한 프로젝트)
```

### 정적 파일 모으고 서버 구동
```
$ cd ~/workspace/ai_api
$ . venv/bin/activate
$ pip install Django gunicorn (Django 와 gunicorn) 설치

-------------------------------
정적 파일이 있을시에
setting.py 에
>STATIC_ROOT = os.path.join(BASE_DIR, 'static/')

$ ./manage.py makemigrations
$ ./manage.py migrate
$ ./manage.py collectstatic
-------------------------------
$ ./manage.py runserver 0.0.0.0:8000
```

> 로컬주소에 8000 번으로 서버를 구동 시켰으니 접속을 해보며 테스트 진행 잘된다면 다음단계 진행

### gunicorn으로 서버 구동 

```
$ gunicorn --bind 0.0.0.0:8000 conf.wsgi:application
```

> gunicorn으로 서버구동 
> 똑같이 접속 하여 테스트 진행 올바르게 동작한다면

```
$ deativate
```

### 서비스 등록 스크립트 생성

/etc/systemd/system/gunicorn.service file 생성 없을 시,

```
[Unit]
Description=gunicorn daemon
After=network.target

[Service]
User=vagrant
Group=vagrant
# 이 두가지는 파일의 권한에 따라 유동적으로 변경

WorkingDirectory=/home/vagrant/workspace/ai_api
ExecStart=/home/vagrant/workspace/ai_api/venv/bin/gunicorn \
        --workers 3 \
        --bind unix:/home/vagrant/workspace/ai_api/gunicorn.sock \
        ai_api.wsgi:application
# 위 사항들도 그 프로젝트 환경에 맞게 구성해 준다.

[Install]
WantedBy=multi-user.target
```

### gunicorn 서비스 등록

```
$ sudo systemctl start gunicorn
$ sudo systemctl enable gunicorn
```
> 첫번째는 아까 등록한 스크립트를 실행 시켜주는 명령어
> 두번째는 서버가 죽었다가 되살아날때 자동으로 서비스를 실행시켜주는 명령어

```
$ systemctl status gunicorn
```
> gunicorn 구동 확인


## nginx
### 사이트 설정 추가

/etc/nginx/sites-available/ai_api 파일 생성

```
server {
        listen 80; # 포트 설정
        server_name 128.199.161.10; # 서버 이름

        location = /favicon.ico { access_log off; log_not_found off; }

        location /static/ {
                root /home/vagrant/workspace/ai_api;
        }

        location / {
                include proxy_params;
                proxy_pass http://unix:/home/vagrant/workspace/ai_api/gunicorn.sock; # sock file 위치
        }
}
```

### 사이트 추가

```
$ sudo ln -s /etc/nginx/sites-available/django_test /etc/nginx/sites-enabled
```

### nginx 설정 문법 검사 및 재기동

```
$ sudo nginx -t
$ sudo systemctl restart nginx
```
