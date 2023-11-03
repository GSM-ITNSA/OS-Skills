# DO IT!

# SSH ( Secure Shell Protocol )

- 여기선 Linux Open SSH를 사용하여 구성 할 것이다.

---

# SSH란 무엇인가?

- 네트워크 프로토콜 중 하나로 OSI 7계층 중 7계층에서 동작하는 프로토콜이다.
- 컴퓨터와 컴퓨터가 인터넷과 같은 Public Network를 통해 서로 통신을 할 때 보안적으로 안전하게 통신하기 위해 사용하는 프로토콜이다.
- 대표적으로 `원격접속`, `데이터 전송`을 할 때 주로 사용된다.

```markdown
데이터 전송 : git 같은 소스코드 관리 프로그램에 PUSH 할 때 SSH를 활용하여 파일을 전송한다.
원격접속 : 클라우드 서비스에서 인스턴스 디바이스에 접속 할 때 SSH를 활용하여 접속한다.
```

- FTP나 Telnet같은 경우에는 데이터들을 직접적인 네트워크로 주고받기 때문에 로그인 정보를 교환한다면 누구나 그 정보를 확인 할 수 있어 `보안`이 상당이 취약하다.
- SSH는 그럼 어떻게 서로 다른 컴퓨터가 통신하는 걸까 ?

---

## Private Key and Public Key

- 기본적으로 SSH는 한 쌍의 Key를 통해 접속하려는 컴퓨터와 인증 과정을 거치게 된다.
    - Private Key
    - Public Key

---

## Public Key

- Public Key는 공개되어도 비교적 안전한 Key이다.
- 이 Public Key를 통해 메시지를 전송하기 전 암호화를 하게 된다. Public Key는 암호화만 가능하지 복호화는 불가능하다.

## Private Key

- 그리고 이와 쌍을 이루는 Private Key는 절대로 외부에 노출이 되어서는 안되는 Key로 본인의 컴퓨터 내부에 저장하게 되어있다. 이 Private Key를 통해서 복호화를 하는것이다.

## &

- 먼저 SSH Client에서 한 쌍의 Key를 생성한다.
- 그리고 접속하고자 하는 SSH Server에 자신의 Public 키를 복사하여 저장한다.
- 그럼 SSH Server는 Client의 Public Key로 암호화를 하게 되고, 이걸 복호화를 할 수 있는 대상을 동일한 키 쌍을 가지고 있는 SSH Client 뿐인것이다.

---

## SSH Option

- SSH의 주요 옵션들이다. 더 자세한 옵션을 알고싶으면 `man ssh`로 찾아보는것을 추천한다.

```markdown
SSH [option]

-1 : SSH version 1을 사용한다.
-2 : SSH version 2를 사용한다.
-4 : IPv4를 사용한다.
-6 : IPv6를 사용한다.
-i : 공개키 인증시 사용되며, 사용할 개인키 파일을 지정할 수 있다.
-p : 원격 호스트에 연결할 포트를 지정한다.
-x : x11 연결을 불가능하게 한다.
-l : 원격 접속할 계정을 설정한다.
-v : Debugging Mode를 활성화 한다.
-g,-G : 장비 관련 옵션.
-L : 원격 호스트와 포트에 전송할 로컬 포트를 설정한다.
-R : 로컬 호스트와 지정된 포트로 전송될 원격 포트를 설정한다.
-e : 세션에 대한 이스케이프 문자를 설정한다.
-C : 모든 데이터에 대한 압축을 요청한다.

명령어 사용 예시 ..
다른 명령어 사용 예시는 실습문서에서 더 자세히 설명할 것이다.

// 기본 포트로 접속하기 (22 포트)
# ssh root@1.1.1.1 
# ssh root@HostAddress

// -l 옵션 이용해서 접속하기
# ssh HostAddress -l root

// 다른 포트로 접속하기 (22022 포트)
# ssh root@1.1.1.1 -p 22022

// 원격 접속 후 명령문 실행
# ssh root@1.1.1.1 netstat -ntap

// 공개키 인증을 통해 원격 접속하기(개인키 지정)
# ssh -i ssh_key root@1.1.1.1
```

## SSH Agent

- 쉽게 말해 Private Key를 Memory에 저장하는 프로그램이다.
- Memory의 저장된 Key들은 Client 들이 사용할 수 있다.
- SSH Agent는 SSH Client에게 직접 Private Key를 노출시키지 않는다.
- 또한 SSH Agent를 사용하면 SSH Key를 사용하여 원격 서버에 접속할 때 비밀번호를 자꾸 물어보지 않게 할 수 있다.

```markdown
이게 무슨 말인가요 ??

* SSH Key 생성시 비밀번호를 입력하면 Key를 이용해 원격 서버에 접속할 때 비밀번호를 물어보는데, 이게 너무 귀찮다.
* ID, PW 넣는게 싫어서 SSH Key를 만들었더니 Key를 만들었더니 또 PW를 요구하는 것이다 ;;
* 이 때, SSH-Agent는 Private Key의 PW를 암호화해 기억해두고 처음 한 번만 Private Key를 입력하면 다음부터는 기억해놓은 PW를 사용한다.
* 그러므로 사용자는 또 PW를 입력하지 않아도 된다.
```

### SSH Agent Forwarding

- SSH Agent Forwarding은 Client가 원격 Server에 접속 한 후 해당 원격 서버를 통해 다른 서버에 접속할 때 SSH Agent를 사용할 수 있게 해주는 것이다.
- 자세한 내용과 구현은 실습을 하면서 설명할 예정이다.