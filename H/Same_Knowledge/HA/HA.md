## Availability

```bash
Availability = Uptime / ( Uptime + Downtime )
```

- 가용성(Available)이란, 서버와 네트워크, 프로그램 등의 정보 시스템이 정상적으로 사용 가능한 정도를 말한다.
- 즉, 시스템 고장 발생 시 얼마나 빠른 시간내에 치료가 되어 다시 정상적으로 서비스 할 수 있는지를 분석하는 척도이다.

## High Availability

- 위에서 설명한 Availability를 극대화 시키는 구성이다.
- 대표적인 HA를 구성하기 위한 기술은 `Clustering, 이중화, RAID` 등이 존재한다.
- HA를 구성하기 위한 목적은 `백업`이나 `장애극복 처리` 및 `데이터 저장` 및 `액세스`에 집중 되어있다.