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