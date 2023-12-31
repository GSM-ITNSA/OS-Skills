# iSCSI

## iSCSI(Internet Small Computer System Interface) 란?
```
인터넷 프로토콜(IP) 기반의 스토리지 네트워킹 표준이며 데이터 스토리지 장치의 연결에 사용
즉, 인터넷을 통해 데이터를 전송하고 보관하게 된다

IP 기반 네트워크로 SCSI 명령을 전달하여 블록 단위의 데이터 전송
NAS 가 파일 공유하는 목적이라면, iSCSI는 스토리지 자체를 1대1로 원격에서 사용하기 위함이다.

서버 역할의 iSCSI Target 과 클라이언트 역할의 iSCSI Initiator로 구분된다.

주로 가상화 환경에서 사용되거나, 중소기업의 중소 및 분산된 IT 환경에서 스토리지를 효율적으로 관리하고 활용하는데 적합하다
```

## iSCSI 장단점

### 장점
```
비용 효율성
    일반적인 IP 네트워크를 사용하기 때문에 별도의 전용 스토리지 네트워크를
    구축할 필요는 없다. 이로써 하드웨어 및 유지보수 비용 절감

구현의 간소화
    IP 기반 프로토콜로서 네트워크의 기술이 풍부하며, 구현 및 관리가 비교적으로 간단합니다.

장거리 연결 가능
    TCP/IP를 사용하므로 지리적으로 떨어진 위치 간에도 스토리지 연결이 가능합니다.
```
### 단점
```
네트워크 부하
    네트워크를 통해 데이터를 전송하므로 네트워크 부하가 발생할 수 있습니다.
    이는 높은 대역폭을 필요로하며, 
    다른 네트워크 트래픽과의 충돌을 방지하기 위해 특별한 주의가 필요하다.

보안 고려 사항
    IP 기반의 프로토콜이므로 네트워크를 통한 데이터 전송 중에 데이터를 
    가로채는 보안 위협이 있을 수 있습니다. 따라서 보안을 강화하기 위해 조치가 필요합니다
```

## iSCSI 용어
1. iSCSI (Internet Small Computer System Interface)
    - 인터넷을 통해 SCSI 프로토콜을 전송하기 위한 표준이자 프로토콜

2. Initator
    - iSCSI 클라이언트를 나타내며, 스토리지 리소스를 요청하는 디바이스

3. Target
    - iSCSI 서버를 나타내며, 스토리지 리소스를 가지고 있고, 이를 제공하는 디바이스

4. IQN (iSCSI Qualified Name)
    - iSCSI 를 식별하는 고유한 이름
    - iSCSI Initiator IQN 이 있음
    - iSCSI Target IQN 이 있음

5. Portal
    - iSCSI 연결에 사용되는 IP 주소 및 포트 번호의 조합을 나타낸다
    - Initiator가 타겟에 연결할 때 사용 된다

6. TPG
    - Target이 여러 개의 IP 주소와 포트 번호를 가질 때, 그 중 하나의 그룹을 나타낸다.
    - 이를 통해 다중 경로(Multipath) 연결을 관리할 수 있습니다.

7. LUN (Logical Unit Number)
    - 논리적인 스토리지 단위를 나타낸다.
    - 하나의 스토리지 시스템에서 여러 개의 LUN을 설정할 수 있다

## 유사한 프로토콜
1. FC (Fibre Channel)
    ```
    유사성 
        iSCSI와 마찬가지로 스토리지 연결을 위한 프로토콜
        하지만 전통적으로 전용의 Fibre Channel 네트워크를 사용합니다

    차이점
        Fibre Channel은 전용 네트워크를 사용함으로 보안이 뛰어나고 성능이 높을 수 있다
        그러나 구축 및 유지보수 비용이 더 높을 수 있다
    ```
---
2. NFS (Network File System)
    ```
    유사성
        iSCSI와 마찬가지로 네트워크를 통해 스토리지를 공유하는 목적을 가지고 있습니다

    차이점
        NFS는 파일 레벨의 스토리지 공유를 제공하는 반면, iSCSI는 블록 레벨 스토리지를 제공
        NFS는 주로 파일 서버와 클라이언트 간 파일 공유에 사용된다
    ```
---
3. FCoE (Fibre Channel over Ethernet)
    ```
    유사성
        Fibre Channel과 Ethernet을 결합하여 스토리지를 전송하는 목적을 가지고 있다

    차이점
        FCoE는 전통적인 Fibre Channel과 iSCSI의 중간에 위치하며,
        이더넷을 통해 스토리지 트래픽을 전송한다
    ```
---
4. AoE (ATA over Ethernet)
    ```
    유사성
        Ethernet을 통해 스토리지를 공유하는 목적을 가지고 있다

    차이점
        AoE는 iSCSI와 유사하게 네트워크를 통해 스토리지를 전송하지만,
        iSCSI보다 간단하고 경량화된 프로토콜이다
    ```