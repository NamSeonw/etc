# python3 install 

```
$ sudo apt update 
```
> apt update 할 시, public key error 발생

스크린샷 2021-05-26 오후 5.21.43![image](https://user-images.githubusercontent.com/54805517/119627164-e5f5a000-be46-11eb-8176-cb367a6b70be.png)

>> 해결방안

```
$ sudo apt-key adv --keyserver hkp://pool.sks-keyservers.net:80 --recv-keys "public key 값 스크린샷에 있는"
ex)
$ sudo apt-key adv --keyserver hkp://pool.sks-keyservers.net:80 --recv-keys FCEF32E745F2C3D5
```

```
$ sudo apt install software-properties-common 
$ sudo add-apt-repository ppa:deadsnakes/ppa 
$ sudo apt update $ sudo apt install python3.7
```
