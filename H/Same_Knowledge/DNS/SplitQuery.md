# Split Query

- DNS의 Query를 네트워크 대역 (사설망,공인망)에 따라서 제한을 시킬 수 있고 Query를 분류하여 응답하게 할 수 있다.
- 즉, DNS Zone을 분리해서 Client의 종류에 따라 Domain의 정보를 다르게 제공하는 기술이다.
- 내부 사용자와 외부 사용자에게 제공할 정보를 다르게 하여 보안적으로도 뛰어난 기술이다.

```markdown
예를 들어, 외부에서 내부 서버의 서비스에 접근하고 싶을 때 ...

* 포트포워딩과 Split Query를 이용하여 내부 서버의 서비스도 도메인 이름으로 접근하게 할 수 있다.
* 외부에서 접근을 할 때에는 특정 Domain에 접근을 하지 못하게 할 수 있다.
```

## Split Brain & View

### View

- View라는 기술은 Linux에서 Query를 분류하기 위해서 사용되는 기술이다.
- match client로 접근할 IP 대역을 구분하고 zonename으로 zone을 구분하여 Query를 구분한다.
- 자세한건 실습하면서 설명하겠다.

### Split Brain

- Split Brain이라는 기술은 Windows에서 Query를 분류하기 위해서 사용되는 기술이다.
- Zone Scope나 DNS server rule, DNS Query Resolution Policy를 설정해서 Query를 구분한다.
- 이것도 자세한건 실습하면서 설명하겠다.