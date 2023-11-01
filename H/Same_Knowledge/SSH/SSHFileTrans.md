# DO IT! (Linux)

## 1. SCP (Secure Copy)

- 아래는 기본적인 SSH로 File을 전송하는 SCP (Secure Copy)의 예시이다.

<img src="./Image/SSH5.png" alt="Alt123" width="600">


- 형식은 아래와 같다.
- SCP [option] Source Destination

## 2. SFTP (SSH File Transfer Protocol)

<img src="./Image/SSH6.png" alt="Alt123" width="600">


- SFTP는 기본적으로 활성화가 되어있지는 않다.
- 활성화를 하려면 /etc/ssh/sshd_config에 아래와 같이 설정해야한다.

```bash
vi /etc/ssh/sshd_config

Subsystem    sftp    /usr/libexec/openssh/sftp-server
```

- 아래는 sftp의 사용방법이다.

```bash
debian@dlp:~$ sftp debian@www.srv.world
debian@www.srv.world's password:     # User의 Password 입력
Connected to www.srv.world.
sftp>

# 접속한 원격 Computer의 현재 디렉토리 위치를 보여준다.
sftp> pwd
Remote working directory: /home/debian

# Local Server의 현재 디렉토리 위치를 보여준다.
sftp> !pwd
/home/debian

# 원격 서버의 현재 디렉토리들을 보여준다.
sftp> ls -l
drwxrwxr-x    2 debian     debian            6 Jul 29 21:33 public_html
-rw-rw-r--    1 debian     debian           10 Jul 28 22:53 test.txt

# 로컬 서버의 현재 디렉토리들을 보여준다.
sftp> !ls -l
total 4
-rw-rw-r-- 1 debian debian 10 Jul 29 21:31 test.txt

# cd 명령어로 디렉터리를 변경한다.
sftp> cd public_html
sftp> pwd
Remote working directory: /home/debian/public_html

# 로컬 컴퓨터의 file을 원격 컴퓨터로 Upload 한다.
# 로컬 컴퓨터의 test.txt를 원격 컴퓨터의 /home/debian/debian.txt로 업로드 한것이다.
sftp> put test.txt debian.txt
Uploading test.txt to /home/debian/debian.txt
test.txt 100% 10 0.0KB/s 00:00
sftp> ls -l
drwxrwxr-x    2 debian     debian            6 Jul 29 21:33 public_html
-rw-rw-r--    1 debian     debian           10 Jul 29 21:39 debian.txt
-rw-rw-r--    1 debian     debian           10 Jul 28 22:53 test.txt

# 이렇게 확인하면 debian.txt가 생긴걸 확인 할 수 있다.
sftp> ls -l
drwxrwxr-x    2 debian     debian            6 Jul 29 21:33 public_html
-rw-rw-r--    1 debian     debian           10 Jul 29 21:39 debian.txt
-rw-rw-r--    1 debian     debian           10 Jul 28 22:53 test.txt

# 원격서버로부터 test.txt 파일을 다운로드 받아온다.
sftp> get test.txt
Fetching /home/debian/test.txt to test.txt
/home/debian/test.txt 100% 10 0.0KB/s 00:00

디렉터리 지울 때는 rmdir
파일을 지울 때는 rm 
```

# DO IT! (Windows)

- 리눅스가 아닌 Windows Client에서도 SSH를 사용하여 파일을 전송할 수 있다.
- WinSCP라는 프로그램을 사용해서 설정 해볼 것이다.

### Step 1

- WinSCP를 설치하고 시작하면 다음과 같은 초기창이 나타난다.
- Hostname, Username, Password를 적절히 설정한 후 Advanced..를 클릭한다.

<img src="./Image/SSH7.png" alt="Alt123" width="600">


### Step 2

- 좌측 메뉴의 [Directory]에서 로그인 시 초기 위치로 [Remote Directory]와 [Local Directory] 항목을 입력하고 OK를 클릭하여 SSH로 접속한다.

<img src="./Image/SSH8.png" alt="Alt123" width="600">


### Step 3

- 로그인이 정상적으로 될것이다.
- 여기서부터는 파일을 Upload하거나 Download 할 수 있다.

<img src="./Image/SSH9.png" alt="Alt123" width="600">
