# 20.04 pyenv install

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
만약 ubuntu 20.04 라면
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
if command -v pyenv 1>/dev/null 2>&1; then
  eval "$(pyenv init --path)"
fi

만약 ubuntu 20.04 가 아니라면
eval "$(pyenv init -)"
```

## pyenv 필수 패키지 설치

```
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
xz-utils tk-dev
```

출처 https://nachwon.github.io/pyenv-virtualenv/

export PATH="~/.pyenv/bin:$PATH"
eval "$(pyenv virtualenv-init -)"

# eval "$(pyenv init -)"

eval "$(pyenv init --path)"


```
$ pyenv install 3.7.9
$ pyenv global 3.7.9
```

# 22.04 pyenv install

```
$ sudo apt-get install make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
$ curl https://pyenv.run | bash
$ sudo vi ~/.profile
```

> ~/.profile
```
# ~/.profile: executed by the command interpreter for login shells.
# This file is not read by bash(1), if ~/.bash_profile or ~/.bash_login
# exists.
# see /usr/share/doc/bash/examples/startup-files for examples.
# the files are located in the bash-doc package.

# the default umask is set in /etc/profile; for setting the umask
# for ssh logins, install and configure the libpam-umask package.
#umask 022

# if running bash
if [ -n "$BASH_VERSION" ]; then
    # include .bashrc if it exists
    if [ -f "$HOME/.bashrc" ]; then
        . "$HOME/.bashrc"
    fi
fi

# set PATH so it includes user's private bin if it exists
if [ -d "$HOME/bin" ] ; then
    PATH="$HOME/bin:$PATH"
fi

# set PATH so it includes user's private bin if it exists
if [ -d "$HOME/.local/bin" ] ; then
    PATH="$HOME/.local/bin:$PATH"
fi

export PYENV_ROOT="$HOME/.pyenv"
[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
```

이 부분 추가

export PYENV_ROOT="$HOME/.pyenv"
[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"

```
$ source ~/.profile
$ pyenv install 3.8.5
$ pyenv local 3.8.5
$ cd ~/workspace
$ python -m venv venv
$ . venv/bin/activate
$ cd quickfinder/
$ pip install --upgrade pip
$ sudo apt-get install libmysqlclient-dev
$ pip install -r requirements.txt 
```
