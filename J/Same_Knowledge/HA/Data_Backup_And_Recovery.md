## Data_Backup_And_recovery

### 데이터 백업과 복구란?
```
중요한 고려사항으로, 데이터 손실을 방지하고 시스템을 복구할 수 있는 강력한 백업 전략이다.
```

### 다음은 HA 환경에서의 데이터 백업과 복구에 관련된 주요 고려 사항
1. 정기적인 데이터 백업
   - HA 환경에서도 정기적으로 일관된 주기로 데이터를 백업해야 한다.
   - 백업은 원격지에 안전하게 저장되어야 한다.
   - 이를 위해 클라우드 저장소 또는 다른 물리적인 장소를 고려할 수 있다.

2. 증분 백업
    - 전체 데이터를 매번 백업하는 것은 효율하지 않을 수 있다.
    - 증분 백업은 이전 백업 이후 변경된 데이터만을 백업하는 방식이다.
    - 대역폭과 저장 공간을 절약할 수 있다.

3. 자동화된 백업 프로세스
   - 백업 프로세스는 자동으로 실행되어야 한다.
   - 이를 통해 인간 오류를 방지하고 일관성을 유지 할 수 있다.

4. 복구 시험 및 계획
   - 주기적으로 백업 복구 시험을 수행하여 데이터가 제대로 복구되는지 확인한다.
   - 또한, 복구 시나리오와 계획을 정의하고 이를 테스트하여 문제 발생 시에 대비해야 한다.

5. 레플리케이션 및 미러링
   - 데이터 레플리케이션 또는 미러링을 통해 실시간으로 데이터를 다른 위치에 복제할 수 있습니다. 
   - 데이터의 가용성을 높이고 복구 시간을 단축할 수 있다.

6. 스냅샷 및 체크포인트
   - 시스템 스냅샷 및 체크포인트를 활용하여 특정 시점의 상태를 저장한다.
   - 필요한 경우 해당 지점으로 데이터를 복구할 수 있다.

7. 보안 및 권한 관리
   - 업 데이터에 대한 보안 및 권한 관리를 강화하여 무단 액세스를 방지한다.