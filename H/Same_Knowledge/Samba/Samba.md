# What is SMB ?

<img src="./Image/S1.png" alt="Alt123" width="600">


- Samba는 쉽게 말해 OS가 다른, 즉 Windows와 Linux 사이의 `접근을 쉽게하기 위해 도와주는 프로그램`이다.
- Samba를 사용하게 되면 Windows에서 Linux Server에 탐색기처럼 접근하여 File을 쉽게 읽고 쓸 수 있다.

```markdown
예시

우리 회사의 Server는 Linux로 구성이 되어있을 때, 회사에서 일 열심히 하라면서 Windows 노트북을 줬다고 가정하겠다.
이 때 Linux Server에 업로드 해놓은 File을 Windows에서 사용하고 싶다. 
또한 반대로 Windows 컴퓨터에서 작업한걸 Linux에서 사용하고 싶어 할 수도 있다.
```

- 이렇게 Windows 시스템이 다른 시스템의 Disk 혹은 Printer 등의 자원을 공유 가능하게 끔 만든 프로토콜이 `SMB` 이다.
- 즉, Samba는 일종의 `공유 폴더`이다.

```markdown
예시

Linux 환경에서 Windows의 기술인 Active Directory를 사용하고 싶을 때 Samba를 사용할 수 있다.
하지만 이때는 DNS 엔진을 Linux의 엔진을 사용해야하므로 Samba DNS에 관한 Database 파일을 Bind9 config 파일에 Include로 참조해야한다. 
```

- Samba Client는 Samba Server에게 TCP/IP를 사용하여 연결한다.
- 연결이 설정되면 Client는 Share된 자원에 Access 할 수 있다.
- 하지만 SMB는 네트워크를 통해 수행된다.

---

## Samba(2)

<img src="./Image/S2.png" alt="Alt123" width="600">


- Samba는 TCP/IP를 제외한 다른 프로토콜을 통해서도 실행될 수 있다.

---

## Samba NetBIOS

- 현재는 순수한 NetBIOS Interface는 사용되지 않지만 이전 Windows의 Network는 NetBIOS 기능을 이용하여 구현되었다.
- Windows OS의 내부에서는 NetBIOS 이름을 그대로 “컴퓨터 이름”으로 사용하고 있었다.
- SMB가 TCP/IP를 통해 사용되는 경우에는 NetBIOS 이름을 사용해야 한다.
- NetBIOS 이름은 `최대 15글자` 까지 가능하며 일반적으로는 SMB Server의 이름과 동일하다.

---

## Samba Port Number

- Samba는 TCP/IP 기반의 NetBIOS 프로토콜을 사용한다고 했다.
- Samba의 Server는 크게 2개(smbd,nmbd)의 Process로 나누어져 있다.
- 대부분의 처리는 smbd에서 한다. 하지만 Windows 사용자의 Computer 이름으로 접속하게 하려면 nmbd를 사용해야한다.

```markdown
nmbd : TCP-139 / UDP-137,UDP-138 사용 
```

---

## 여러 Samba Protocol Version

- 각 Version은 다양한 기능 개선과 보안 업데이트를 포함하고 있다.
- 아래는 주요한 Samba Version들이다.

### 1. Samba 1.0

- 1992년 처음 개발된 Samba의 초기 버전이다.
- 기본적인 파일 및 프린터 공유를 제공했다.

### 2. Samba 2.0

- 1999년에 도입된 Version이다.
- `Windows 도메인 인증을 지원`하는 중요한 업데이트를 포함하였다.

### 3. Samba 3.0

- 2003년에 개발된 Version이다.
- Active Directory와의 통합, Group Policy 지원, 파일 시스템 제약 사항 해결 등이 개선되었다.

### 4. Samba 3.5

- 2010년에 개발된 Version이다.
- SMB2 프로토콜의 일부 지원과 성능 향상이 추가되었다.

### 5. Samba 4.0

- 2012년에 개발된 Version이다.
- Active Directory 도메인 컨트롤러로서 기능하는 첫 번째 Version이다.
- 이로써 Samba는 Windows 도메인과의 통합을 완벽하게 지원하게 되었다.

### 6. Samba 4.x

- 2012년 이후에 개발된 Version이다.
- AD 통합 및 보안 업데이트와 같은 다양한 기능이 추가되었다.