# HTTP

# HTTP (HyperText Transfer Protocol)이란 ?

- Text 기반의 통신 규약으로 `인터넷 환경에서 Data를 주고받을 수 있는 Protocol`이다.
- `HTTP`라는 규약을 정해두었기 때문에 모든 프로그램이 이 규약에 맞춰 개발하므로 서로 정보를 쉽게 교환할 수 있다.

---

## HTTP의 기본 동작

<img src="./Image/Web1.png" alt="Alt123" width="600">


- Client 즉, 사용자가 Browser를 통해서 어떠한 서비스를 `URL`을 통하거나 다른 것을 통해서 `Web Server에 Request`(요청)를 하면 Server는 해당 요청 사항에 맞는 결과를 찾아서 `사용자에게 응답(Response)`하는 형태로 동작한다.

```markdown
요청 : Client -> Server
응답 : Server -> Client
```

- `HTML 문서`만이 `HTTP 통신`을 위한 유일한 정보 문서는 아니다.
- Plain Text로 `JSON` 데이터 및 `XML`과 같은 형태의 정보도 주고 받을 수 있으며, 보통은 Client가 Data를 HTML 형태로 받고 싶은지 JSON 형태로 받고 싶은지 Client에서 명시해주는 경우가 대부분이다.

```markdown
HTTP Message에 담아서 전송할 수 있는 것.

* HTML,TEXT
* Image,File,음성,영상
* JSON,XML

- 사실 거의 모든 데이터를 주고 받을 수 있다.
- 서버 간에 데이터를 주고받을 때도 HTTP를 사용한다.
```

---

## HTTP의 특징

### 1. Client - Server 구조

<img src="./Image/Web2.png" alt="Alt123" width="600">


- HTTP Message는 `HTTP Server - HTTP Client`에 의해 해석이 된다.
- Client가 Server에 Request(요청)을 보내면 Server는 그에 맞는 Response(응답)를 보내주는 `Client-Server` 구조이다.

### 2. 무 상태 프로토콜 (Stateless Protocol)

- HTTP에서는 Server가 Client의 상태를 보존하지 않는다.
    - 여기서 말하는 State란 Client와 Server가 주고받는 모든 Data를 말한다.

```markdown
이게 무슨 말이냐?

* 각각의 Client 요청이 Server에 도착할 때마다 Server는 그 요청을 이전 요청과 별개로 처리한다는 것이다.
* 잘 이해가 안될 수 있으니 예시를 들어보겠다.

예시

1. 장바구니 예시

Stateless 
- Client가 장바구니에 상품을 추가하면 Server는 그 요청에 대한 응답으로 "이 상품은 장바구니에 추가되었습니다!" 라고 알려준다.
- 하지만 Stateless는 다른 상품을 장바구니에 추가하려면 이전에 장바구니에 추가하였던 상품을 다시 알려줘야한다.
- 이렇게 이전 요청과는 아예 독립적으로 처리되는 것이 Stateless이다.

Stateful
- Client가 장바구니에 상품을 추가하면 Server는 그 요청에 대한 응답으로 "이 상품은 장바구니에 추가되었습니다!" 라고 알려준다.
- Stateful은 추가한 상품의 정보를 Server 측에서 기억하고 있는다.
- 그러므로 Client는 다른 상품을 장바구니에 추가할 때 Server 측은 이전 요청을 기억하고 있으므로 이전 상품을 알려주지 않아도 된다.
```

- 장점 : 서버 확장성이 높다.
    - 응답 Server를 쉽게 변경 할 수 있으므로 무한한 서버 증설이 가능하다. (Scale-out)
- 단점 : Client가 추가 데이터를 전송해야 한다.
    - 위에 예시로 들었던 상황 같은 상황에서 추가 데이터를 전송해야 한다는 단점이 있다.

```markdown
Stateless의 한계

* Login과 같은 User의 상태를 유지해야 하는 서비스라면, Stateless 하나만 사용해서는 부적합하다고 볼 수 있다.
* 그러므로 브라우저 쿠키, Server Session Token 등을 이용해 상태를 유지해야 한다.
```

### 3. 비 연결성 (Connectionless)

### Connection Oriented (연결을 유지하는 모델)

<img src="./Image/Web3.png" alt="Alt123" width="600">


- TCP/IP는 기본적으로 연결을 유지한다.
- 연결을 유지하는 모델에서는 Client가 요청을 보내지 않더라도 계속 연결을 유지해야한다.

→ 이 경우, 연결을 유지하는 `서버의 자원이 계속 소모`된다는 단점이 있다.

### Connectionless (연결을 유지하지 않는 모델)

<img src="./Image/Web4.png" alt="Alt123" width="600">


- HTTP는 TCP를 사용함에도 불구하고 실제 요청을 주고받을 때만 연결을 유지하고                     `응답을 주고 받고 나면 TCP/IP 연결을 끊어버린다.`

→ 이를 통해 최소한의 자원으로 서버를 유지할 수 있다.

- Traffic이 많지 않고, 빠른 응답을 제공할 수 있는 환경에서는 효율적으로 작동한다.
- 하지만 Traffic이 많고, 큰 규모의 서비스를 운영할 때는 `비연결성은 한계를 보인다`

### 비연결성의 한계

- 요청을 주고 받을 때마다 TCP/IP 연결을 새로 맺어야 하므로 **3-way handshake 시간이 추가된다**.
- Web Browser로 사이트를 요청하면 HTML,CSS,JavaScript, 추가 이미지 등 많은 자원이 함께 다운로드 된다.
- 이러한 자원들을 각각 보낼 때마다 끊고 다시 연결하고 이 작업을 반복하면 굉장히 비 효율적이다.

<img src="./Image/Web5.png" alt="Alt123" width="600">

- HTTP 1.0에서는 각각의 자원을 다운로드 하기 위해 연결과 종료를 반복해야 했다.
- 하지만 HTTP1.1부터는 지속 연결이 가능해졌다
---
## 실제 HTTP의 동작 과정

- 위에서 HTTP는 `Stateless`한 프로토콜인 것을 알아보았다.
- 즉, 각 요청은 독립적이며 Client가 Server에게 요청하기 전에 Connect 하는 과정이 필요하다.
- Client는 Server의 응답을 받으면 종료(Close)하게 된다.

```markdown
시나리오 

#  1. 사용자가 www.google.com URL을 Web Browser에 입력하였다.
#  2. 사용자가 https://www.google.com URL을 Web Browser에 입력하였다.

이 때 HTTP 패킷은 어떻게 동작할까 ?
```

---

1. **사용자가 Web Browser에 URL 주소를 입력한다.** 

<img src="./Image/Web51.png" alt="Alt123" width="300">


2. **DNS Server가 Web Server의 Domain 이름에 대한 IP를 알아와 준다.** 
3. **[www.google.com](http://www.google.com) Server와 TCP 연결을 시도한다.** 
    - 3-way Handshaking : Client와 Server 간 신뢰성 있는 연결을 위한 3번의 Packet 교환
4. **Server에게 Get Method를 사용하여 Client는 자신이 원하는 Resource를 요청한다.** 

```markdown
예시

GET /index.html HTTP/1.1		-> 요청문
Host : www.google.com			-> 헤더
```

5. **Server는 Client로부터 받은 Get Request Message에 대한 Response를 만들어 Client에게 보낸다.**

```markdown
예시

HTTP/1.1 200 OK					           -> 상태문

Date: Thu, 12 Feb 2009 06:29:38 GMT 	            -> 헤더 시작
Server: Apache/1.3.29 (Unix) PHP/4.3.4RC3 
X-Powered-By: PHP/4.3.4RC3 
Transfer-Encoding: chunked 
Content-Type: text/html				           -> 헤더 끝

<HTML>							          -> body
<HEAD>
<TITLE> test </TITLE>
</HEAD>
...생략...
```

6. **Server와 Client가 서로 원하는 Data를 주고 받았으면 연결을 해제하는 과정을 거친다.** 
    - 4-way Handshaking : 서버와 클라이언트 양쪽 다 연결이 종료 시킨다는 메시지를 보낸다.
    - (양쪽 다 각각이므로 4번의 Packet 교환이 일어남)
7. **Web Browser가 Response Message의 Body 내용을 Client에게 보여준다.** 

---

- HTTPS도 다 똑같지만 3-way Handshaking을 거치고 TLS Handshaking을 거친다.
- 그 후 Data는 TLS Handshaking으로 생성된 Session Key로 암호화가 되어 통신하게 된다.

```markdown
자세한건 HTTPS 문서를 참조하길 바란다.
```