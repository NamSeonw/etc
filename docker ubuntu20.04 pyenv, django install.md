### 

```
$ apt update
$ apt upgrade
$ apt install git curl vim
$ apt-get install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev \
libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python-openssl
$ git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```

환경 변수 추가

```
$ vi ~/.bashrc
export PYENV_ROOT="$HOME/.pyenv
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"

$ source ~/.bashrc
```
