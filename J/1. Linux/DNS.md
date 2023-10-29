# BIND9_basic
### What is BIND
```
BIND는 DNS 서비스를 위한 모든 기능을 갖춘 확장 가능한 오픈 소스 소프트웨어
BIND9은 DNS 네임 서버를 구축하고 레코드를 관리할 수 있도록 도와주는 패키지
```
### BIND9 Configuration File
```
named.conf 파일은 BIND9의 기본 구성 파일이다.
/etc/bind/named.conf.options 파일에는 구성에 필요한 옵션을 지정할 수 있는 위치에 대한 참조가 포함되어 있으며 네 가지를 수정하여 BIND9을 구성할 수 있다.

1. acl <acl 이름> {<범위>} : LAN을 정의하는 지시문
(정의 하지 않으면 모든 IP 주소로부터 DNS 쿼리를 허용하는 기본 동작을 따름) 

2. allow-query {<범위>} : 서버에 DNS 쿼리를 보낼 수 있는 IP 주소를 정의하는 지시문
(정의 하지 않으면 기본적으로 모든 클라이언트의 DNS 쿼리를 허용함)

3. forwarders {<범위>} : 이 서버가 재귀 쿼리를 전달할 DNS 서버를 정의하는 지시문
(정의 하지 않아도 recursion 방식으로 동작)

4. recursion <yes/no> : 서버에 대한 재귀적인 DNS 쿼리를 허용하는 지시문 
(recursion no 를 할 경우 iterative DNS 쿼리를 허용함)
(기본 동작 방식은 recursion yes)

모든 configuration 이 끝난 경우 bind9 을 재시작 해줘야 한다.
```

### Client Configuration
```
1. IP 와 local server address 를 정의
2. nslookup 을 통해 쿼리가 되는지 확인
```
