# ubuntu 22.04

```
$ sudo vi /etc/nginx/nginx.conf
```

> nginx.conf
```
http {

      ...

      log_format combined_realip '$remote_addr - $http_x_forwarded_for - $remote_user [$time_local] '
                                   '"$request" $status $body_bytes_sent '
                                   '"$http_referer" "$http_user_agent"';

      server_tokens off;

      fastcgi_hide_header X-Powered-By;
      fastcgi_hide_header X-Pingback;
      fastcgi_hide_header Link;
      proxy_hide_header X-Powered-By;
      proxy_hide_header X-Pingback;
      proxy_hide_header X-Link;

      ...

}
```

위 설정을 기본으로 가져갔다.

주석해제( server_tokens off; ) 및 코드 추가 ( 나머지 )
