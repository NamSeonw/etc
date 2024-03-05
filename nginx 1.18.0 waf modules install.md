# nginx 1.18.0 waf modules install

sudo su -> 처음에 su 권한을 주고 시작을 하던가 모든 명령어 앞에 sudo를 붙이던가 둘 중 택1 해야함
이유는 모든 작업이 /usr/local/src/.... 밑의 경로에서 진행되기 때문에 /usr/local/src/ 의 기본소유자는 root이고 
현재 작업 계정은 ubuntu이므로 쓰기 권한이 없다.

나는 모든 명령어 앞에 sudo를 붙여서 진행

> nginx install & git install
> 다음 명령어 진행, nginx와 git이 설치되어있을시, 수행안해도 됌
```
$ sudo apt update
$ apt install nginx=1.18.0-0ubuntu1.4
$ sudo apt install nginx=1.18.0-0ubuntu1.4
$ nginx -v
$ sudo apt install git -y
```

> nginx waf module install 
```
$ sudo git clone --depth 1 -b v3/master --single-branch https://github.com/SpiderLabs/ModSecurity /usr/local/src/ModSecurity/
$ cd /usr/local/src/ModSecurity/
$ sudo apt install gcc make build-essential autoconf automake libtool libcurl4-openssl-dev liblua5.3-dev libfuzzy-dev ssdeep gettext pkg-config libpcre3 libpcre3-dev libxml2 libxml2-dev libcurl4 libgeoip-dev libyajl-dev doxygen -y
$ sudo git submodule init
$ sudo git config --global --add safe.directory /usr/local/src/ModSecurity
$ sudo git submodule update
$ sudo ./build.sh
$ sudo ./configure
$ sudo make
$ sudo make install
$ sudo git clone --depth 1 https://github.com/SpiderLabs/ModSecurity-nginx.git /usr/local/src/ModSecurity-nginx/
$ cd /usr/local/src/
$ sudo wget http://nginx.org/download/nginx-1.18.0.tar.gz
$ sudo tar -xvzf nginx-1.18.0.tar.gz 
$ cd nginx-1.18.0
$ sudo cp /etc/apt/sources.list /etc/apt/sources.list~
$ sudo sed -Ei 's/^# deb-src /deb-src /' /etc/apt/sources.list
$ sudo apt-get update
$ sudo apt build-dep nginx && sudo apt install uuid-dev -y
$ sudo ./configure --with-compat --add-dynamic-module=/usr/local/src/ModSecurity-nginx
$ sudo make modules
$ sudo cp objs/ngx_http_modsecurity_module.so /usr/share/nginx/modules/
$ sudo vi /etc/nginx/nginx.conf
```

> waf conf change
> nginx.conf 에 추가
```
change

-- In the file, add this line on the top:-- 

load_module modules/ngx_http_modsecurity_module.so;

-- Under the HTTP {} section, add the following code lines: --

modsecurity on;
modsecurity_rules_file /etc/nginx/modsec/modsec-config.conf;
```

> nginx conf change
> /etc/nginx/nginx.conf
```
user www-data;
worker_processes auto;
pid /run/nginx.pid;
include /etc/nginx/modules-enabled/*.conf;
load_module modules/ngx_http_modsecurity_module.so;

events {
	worker_connections 768;
	# multi_accept on;
}

http {

	##
	# Basic Settings
	##

	modsecurity on;
	modsecurity_rules_file /etc/nginx/modsec/modsec-config.conf;
	sendfile on;
	tcp_nopush on;
	tcp_nodelay on;
	keepalive_timeout 65;
	types_hash_max_size 2048;
	# server_tokens off;

	# server_names_hash_bucket_size 64;
	# server_name_in_redirect off;

	include /etc/nginx/mime.types;
	default_type application/octet-stream;

	##
	# SSL Settings
	##

	ssl_protocols TLSv1 TLSv1.1 TLSv1.2 TLSv1.3; # Dropping SSLv3, ref: POODLE
	ssl_prefer_server_ciphers on;

	##
	# Logging Settings
	##

	access_log /var/log/nginx/access.log;
	error_log /var/log/nginx/error.log;

	##
	# Gzip Settings
	##

	gzip on;

	# gzip_vary on;
	# gzip_proxied any;
	# gzip_comp_level 6;
	# gzip_buffers 16 8k;
	# gzip_http_version 1.1;
	# gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;

	##
	# Virtual Host Configs
	##

	include /etc/nginx/conf.d/*.conf;
	include /etc/nginx/sites-enabled/*;
}


#mail {
#	# See sample authentication script at:
#	# http://wiki.nginx.org/ImapAuthenticateWithApachePhpScript
# 
#	# auth_http localhost/auth.php;
#	# pop3_capabilities "TOP" "USER";
#	# imap_capabilities "IMAP4rev1" "UIDPLUS";
# 
#	server {
#		listen     localhost:110;
#		protocol   pop3;
#		proxy      on;
#	}
# 
#	server {
#		listen     localhost:143;
#		protocol   imap;
#		proxy      on;
#	}
#}
```

```
$ sudo mkdir /etc/nginx/modsec/
$ sudo cp /usr/local/src/ModSecurity/modsecurity.conf-recommended /etc/nginx/modsec/modsecurity.conf
$ sudo vi /etc/nginx/modsec/modsecurity.conf
```

> waf 관련 conf change
> modsecurity.conf 파일 변경
```
SecRuleEngine On
SecAuditLogParts ABCDEFHJKZ
```

> /etc/nginx/modsec/modsecurity.conf
```
# -- Rule engine initialization ----------------------------------------------

# Enable ModSecurity, attaching it to every transaction. Use detection
# only to start with, because that minimises the chances of post-installation
# disruption.
#
SecRuleEngine on


# -- Request body handling ---------------------------------------------------

# Allow ModSecurity to access request bodies. If you don't, ModSecurity
# won't be able to see any POST parameters, which opens a large security
# hole for attackers to exploit.
#
SecRequestBodyAccess On


# Enable XML request body parser.
# Initiate XML Processor in case of xml content-type
#
SecRule REQUEST_HEADERS:Content-Type "^(?:application(?:/soap\+|/)|text/)xml" \
     "id:'200000',phase:1,t:none,t:lowercase,pass,nolog,ctl:requestBodyProcessor=XML"

# Enable JSON request body parser.
# Initiate JSON Processor in case of JSON content-type; change accordingly
# if your application does not use 'application/json'
#
SecRule REQUEST_HEADERS:Content-Type "^application/json" \
     "id:'200001',phase:1,t:none,t:lowercase,pass,nolog,ctl:requestBodyProcessor=JSON"

# Sample rule to enable JSON request body parser for more subtypes.
# Uncomment or adapt this rule if you want to engage the JSON
# Processor for "+json" subtypes
#
#SecRule REQUEST_HEADERS:Content-Type "^application/[a-z0-9.-]+[+]json" \
#     "id:'200006',phase:1,t:none,t:lowercase,pass,nolog,ctl:requestBodyProcessor=JSON"

# Maximum request body size we will accept for buffering. If you support
# file uploads then the value given on the first line has to be as large
# as the largest file you are willing to accept. The second value refers
# to the size of data, with files excluded. You want to keep that value as
# low as practical.
#
SecRequestBodyLimit 13107200
SecRequestBodyNoFilesLimit 131072

# What to do if the request body size is above our configured limit.
# Keep in mind that this setting will automatically be set to ProcessPartial
# when SecRuleEngine is set to DetectionOnly mode in order to minimize
# disruptions when initially deploying ModSecurity.
#
SecRequestBodyLimitAction Reject

# Maximum parsing depth allowed for JSON objects. You want to keep this
# value as low as practical.
#
SecRequestBodyJsonDepthLimit 512

# Maximum number of args allowed per request. You want to keep this
# value as low as practical. The value should match that in rule 200007.
SecArgumentsLimit 1000

# If SecArgumentsLimit has been set, you probably want to reject any
# request body that has only been partly parsed. The value used in this
# rule should match what was used with SecArgumentsLimit
SecRule &ARGS "@ge 1000" \
"id:'200007', phase:2,t:none,log,deny,status:400,msg:'Failed to fully parse request body due to large argument count',severity:2"

# Verify that we've correctly processed the request body.
# As a rule of thumb, when failing to process a request body
# you should reject the request (when deployed in blocking mode)
# or log a high-severity alert (when deployed in detection-only mode).
#
SecRule REQBODY_ERROR "!@eq 0" \
"id:'200002', phase:2,t:none,log,deny,status:400,msg:'Failed to parse request body.',logdata:'%{reqbody_error_msg}',severity:2"

# By default be strict with what we accept in the multipart/form-data
# request body. If the rule below proves to be too strict for your
# environment consider changing it to detection-only. You are encouraged
# _not_ to remove it altogether.
#
SecRule MULTIPART_STRICT_ERROR "!@eq 0" \
"id:'200003',phase:2,t:none,log,deny,status:400, \
msg:'Multipart request body failed strict validation: \
PE %{REQBODY_PROCESSOR_ERROR}, \
BQ %{MULTIPART_BOUNDARY_QUOTED}, \
BW %{MULTIPART_BOUNDARY_WHITESPACE}, \
DB %{MULTIPART_DATA_BEFORE}, \
DA %{MULTIPART_DATA_AFTER}, \
HF %{MULTIPART_HEADER_FOLDING}, \
LF %{MULTIPART_LF_LINE}, \
SM %{MULTIPART_MISSING_SEMICOLON}, \
IQ %{MULTIPART_INVALID_QUOTING}, \
IP %{MULTIPART_INVALID_PART}, \
IH %{MULTIPART_INVALID_HEADER_FOLDING}, \
FL %{MULTIPART_FILE_LIMIT_EXCEEDED}'"

# Did we see anything that might be a boundary?
#
# Here is a short description about the ModSecurity Multipart parser: the
# parser returns with value 0, if all "boundary-like" line matches with
# the boundary string which given in MIME header. In any other cases it returns
# with different value, eg. 1 or 2.
#
# The RFC 1341 descript the multipart content-type and its syntax must contains
# only three mandatory lines (above the content):
# * Content-Type: multipart/mixed; boundary=BOUNDARY_STRING
# * --BOUNDARY_STRING
# * --BOUNDARY_STRING--
#
# First line indicates, that this is a multipart content, second shows that
# here starts a part of the multipart content, third shows the end of content.
#
# If there are any other lines, which starts with "--", then it should be
# another boundary id - or not.
#
# After 3.0.3, there are two kinds of types of boundary errors: strict and permissive.
#
# If multipart content contains the three necessary lines with correct order, but
# there are one or more lines with "--", then parser returns with value 2 (non-zero).
#
# If some of the necessary lines (usually the start or end) misses, or the order
# is wrong, then parser returns with value 1 (also a non-zero).
#
# You can choose, which one is what you need. The example below contains the
# 'strict' mode, which means if there are any lines with start of "--", then
# ModSecurity blocked the content. But the next, commented example contains
# the 'permissive' mode, then you check only if the necessary lines exists in
# correct order. Whit this, you can enable to upload PEM files (eg "----BEGIN.."),
# or other text files, which contains eg. HTTP headers.
#
# The difference is only the operator - in strict mode (first) the content blocked
# in case of any non-zero value. In permissive mode (second, commented) the
# content blocked only if the value is explicit 1. If it 0 or 2, the content will
# allowed.
#

#
# See #1747 and #1924 for further information on the possible values for
# MULTIPART_UNMATCHED_BOUNDARY.
#
SecRule MULTIPART_UNMATCHED_BOUNDARY "@eq 1" \
    "id:'200004',phase:2,t:none,log,deny,msg:'Multipart parser detected a possible unmatched boundary.'"


# PCRE Tuning
# We want to avoid a potential RegEx DoS condition
#
SecPcreMatchLimit 1000
SecPcreMatchLimitRecursion 1000

# Some internal errors will set flags in TX and we will need to look for these.
# All of these are prefixed with "MSC_".  The following flags currently exist:
#
# MSC_PCRE_LIMITS_EXCEEDED: PCRE match limits were exceeded.
#
SecRule TX:/^MSC_/ "!@streq 0" \
        "id:'200005',phase:2,t:none,deny,msg:'ModSecurity internal error flagged: %{MATCHED_VAR_NAME}'"


# -- Response body handling --------------------------------------------------

# Allow ModSecurity to access response bodies. 
# You should have this directive enabled in order to identify errors
# and data leakage issues.
# 
# Do keep in mind that enabling this directive does increases both
# memory consumption and response latency.
#
SecResponseBodyAccess On

# Which response MIME types do you want to inspect? You should adjust the
# configuration below to catch documents but avoid static files
# (e.g., images and archives).
#
SecResponseBodyMimeType text/plain text/html text/xml

# Buffer response bodies of up to 512 KB in length.
SecResponseBodyLimit 524288

# What happens when we encounter a response body larger than the configured
# limit? By default, we process what we have and let the rest through.
# That's somewhat less secure, but does not break any legitimate pages.
#
SecResponseBodyLimitAction ProcessPartial


# -- Filesystem configuration ------------------------------------------------

# The location where ModSecurity stores temporary files (for example, when
# it needs to handle a file upload that is larger than the configured limit).
# 
# This default setting is chosen due to all systems have /tmp available however, 
# this is less than ideal. It is recommended that you specify a location that's private.
#
SecTmpDir /tmp/

# The location where ModSecurity will keep its persistent data.  This default setting 
# is chosen due to all systems have /tmp available however, it
# too should be updated to a place that other users can't access.
#
SecDataDir /tmp/


# -- File uploads handling configuration -------------------------------------

# The location where ModSecurity stores intercepted uploaded files. This
# location must be private to ModSecurity. You don't want other users on
# the server to access the files, do you?
#
#SecUploadDir /opt/modsecurity/var/upload/

# By default, only keep the files that were determined to be unusual
# in some way (by an external inspection script). For this to work you
# will also need at least one file inspection rule.
#
#SecUploadKeepFiles RelevantOnly

# Uploaded files are by default created with permissions that do not allow
# any other user to access them. You may need to relax that if you want to
# interface ModSecurity to an external program (e.g., an anti-virus).
#
#SecUploadFileMode 0600


# -- Debug log configuration -------------------------------------------------

# The default debug log configuration is to duplicate the error, warning
# and notice messages from the error log.
#
#SecDebugLog /opt/modsecurity/var/log/debug.log
#SecDebugLogLevel 3


# -- Audit log configuration -------------------------------------------------

# Log the transactions that are marked by a rule, as well as those that
# trigger a server error (determined by a 5xx or 4xx, excluding 404,  
# level response status codes).
#
SecAuditEngine RelevantOnly
SecAuditLogRelevantStatus "^(?:5|4(?!04))"

# Log everything we know about a transaction.
SecAuditLogParts ABCDEFHJKZ

# Use a single file for logging. This is much easier to look at, but
# assumes that you will use the audit log only ocassionally.
#
SecAuditLogType Serial
SecAuditLog /var/log/modsec_audit.log

# Specify the path for concurrent audit logging.
#SecAuditLogStorageDir /opt/modsecurity/var/audit/


# -- Miscellaneous -----------------------------------------------------------

# Use the most commonly used application/x-www-form-urlencoded parameter
# separator. There's probably only one application somewhere that uses
# something else so don't expect to change this value.
#
SecArgumentSeparator &

# Settle on version 0 (zero) cookies, as that is what most applications
# use. Using an incorrect cookie version may open your installation to
# evasion attacks (against the rules that examine named cookies).
#
SecCookieFormat 0

# Specify your Unicode Code Point.
# This mapping is used by the t:urlDecodeUni transformation function
# to properly map encoded data to your language. Properly setting
# these directives helps to reduce false positives and negatives.
#
SecUnicodeMapFile unicode.mapping 20127

# Improve the quality of ModSecurity by sharing information about your
# current ModSecurity version and dependencies versions.
# The following information will be shared: ModSecurity version,
# Web Server version, APR version, PCRE version, Lua version, Libxml2
# version, Anonymous unique id for host.
SecStatusEngine On
```

```
$ sudo git clone https://github.com/coreruleset/coreruleset /usr/local/modsecurity-crs
$ sudo mv /usr/local/modsecurity-crs/crs-setup.conf.example /usr/local/modsecurity-crs/crs-setup.conf
$ sudo mv /usr/local/modsecurity-crs/rules/REQUEST-900-EXCLUSION-RULES-BEFORE-CRS.conf.example /usr/local/modsecurity-crs/rules/REQUEST-900-EXCLUSION-RULES-BEFORE-CRS.conf
$ sudo mkdir -p /etc/nginx/modsec
$ sudo vi /etc/nginx/modsec/modsec-config.conf
$ sudo service nginx restart
```

### injection Test
```
?Username='%20or%20'1'='1 & Password='%20or%20'1'='1
```

> nginx_log
```
2023/12/05 16:28:14 [error] 2924930#2924930: *182631 [client 192.168.0.42] ModSecurity: Access denied with code 403 (phase 2). Matched "Operator `Ge' with parameter `5' against variable `TX:BLOCKING_INBOUND_ANOMALY_SCORE' (Value: `5' ) [file "/usr/local/modsecurity-crs/rules/REQUEST-949-BLOCKING-EVALUATION.conf"] [line "176"] [id "949110"] [rev ""] [msg "Inbound Anomaly Score Exceeded (Total Score: 5)"] [data ""] [severity "0"] [ver "OWASP_CRS/4.0.0-rc2"] [maturity "0"] [accuracy "0"] [tag "anomaly-evaluation"] [hostname "192.168.0.94"] [uri "/static/images/favicon.png"] [unique_id "170176129483.253025"] [ref ""], client: 192.168.0.42, server: quickfinder.co.kr, request: "GET /static/images/favicon.png HTTP/1.1", host: "quickfinder.co.kr", referrer: "https://quickfinder.co.kr/shop/invoice_reg/?Username=%27%20or%20%271%27=%271%20&%20Password=%27%20or%20%271%27=%271"
2023/12/05 16:28:14 [error] 2924930#2924930: *182631 [client 192.168.0.42] ModSecurity: Access denied with code 403 (phase 2). Matched "Operator `Ge' with parameter `5' against variable `TX:BLOCKING_INBOUND_ANOMALY_SCORE' (Value: `5' ) [file "/usr/local/modsecurity-crs/rules/REQUEST-949-BLOCKING-EVALUATION.conf"] [line "176"] [id "949110"] [rev ""] [msg "Inbound Anomaly Score Exceeded (Total Score: 5)"] [data ""] [severity "0"] [ver "OWASP_CRS/4.0.0-rc2"] [maturity "0"] [accuracy "0"] [tag "anomaly-evaluation"] [hostname "192.168.0.94"] [uri "/static/images/favicon.png"] [unique_id "17017612940.527480"] [ref ""], client: 192.168.0.42, server: quickfinder.co.kr, request: "GET /static/images/favicon.png HTTP/1.1", host: "quickfinder.co.kr", referrer: "https://quickfinder.co.kr/shop/invoice_reg/?Username=%27%20or%20%271%27=%271%20&%20Password=%27%20or%20%271%27=%271"
```
