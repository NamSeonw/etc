# ubuntu 16.04 django nginx gunicorn.md 구성

>디렉토리 구성
```
home
-vagrant
 -workspace
  -Kice_CMS (확실치는 않음)
  -ai_api (내가 한 프로젝트)
```

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
로컬주소에 8000 번으로 서버를 
