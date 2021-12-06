# rc.local ubuntu 활성화 하기

1. etc 밑에 rc.local 파일 존재 여부 확인
2. 없다면 root 권한으로 create /etc/rc.local

> 기본 파일
```
#! /bin/sh
exit 0
```

3. /etc/rc.local 파일 권한 실행 파일로 변경
```
$ chmod +x /etc/rc.local
```

4. rc-local.service 파일 수정
```
$ sudo vi /lib/systemd/system/rc-local.service

---- 기본 파일 -----
[Unit] 
Description=/etc/rc.local Compatibility 
Documentation=man:systemd-rc-local-generator(8) ConditionFileIsExecutable=/etc/rc.local
After=network.target
 
[Service]
Type=forking 
ExecStart=/etc/rc.local start 
TimeoutSec=0 
RemainAfterExit=yes 
GuessMainPID=no

---- 추가 내용 -----
[Install] 
WantedBy=multi-user.target
```

5. rc.local 활성화 및 실행
```
$ systemctl enable rc-local.service
$ systemctl start rc-local.service
```
