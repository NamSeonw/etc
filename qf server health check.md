
# Quickfinder Server Health Check

> 어느 곳 ( 아직 정해지지 않았음 ) 에서 각 서버 ( 220, 93, 94 ) 에 요청을 한다.

> 각 서버에 아래와 같은 서비스들을 체크한다.

```
- 220 
nginx            80
web service      8000
db service       43309

- 93
nginx 80
web service 8000

- 94
nginx 80
web service 8000
```

## 시나리오

원래는 220, 93, 94에서 서로 간의 health check를 하려고 했으나<br> 같은 구조의 웹 서비스 이기에 220번의 데이터베이스가 죽으면
웹서비스도 같이 죽는 문제가 있어 문자 발송이 불가함<br>
그래서 새로운 서비스를 올릴지 quickfinder 프로젝트에 추가할지 ( 개발서버에서 하면 같은 데이터베이스가 아니기때문에 괜찮음 ) 고민 중

220 ( 제일 중요 )

1. db service 체크
    * 체크 순간에 디비에 연결해 확인 
    * 문제 발생시, 문자 발송 및 데이터 베이스에 기록
       
2. nginx 체크
    * python code로 requests module을 사용하여 status가 200인지 체크한다.
    * nginx 요청에 헬스체크 url를 프록시( django 서비스에 영향이 가지않게 nginx에서 처리하는 )하도록 설정한다.
    * 문제 발생시, 문자 발송 및 데이터 베이스에 기록
        
4. web service 체크
    * python code로 requests module을 사용하여 status가 200인지 체크한다.
    * 웹 서비스 되고 있는 포트로 다이렉트 요청 ( 80 port로 요청해도되나 nginx 포트가 80번이라 다이렉트로 요청 )
    * 문제 발생시, 문자 발송 및 데이터 베이스에 기록
        
93, 94 번은 220번에서 db service 체크를 제외한 두 가지 ( nginx, web service ) 체크
