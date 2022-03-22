
#### 아래 명령어로 추천 drive 검색
```
$ sudo ubuntu-drivers devices
```

#### 에러시 실행
```
$ sudo apt install -y ubuntu-drivers-common
```

```
$ add-apt-repository ppa:graphics-drivers/ppa
$ sudo apt-cache search nvidia | grep nvidia-driver
$ sudo apt-get install [드라이버 이름]
```
