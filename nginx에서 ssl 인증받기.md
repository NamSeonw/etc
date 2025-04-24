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
