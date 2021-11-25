# ubuntu 20.04 os 재기동시, 특정 sh 실행 하기, rc.local 활성화

### rc.local 이라는 파일 생성
```
$ sudo vi /etc/rc.local // 없을 시, 파일 생성해도 무관
```

### rc.local 파일 내용 작성
```
#! /bin/sh

echo "[$(date +%Y)-$(date +%m)-$(date +%d) $(date +%H):$(date +%M):$(date +%S)] system on restart, mount start, docker start" >> /home/ubuntu/workspace/systemlog/systemlog
sudo systemctl start docker.service
sudo systemctl start docker.socket
sudo mount -t cifs -o username=quickfinderUser,password=quickfinderUser1! //192.168.0.111/quickfinder/webUpload /home/ubuntu/workspace/upload
sudo mount -t cifs -o username=quickfinder,password='tkdydwk!2#4',vers=3.0 //192.168.3.5/service /home/ubuntu/workspace/video/3
echo "[$(date +%Y)-$(date +%m)-$(date +%d) $(date +%H):$(date +%M):$(date +%S)] system on restart, mount end, docker end" >> /home/ubuntu/workspace/systemlog/systemlog

exit 0
```
> 쉘 내용은 현재 시간 로그에 담고 docker service 기동, mount 하는 것이 필요하여 그 내용을 담음

### 파일 실행 권한 주기
```
$ chmod +x /etc/rc.local
```

### rc-local.service file 수정
```
$ vi /lib/systemd/system/rc-local.service
```
> 기존의 내용
```
[Unit]
Description=/etc/rc.local Compatibility
Documentation=man:systemd-rc-local-generator(8)
ConditionFileIsExecutable=/etc/rc.local
After=network.target

[Service]
Type=forking
ExecStart=/etc/rc.local start
TimeoutSec=0
RemainAfterExit=yes
GuessMainPID=no
```
> 추가할 내용
```
[Install]
WantedBy=multi-user.target
```

### service 활성화
```
$ systemctl enable rc-local.service
$ systemctl start rc-local.service
$ systemctl status rc-local.service
```
이러한 과정을 거치면 
ubuntu 재 시작과 동시에 저 sh이 실행된다.
