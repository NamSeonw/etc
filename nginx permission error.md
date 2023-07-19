# Nginx permission error

서버 작업 중 

nginx static file에 대한 permission error 가 발생하였다.

해당 static file에 권한을 다 줘보았지만 효과는 없었다.

### 다시 nginx 설정 파일
```
server {
#    listen 80 default_server;
    listen 443 ;
#    listen [::]:80 default_server;
#    server_name 127.0.0.1;
    server_name fa.kotech.co.kr;

    ssl on;
    ssl_certificate /etc/ssl/certificate.crt;
    ssl_certificate_key /etc/ssl/private.key;

    location / {
        proxy_pass http://127.0.0.1:8000;

        proxy_connect_timeout   3600;
        proxy_send_timeout      3600;
        proxy_read_timeout      3600;
        send_timeout            3600;

        proxy_buffer_size          128k;
        proxy_buffers              4 256k;
        proxy_busy_buffers_size    256k;
    }

        location /DataServer/ {
                proxy_pass http://127.0.0.1:8282;
        }

        location /ReportingServer/ {
                proxy_pass http://127.0.0.1:8283;
        }

    location /ksign/ {
        proxy_pass http://127.0.0.1:8080;
    }

    location /kcase {
        alias /usr/local/tomcat8/webapps/epki/ksign/kcase;
        #alias /tmp/;
    }

    location /static/ {
        alias /home/vagrant/workspace/kice/home/static/;
    }

}

```

저기서 다른 location들은 정상 작동하였지만 static만 permission 발생

검색 해보니

![image](https://github.com/NamSeonw/etc/assets/54805517/2d9d37c6-4da8-456e-b2b5-e69945957e29)
위 사진 처럼 

drwxrwxr-x. vagrant vagrant uncinfined_u:object_r:user_home_t:s0 에서 user_home_t 부분이 nginx가 읽으려면 httpd_sys_content_t 되어 있어야 한다는것

그래서

```
$ sudo chcon -R -t httpd_sys_content_t .
```

로 명령어 실행 후 정상작동
