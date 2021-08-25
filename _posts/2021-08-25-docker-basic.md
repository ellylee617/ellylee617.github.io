---

layout: single

title: "[docker] docker 기초" #제목
excerpt: "유튜브 생활코딩 - docker 입문수업 정리 + α" #발췌

date: 2021-08-25
lastmod: 2021-08-25

author_profile: true 

categories: 
  - docker

tags: 

- docker
- image
- container

toc: true
toc_label: "docker 기초 # toc 이름 설정
toc_icon: "docker" # 아이콘 설정
toc_sticky: true # 마우스 스크롤과 함께 내려갈 것인지 설정

---

## Docker

<br><br>![Docker-Logo-White-RGB_Vertical-BG_0](https://user-images.githubusercontent.com/78994909/130030752-ca246d13-597d-4e7f-acb7-3ffa6167a9bb.png)<br><br>

### 1. Docker ?

Linux 컨테이너 기반. 애플리케이션을 쉽고 신속하게 구축, 테스트 및 배포할 수 있는 오픈소스 플랫폼.
기존 VM과는 다르게 호스트 OS를 그대로 사용하고 컨테이너라는 유닛을 사용하여 호스트의 리소스를 공유하여 효율적인 환경을 제공함.

> Docker hub ≒ App store
> Image ≒ Program
> Container ≒ Process

> 이미지들은 리눅스 베이스이므로 리눅스 OS가 필요하지만
> 따로 세팅하지 않아도 도커가 알아서 처리함.

<br><br>

### 2. Docker의 장점

- **운영 표준화** 
  - '이미지'만 만들어 전달하면 환경 세팅 필요 없이 배포 가능
  - 로컬에서 개발하여 클라우드 환경에서의 배포 가능
  - 이미지의 크기가 작아 배포 속도가 빠르고 여러개의 컨테이너를 동시에 구동할 수 있음
    <br>
- **애플리케이션의 독립성과 확장성**
  - 여러 모듈(**Micro Services**)로 구성되기에 배포/운영/확장이 유연함
  - 각 모듈에게 독립된 환경을 제공함

<br>

<br>

### 3. Dashboard

CLI(Comand Line Interface/명령어 입력 방식)인 기본 도커를
GUI(Graphic User Interface/그래픽 기반 인터페이스)로 도와줌.

하지만 도커의 중심은 CLI!

Dashboard가 있고 어떻게 사용하는지만 기본적으로 알아두면 충분.
<br><br>

### 4. Docker  Command

> 정확한 참고는 [Docker Docs-Reference](https://docs.docker.com/engine/reference/run/)

Window10 기준 - 명령 프롬프트(cmd) 또는 Windows PowerShell 이용

> Docker Desktop Download for Windows 할 경우
> 추가로 WSL2를 설치 해야 함. (알림 팝업창이 뜬다!)
> WSL은 Windows Subsystem for Linux의 약자로, 
> windows10에 리눅스를 하위 시스템으로 설치 하게 됨.

- 모든 명령어는 docker를 앞에 붙여 사용한다.

  <br>

- 생활코딩 - docker 입문 수업에서는 apache webserver(docker hub에서 검색해보면 httpd라는 이름)를 기준으로 실습을 진행하여 이 글도 해당 강의를 바탕으로 작성 하겠다.

  <table text-align="center">
      <tr>
      	<th>명령어</th>
          <th>역할</th>
          <th>예시</th>
      </tr>
      <tr>
      	<th>pull</th>
          <td>이미지를 다운 받기</td>
          <td>docker pull httpd</td>
      </tr>
      <tr>
      	<th>images</th>
          <td>다운 받은 이미지 목록 보기</td>
          <td>docker images</td>
      </tr>
      <tr>
      	<td colspan="3">
      		<img src="https://user-images.githubusercontent.com/78994909/130162109-97525269-b638-4914-9a15-9fd4aa69669e.png"><br>tag의 latest는 최신버전이라는 의미
      	</td>
      </tr>
      <tr>
      	<th>run</th>
          <td>이미지 실행</td>
          <td>docker run httpd</td>
      </tr>
      <tr>
      	<td>[--name 설정할 이름]</td>
          <td>run과 함께 사용 시<br>실행하는 컨테이너 이름 설정 옵션</td>
          <td>docker run --name ws2 httpd<br>[ ]부분들은 옵션. 생략 가능</td>
      </tr>
      <tr>
      	<th>stop</th>
          <td>실행된 컨테이너 멈추기</td>
          <td>docker stop ws2<br>(Container ID || name)</td>
      </tr>
      <tr>
      	<th>ps</th>
          <td>컨테이너 리스트<br>(default 실행중인 것만)</td>
          <td>docker ps</td>
      </tr>
      	<td>[-a || --all]</td>
          <td>모든 컨테이너 리스트 옵션<br>실행 멈춘 컨테이너까지</td>
          <td>docker ps -a</td>
      </tr>
  	<tr>
      	<th>start</th>
          <td>컨테이너 재실행<br>(run은 새로운 컨테이너 실행)</td>
          <td>docker start ws2</td>
      </tr>
  	<tr>
      	<th>logs</th>
          <td>로그 보기(default 일회성 명령)</td>
          <td>docker logs ws2</td>
      </tr>
  	<tr>
      	<td>[-f || --follow]</td>
          <td>출력되는 모든 로그 보기 옵션</td>
          <td>docker logs -f ws2</td>
      </tr>
  	<tr>
      	<th>rm</th>
          <td>컨테이너 삭제<br>실행 중이면 에러. stop 후 진행</td>
          <td>docker rm ws2</td>
      </tr>
  	<tr>
      	<td>[--force || -f]</td>
          <td>컨테이너 강제 삭제 옵션<br>실행중이어도 삭제됨</td>
          <td>docker rm --force ws2</td>
      </tr>
  	<tr>
      	<th>rmi</th>
          <td>이미지 삭제</td>
          <td>docker rmi httpd</td>
      </tr>
  </table>

  <br>

  <br>

  > 도커가 설치되어 있는 곳이 host OS
  > 하나의 호스트에 여러개의 컨테이너를 올릴 수 있음.
  > 호스트와 컨테이너는 독립적인 시스템을 가지므로 각자의 포트와 파일 시스템을 가짐.
  >
  > docker run httpd만 했을 경우엔 현재 호스트와 컨테이너의 연결은 끊겨 있는 상태.
  > 포트와 포트를 연결해주려면 docker run -p 80:80 httpd의 식으로 명령하여 연결.
  > 이렇게 포트를 연결하여 전송하는 것을 **Port forwarding**라 한다. 

  <table>
      <tr>
      	<td>[-p || --publish] port:port</td>
          <td>포트 포워딩 실행 옵션</td>
          <td>docker run --name ws3-p 8080:80 httpd<br>앞에 있는 포트 번호는 호스트 포트<br>뒤에 있는 포트 번호는 컨테이너 포트</td>
      </tr>
      <tr>
      	<th>exec</th>
          <td>컨테이너 안에서 명령 실행<br>(default 일회성 명령)</td>
          <td>docker exec ws3 pwd || ls<br>ws3의 pwd(현재 디렉토리의 절대 경로를 출력)<br>ls(현재 디렉토리의 내용을 출력)</td>
      </tr>
      <tr>
      	<td>[-i || --interactive]</td>
          <td>연결되지 않은 경우에도 STDIN을 여는 옵션<br>STDIN : Standard Input, 표준 입력 스트림</td>
          <td>docker exec -i ws3</td>
      </tr>
  	<tr>
          <td>[-t || --tty]</td>
          <td>가상 터미널 할당 옵션<br>STDIN : Standard Input, 표준 입력 스트림</td>
          <td>docker exec -it ws3 /bin/sh<br>ws3안으로 진입(기본 쉘로)</td>
      </tr>
      <tr>
          <th>exit</th>
          <td>컨테이너 안에서 다시 호스트로 나오기</td>
          <td>exit</td>
      </tr>
      <tr>
          <th>cd</th>
          <td>change Directory</td>
          <td>. 현재 디렉토리 .. 이전 디렉토리</td>
      </tr>
  </table>
  <br>

- 컨테이너 안에서 수정할 것이 있다면 직접 진입하여 수정할 수도 있으나 
  불편하고 위험할 수 있으며 번거로움
  ∴ 호스트에서 해당 파일을 수정해서 컨테이너에 적용하기

  ```dockerfile
  docker run -p 8888:80 -v C:\Users\Elly\Desktop\htdocs\:usr/local/apache2/htdocs/ httpd
  ```

  이런 식으로 하면 포트 포워딩하며 호스트의 파일과 컨테이너의 파일을 연결하여 실행
  -v는 --volume, 호스트와 컨테이너의 디렉토리를 연결하는 옵션(마운트)
  <br>

  ⇒ 호스트 환경 안에서 파일에 대한 버전 관리라던지, 
  백업, 에디터로 코드를 편집 한다던지의 작업이 가능하다. 
  (호스트에서 해당 파일 수정시 즉시 컨테이너에 적용됨)

<br><br>

### 5. ETC

- 하나의 이미지는 여러개의 컨테이너를 가질 수 있다.
- container는 가볍기에 자잘한 파일들은 가지고 있지 않을 수 있다. 해당 컨테이너 패키지를 업데이트 하려면 apt update 라는 명령어로 추가 다운을 한다.
- 컨테이너는 쉽게 만들고 쉽게 없애는 용도이므로 쉽게 날라갈 수 있다.
  만약 중요한 컨테이너라면 이미지로 만들어 저장한다.
- 

<br><br>

<br>

