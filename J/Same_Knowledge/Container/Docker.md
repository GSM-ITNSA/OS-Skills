# Docker

## Docker 란
```
컨테이너화 기술을 제공하는 소프트웨어 플랫폼이다.

소프트웨어를 표준화된 단일 유닛인 컨테이너로 패키징하고 배포하는 데 사용된다.
도커는 애플리케이션을 샐행하는 데 필요한 모든 것을 포함하며, 환경에 관계없이 일관된 실행 환경을 제공한다.
이를 통해 개발, 테스트 및 배포 프로세스를 효율적으로 관리할 수 있다.
```

## Docker 구성
### Docker Image
<img src="./Images/Container_DockerImage.png" width=700>

```
Docker Image란 컨테이너를 실행할 수 있는 실행파일, 설정 값 들을 가지고 있는 것이라고 생각하면 된다.

그림처럼 Image를 컨테이너에 담고 실행을 시킨다면 해당 프로세스가 동작하게 되는 것이다.

그럼 이미지는 어떻게 만들어질까? (Ubuntu Linux를 예시로 들겠다.)
```
<img src="./Images/Container_DockerImage2.png">

1. Ubuntu 이미지를 만들기 위해 Layer A, B, C가 들어간다 (각 Layer은 Ubuntu를 구성하는 구성파일이다.)
2. Ubuntu 이미지를 사용하여 Nginx Layer을 추가 함으로써 Nginx 이미지를 만든다.
3. Nginx 이미지에 Web app Source Layer을 추가하여 Web app 이미지가 만들어진다.
4. 이렇게 만들어진 Web app Image로 Docker Container를 구축한다.