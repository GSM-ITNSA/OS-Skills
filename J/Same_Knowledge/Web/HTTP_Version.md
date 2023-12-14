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
        - 단일 TCP 연결을 통해 여러 요청과 응답을 병렬로 처리할 수 있다.
        - 여러 요청이 동시에 이루어지더라도 각각의 요청이 서로 Block 되지 않고 효율적으로 처리될 수 있도록 한다.
    3. Stream Prioritization (우선순위 지정)
        - 각각의 요청과 응답에 대해 우선순위를 지정하여 중요한 리소스에 대한 처리를 강조할 수 있다.
        - 웹 페이지의 렌더링을 최적화하고 사용자 경험을 향상시키는데 도움이 된다.
    4. Server Push
        - 서버가 클라이언트의 요청 없이 미리 필요한 리소스를 적극적으로 전송하는 메커니즘을 지원한다.  
        - 클라이언트는 필요한 리소스를 기다리지 않고 빠르게 가져올 수 있다.
    5. Header Compression
        - 불필요한 데이터 전송을 줄이고 대역폭을 절약할 수 있도록 도와준다.