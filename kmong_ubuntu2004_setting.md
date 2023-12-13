
# AWS 기준 작업시작

key 접속 시, 

![image](https://github.com/NamSeonw/etc/assets/54805517/29bda9a0-72f9-4d74-a4ac-693626da2728)

뜨면

chmod 400 으로 키 권한 변경

 
> nginx install

```bash 
$ sudo apt update
$ sudo apt install nginx
```

> 1. workspace에 프로젝트 clone
> 2. pyenv install
> 3. gunicorn 설치 및 gunicorn 셋팅

1. workspace에 프로젝트 clone
```bash
$ cd ~
$ mkdir workspace
$ git clone 본인 프로젝트
$ git checkout ( branch_nm )
```

2. pyenv install
```bash
$ curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash
$ vi ~/.bashrc
```

> ~/.bashrc
```
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
if command -v pyenv 1>/dev/null 2>&1; then
  eval "$(pyenv init --path)"
fi
```
추가

```bash
$ sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
xz-utils tk-dev
$ sudo apt-get install liblzma-dev
$ source ~/.bashrc
$ pyenv install ( python version )
$ pyenv versions
$ pyenv local ( python version )
$ python -> version check
$ cd ~/workspace
$ python -m venv venv
$ . venv/bin/activate
$ pip install --upgrade pip
$ sudo apt-get install python-dev libmysqlclient-dev --> mysql 사용시
$ pip install -r requirement.txt
$ python manage.py runserver 0:8000
```

### 정적 파일 모으고 서버 구동
```
$ cd ~/workspace/( 프로젝트 )
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
$ gunicorn --bind 0.0.0.0:8000 (settings.py 디렉토리).wsgi:application
```

> gunicorn으로 서버구동 
> 똑같이 접속 하여 테스트 진행 올바르게 동작한다면

### 서비스 등록 스크립트 생성

/etc/systemd/system/gunicorn.service file 생성 없을 시,

```
[Unit]
Description=gunicorn daemon
After=network.target

[Service]
User=ubuntu
Group=ubuntu
# 이 두가지는 파일의 권한에 따라 유동적으로 변경

WorkingDirectory=/home/ubuntu/workspace/(프로젝트)
ExecStart=/home/ubuntu/workspace/venv/bin/gunicorn \
        --workers 3 \
        --bind 0.0.0.0:8000 \
        (settings.py 디렉토리).wsgi:application
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
        server_name localhost; # 서버 이름

        location = /favicon.ico { access_log off; log_not_found off; }

        location /static/ {
                root /home/ubuntu/workspace/(프로젝트 명);
        }

        location / {
                proxy_pass http://localhost:8000; # sock file 위치
        }
}
```

### 사이트 추가

```
$ sudo ln -s /etc/nginx/sites-available/( nginx conf ) /etc/nginx/sites-enabled
```

### nginx 설정 문법 검사 및 재기동

```
$ sudo nginx -t
$ sudo systemctl restart nginx
```





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
