# HTTP

## HTTP(Hyper Text Transfer Protocol) 란 ?
```
텍스트 기반의 통신 규약으로 인터넷, 월드 와이드 웹(WWW)에서 데이터를 주고받을 수 있는 프로토콜이다.

이렇게 규약을 정해두었기 때문에 모든 프로그램이 이 규약에 맞춰 개발해서 서로 정보를 교환할 수 있다.

주로 HTML 문서를 주고 받는 데 사용된다.
```

## 특징
- HTTP Message 는 HTTP Server와 HTTP Client에 의해 해석 된다.

- TCP/IP를 이용하는 응용 프로토콜이다.

- HTTP는 연결 상태를 유지하지 않는 비연결성 프로토콜이다. (이러한 단점을 해결하기 위해 Cookie와 Session이 등장하였다.)

- 클라이언트/서버 모델이기 때문에 클라이언트는 요청(Request)하고, 서버는 응답(Response)하는 방식이다.

### Request
```
클라이언트가 서버에게 연락하는 것을 요청이라 한다.
```
#### Request Method (요청의 종류, 흔하게 사용하는 Method 4가지)

- GET : 
    - `리소스 조회`
    - 리소스를 요청할 때 사용
- POST : 
    - `데이터 전송`
    - 리소스의 생성을 요청할 때 사용
- PUT : 
    - `리소스 업로드 또는 생성`
    - 리소스의 수정을 요청할 때 사용
- DELETE : 
    - `리소스 삭제`
    - 리소스의 삭제를 요청할 때 사용

#### Request Message
ex)
<img src="./Images/HTTP_Request_Message.png" width="700">

1. Start Line (첫 줄)
    ```
    첫 줄은 시작줄로 메서드 구조 버전으로 다음과 같이 구성된다.
    ```
    - HTTP Method
    - 요청 대상 URL
    - HTTP 버전
2. Header Field (두 번째 줄부터)
    ```
    두 번째 줄부터는 헤더이며 요청에 대한 정보를 담고 있고 다음과 같이 이루어진다.
    ```
    - Host : 요청을 받을 호스트의 도메인 또는 IP 주소
    - User-Agent : 클라이언트 소프트웨어 정보
    - Content-Type : 요청 본문의 데이터 타입
    - 기타 등등..
3. Blank Line (빈 줄)
    - 헤더와 본문을 구분하는 빈 줄이 삽입된다.

4. Message Body (메시지 본문)
    - 필수는 아니지만, 요청에 데이터가 포함되어야 할 경우에 사용됩니다.
    - 주로 POST 메서드 등에서 사용된다.

### Response
```
서버가 요청에 대한 답변을 클라이언트에게 보내는 것을 응답이라고 한다.
```

#### Status Code 
```
상태 코드에는 굉장히 많은 종류가 있다.
모두 숫자 세 자리로 이루어져 있으며, 아래와 같이 크게 다섯 부류로 나눌 수 있다.

1. 1XX (조건부 응답) : 요청을 받았으며 작업을 계속한다.
2. 2XX (성공) : 클라이언트가 요청한 동작을 수신하여 이해했고 승낙했으며 성공적으로 처리했음을 가리킨다
3. 3XX (리다이렉션 완료) : 클라이언트는 요청을 마치기 위해 추가 동작을 취해야 한다.
4. 4XX (요청 오류) : 클라이언트에 오류가 있음을 나타낸다.
5. 5XX (서버 오류) : 서버가 유효한 요청을 명백하게 수행하지 못했음을 나타낸다.
```

#### Response Message
ex)
<img src="./Images/HTTP_Response_Message.png" width="700">

1. Start Line (첫 줄)
    ```
    첫 줄은 버전 상태코드 상태메시지로 구성되어 있다.
    ```
    - HTTP 버전
    - Status Code
    - Status Message
2. Header Field (두 번째 줄 부터)
    ```
    두 번째 줄부터는 헤더로 응답에 대한 정보를 담고 있다.
    ```
    - Content-Type : Response Body 의 데이터 타입
    - Content-Length : Response Body 의 길이
    - 기타 등등..
3. Blank Line (빈 줄)
    - 헤더와 본문을 구분하는 빈 줄이 삽입된다.
    
4. Message Body (메시지 본문)
    - Request Message와 마찬가지로 필수는 아니지만, 응답에 데이터가 포함되어야 할 경우에 사용된다.
    - HTML 문서, 이미지 등이 여기에 포함될 수 있다.