# URI / URL / URN

## URI
- Uniform Resource Identifier

    - Uniform : 리소스를 식별하는 통일된 방식
    - Resource : 자원, URI로 식별할 수 있는 모든 것
    - Identifier : 다른 항목과 구분 / 식별 하는데 필요한 정보
- 문법 : scheme://[userinfo@]host[:port][/path][?query][$fragment]
- 예시 : https://www.google.com:443/search?q=hello&hl=ko
- 구성
  - scheme : 주로 프로토콜을 명시 [ http/https ]
  - userinfo : URL에 사용자정보를 포함해서 인증 -> 거의 사용하지 않음
  - host : 호스트명으로 도메인명이나 IP 주소를 직접 사용 가능
  - port : http 는 80 / https 는 443 ,생략 가능하며 다른 포트도 사용 가능
  - path : 리소스 경로, 보통 계층적 구조를 가지도록 설계
  - query : key=value 형태로 값을 나타냄, query parameter, query string으로 불림
  - fragment : html 내부 북마크 등에 사용 (서버에 전송하는 정보는 아님)

## URL
- Uniform Resource Locator
- 리소스가 있는 위치

## URN
- Uniform Resource Name
- 리소스에 부여한 이름
- URN 이름만으로 실제 리소스를 찾는 방법이 보편화되지 않았음
    - URI / URL만 우리는 인지하고 있으면 됨