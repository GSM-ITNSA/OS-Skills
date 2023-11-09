# Linux Scheduler의 개발 배경

- 우리는 Linux System이 탑재되어있는 휴대폰, 라즈베리파이를 사용하면 동시에 여러 Application을 사용할 수 있다.

```markdown
예를 들어 ...

브라우저를 실행하면서 음악 듣기.
SNS을 하면서 앱 다운로드 하기 등등
```

- 그래서 대부분은 하나의 CPU에서 여러 Process들이 동작하고 있다고 생각할 수 있다.
- 하지만 절대로 그렇지 않다. 하나의 CPU에서는 하나의 Process만 동작할 수 있다.
- Linux Kernel을 포함한 다양한 OS에서 Scheduling과 멀티 태스킹 기법이 생겨난 이유는 ..

### `CPU는 한 순간에 한 개의 Process Code만을 실행 할 수 있다.`

## Scheduler란 ?

- 여러 개의 Process들이 `효율적으로 번갈아`가면서 `CPU에서 실행될 수` 있게 규칙을 부여하고 Process들을 관리하는 SW 모듈이다.
- 하나의 Process는 CPU에서 실행을 시작하면 계속 실행 되는 것이 아니라 꺼졌다 켜졌다를 반복하게 된다.

```markdown
즉, Process는 CPU를 점유하면서 실행 중인 상태와 실행 대기하는 상태로 계속 변경하는 것이다.
```

- Memory에 존재하는 여러 Process 중 실제 CPU에서 동작할 Process를 선택하는 일은 `스케쥴링` 이라고 한다.
- Scheduler는 무슨 Process를 어떻게 CPU에서 동작 시킬건지를 결정을 해야한다.
- Process Scheduler Scheduler에 대해서 알아보자.

---

## Process Scheduler

- Process란 무엇일까 ?

```docker
Process는 메인 메모리에 할당되어 실행중인 상태인 프로그램을 말한다.

- Disk에 있는 프로그램을 실행하면, 실행을 위해 Memory 할당이 이루어지고, 할당된 Memory로 Binary Code가 올라가게 되는데 이때부터 Process라고 한다.
```

## Linux CFS Scheduling

- Linux는 CFS(Completely Fair Scheduler)라는 CPU Scheduling 알고리즘을 사용한다.
- CFS는 모든 Process가 공평하게 CPU 분배를 받도록 하는 동적 우선 순위 기반 알고리즘이다.

```docker
이게 무슨 말이냐 ...

Process가 CPU를 기다리는데 소요한 시간을 계산하여 우선순위를 부여하는것이다.
그리고 오래 기다린 Process가 더 높은 우선순위를 차지할 확률이 높아진다. 

물론 우선순위는 단순히 기다린 시간에 비례하지는 않고 다양한 조건들을 고려해서 매기는 것이다..
```

### Time slot

- `Time Slot` 은 Linux Scheduler에서 사용되는 개념이다.
- CPU를 Process들 사이에서 공정하게 분배하기 위해 사용되는 시간 단위이다.
- Scheduler는 CPU를 여러 Process들 사이에서 공유하므로 각 Process는 CPU를 사용할 수 있는 시간을 할당 받아 실행된다.
- 또한, Time Slot은 매우 작은 시간 단위이다.
- 이를 통해 CPU는 매우 짧은 시간 동안 여러 Process들을 공정하게 분배하여 실행할 수 있다.
- Scheduler는 각 Process에게 Time Slot을 할당하고 해당 시간동안 Process가 실행된다.
- Time Slot이 끝나게 되면 Scheduler는 다음 Process에게 Time Slot을 할당한다. `이를 반복하여 모든 Process가 실행될 수 있도록 하는것이다.`
- Time Slot의 크기는 Scheduler의 설정에 따라 다를 수 있지만 작을 수록 더 공정하게 실행될 수 있다.
- Process는 주어진 Time Slot을 소진하게 되면 컨텍스트 스위칭 된다. 
    - 컨텍스트 스위칭이란, CPU 위에서 동작하는 Process가 변경되는 것을 뜻한다.

```docker
하지만 너무 작은 시간단위로 Time Slot을 설정해버리면 OverHead가 발생할 수 있으므로 
적절한 크기를 선택하는것이 중요하다. 
```