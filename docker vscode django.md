# docker, django 구성 부터 ~ vscode로 docker 환경 코드 사용하기 

> 나의 로컬 컴퓨터에서 시작한다.

### local 에 docker contianer 생성 후 , container접속 까지
```
$ docker ps           --> docker 프로세스 (실행중인 프로그램 체크)
$ docker images       --> docker images (docker image 확인)
$ docker run -it --name "qf" ubuntu:20.04   --> docker container을 만드는데 container 이름은 qf 이미지는 ubuntu20.04 로 한다.
docker shell $ exit
```
> 이때 명령어가 컨테이너 쉘로 들어가는 명령어 이다.
> docker 쉘로 들어간 후 exit 명령어를 쳐 나온다.
> 이렇게 했을 경우 docker ps 즉 docker process에는 잡히지 않게 된다. (현재 실행중이지 않기 때문에)

```
$ docker ps -a
```

![image](https://user-images.githubusercontent.com/54805517/120100303-11e09080-c17b-11eb-82c8-7ec0c88c19b3.png)
> 위의 명령으로 쳐 실행중이지 않은 container을 리스트로 보면 사진과 같이 방금 종료한 container는 남게 되어있다.

```
$ docker start qf
$ docker ps
$ docker exec -it a4 bash
```

![image](https://user-images.githubusercontent.com/54805517/120100481-f45ff680-c17b-11eb-843d-46904af936b9.png)

> container 이름이 qf인 container 실행
> 실행중인 container확인
> docker container id 가 a4로 시작하는 container 안으로 접속

### docker container 안에 작업 환경 구성

```
$ cd ~
$ mkdir workspace
$ cd workspace/
$ apt update
$ apt install python3
$ apt install python3-venv
$ python3
$ python3 -m venv venv
$ . venv/bin/activate
$ pip install django==2.2
$ apt install git
```
> 위에서 부터 설명
> home dir로 이동 
> workspace dir 생성
> apt package관리자 update
> python3, python3-vevn 설치
> python3 설치 확인
> venv 가상환경 모듈 생성
> 가상환경 접속
> django 설치
> git 설치

### vs code 에 docker 환경 구성 및 소스 수정 하기위해 구성

command left shift p (vs code extension install)
extension 
remote-containers
docker
> remote-container 로 실행중인 컨테이너에 접속할 수 있다.

![image](https://user-images.githubusercontent.com/54805517/120100843-e7dc9d80-c17d-11eb-88fb-4c477def198b.png)

![image](https://user-images.githubusercontent.com/54805517/120100852-f88d1380-c17d-11eb-9c29-9138688c9833.png)
> source 관리를 원하는 container 에 우 클릭 후
> attach visual studio code click
> 새로운 창이 하나 뜨게 되는데 이것이 docker 환경으로 구성된 창이 뜨게 된 것이다.
> open folder 로 내가 원하는 프로젝트 선택
> 이제 부터는 docker 환경내에 extension을 설치하는것이다
> 설치 해야될 extension 은 python 설치 후
> python: select interpreter

