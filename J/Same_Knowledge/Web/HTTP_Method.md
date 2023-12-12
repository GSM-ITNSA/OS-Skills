# HTTP_Method 

## 종류
```
클라이언트와 서버 사이에 이루어지는 요청(Request)과 응답(Response) 데이터를 전송하는 방식

서버에 주어진 리소스에 수행하길 원하는 행동, 서버가 수행해야 할 동작을 지정하는 요청을 보내는 방법이다.

HTTP 메소드의 종류는 총 9가지가 있다. 이 중 주로 쓰이는 메소드는 5가지로 보면 된다.

"주요 메소드"
GET : 리소스 조회
POST : 요청 데이터 처리, 주로 등록에 사용
PUT : 리소스를 대체(덮어쓰기), 해당 리소스가 없으면 생성
PATCH : 리소스 부분 변경 (PUT이 전체 변경, PATCH는 일부 변경)
DELETE : 리소스 삭제

"기타 메소드"
HEAD : GET과 동일하지만 메시지 부분(Body 부분)을 제외하고, Status Line과 Header 반환
OPTIONS : 대상 리소스에 대한 통신 가능 옵션(메서드)을 설명(주로 CORS에서 사용)
CONNECT : 대상 리소스로 식별되는 서버에 대한 터널을 설정
TRACE : 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행
```

## GET
- `리소스 조회 메서드` [READ]
- 만일 서버에 전달하고 싶은 데이터는 `쿼리스트링`를 통해서 전달
    - ex) GET /members/100?username=inpa&height=200
- 쿼리스트링 외에 메시지 바디를 사용해서 데이터를 전달할 수 있지만, 서버에서 따로 구성해야 되기 때문에 지원하지 않는 곳이 많아서 권장하지 않음
- 조회할 때 POST도 사용할 수 있지만, GET 메서드는 캐싱이 가능하기에 GET을 사용하는 것이 유리하다.

### 정적 데이터 조회 과정
---
1. 클라이언트에서 `/members/100`으로 100번 맴버를 조회해서 정보를 달라고 GET 요청
<img src="./Images/HTTP_Method_GETStatic.png" width="700">

2. 서버에서는 요청 메세지를 분석해 내부의 유저정보를 조회한 뒤 결과 Response를 만든다.
<img src="./Images/HTTP_Method_GETStatic2.png" width="700">

3. 서버에서 클라이언트로 응답을 해준다. 클라이언트에서 정상적으로 받으면 200 OK Status를 가지며, 회원정보를 얻게 된다.
<img src="./Images/HTTP_Method_GETStatic3.png" width="700">

### 동적 데이터 조회 과정
---
1. 요청 URL 뒤에 ?q=hello&hl=ko 쿼리 파라미터를 줘서 상세한 조회 데이터를 얻는다.
<img src="./Images/HTTP_Method_GETDynamic.png" width="700">

2. 서버는 요청에 따라 데이터베이스나 다른 소스로부터 데이터를 가져와서 동적으로 페이지를 생성한다.

3. 서버는 생성된 페이지를 클라이언트에게 응답으로 전송한다.

### 정적 조회와 동적 조회 차이점
```
정적 데이터는 미리 만들어져 있어 변하지 않고, 여러 클라이언트에게 동일한 내용을 제공한다.

동적 데이터는 요청 시에 생성되며, 데이터 소스에 따라 결과가 달라질 수 있다.
동적 데이터는 사용자에 따라 다른 컨텐츠를 제공할 수 있다.

웹 애플리케이션에서는 정적 데이터와 동적 데이터를 조합하여 다양한 형태의 콘텐츠를 제공하는 것이 일반적이다.
```

### HTML Form 데이터 조회 과정
---
- HTML Form 태그 문서로 사용자와 UI로 상호작용하여 서버와 통신
- HTML Form 전송은 GET, POST만 지원
1. 웹문서에서 폼 입력칸에 데이터를 적고 전송 버튼을 누른다.
<img src="./Images/HTTP_Method_GETFORM.png" width="400">

2. 지정한 GET 메서드 동작에 따라 input 태그안에 들어간 값들이 쿼리스트링으로 서버로 전달된다.
<img src="./Images/HTTP_Method_GETFORM2.png" width="700">

## POST
- `전달한 데이터 처리/생성 요청 메서드` [CREATE]
- Message Body를 통해 서버로 요청 데이터를 전달하면 서버는 요청 데이터를 처리하여 업데이트 한다.
- 전달된 데이터로 주로 신규 리소스 등록, 프로세스 처리에 사용한다.

### JSON 데이터 전송 과정
---
1. 클라이언트는 Body에 등록할 회원 정보를 JSON 형태로 만들어 담고 서버로 전송한다.
<img src="./Images/HTTP_Method_POSTJSON.png" width="700">

2. 서버에서는 받은 메세지를 분석해 로직 대로 처리 한다. 예를 들어 데이터베이스에 등록하고 신규 아이디를 생성한다.
<img src="./Images/HTTP_Method_POSTJSON2.png" width="700">

3. 신규회원에 대한 데이터를 Body에 담아서 클라이언트로 응답한다.
<img src="./Images/HTTP_Method_POSTJSON3.png" width="700">

### HTML Form 데이터 전송 과정
---
1. 웹문서에서 폼 입력칸에 데이터를 적고 전송 버튼을 누른다.
<img src="./Images/HTTP_Method_GETFORM.png" width="400">

2. 지정한 POST 메서드 동작에 따라 input 태그안에 들어간 값들이 쿼리스트링으로 서버로 전송된다.
<img src="./Images/HTTP_Method_POSTFORM.png" width="700">

### 파일 데이터 전송 과정
---
- enctype을 `multipart/form-data` 로 작성해 해당 폼에 파일이 있다는 것을 표시한다.
- Binary 데이터 전송시 사용한다.
- `multipart/form-data` 형식이라면 HTTP 메세지에 임의의 구분자(------XXX)가 FORM 데이터간 구분을 지어준다.
- 여러 개의 Content-Type에 대한 데이터를 보낼 수 있다.

<img src="./Images/HTTP_Method_POSTFILE.png" width="700">

## PUT
- `리소스 대체(수정)하는 메서드` [UPDATE]
- 