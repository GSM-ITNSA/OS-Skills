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
