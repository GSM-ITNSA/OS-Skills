# AD (Active Directory)

- Network 환경이 커질수록 Object의 개수가 많아지기 때문에 관리하는 것이 어려워진다.
- 사용자가 Resource의 위치(IP 주소)와 해당 Server의 Local 사용자 계정 정보를 알고 있어야        정상적으로 접근 할 수 있다.
- 이와 같은 문제점을 해결하기 위해 중앙 서버에 공통된 Database를 생성한다.
    - 각 Server와 Client는 중앙의 DB를 공유하여 Object를 검색한다.

즉, 중앙에서 사용자 인증 및 권한 부여 처리가 가능하도록 처리해주는 서비스를 **`Directory Service`**  

- Windows에서 사용하는 **Directory Service**를 **`Active Directory`**라고 한다.
- AD는 **LDAP**을 사용하여 AD 상에서 Resource를 효과적으로 검색할 수 있다.

### Object

- **User, Computer, Share Folder, Printer** 등 각종 자원을 의미한다.

### Directory

- **Object** 정보를 저장할 수 있는 정보 저장소를 의미한다.

### Directory Service

- Object를 **생성, 관리, 검색, 사용** 등 유용하게 활용할 수 있는 서비스를 의미한다.

### ADDS (Active Directory Domain Service)

- **Windows Server**에서 제공하는 **Directory Service**를 의미한다.

---

## Active Directory 용어

<img src="./Image/AD1.png" alt="Alt123" width="600">


### 1. 도메인 (Domain)

**Active Directory**의 가장 기본이 되는 단위이다.

- **AD**가 설치된 **Windows Server**가 하나의 `Domain`이라고 보면 된다.
- 관리를 하기 위한 하나의 큰 단위의 범위를 표현하며, 관리를 위해서 지역적인 범위로 구분될 수 있다.
- Domain은 상속 적인 개념으로 부모 Domain과 자식 Domain으로 나뉠 수도 있다.

<img src="./Image/AD2.png" alt="Alt123" width="600">


### 2. 트리 (Tree)

**트리**는 `Domain의 집합`이다. 물리적인 개념보다 논리적인 개념으로 보면 된다.

- 제일 상위의 Root Domain 이름을 가지는 Domain과 계층 구조로 이루어져 있는 구조.

**예시**

Root DC (Parent DC ) : [korea.com](http://korea.com) 

Second DC (Child DC) : busan.korea.com

```json
부모-자식 관계를 Tree 구조라고 할 수 있다. 
```

<img src="./Image/AD3.png" alt="Alt123" width="600">


### 3. 포레스트 (Forest)

**포레스트**는 하나 이상의 Tree의 집합이다. 

- Forest를 만드는 이유는 Tree의  확장이다.

<img src="./Image/AD4.png" alt="Alt123" width="600">

Forest2 : Forest1과 Forest3의 모든 기본 Resource에 Access 할 수 있다. 

Forest1 : Forest2의 모든 기본 Resource에 Access 할 수 있다.

Forest3 : Forest2의 모든 기본 Resource에 Access 할 수 있다. 

**예시**

Forest Root Domain : [example111.co m](http://example111.com) 

Tree DC : [example222.com](http://example222.com) 

약간 요런 느낌 ! 

### 4. Forest Root Domain

- Forest와 동일하지만, 특정 Root Domain에 전체 Forest에 대한 Root 권한을 주는 것이다.