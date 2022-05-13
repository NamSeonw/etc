
# eosio

github : https://github.com/EOSIO    

doc : https://developers.eos.io/welcome/v2.1/getting-started-guide/local-development-environment/installing-eosio-binaries


### install eosio 
```bash
$ wget https://github.com/eosio/eos/releases/download/v2.1.0/eosio_2.1.0-1-ubuntu-20.04_amd64.deb
```
```bash
$ sudo apt install ./eosio_2.1.0-1-ubuntu-20.04_amd64.deb

Reading package lists... Done
Building dependency tree
Reading state information... Done
Note, selecting 'eosio' instead of './eosio_2.1.0-1-ubuntu-20.04_amd64.deb'
The following additional packages will be installed:
libpq5 libtinfo5
The following NEW packages will be installed:
eosio libpq5 libtinfo5
0 upgraded, 3 newly installed, 0 to remove and 0 not upgraded.
Need to get 199 kB/35.4 MB of archives.
After this operation, 944 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 /home/vagrant/eos/eosio_2.1.0-1-ubuntu-20.04_amd64.deb eosio amd64 2.1.0-1 [35.2 MB]
Get:2 http://archive.ubuntu.com/ubuntu focal/universe amd64 libtinfo5 amd64 6.2-0ubuntu2 [83.0 kB]
Ign:3 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libpq5 amd64 12.7-0ubuntu0.20.04.1
Err:3 http://security.ubuntu.com/ubuntu focal-updates/main amd64 libpq5 amd64 12.7-0ubuntu0.20.04.1
404  Not Found [IP: 91.189.88.152 80]
Fetched 83.0 kB in 2s (35.2 kB/s)
**E:** Failed to fetch http://security.ubuntu.com/ubuntu/pool/main/p/postgresql-12/libpq5_12.7-0ubuntu0.20.04.1_amd64.deb  404  Not Found [IP: 91.189.88.152 80]
**E:** Unable to fetch some archives, maybe run apt-get update or try with --fix-missing?
```
error...

```bash
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install ./eosio_2.1.0-1-ubuntu-20.04_amd64.deb

Reading package lists... Done
Building dependency tree
Reading state information... Done
Note, selecting 'eosio' instead of './eosio_2.1.0-1-ubuntu-20.04_amd64.deb'
The following additional packages will be installed:
libpq5 libtinfo5
The following NEW packages will be installed:
eosio libpq5 libtinfo5
0 upgraded, 3 newly installed, 0 to remove and 0 not upgraded.
Need to get 117 kB/35.4 MB of archives.
After this operation, 944 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 /home/vagrant/eos/eosio_2.1.0-1-ubuntu-20.04_amd64.deb eosio amd64 2.1.0-1 [35.2 MB]
Get:2 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libpq5 amd64 12.9-0ubuntu0.20.04.1 [117 kB]
Fetched 117 kB in 2s (69.1 kB/s)
Selecting previously unselected package libtinfo5:amd64.
(Reading database ... 48396 files and directories currently installed.)
Preparing to unpack .../libtinfo5_6.2-0ubuntu2_amd64.deb ...
Unpacking libtinfo5:amd64 (6.2-0ubuntu2) ...
Selecting previously unselected package libpq5:amd64.
Preparing to unpack .../libpq5_12.9-0ubuntu0.20.04.1_amd64.deb ...
Unpacking libpq5:amd64 (12.9-0ubuntu0.20.04.1) ...
Selecting previously unselected package eosio.
Preparing to unpack .../eosio_2.1.0-1-ubuntu-20.04_amd64.deb ...
Unpacking eosio (2.1.0-1) ...
Setting up libpq5:amd64 (12.9-0ubuntu0.20.04.1) ...
Setting up libtinfo5:amd64 (6.2-0ubuntu2) ...
Setting up eosio (2.1.0-1) ...
Processing triggers for libc-bin (2.31-0ubuntu9.2) ...
```

### install eosio.cdt

cdt = Contract Development Toolkit

```bash
$ wget https://github.com/eosio/eosio.cdt/releases/download/v1.8.0/eosio.cdt_1.8.0-1-ubuntu-18.04_amd64.deb

$ sudo apt install ./eosio.cdt_1.8.0-1-ubuntu-18.04_amd64.deb

$ mkdir contracts
$ cd contracts
```
  


### wallet	

make     

```bash
$ cleos wallet create --to-console
"/usr/opt/eosio/2.1.0/bin/keosd" launched
Creating wallet: default
Save password to use in the future to unlock this wallet.
Without password imported keys will not be retrievable.
"PW5K1VtM4NxHZR9wSVNrKxSbKf2RqmX99sbYn3STe3WpgStojjqdJ"
```
open
```bash
$ cleos wallet open
Opened: default

$ cleos wallet list
Wallets:
[
    "default"
]
```
unlock
```bash
$ cleos wallet unlock
password:
PW5K1VtM4NxHZR9wSVNrKxSbKf2RqmX99sbYn3STe3WpgStojjqdJ

$ cleos wallet list
Wallets:
[
    "default *"
]
```
import key into wallet 

```bash
$ cleos wallet create_key
Created new private key with a public key of: "EOS8fjXhhc4PHHcxXE3MFS6FGjcEJwJm2PZa57gEpMG86KFhoAZ7K
```
	 
import development key

```bash
$ cleos wallet import
private key:
5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3

imported private key for:
EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
```

> 여기서 privat key 입력을 해야 되는데... 
지금 까지 생성된 wallet 의 private key로는 동작을 하지 않음... 
제공되는 개발 private key 를 입력해야 다음 단계로 넘어감.
나중에 개발용 private key를 어떻게 생성하는지 찾아서 수정해야됨. 


### strat keosd

keosd = key + eos    	

```bash
$ keosd &
info  2022-01-T0::0. keosd wallet_plugin.cpp:38  plugin_initialize  ] initializing wallet plugin
warn  2022-01-T0::05 keosd wallet_plugin.cpp:65  plugin_initialize  ] 3120000 wallet_exception: Wallet exception
Failed to lock access to wallet directory; is another keosd running?
{}
keosd  wallet_manager.cpp:304 initialize_lock

Failed to initialize
```
error..... 
keosd 를 kill 하고 다시 실행 

```bash
$ pkill keosd

// 특정  ip, port 를 설정하기 위한 option (기본: 8888port사용)
$ keosd --http-server-address=127.0.0.1:8900 &

info  2022-01-T01:05 keosd     http_plugin.cpp:798           plugin_initialize    ] configured http to listen on localhost:8900
info  2022-01-T0:. keosd     wallet_api_plugin.cpp:84      plugin_startup       ] starting wallet_api_plugin
info  2022-01-T0::0. keosd     http_plugin.cpp:983           add_handler          ] add api url: /v1/wallet/create
info  2022-01-T0:: keosd     http_plugin.cpp:983           add_handler          ] add api url: /v1/wallet/create_key
info  2022-01-T01: keosd     http_plugin.cpp:983           add_handler          ] add api url: /v1/wallet/get_public_keys
info  2022-01-T0::sd     http_plugin.cpp:983           add_handler          ] add api url: /v1/wallet/import_key
info  2022-01-T01:sd     http_plugin.cpp:983           add_handler          ] add api url: /v1/wallet/list_keys
info  2022-01-T0::05 keosd     http_plugin.cpp:983           add_handler          ] add api url: /v1/wallet/list_wallets
info  2022-01-T01:05 keosd     http_plugin.cpp:983           add_handler          ] add api url: /v1/wallet/lock
info  2022-01-T01:0. keosd     http_plugin.cpp:983           add_handler          ] add api url: /v1/wallet/lock_all
info  2022-01-T0::0. keosd     http_plugin.cpp:983           add_handler          ] add api url: /v1/wallet/open
info  2022-01-T0::05 keosd     http_plugin.cpp:983           add_handler          ] add api url: /v1/wallet/remove_key
info  2022-01-20T01:24:05.022 keosd     http_plugin.cpp:983           add_handler          ] add api url: /v1/wallet/set_timeout
info  2022-01-20T01:24:05.022 keosd     http_plugin.cpp:983           add_handler          ] add api url: /v1/wallet/sign_digest
info  2022-01-20T01:24:05.022 keosd     http_plugin.cpp:983           add_handler          ] add api url: /v1/wallet/sign_transaction
info  2022-01-20T01:24:05.022 keosd     http_plugin.cpp:983           add_handler          ] add api url: /v1/wallet/unlock
info  2022-01-20T01:24:05.023 keosd     http_plugin.cpp:877           operator()           ] start listening for http requests
info  2022-01-20T01:24:05.023 keosd     http_plugin.cpp:983           add_handler          ] add api url: /v1/node/get_supported_apis
```

> 옵션의  --http-server-address 값을 default로 주고 싶으면 
>  ~/eosio-wallet/config.ini 파일에 넣어 주면 됨

### strat nodeos
```bash
$ nodeos -e -p eosio \
--plugin eosio::producer_plugin \
--plugin eosio::producer_api_plugin \
--plugin eosio::chain_api_plugin \
--plugin eosio::http_plugin \
--plugin eosio::history_plugin \
--plugin eosio::history_api_plugin \
--filter-on="*" \
--access-control-allow-origin='*' \
--contracts-console \
--http-validate-host=false \
--http-server-address=0.0.0.0:8900 \
--verbose-http-errors >> nodeos.log 2>&1 &
```
check node
```bash
$ tail -f nodeos.log
```

check wallet 

```bash
$ cleos wallet list

Wallets:
[]
```
비어있는 리스트가 정상이라는데... wallet이 왜 비어 있는지?? 
  

check node endpoint

```bash
$ curl http://localhost:8888/v1/chain/get_info

{"server_version":"26a4d285","chain_id":"8a34ec7df1b8cd06ff4a8abbaa7cc50300823350cadc59ab296cb00d104d2b8f","head_block_num":37884,"last_irreversible_block_num":37883,"last_irreversible_block_id":"000093fb9e114968502d1d7335838377bbaafc9bcd5fcc2af84ad848f6099866","head_block_id":"000093fcc09baed7bc59d3cbf538bfefd3ab450d770b008788104df3eaac7bc8","head_block_time":"2022-01-20T06:41:39.500","head_block_producer":"eosio","virtual_block_cpu_limit":200000000,"virtual_block_net_limit":1048576000,"block_cpu_limit":200000,"block_net_limit":1048576,"server_version_string":"v2.1.0","fork_db_head_block_num":37884,"fork_db_head_block_id":"000093fcc09baed7bc59d3cbf538bfefd3ab450d770b008788104df3eaac7bc8","server_full_version_string":"v2.1.0-26a4d285d0be1052d962149e431eb81500782991","last_irreversible_block_time":"2022-01-20T06:41:39.000"}vagrant@vagrant:~/eos/contracts$ 
```
 > 정상


### make Accounts
위에서 만든 지갑(wallet) 하고 계정(Account)이 다른 의미로 사용 되는듯..    
새로 만드는 accounts 가 wallet 안에 포함된다는 의미인지?  
일단 그냥 따라해보는 걸로.....   

```bash
$ cleos create account eosio bob EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV

Error 3120006: No available wallet
Ensure that you have created a wallet and have it open
Error Details:
You don't have any wallet!
```
wallet이 없다는 에러.. 
위에서 비어있는 wallet 리스트가 정상이라는데.. 여기선 wallet이 없어서 에러???

wallet을 새로 하나 더 만들어 보고 .. 
```bash
$ cleos wallet create --to-console

Error 3120001: Wallet already exists
Try to use different wallet name.
Error Details:
Wallet with name: 'default' already exists at /home/vagrant/eosio-wallet/./default.wallet
```
이미 default 가 있어서 안됨. 

해결.. 
처음에 만들었던 wallet을 다시 unlock 해주고 제공되는 개발 private key로 만들었던 wallet public key를 입력해 주면 됨. 

```bash
$ cleos wallet open
Opened: default

$ cleos wallet list
Wallets:
[
  "default"
]

$ cleos wallet unlock
password[input wallet password] : Unlocked: default

$ cleos wallet list
Wallets:
[
  "default *"
]

$ cleos create account eosio bob EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV

executed transaction: afcf445564f1f4a875392acd7ecf41d869d09e2449f80abdb3e0f62d44f3a657  200 bytes  215 us
#         eosio <= eosio::newaccount            {"creator":"eosio","name":"bob","owner":{"threshold":1,"keys":[{"key":"EOS6MRyAjQq8ud7hVNYcfnVPJqcVp...
warning: transaction executed locally, but may not be confirmed by the network yet         ] 

$  cleos create account eosio alice EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV

executed transaction: 41406af7f2c3f78f14e78853ae0df25a0dff85acc2ac6774df884c911095395f  200 bytes  129 us
#         eosio <= eosio::newaccount            {"creator":"eosio","name":"alice","owner":{"threshold":1,"keys":[{"key":"EOS6MRyAjQq8ud7hVNYcfnVPJqc...
warning: transaction executed locally, but may not be confirmed by the network yet         ] 
```

#### token deploy 

contract source
```bash
$ cd contracts
	
$ ```shell
git clone https://github.com/EOSIO/eosio.contracts --branch v1.7.0 --single-branch

$ cd eosio.contracts/contracts/eosio.token
```

make account for contract

```bash
$ cleos create account eosio eosio.token EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV

executed transaction: a488f093b5d5a086f6873ad6df16eaf5d8f3c29d8b7abce4674ed8858c8db508  200 bytes  143 us
#         eosio <= eosio::newaccount            {"creator":"eosio","name":"eosio.token","owner":{"threshold":1,"keys":[{"key":"EOS6MRyAjQq8ud7hVNYcf...
warning: transaction executed locally, but may not be confirmed by the network yet         ] 
```

complie contract

```bash
$ eosio-cpp -I include -o eosio.token.wasm src/eosio.token.cpp --abigen
```
> eosio.cdt 제거후 다시 설치 

```bash
$ sudo apt remove eosio.cdt
$ sudo apt install ~/eosio.cdt_1.8.0-1-ubuntu-18.04_amd64.deb

$ eosio-cpp
eosio-cpp: Not enough positional command line arguments specified!
Must specify at least 1 positional argument: See: eosio-cpp --help
```
> eosio-cpp 정상동작 확인 

```bash
$ eosio-cpp -I include -o eosio.token.wasm src/eosio.token.cpp --abigen

/home/vagrant/eos/contracts/eosio.contracts/contracts/eosio.token/src/eosio.token.cpp:5:13: warning: abigen warning (Action <create> does not have a ricardian contract)
void token::create( const name&   issuer,
            ^
Warning, action <create> does not have a ricardian contract
/home/vagrant/eos/contracts/eosio.contracts/contracts/eosio.token/src/eosio.token.cpp:27:13: warning: abigen warning (Action <issue> does not have a ricardian contract)
void token::issue( const name& to, const asset& quantity, const string& memo )
            ^
Warning, action <issue> does not have a ricardian contract
/home/vagrant/eos/contracts/eosio.contracts/contracts/eosio.token/src/eosio.token.cpp:53:13: warning: abigen warning (Action <retire> does not have a ricardian contract)
void token::retire( const asset& quantity, const string& memo )
            ^
Warning, action <retire> does not have a ricardian contract
/home/vagrant/eos/contracts/eosio.contracts/contracts/eosio.token/src/eosio.token.cpp:77:13: warning: abigen warning (Action <transfer> does not have a ricardian contract)
void token::transfer( const name&    from,
            ^
Warning, action <transfer> does not have a ricardian contract
/home/vagrant/eos/contracts/eosio.contracts/contracts/eosio.token/src/eosio.token.cpp:129:13: warning: abigen warning (Action <open> does not have a ricardian contract)
void token::open( const name& owner, const symbol& symbol, const name& ram_payer )
            ^
Warning, action <open> does not have a ricardian contract
/home/vagrant/eos/contracts/eosio.contracts/contracts/eosio.token/src/eosio.token.cpp:149:13: warning: abigen warning (Action <close> does not have a ricardian contract)
void token::close( const name& owner, const symbol& symbol )
            ^
Warning, action <close> does not have a ricardian contract
6 warnings generated.
```

> src/eosio.token.cpp 이  contract source

deploy contract
	
```bash
$ cleos set contract eosio.token /home/vagrant/eos/contracts/eosio.contracts/contracts/eosio.token --abi eosio.token.abi -p eosio.token@active

Reading WASM from /home/vagrant/eos/contracts/eosio.contracts/contracts/eosio.token/eosio.token.wasm...
Publishing contract...
executed transaction: f11972386600ef10a749eb68def7e3a9287a56bafff61d9608e77dbcddb91da4  19368 bytes  2737 us
#         eosio <= eosio::setcode               {"account":"eosio.token","vmtype":0,"vmversion":0,"code":"0061736d010000000180022860000060037f7f7f01...
#         eosio <= eosio::setabi                {"account":"eosio.token","abi":"0e656f73696f3a3a6162692f312e320008076163636f756e7400010762616c616e63...
warning: transaction executed locally, but may not be confirmed by the network yet         ] 
```
*  시간이 지나면 wallet 이 lock이 되므로 unlock 해줘야 한다. 

create token

> ethereum, orbs와는 다르게 deploy와 token create가 따로 일어남.

```bash
$ cleos push action eosio.token create '[ "alice", "1000000000.0000 SYS"]' -p eosio.token@active

or 


cleos push action eosio.token create '{"issuer":"alice", "maximum_supply":"1000000000.0000 SYS"}' -p eosio.token@active
```
> 앞에서 만든 계정 "alice"가 token 발행자가 됨.
> 또한 앞서 contract를 deploy한 계정 eosio.token@active의 권한을  따라야 해서 -p eosio.token@active 를 해줘야함. 
> issuer 와 deploy account를 같이 사용할 수 있는지 테스트 필요

token 발행 

> 위에서 token을 만들었지만 아직 발행은 안된 상태로... 그 누구도  1000000000.0000 SYS를 가지고 있지 않음??
> balance 확인 

```bash
$ cleos get currency balance eosio.token bob SYS

$ cleos get currency balance eosio.token alice SYS  

$ cleos get currency balance eosio.token eosio.token SYS
```
> push action issue 로 발행을 해줘야 token이 생성되는것으로 보임.

```bash
$ cleos push action eosio.token issue '[ "alice", "100.0000 SYS", "memo" ]' -p alice@active

executed transaction: 18aadc3607f98afc6300c1c860367fd129650cd067b7697a56b21d4d288424c2  128 bytes  182 us
#   eosio.token <= eosio.token::issue           {"to":"alice","quantity":"100.0000 SYS","memo":"memo"}
warning: transaction executed locally, but may not be confirmed by the network yet         ] 
```

> 발행자가 아닌 계정에는 issue 명령어가 동작 안함. 
> alice가 아닌 bob에게 push action issue 명령어 해보기 
```bash
$ cleos push action eosio.token issue '[ "bob", "100.0000 SYS", "memo" ]' -p alice@active

Error 3050003: eosio_assert_message assertion failure
Error Details:
assertion failure with message: tokens can only be issued to issuer account
pending console output: 
``` 

transfer

> alice to bob  25 SYS

```bash
$ cleos push action eosio.token transfer '[ "alice", "bob", "25.0000 SYS", "m" ]' -p alice@active

executed transaction: da02c29499f818b3c320385f303c213562879354d1d77271a15b554aef1b1e93  128 bytes  155 us
#   eosio.token <= eosio.token::transfer        {"from":"alice","to":"bob","quantity":"25.0000 SYS","memo":"m"}
#         alice <= eosio.token::transfer        {"from":"alice","to":"bob","quantity":"25.0000 SYS","memo":"m"}
#           bob <= eosio.token::transfer        {"from":"alice","to":"bob","quantity":"25.0000 SYS","memo":"m"}
warning: transaction executed locally, but may not be confirmed by the network yet ] 
```



## 참고 사이트 
https://www.hanbit.co.kr/media/openbook/eos/
> 공식 문서 보다 좀더 친절하고 자세히 설명을 하고 있으나... eos 소스가 예전 소스로 보임. 따라서 중간중간 소스 수정이 필요함. 
> 






# 2021.02.08

```bash
$ cleos wallet create -n test2 --to-console
warn  2022-02-08T06:54:21.284 keosd     wallet.cpp:218                save_wallet_file     ] saving wallet to file /home/vagrant/eosio-wallet/./test2.wallet
Creating wallet: test2
Save password to use in the future to unlock this wallet.
Without password imported keys will not be retrievable.
"PW5KVHTyjs9jGNsKycqiCSV4tC4kpy58rGG6gG5q7PnmFT5rkfkYD"

$ cleos wallet create_key -n test2

warn  2022-02-08T07:13:00.685 keosd     wallet.cpp:218                save_wallet_file     ] saving wallet to file /home/vagrant/eosio-wallet/./test2.wallet
Created new private key with a public key of: "EOS5XPD91FrjYkviKA3f99FZviaMnpN7YDKLY18fAzDApDqSEUmWq"



$ cleos create key --to-console
Private key: 
5KLBed2MK3Ns9CRGxspieEhv3S4FU32TVAcmVMCVuUEqXrYhvsU
Public key: EOS8LvpGUZNpukb3k5mu26MczB81GU2SNESYJRVcuyeSUKwiy6NmR

$ cleos create key --to-console
Private key:  5JBjteeJzSdN8y4AaPTQZr23Q7FWWvwraZN6m4bYXtJwDHfM3zX
Public key: EOS8RzWuBGdfGX8DMq51BXqJFr3wnTyKpG5ofimiWDvDJWp8Hc9qQ

$ cleos create key --to-console
Private key: 5HrKr3c1sKfQpRbboQZ7xEbMQ1rvfjGptnpQXHvUi45PXJDRggP
Public key: EOS6AE6ZsMZbChSymHiHQ5Wuy7JQYX4LJbdi75zTC8vukUp1N9NDz
	

$ cleos wallet import --private-key 5JBjteeJzSdN8y4AaPTQZr23Q7FWWvwraZN6m4bYXtJwDHfM3zX -n test2

warn  2022-02-08T06:58:45.171 keosd     wallet.cpp:218                save_wallet_file     ] saving wallet to file /home/vagrant/eosio-wallet/./test2.wallet
imported private key foryjNcqVp58GqT5D

: EOS8RzWuBGdfGX8DMq51BXqJFr3wnTyKpG5ofimiWDvDJWp8Hc9qQ

$ cleos wallet import --private-key 5KLBed2MK3Ns9CRGxspieEhv3S4FU32TVAcmVMCVuUEqXrYhvsU -n test2

warn  2022-02-08T06:59:08.997 keosd     wallet.cpp:218                save_wallet_file     ] saving wallet to file /home/vagrant/eosio-wallet/./test2.wallet
imported private key for: EOS8LvpGUZNpukb3k5mu26MczB81GU2SNESYJRVcuyeSUKwiy6NmR

$ cleos wallet import --private-key 5HrKr3c1sKfQpRbboQZ7xEbMQ1rvfjGptnpQXHvUi45PXJDRggP -n test2

warn  2022-02-08T07:01:40.661 keosd     wallet.cpp:218                save_wallet_file     ] saving wallet to file /home/vagrant/eosio-wallet/./test2.wallet
imported private key for: EOS6AE6ZsMZbChSymHiHQ5Wuy7JQYX4LJbdi75zTC8vukUp1N9NDz

$ 
```





```bash
$ cleos wallet create --to-console -n test3

Creating wallet: test3
Save password to use in the future to unlock this wallet.
Without password imported keys will not be retrievable.
"PW5KcRrZiXBLoBTTJQxhC5co5JP1YToWGAYJZZFhea3HMvEhxq8n8"

$ cleos wallet create_key -n test3

Created new private key with a public key of: "EOS7P3rhVcXGA5feb9WERBYMkuq5ohWDLBgUXnUPPGVrgfsza1Cd1"

//masterMASTER
$ cleos create key --to-console
Private key: 
5KLBed2MK3Ns9CRGxspieEhv3S4FU32TVAcmVMCVuUEqXrYhvsU
Public key: EOS8LvpGUZNpukb3k5mu26MczB81GU2SNESYJRVcuyeSUKwiy6NmR


//issuerISSUER
$ cleos create key --to-console
Private key:  5JBjteeJzSdN8y4AaPTQZr23Q7FWWvwraZN6m4bYXtJwDHfM3zX
Public key: EOS8RzWuBGdfGX8DMq51BXqJFr3wnTyKpG5ofimiWDvDJWp8Hc9qQ


//player
$ cleos create key --to-console
Private key: 5HrKr3c1sKfQpRbboQZ7xEbMQ1rvfjGptnpQXHvUi45PXJDRggP
Public key: EOS6AE6ZsMZbChSymHiHQ5Wuy7JQYX4LJbdi75zTC8vukUp1N9NDz


//master
$ cleos walet import --private-key 5K3sRxpieEhS4TCuUssLBed2MK3Ns9CRGxspieEhv3S4FU32TVAcmVMCVuUEqXrYhvsU -n test3

//issuer
$ cleos wallet import --privatekey 5JBjteeJzSdN8y4AaPTQZr23Q7FWWvwraZN6m4bYXtJwDHfM3zX e3

//player
$ cleos et wallet import --private-key 5QZrQv4XJDHrKr3c1sKfQpRbboQZ7xEbMQ1rvfjGptnpQXHvUi45PXJDRggP -n test3


$ cleos create account eosio master EOS8LvpGUZNpukb3k5mu26MczB81GU2SNESYJRVcuyeSUKwiy6NmR

$ cleos create account eosio issuer EOS8RzWuBGdfGX8DMq51BXqJFr3wnTyKpG5ofimiWDvDJWp8Hc9qQ

$ cleos create account eosio player EOSmaster
$ cleos wallet import --private-key 5K
//player
$ cleos  --privatekey 5 -n test3
6AE6ZsMZbChSymHiHQ5Wuy7JQYX4LJbdi75zTC8vukUp1N9NDz


$ cleos set contract master ./ ./play.wasm ./play.abi

$ cleos push action master create '[ "issuer", "1000000000.0000 TEST"]' -p master@active     

$ cleos push action master issue '[ "issuer", "10000.0000 TEST", "memo" ]' -p issuer@active  

$ cleos push action master transfer '[  "issuer","player", "400.0000 TEST", "m" ]' -p issuer@active
```



# VSCode 

https://medium.com/infinitexlabs/how-to-setup-vs-code-and-clion-for-eos-dapp-development-da103f454fd8

https://homoefficio.github.io/2018/06/06/EOS-Visual-Studio-Code-%EA%B0%9C%EB%B0%9C-%ED%99%98%EA%B2%BD-%EA%B5%AC%EC%84%B1/



## Owner Transfer

make wallet 
```bash
$ cleos wallet create -n owner_wallet -f owner_wallet
PW5KbF86ByrxxpbVpzumQPnh2VbhrbM8xMFJNFpeBZSgk3ogFMS3s
```
create  wallet key
```bash
$ cleos wallet create_key -n owner_wallet
Created new private key with a public key of: "EOS6Ua77ESTmDF1CzuQfRMc2GMBqHFuEpFCPgbXL44jDH945kW6xA"
```

make keys
```bash
$ cleos create key -f issuer
$ cleos create key -f owner
$ cleos create key -f bob
$ cleos create key -f alice
```
keys
```
issuer
Private key: 5KhpiSHoWFD6uz12JteaHR1XcANByPw48uvEeRpYbhoCCDEcdW2
Public key: EOS78eKu797Cvb8RAA9D5rGFeqmtfSv2PnofvLocdKvbiR2R1nxEy

owner
Private key: 5JejLYkyNKiPuujF44GhyLmCwcAHZBoWrEu4e3dzqWN9a9cfS83
Public key: EOS5KZceznbnX4NQTBbeRQzSbbXWZqsB7RG6ugDeT2mBuc4hUzKKg

bob 
Private key: 5Hpc1S3gJobHx2MFaXvXqHcizevVZV9aSRyjNLFV4o8fSoW8zWY
Public key: EOS5K84erMGq2FT5XynTjdkz2fucDgsaxfSe9SyNd68HDHwr28nwB

alice
Private key: 5Hs9M6k3bf4PLxmpJx1gCEGWPaA2wcbcCBKDfAEjfAor6VWooqt
Public key: EOS8BkzsP856wQYxZNcDnCngxooRc1zEUBFe3Sq5FgiFk272oYiT2
```

key import to wallet
issuer, owner, bob, alice 의 private key를 차례로 입력
```bash
$ cleos wallet import -n owner_wallet
```

create accounts
```bash
$ cleos create account eosio issuer 
```


### multiple node test

#### vagrant info    

node1 :
``` 
config.vm.network "forwarded_port", guest: 8900, host: 8900
config.vm.network "forwarded_port", guest: 8901, host: 8901
config.vm.network "private_network", ip: "192.168.33.33"
```
node2 :
``` 
config.vm.network "forwarded_port", guest: 8902, host: 8902
config.vm.network "forwarded_port", guest: 8903, host: 8903
config.vm.network "private_network", ip: "192.168.33.34"
```
node3 : 
```
config.vm.network "forwarded_port", guest: 8904, host: 8904
config.vm.network "forwarded_port", guest: 8905, host: 8905
config.vm.network "private_network", ip: "192.168.33.35"
```


#### conndect node1 and node2
```bash
$ sudo apt update
$ sudo apt upgrade -y
$ wget https://github.com/eosio/eos/releases/download/v2.1.0/eosio_2.1.0-1-ubuntu-20.04_amd64.deb
$ sudo apt install ./eosio_2.1.0-1-ubuntu-20.04_amd64.deb
```

node1 only
```bash
$ wget https://github.com/eosio/eosio.cdt/releases/download/v1.8.0/eosio.cdt_1.8.0-1-ubuntu-18.04_amd64.deb
$ sudo apt install ./eosio.cdt_1.8.0-1-ubuntu-18.04_amd64.deb

$ mkdir contracts
$ cd contracts
$ git clone https://github.com/EOSIO/icontacts--ranh v1.7.0 --single-branch

$ cd 
$ mkdir accounts
$ cd accounts
$ cleos wallet create -f wallet
$ cleos waalet create_key
Created new private key with a public key of: "EOS5gFrBcL1ToVzdUeCbrkPd76d1m8fVNHbHtkwTu8ZdLQqWnyw54"

$ cleos create key -f deployer
$ cleos create key -f creatr
$ cleos create key -f bob
$ cleos create key -f alice

```

#### keys
wallet : 
`private key: PW5KWwQmDFPJCdcCo54WwKs99dTzbPFmMdJpGsgFErLseKzjifsyQ`
`public key: EOS5gFrBcL1ToVzdUeCbrkPd76d1m8fVNHbHtkwTu8ZdLQqWnyw54`

producer:
`Private key: 5JZiBgr2xW2pf9LNr19uUbxHfPcTibiK4U7mGFMRY6gw8URBGRh`
`Public key: EOS7Zonw42GzTHTp7ewvK7dJXyz2Ub5GojpgxsjdNE5qUcZAXJJbT`

deployer : 
`Private key: 5JQMHjFnwAuNUxiiDyjwRPZS8LL7mf2f2WbowR4vkbHgKJS1a2q`
`Public key: EOS857N9A4XwnBaPEtNga5ZRuP5cSA73xoxPP4xWebsezkYnHcfan`

creator:
`Private key: 5Jt7e74QLT1KiB2jQBnUDAfnQXYPUpSchFdagM5D7QKEp1dQwxF`
`Public key: EOS8mi1UZznN8H7CCxRXRtMVu5Tz5kwLeLRdxV2hteqHkXRvG17nj`

bob :
`Private key: 5K7gz9r342tQxdaqRQvbJ73sW9vg3uippLhiCuyGAEqdnJVfNSj`
`Public key: EOS8WQKyJU54pCFuMx71WJntyHi4Rx5jELvqQVVZyVU5XLrnxvbs7`

alice:
`Private key: 5JqufopuzigmBnkpGKSEA6rCzVqis2YMbLEbV62uqwJEZxhq8Vq`
`Public key: EOS4tzEi8FjcjCXRkBENSixEgAHQvsgyBYhxiLdFzHGwZJGb4gNjs`

import key
```bash
$ cleos -u http://localhost:8900 import key

$ cleos wallet keys
[
"EOS4tzEi8FjcjCXRkBENSixEgAHQvsgyBYhxiLdFzHGwZJGb4gNjs",
"EOS5gFrBcL1ToVzdUeCbrkPd76d1m8fVNHbHtkwTu8ZdLQqWnyw54",
"EOS857N9A4XwnBaPEtNga5ZRuP5cSA73xoxPP4xWebsezkYnHcfan",
"EOS8WQKyJU54pCFuMx71WJntyHi4Rx5jELvqQVVZyVU5XLrnxvbs7",
"EOS8mi1UZznN8H7CCxRXRtMVu5Tz5kwLeLRdxV2hteqHkXRvG17nj"
]
```

node1 start
```bash
$ nodeos -e -p eosio \
--plugin eosio::producer_plugin \
--plugin eosio::producer_api_plugin \
--plugin eosio::chain_api_plugin \
--plugin eosio::http_plugin \
--plugin eosio::history_plugin \
--plugin eosio::history_api_plugin \
--plugin eosio::net_plugin \
--filter-on="*" \
--access-control-allow-origin='*' \
--contracts-console \
--http-validate-host=false \
--http-server-address=0.0.0.0:8900 \
--p2p-listen-endpoint=0.0.0.0:8901 \
--p2p-peer-address=192.168.33.34:8903 \
--p2p-peer-address=192.168.33.35:8905 \
--genesis-json "/home/vagrant/genesis.json" \
--verbose-http-errors >> nodeos.log 2>&1 &

$ curl http://localhost:8900/v1/chain/get_info
```

create accounts
```bash
$ cleos -u http://localhost:8900 create account eosio deployer EOS857N9A4XwnBaPEtNga5ZRuP5cSA73xoxPP4xWebsezkYnHcfan

$ cleos -u http://localhost:8900 create account eosio creator EOS8mi1UZznN8H7CCxRXRtMVu5Tz5kwLeLRdxV2hteqHkXRvG17nj  

$ cleos -u http://localhost:8900 create account eosio bob EOS8WQKyJU54pCFuMx71WJntyHi4Rx5jELvqQVVZyVU5XLrnxvbs7

$ cleos -u http://localhost:8900 create account eosio alice EOS4tzEi8FjcjCXRkBENSixEgAHQvsgyBYhxiLdFzHGwZJGb4gNjs
```


deploy
```bash
$ cd contract/eosio.contracts/contracts/eosio.token
$ eosio-cpp -I include -o eosio.token.wasm src/eosio.token.cpp --abigen
$ cleos -u http://localhost:8900 set contract owner ./ --abi eosio.token.abi -p owner@active


$ cleos -u http://localhost:8900 push action owner create '{"issuer":"alice", "maximum_supply":"1000000000.0000 SYS"}' -p owner@active

$ cleos -u http://localhost:8900 push action owner issue '[ "alice", "100.0000 SYS", "memo" ]' -p alice@active

$ cleos -u http://localhost:8900 push action owner transfer '[ "alice", "bob", "25.0000 SYS", "m" ]' -p alice@active

$ cleos -u http://192.168.33.33:8900 push action owner transfer '[ "alice", "bob", "25.0000 SYS", "m" ]' -p alice@active

```


node2

```bash
$ nodeos -e -p eosio2 \
--plugin eosio::producer_plugin \
--plugin eosio::producer_api_plugin \
--plugin eosio::chain_api_plugin \
--plugin eosio::http_plugin \
--plugin eosio::history_plugin \
--plugin eosio::history_api_plugin \
--plugin eosio::net_plugin \
--filter-on="*" \
--access-control-allow-origin='*' \
--contracts-console \
--http-validate-host=false \
--http-server-address=0.0.0.0:8902 \
--p2p-listen-endpoint=0.0.0.0:8903 \
--p2p-peer-address=192.168.33.33:8901 \
--p2p-peer-address=192.168.33.35:8905 \
--verbose-http-errors >> nodeos.log 2>&1 &
```
node3
```
$ nodeos -e -p eosio3 \
--plugin eosio::producer_plugin \
--plugin eosio::producer_api_plugin \
--plugin eosio::chain_api_plugin \
--plugin eosio::http_plugin \
--plugin eosio::history_plugin \
--plugin eosio::history_api_plugin \
--plugin eosio::net_plugin \
--filter-on="*" \
--access-control-allow-origin='*' \
--contracts-console \
--http-validate-host=false \
--http-server-address=0.0.0.0:8904 \
--p2p-listen-endpoint=0.0.0.0:8905 \
--p2p-peer-address=192.168.33.33:8901 \
--p2p-peer-address=192.168.33.34:8903 \
--verbose-http-errors >> nodeos.log 2>&1 &
```


###  확인

node2 or node3

```bash
$ cleos -u http://192.168.33.33:8900 get currency balance owner bob -j
```
당연히 node1 주소를 넣었기 때문에 정상 확인... 

```
$ cleos -u http://localhost:8902 get currency balance owner bob -j
```
아직 블록 동기화가 안되어 있는것으로 확인... 



### 다시
genesis file 로 실행하기

wallet : 
`private key: PW5KWwQmDFPJCdcCo54WwKs99dTzbPFmMdJpGsgFErLseKzjifsyQ`
`public key: EOS5gFrBcL1ToVzdUeCbrkPd76d1m8fVNHbHtkwTu8ZdLQqWnyw54`

producer:
`Private key: 5JZiBgr2xW2pf9LNr19uUbxHfPcTibiK4U7mGFMRY6gw8URBGRh`
`Public key: EOS7Zonw42GzTHTp7ewvK7dJXyz2Ub5GojpgxsjdNE5qUcZAXJJbT`

create accounts
```bash
$ cleos -u http://localhost:8900 create account eosio deployer EOS857N9A4XwnBaPEtNga5ZRuP5cSA73xoxPP4xWebsezkYnHcfan

$ cleos -u http://localhost:8900 create account eosio creator EOS8mi1UZznN8H7CCxRXRtMVu5Tz5kwLeLRdxV2hteqHkXRvG17nj  

$ cleos -u http://localhost:8900 create account eosio bob EOS8WQKyJU54pCFuMx71WJntyHi4Rx5jELvqQVVZyVU5XLrnxvbs7

$ cleos -u http://localhost:8900 create account eosio alice EOS4tzEi8FjcjCXRkBENSixEgAHQvsgyBYhxiLdFzHGwZJGb4gNjs
```

`genesis.json`
> node1, node2, node3에서 공통으로 사용되는 genesis.json
```json
{  
"initial_timestamp": "2022-03-28T14:55:11.000",  
"initial_key": "EOS7Zonw42GzTHTp7ewvK7dJXyz2Ub5GojpgxsjdNE5qUcZAXJJbT",  
"initial_configuration": {  
"max_block_net_usage": 1048576,  
"target_block_net_usage_pct": 1000,  
"max_transaction_net_usage": 524288,  
"base_per_transaction_net_usage": 12,  
"net_usage_leeway": 500,  
"context_free_discount_net_usage_num": 20,  
"context_free_discount_net_usage_den": 100,  
"max_block_cpu_usage": 100000,  
"target_block_cpu_usage_pct": 500,  
"max_transaction_cpu_usage": 50000,  
"min_transaction_cpu_usage": 100,  
"max_transaction_lifetime": 3600,  
"deferred_trx_expiration_window": 600,  
"max_transaction_delay": 3888000,  
"max_inline_action_size": 4096,  
"max_inline_action_depth": 4,  
"max_authority_depth": 6  
},  
"initial_chain_id": "0000000000000000000000000000000000000000000000000000000000000000"  
}
```


### node1
```bash
$ cleos create key -f provider
```
`Private key: 5JZiBgr2xW2pf9LNr19uUbxHfPcTibiK4U7mGFMRY6gw8URBGRh`
`Public key: EOS7Zonw42GzTHTp7ewvK7dJXyz2Ub5GojpgxsjdNE5qUcZAXJJbT`
```bash
$ nodeos -e -p eosio \
--signature-provider EOS7Zonw42GzTHTp7ewvK7dJXyz2Ub5GojpgxsjdNE5qUcZAXJJbT=KEY:5JZiBgr2xW2pf9LNr19uUbxHfPcTibiK4U7mGFMRY6gw8URBGRh \
--plugin eosio::producer_plugin \
--plugin eosio::producer_api_plugin \
--plugin eosio::chain_api_plugin \
--plugin eosio::http_plugin \
--plugin eosio::history_plugin \
--plugin eosio::history_api_plugin \
--plugin eosio::net_plugin \
--filter-on="*" \
--access-control-allow-origin='*' \
--contracts-console \
--http-validate-host=false \
--http-server-address=0.0.0.0:8900 \
--p2p-listen-endpoint=0.0.0.0:8901 \
--p2p-peer-address=192.168.33.34:8903 \
--p2p-peer-address=192.168.33.35:8905 \
--genesis-json "/home/vagrant/genesis.json" \
--verbose-http-errors >> nodeos.log 2>&1 &
```

### node2
```bash
$ cleos create key -f provider
```
`Private key: 5J1ny6BxNeCzMmVckzmwXZ5z88eeetzULWoePBPtoSJFTyH7GqY`
`Public key: EOS84mn3hnCSeahxV8ZYWxS9XrwG1WAora3FYigxJxztRZne82VeT`
```bash
$ nodeos -e -p second \
--signature-provider EOS84mn3hnCSeahxV8ZYWxS9XrwG1WAora3FYigxJxztRZne82VeT=KEY:5J1ny6BxNeCzMmVckzmwXZ5z88eeetzULWoePBPtoSJFTyH7GqY \
--plugin eosio::producer_plugin \
--plugin eosio::producer_api_plugin \
--plugin eosio::chain_api_plugin \
--plugin eosio::http_plugin \
--plugin eosio::history_plugin \
--plugin eosio::history_api_plugin \
--plugin eosio::net_plugin \
--filter-on="*" \
--access-control-allow-origin='*' \
--contracts-console \
--http-validate-host=false \
--http-server-address=0.0.0.0:8902 \
--p2p-listen-endpoint=0.0.0.0:8903 \
--p2p-peer-address=192.168.33.33:8901 \
--p2p-peer-address=192.168.33.35:8905 \
--genesis-json "/home/vagrant/genesis.json" \
--verbose-http-errors >> nodeos.log 2>&1 &
```


### node3
```bash
$ cleos create key -f provider
```
`Private key: 5KhatshdoiNvWieTeXVMyU6p16gpSbe58uJko6HHjCURqcxaPip`
`Public key: EOS55XhgJj14ojhwNXhk1as6XGa59uChcMC1szCukfwwtjvvMhLtE`
```bash
$ nodeos -e -p third \
--signature-provider EOS55XhgJj14ojhwNXhk1as6XGa59uChcMC1szCukfwwtjvvMhLtE=KEY:5KhatshdoiNvWieTeXVMyU6p16gpSbe58uJko6HHjCURqcxaPip \
--plugin eosio::producer_plugin \
--plugin eosio::producer_api_plugin \
--plugin eosio::chain_api_plugin \
--plugin eosio::http_plugin \
--plugin eosio::history_plugin \
--plugin eosio::history_api_plugin \
--plugin eosio::net_plugin \
--filter-on="*" \
--access-control-allow-origin='*' \
--contracts-console \
--http-validate-host=false \
--http-server-address=0.0.0.0:8904 \
--p2p-listen-endpoint=0.0.0.0:8905 \
--p2p-peer-address=192.168.33.33:8901 \
--p2p-peer-address=192.168.33.34:8903 \
--genesis-json "/home/vagrant/genesis.json" \
--verbose-http-errors >> nodeos.log 2>&1 &
```


## eosjs-test
kotech0의 container eosjs-test 생성

wallet key 
`private key : PW5J5Wc6Sr8EJxDfeAvgHvraLhR4X3UnryG1bw26Jn3YDj1p9B54C`

producer 
`Private key: 5JnaNQxTgbEBQcitY8Rks2U7Ws1sh48SiwJodVaKXP59TCR56RY`
`Public key: EOS6eQ426ThEZzTTBjixgndqPS1bVm5ZHtThdyky78oPT6LTSKnN9`

owner 
`Private key: 5K3CpuTsjcWa15Lg8T8CP6jNipUVUQh3PY8TT9F2ECsgoG139qf`
`Public key: EOS6sNbuznaWLMpqr7ymxbULxFXG6hmXSoGwKyrt6WrzpbpjfDpke`

alice
`Private key: 5JEKaDPVXxrnjiv3qmNFwAHFniqbGYXWg6ctiVxUN4Bq46rgrdZ`
`Public key: EOS6HyzaCSEDgBRyZv4TW3L4FxiTstT1P6i24oVVahYKYt6W23Zgn`

bob
`Private key: 5KP5fTDJVow9mcGmMKgnBmG74PcugPuGr3NoEDiHmkTuhfELsV5`
`Public key: EOS5s2hvjtPmsRSuHu9MvLEqZs9YJUvRHNdnG6WSDHXyJt6YxFHjE`

#### node start
```bash
nodeos -e -p eosio \
--signature-provider EOS6eQ426ThEZzTTBjixgndqPS1bVm5ZHtThdyky78oPT6LTSKnN9=KEY:5JnaNQxTgbEBQcitY8Rks2U7Ws1sh48SiwJodVaKXP59TCR56RY \
--plugin eosio::producer_plugin \
--plugin eosio::producer_api_plugin \
--plugin eosio::chain_api_plugin \
--plugin eosio::http_plugin \
--plugin eosio::history_plugin \
--plugin eosio::history_api_plugin \
--plugin eosio::net_plugin \
--filter-on="*" \
--access-control-allow-origin='*' \
--contracts-console \
--http-validate-host=false \
--http-server-address=0.0.0.0:9100 \
--genesis-json "/root/workspace/genesis.json" \
--verbose-http-errors >> nodeos.log 2>&1 &
```

#### chain_info
```json
{
  "server_version": "26a4d285",
  "chain_id": "d5b6fa7019617ba791c9ee92a790a856604f88bcab0bf9a73fdc2e6aab464d3f",
  "head_block_num": 160247,
  "last_irreversible_block_num": 160246,
  "last_irreversible_block_id": "000271f62af047b59dd4784b7245b3b78fcdfa4a5d56bba8bb02f22718242b18",
  "head_block_id": "000271f7c1ce8ee51289d86b8da5c78648e661daede5345e25d9bd3e163aa713",
  "head_block_time": "2022-04-08T00:31:06.000",
  "head_block_producer": "eosio",
  "virtual_block_cpu_limit": 100000000,
  "virtual_block_net_limit": 1048576000,
  "block_cpu_limit": 99900,
  "block_net_limit": 1048576,
  "server_version_string": "v2.1.0",
  "fork_db_head_block_num": 160247,
  "fork_db_head_block_id": "000271f7c1ce8ee51289d86b8da5c78648e661daede5345e25d9bd3e163aa713",
  "server_full_version_string": "v2.1.0-26a4d285d0be1052d962149e431eb81500782991",
  "last_irreversible_block_time": "2022-04-08T00:31:05.500"
}
```


kotech1 에서 nodejs test

1. virtualenv 와 nodeenv 따로 설정하는 법
```bash
$ python3 -m venv venv
$ . venv/bin/activate
(venv)$ pip install nodeenv
(venv)$ nodeenv --node=10.19.0 nenv
(venv)$ . nenv/bin/activate
(nenv)(venv)$ npm install eosjs
(nenv)(venv)$ npm install eosjs-api
(nenv)(venv)$ npm install eosjs-ecc
(nenv)(venv)$ node test.js
```

2. 현재 virtualenv에 nodeenv를 설정하는 법
- pyenv로 python 버전을 지정해 놓고 하는게 좋음..
```bash
$ pyenv install 3.8.10
$ pyenv shell 3.8.10
$ python -m venv nenv
$ . nenv/bia/activate
(nenv) $ pip install nodeenv
(nenv) $ nodeenv --node=10.19.0 -p
(nenv) $ npm install eosjs
(nenv) $ npm install eosjs-api
(nenv) $ npm install eosjs-ecc
(nenv) $ node test.js
```

#### test.js
```js
const EosApi  = require('eosjs-api');

const options = {
       httpEndpoint: 'http://sw112.iptime.org:7100', // default, null for cold-storage
}

eos = EosApi(options);

var block_num;
const get_block_num = async () => {
        //console.dir(await eos.getInfo({}), {'maxArrayLength': null});
        const info = await eos.getInfo({});
        //console.dir(typeof info);
        block_num = info['head_block_num'];
        //console.dir(info['fork_db_head_block_num'], {'maxArrayLength': null}); 
};

const get_block = async (num) => {
        const info = await eos.getBlock(num);
        console.log(info);
        //console.log('###########################');
        //console.log(info['transactions'][0]['trx']['signatures']);

};

get_block(383);
```

#### test2.js
```js
const fs = require('fs');

const path = require('path');

const { JsonRpc, RpcError, Api } = require('eosjs');

const { JsSignatureProvider } = require('eosjs/dist/eosjs-jssig');

const fetch = require('node-fetch');

const { TextEncoder, TextDecoder } = require('util');

const ecc = require('eosjs-ecc');

const EosApi = require('eosjs-api');

var contract = 'eosio.token';

var tx_send;

var tx_send_str;

endpoint = 'http://127.0.0.1:9100';

const options = {

httpEndpoint: endpoint,

}

eos = EosApi(options);

var signer = 'bob';

var from = 'bob';

var to = 'alice';

var amount = '0.0001 SYS';

var memo = 'transactiontest';

const privateKey = '5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3'; // replace with "bob" account private key

const rpc = new JsonRpc(endpoint, { fetch });

//const signatureProvider = new JsSignatureProvider([privateKey, r1PrivateKey, cfactorPrivateKey]);

const signatureProvider = new JsSignatureProvider([privateKey]);

const api = new Api({ rpc, signatureProvider, textDecoder: new TextDecoder(), textEncoder: new TextEncoder() });

function toHexString(byteArray) {

return Array.prototype.map.call(byteArray, function(byte) {

return ('0' + (byte & 0xFF).toString(16)).slice(-2);

}).join('');

}

function toUint8Array(hexString) {

var result = [];

for (var i = 0; i < hexString.length; i += 2) {

result.push(parseInt(hexString.substr(i, 2), 16));

}

return result;

}

function toBase64(obj) {

obj['serializedTransaction'] = toHexString(obj['serializedTransaction']);

return new Buffer(JSON.stringify(obj)).toString("base64");

}

function toObj(base64) {

var tx = JSON.parse( new Buffer(base64, 'base64').toString('utf8') );

tx['serializedTransaction'] = toUint8Array(tx['serializedTransaction']);

return tx;

}

const signtx = async () => {

await api.getAbi(contract);

tx_send = await api.transact({

actions: [api.with(contract).as(signer).transfer(from, to, amount, memo)]

}, {

blocksBehind: 3,

expireSeconds: 30,

broadcast: false,

});

tx_send_str = toBase64(tx_send);

// tx_send['serializedTransaction'] = toHexString(tx_send['serializedTransaction']);

//console.log(tx_send);

// tx_send_str = new Buffer(JSON.stringify(tx_send)).toString("base64");

//console.log(tx_send_str);

};

const broadcast = async(obj) => {

await api.getAbi(contract);

result = await api.pushSignedTransaction(obj);

console.dir(result);

};

signtx().then(() => {

//console.log(tx_send_str);

broadcast(toObj(tx_send_str));

//var tx = JSON.parse( new Buffer(tx_send_str, 'base64').toString('utf8') );

//tx['serializedTransaction'] = toByteArray(tx['serializedTransaction']);

//console.log(ascii);

});
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMjIwMDMxNDksMjA4OTM3MTYwNywtMT
cxMDEzMTUyMCw4NTk4NDE5MDYsLTIxMzY5MDIyNDIsMTM3Njc0
Njg2Miw1MzUzNjA3NDcsMTcwOTYyMDM4LDYxOTU4NzI1MCwtNz
Y1MjMwMzkzLDcxNDEyLDg0NjQ0NjE4MiwxOTkwNzEyNTQ2LDEz
Mzg0OTQwNTcsLTE3Nzc2MjY0MDksLTg2ODM4MDMwOCwtNDY4MD
Y3NjM2LC0xODgwMjE5NzgwLC0yMzg0MDI4NjQsLTE4ODAyMTk3
ODBdfQ==
-->
