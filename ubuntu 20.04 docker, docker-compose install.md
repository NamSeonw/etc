## ubuntu 20.04 docker / docker-compose install 

1.  docker install
```
$ sudo apt update -y && sudo apt upgrade -y  
$ sudo apt-get install apt-transport-https ca-certificates curl    gnupg-agent software-properties-common  
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository \
"deb [arch=amd64] https://download.docker.com/linux/ubuntu \
bionic \
stable"
$ sudo apt-get update && sudo apt-get install docker-ce docker-ce-cli containerd.io  
$ docker -v  
$ sudo systemctl enable docker && sudo service docker start  
$ sudo service docker status
$ sudo usermod -a -G docker $USERs
```

2. docker-compose install
 > version은 그에 맞게 설정
```
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose  
$ sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose 
$ docker-compose -version
```
