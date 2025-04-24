
```
server {
    #if ($host = kiccs.ssu.ac.kr) {
    #    return 301 https://$host$request_uri;
    #} # managed by Certbot

    #location = /.well-known/pki-validation/AD9474C006185A2D8CF8D1C65A014AD2.txt {
#           default_type text/plain;
#           alias /home/ubuntu/workspace/AD9474C006185A2D8CF8D1C65A014AD2.txt;
 #   }

    listen 80;
    server_name kiccs.ssu.ac.kr;
    # return 404; # managed by Certbot

    location = /.well-known/pki-validation/AD9474C006185A2D8CF8D1C65A014AD2.txt {
          alias /var/www/html/AD9474C006185A2D8CF8D1C65A014AD2.txt;
          default_type text/plain;
    }


}
```

만약 파일을
```
-rw-r--r--@ 1 nsw  staff   5.5K  6 27  2022 Chain_RootCA_Bundle.crt                CA 체인 
-rw-r--r--@ 1 nsw  staff   1.0K  4 24 10:15 kiccs.ssu.ac.kr.csr                    csr은 인증서 발급을 위한 "요청 파일" 이걸 바탕으로 제출을 하면 crt인증서를 받을수 있음
-rw-r--r--@ 1 nsw  staff   1.8K  4 24 10:15 kiccs.ssu.ac.kr.key                    개인 Key
-rw-r--r--@ 1 nsw  staff   2.1K  4 24 10:15 kiccs.ssu.ac.kr.pem                    서버 인증서
-rw-r--r--@ 1 nsw  staff   1.7K  4 24 10:15 kiccs.ssu.ac.kr_nopass.key             인증이 필요없는 개인 Key
```
와 같이 받았을때

```
$ cat kiccs.ssu.ac.kr.pem Chain_RootCA_Bundle.crt > kiccs.ssu.ac.kr.fullchain.pem
```

서버 인증서 + CA 체인을 하여 저 파일을 이용해서 설정

```
ssl_certificate     /etc/ssl/ikcc/kiccs.ssu.ac.kr.fullchain.pem;
ssl_certificate_key /etc/ssl/ikcc/kiccs.ssu.ac.kr_nopass.key;
```
