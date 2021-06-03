# pyenv install

#### pyenv란?
Python 버전 관리 프로그램
프로젝트에 따라 서로 다른 버전의 Python이 필요한 경우 각각의 프로젝트에 다른 버전의 Python 개발 환경을 적용할 수 있게 해주는 프로그램.

## pyenv install

```
$ apt install curl
$ apt install git
$ apt install vim
$ curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash
```

## pyenv 환경변수 설정

```
$ vi ~/.bashrc
```

내용 추가
```
export PATH="~/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

## pyenv 필수 패키지 설치

```
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
xz-utils tk-dev
```

출처 https://nachwon.github.io/pyenv-virtualenv/
