# HTTP_Version

## [ HTTP 0.9 ]

- HTTP 초기 버전을 구분하기 위해 부르는 버전 (1991년)
- 요청은 단일 라인으로 구성되며, 리소스에 대한 Method는 GET만 존재
- 응답도 극도로 단순 (파일 내용 자체로만 구성)
- HTTP 헤더도 없고, HTML파일만 전송 가능했던 것이 특징
    ```html
    \* 요청 */
    GET /mypage.html

    \* 응답 */
    <HTML>
    A very simple HTML page
    </HTML>
    ```

## [ HTTP 1.0 ]
- 특징
    - HTTP Header 개념이 도입되어 요청과 응답에 추가되며, 메타데이터를 주고 받고 프로토콜을 유연하고 확장 가능하도록 개선됨 (1996년)
    - 버전 정보와 요청 Method가 함께 전송되기 시작
    - Status Code Line도 응답의 시작부분에 추가되어 브라우저 요청의 성공과 실패를 파악 가능해짐 (해당 결과에 대한 로컬 캐시 갱신 등의 사용이 가능해짐)
    - Content-Type 도입으로 HTML 이외의 문서 전송 기능이 가능해짐
    
- 한계
    - 커넥션 하나당 요청 하나와 응답 하나만 처리 가능했음
        - 매우 비효율적인 동작이며, 서버 부하도 문제
        - HTTP 1.1에서 개선
    ```HTML
    \* 요청 */
    GET /mypage.html HTTP/1.0
    User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)

    \* 응답 */
    200 OK
    Date: Tue, 15 Nov 1994 08:12:31 GMT
    Server: CERN/3.0 libwww/2.17
    Content-Type: text/html
    <HTML>
    A page with an image
        <IMG SRC="/myimage.gif">
    </HTML>
    ```

## [ HTTP 1.1 ]
- 특징
    - 1997년 등장
    - Persistent Connection 추가
        - 지정한 Timeout동안 커넥션을 닫지 않는 방법을 통해 커넥션의 사용성이 높아짐
    - Pipelining 추가
        - 앞 요청의 응답을 기다리지 않고 순차적인 여러 요청을 연속적으로 보내고 그 순서에 맞춰 응답을 받는 방식이 등장
        - 순차적으로 하나씩 요청/응답이 처리되는 기존 방식을 개선
        - 하나의 커넥션에 요청이 들어 있을 뿐, 동시에 여러개의 요청을 처리해 응답으로 보내주는 것은 아니다 (multiplexing 되지는 않음)
- 한계
    - Head Of Line Blocking (HOL)
        - 결국 앞 요청의 응답이 너무 오래걸리면 뒤 요청은 Blocking 되어 버림
    - Header 구조의 중봅
        - 연속된 요청의 헤더의 많은 중복이 발생
    
    ```HTML
    \* 요청 */
    GET /en-US/docs/Glossary/Simple_header HTTP/1.1
    Host: developer.mozilla.org
    User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:50.0) Gecko/20100101 Firefox/50.0
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
    Accept-Language: en-US,en;q=0.5
    Accept-Encoding: gzip, deflate, br
    Referer: https://developer.mozilla.org/en-US/docs/Glossary/Simple_header

    \* 응답 */
    200 OK
    Connection: Keep-Alive
    Content-Encoding: gzip
    Content-Type: text/html; charset=utf-8
    Date: Wed, 20 Jul 2016 10:55:30 GMT
    Etag: "547fa7e369ef56031dd3bff2ace9fc0832eb251a"
    Keep-Alive: timeout=5, max=1000
    Last-Modified: Tue, 19 Jul 2016 00:59:33 GMT
    Server: Apache
    Transfer-Encoding: chunked
    Vary: Cookie, Accept-Encoding

    (content)
    ```

## [ HTTP 2.0 ]
- 설명
    - 기존 HTTP 1.X 버전의 성능 향상에 초점을 맞춘 프로토콜 (2015년 등장)
    - 표준의 대체가 아닌 확장 (표준 : HTTP 1.1)
- 특징
    1. HTTP 메시지 전송 방식의 전환
    2. Multiplexed Streams (다중화 스트림)
    3. Stream Prioritization (우선순위 지정)
    4. Server Push
    5. Header Compression

### HTTP 메시지 전송 방식의 전환
```
기존 : 
    일반 텍스트 형식

개선 :
    Binary Framing 계층을 추가해서 보내는 메시지를 프레임(Frame)이라는 단위로 분할하여 추가적으로 바이너리로 인코딩한다
    (바이너리 형식 사용으로 파싱속도 및 전송속도가 빠르고 오류 발생 가능성이 낮아진다.)
```

### Multiplexed Streams
```
기존 :
    HTTP 1.1의 Pipelining 으로 하나의 커넥션에 여러 요청이 있지만, 
    결국 동시에 여러 요청을 처리해 응답으로 주지는 못했다.

개선 :
    - 구성된 연결 내에 전달되는 바이트의 양방향 흐름을 의미하는 Stream으로 요청/응답이 교환된다. 
    (하나의 커넥션 안에 여러개의 Stream 존재 가능)
    - 메시지가 이진화된 텍스트인 프레임으로 나뉘어 요청마다 구분되는 Frame을 통해 전달한다.

    -> 동시에 여러 요청을 처리하는 것이 가능해짐
    -> Stream을 통해서 각 요청의 응답의 순서가 의미가 없어져서 HOL Blocking이 자연스럽게 해결됨
```

### Stream Prioritization
- 리소스간 우선순위를 설정하는 기능
- Stream에 우선순위를 부여해서 순위에 맞게 전달되는 것이 가능해짐

### Server Push
- 단일 클라이언트 요청에 여러 응답을 보낼 수 있는 특징을 통해 Server에서 client에게 필요한 추가적인 리소스를 push해주는 기능

### Header Compression 
```
기존 :
    연속된 요청의 경우 많은 중복된 헤더의 전송으로 오버헤드가 많이발생했다.

개선 :
    요청과 응답의 헤더 메타데이터를 압축해서 오버헤드를 감소

```

### HTTP 2.0의 한계

- 각 요청마다 Stream으로 구분해서 병렬적으로 처리하지만, 결국 이에는 TCP 고유의 HOL Blocking이 존재한다.
  
- 왜냐하면, 서로 다른 Stream이 전송되고 있을 때, 하나의 Stream에서 유실이 발생하거나 문제가 생기면 결국 다른 Stream도 문제가 해결될 때 까지 지연되는 현상이 발생되기 때문이다.

- 이 문제를 위해 QUIC / HTTP3.0 이 등장했다.

## [ QUIC / HTTP 3.0 ]
- QUIC ?
    - Google 에서 개발한 UDP 기반의 전송 프로토콜 (Quick UDP Internet Connections)
    - TCP의 구조적 문제로 성능 향상이 어렵다고 판단하여 UDP 기반을 선택
    - QUIC 은 TCP 의 3-way-handshake 과정을 최적화 하는 것을 초점으로 두고 개발 되었다 (QUIC은 3-way-handshake를 간소화한 Quick HandShake를 사용)
    - QUIC은 TCP의 Stream은 하나의 chain으로 연결되는 것과 다르게 각 Stream당 독립된 Stream chain을 구성하여 TCP HOL Blocking을 해결하였다

- HTTP 3.0
    - QUIC 기반으로 나온 새로운 HTTP 메이저 버전