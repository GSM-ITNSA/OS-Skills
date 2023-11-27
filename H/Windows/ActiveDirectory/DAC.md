# AD DAC (Dynamic Access Control)

**동적 Access Control은 무엇일까 ?**

## DAC의 개요

Domain 기반의 DAC를 사용하여 Administrator는 Resource의 접근 제어를 보다 구체적으로 설정 할 수 있다. 

```markdown
DAC를 사용하는 예시 

사용자 1 : (회사 사무실에서 Resource에 Access 하려고 시도)
사용자 2 : (가정에서 Resource에 Access 하려고 시도)
(이러한 상황에서는 사용자 마다 접근 권한이 달라질 수 있다.)

DAC를 사용하는 예시 2 

Administrator가 설정해둔 네트워크 보안 정책을 통과해야 Resource를 접근하도록 설정 할 때
```

위와 같은 상황처럼 각각의 사용자마다 Access 권한이 분류 될 수가 있다. 

아래는 DAC의 주요 개념과 이어져 있는 중요한 이론이다. 

1. **중앙 액세스 규칙**
2. **중앙 액세스 정책**
3. **Claim - 클레임**
4. **조건** **식**

---

## 중앙 액세스 규칙

중앙 액세스 규칙은 **User Group, User Claim, Device Claim 및 Resource 속성**과 관련된                  `하나 이상의 조건을 포함` 할 수 있는 **권한 부여 규칙 식**이다. 

- 여러 중앙 액세스 규칙 → 단일 중앙 액세스 정책

Domain에 대해 하나 이상의 중앙 액세스 규칙이 정의 되었을 경우, Admin은 **특정 규칙**을                 **특정 Resource**에 맞출 수 있다. 

ex ) [skill.com](http://skill.com) Domain은 신뢰된 Domain 일 때 ..

- C:\Secret\secret.txt     -      [skill.com](http://skill.com) 도메인 Member만 접근 가능

## 중앙 액세스 정책

중앙 액세스 정책은 **조건식을 포함**하는 **권한 부여 정책**이다.

**중앙 액세스 정책**은 전반적인 보안 원칙과 방향성을 나타내고,                                                          **중앙 액세스 규칙**은 이러한 원칙을 구체적으로 구현하는 규칙을 정의한다. 

```markdown
예시 

**중앙 액세스 정책** 

정책 설명 : 모든 기업 내 직원은 강력한 암호를 사용해야 한다. 
적용 범위 : 모든 사용자 및 시스템에 대한 Access 규정
목적 : 전반적으로 보안을 향상시키고, 일관된 보안 표준을 유지하기 위한 정책

**중앙 액세스 규칙**

규칙 설명 : Intranet Server에서 외부에서 들어오는 Traffic은 80 Port만 허용한다. 
적용 범위 : 특정 Server에서 적용되는 Traffic 허용 규칙.
목적 : 서버에 대한 특정 보안 규칙을 정의하여 외부에서의 액세스를 제한.

요약하자면 ...

"중앙 액세스 정책"은 조직 전체의 보안 정책을 일반적으로 설명하고, "중앙 액세스 규칙"은 특정 장비나 시스템에서 적용되는 특정 규칙을 구체화합니다.
```

## Claim - 클레임

**Claim**은 DC에서 게시한 User, Device 또는 Resource에 대한 **고유한 정보**이다. 

**사용자의 이름**, **File이 속해있는 부서** 등이 `Claim`의 예시이다. 

Entity는 둘 이상의 Claim을 포함할 수 있으며, Claim 결합을 통해 Resource에 대한 Access 권한을 부여할 수 있다.

- 둘 이상의 Claim 포함 예시 : [기능 부서 Lee Hyeonjun]
    1. 이름 Claim - Lee Hyeonjun
    2.  부서 Claim - 기능 부서
- Claim 결합의 예시
    
    ```markdown
    A 사용자
    
    이름 : JongHan
    역할 : 관리자 
    부서 : IT 부서
    
    B 사용자
    
    이름 : Hyunjun
    역할 : 사용자
    부서 : 마케팅 부서
    
    C 사용자 
    
    이름 : Seongho
    역할 : 관리자 
    부서 : 마케팅 부서
    
    C 사용자는 A 사용자와 B 사용자의 Claim을 사용하여 자신의 Claim 정보를 얻을 수 있게 되었다.
    이게 바로 Claim 결합이다. 
    ```
    

아래와 같은 Claim 유형은 지원되는 Windows Version에서 사용할 수 있다.

**User Claim**

- 특정 사용자와 관련된 Active Directory 특성이다.
- **이름, 역할, 부서, 이메일** 등등 ….

**Device** **Claim**

- 특정 Computer 개체와 관련된 Active Directory 특성이다.
- **장치 유형(Desktop,Phone),운영 체제(Mac OS), MAC 주소(고유 식별자)**

**Resource 특성**

- Resource에 대한 Access 권한을 나타내는 정보이다**.**
- **Resource 유형(Database), Resource 소유자(Lee Hyeonjun),Resource Group(IT 부서)**

## 조건 식

조건 식은 특정 조건이 충족되면 Resource에 대한 Access 권한을 허용하거나 거부하는 향상된 Access 제어 관리 기능이다. 

일반적으로 조건 식은 아래와 같은 형태이다. 

`조건 식 = 속성 비교 연산자 값`

```markdown
조건 식 예시

1. **역할 기반 조건 식**
사용자의 역할 Claim = 관리자

2. **사용자의 속성 기반 조건 식**
사용자의 직책 Claim = Manager

3. **사용자의 위치 기반 조건 식**
사용자의 위치 = 회사 내부

등등이 있다. 

이런식으로 **조건 식 = 속성 비교 연산자 값** 으로 이루어져 있다
```