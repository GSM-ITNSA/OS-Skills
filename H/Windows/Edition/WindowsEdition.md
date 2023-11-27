# Windows Edition 차이

Windows 10을 기준으로 여러 Edition이 존재한다. 

Windows Edition들은 Server와 Client의 Edition으로 구분된다. 

어떤 Edition들이 있는지 알아보자. 

---

# Windows Server Edition

## Windows 10 Home

- 일반 가정용으로 출시되는 제품이다.
- 아래는 Home Edition의 특징이다.
1. **사용 편의성** 
    - 전체 화면 시작 메뉴를 포함한 **Start Menu**를 제공한다.
    - 직관적인 Interface와 간단한 설정으로 사용자가 쉽게 System을 관리 할 수 있게 한다.
2. **Cortana 전자 비서**
    - Cortana라는 전자 비서를 활용하여 음성을 이용한 다양한 서비스를 이용할 수 있게 한다.
3. **Microsoft Edge**
    - Home Edition은 기본적으로 Microsoft Edge가 기본적인 Home page로 작동한다.
    - 위의 Cortana 전자 비서와도 통합 할 수 있다.
4. **기능적 한계**
    - Home Edition은 Enterprise 수준의 기술들이 지원되지 않는다.
    - 따라서 Bitlocker, Active Directory, Hyper-v 같은 기술을 제공하지 않는다.

## Windows 10 Pro

- Home Version에 비해, 공유와 관련된 기능이 많으며, **일부 기업용** 기능을 제공한다.
- 아래는 Pro Edition의 특징이다.
1. **가상화 및 Hyper-v** 
    - Home Edition과 다르게 가상화를 지원한다.
    - 가상화 환경에서 Server를 구축하고 애플리케이션을 실행 할 수 있다.
2. **Bitlocker Disk 암호화**
    - Bitlocker를 사용하여 Disk 암호화 기능을 지원한다.
    - 이는 Disk Data를 암호화하여 Data 보안을 향상 시킨다.
3. **Group Policy** 
    - Group Policy를 사용하여 컴퓨터 및 사용자 설정을 중앙에서 효율적으로 관리 할 수 있다.
4. **Remote Desktop Service**
    - 또한, Pro Edition은 원격으로 Server와 Computer에 접근하여 애플리케이션을 실행하거나 관리 할 수 있다.

## Windows Enterprise

- 대규모의 기업을 위한 Edition Version이다.
- 아래는 Enterprise Edition의 특징이다.
1. **다양한 가상화 지원**
    - Hyper-v를 포함하여 Live Migration 등 여러 가상화 기술을 지원한다.
2. **Shielded Virtual Machines**
    - VM의 보안을 강화하기 위한 기능으로, VM 및 Data를 암호화 한다.
3. **Clustering 및 High Available**
    - Enterprise Edition은 Fail Over Clustering을 지원하여 HA를 지원한다.
4. **Active Directory 확장 기능** 
    - 더 많은 Active Directory 기능과 관리 도구를 지원한다.

## Windows Education

- Windows 10에서 최초로 교육 기관용 Edition이 출시된다.
- Enterprise Version의 `Long Term Servicing Branch` 기능을 제외하면 모두 동일하다.

---

# Windows Client Edition

## Windows Standard Edition

- Standard Edition은 기업용 Server OS로 주로 많이 사용이 된다.
- 다음은 Standard Edition에서 지원하는 주요한 기능들이다.
1. **Hyper-v** 
    - Standard는 License를 활용하여 가상 머신 2개를 무료로 사용할 수 있다.
2. **Server 역할 및 기능**
    - File Server, DHCP, DNS 등 여러 Server 역할을 호스팅 할 수 있다.
3. **Storage Service** 
    - Storage 관리를 위한 Storage 기술을 다양하게 지원한다.
4. **Remote Desktop Service**
    - 원격으로 Server에 접속하고 애플리케이션을 실행 할 수 있다.
5. **PowerShell 자동화**
    - Powershell을 사용하여 Server 관리 및 자동화 작업을 수행할 수 있다.

## Windows Datacenter Edition

- **Windows Datacenter**는 **Standard**가 지원하는 기술을 모두 지원하면서,  더 높고 많은 기술을 지원한다.
- 다음은 더 나은 기술을 지원하는 예시이다.
1. **무제한 가상화**
    - License를 활용하여 기존의 2개가 아닌 가상 머신을 무제한으로 구성할 수 있다.
2. **Shield Virtual Machine**
    - VM의 보안을 강화하기 위한 기능으로, VM 및 Data를 암호화 한다.
3. **Clustering**
    - High Available 및 Load Balancing을 위한 Clustering 기능을 지원한다.
4. **Host Guardian Service**
    - [2]번의 기술과 함께 사용된다.
    - Host OS와 VM 간의 신뢰성을 확인하여 보안을 강화한다.
5. **Storage Replica**
    - 여러 Site 간에 Data를 동기화 하여 Failover 기능을 수행할 수 있다.