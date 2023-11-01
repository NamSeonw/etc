## mac에서 사용하기 ( 설치과정은 없음 )

```
$ open /usr/local/bin/jmeter
```

실행

![image](https://github.com/NamSeonw/etc/assets/54805517/04e532a5-b3a4-4445-ac82-212ccc5a0354)

Test Plan -> Add -> Threads (Users) -> Thread Group 순으로 클릭

![image](https://github.com/NamSeonw/etc/assets/54805517/ef8b9d89-35c9-4eaf-8d81-21460f01d740)

Thread Group ( 방금 생성 한 ) -> Add -> Sampler -> HTTP Request 클릭

![스크린샷 2023-11-01 오전 9 33 27](https://github.com/NamSeonw/etc/assets/54805517/8ddc8247-7541-4403-a7a6-ce092adb404c)

항목에 맞게 입력

![스크린샷 2023-11-01 오전 9 36 12](https://github.com/NamSeonw/etc/assets/54805517/ac4cc02f-fa3d-4883-981c-80f9a191019e)

Thread Group 에서
Number of Threads (users) 는 가상 사용자를 몇 명으로 설정할지를 의미합니다.
Ramp-up 시간은 쓰레드 수들을 얼마 시간 동안 테스트할지에 대한 설정입니다.
