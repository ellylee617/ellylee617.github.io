---
layout: single

title: "[Web] Web Server와 WAS, Cloud"
excerpt: "210813"

date: 2021-08-17
lastmod: 2021-08-17

author_profile: true

categories: 
  - Web

tags: 
   - Web Server
   - WAS
   - Legacy
   - Cloud
   - On-premise
   - Docker
   - Kubernetes

toc: true
toc_sticky: true
toc_label: "Web Server와 WAS, Cloud"
toc_icon: "server"

---

<br>

###  1. Web Server와 WAS

- #### Web Server 

  **클라이언트**로부터 **HTTP** 요청을 받아 **정적 콘텐츠**를 제공<br>
  (정적 콘텐츠 : HTML, CSS, image 등)
  Apache 비율 ↑으나, 점점 ↓, Nginx 점차 ↑
  <br>

- #### WAS(Web Application Server)
  **동적 컨텐츠** 요청시 가공하여 전달. 미들웨어.<br>
  (동적 컨텐츠 : 비즈니스 로직 처리, DB 조회 등)<br>
  웹 컨테이너(Web Container) 또는 서블릿 컨테이너(Servlet Container) 라고도 불림. 

  <br>

  즉, WAS는 JSP, Servlet 구동 환경을 제공한다.<br>

  Container는 JSP, Servlet, .net, ASP 등을 실행 시킬 수 있는 SW.<br>

  * Tomcat은 무료지만 장애시 책임X, 책임 소재 이슈
    → 클라우드 환경으로 변화하며 점차 사용↑(스프링부트 임배디드 톰캣)

  * JBoss EAP(Red Hat), WebSphere(IBM), JEUS(Tmax), WebLogic(Oracle)

    <br><br>

### 2. 웹서버와 WAS 분리

WAS에서 웹서버 모듈을 포함하여 제공하므로 웹서버를 별도 설치하지 않아도 됨.

하지만,<br>

* 서버 부하 방지
* 물리적 분리로 보안 강화

의 이유로 분리함.

<br><br>

### 3. 3Tier

* PT(Presentation Tier)
* BT(Business Tier)
* DT(Data Tier)

<br><br>

### 4. DMZ

브라우저 → (FW) → **Web Server**→(FW)→WAS→(FW)→DB Server<br>

기업의 내부 네트워크(WAS와 DB Server)와 외부 네트워크(클라이언트) 사이에 일종의 중립 지역 네트워크(Web Server).

외부 사용자가 기업의 정보를 담고 있는 내부 서버에 직접 접근 하는 것을 방지하며, 외부 사용자가 DMZ 호스트 보안을 뚫고 들어오더라도 기업 내부의 정보는 유출되지 않음.

<br><br>

### 5. On-premise와 Cloud 서비스

- #### On-premise<br>
  자체적으로 보유한 전산실 서버에 직접 설치해 운영하는 방식. 프라이빗 데이터센터.<br>

  - 인프라 구축을 위한 시간, 비용, 운영, 관리 등 비용이 많이 드는 단점이 있음

  - 하지만 보안적인 이유로 보안이 필요한 서비스와 데이터는 온프레미스 환경에서, 덜 중요한 것은 퍼블릭 클라우드 환경을 사용하는 하이브리드 IT 인프라가 대세를 이루고 있음.

  - 장비가 고정되어 있으므로 부하시 튜닝 또는 Scale-Up<br><br>![image](https://user-images.githubusercontent.com/78994909/129817202-41082fc5-0e3c-47b8-b632-f4867dd2a65a.png)

    <br><br>

- #### Cloud 서비스 - Iaas(이아스)

  Infrastructure as a Service의 약자. 

  서버, 네트워크, 스위치등의 하드웨어 인프라 자원을 직접 구축하지않고, 클라우드에 있는 인프라 자원을 사용하도록 해주는 서비스.
  <br>

  사용자들은 더 이상 인프라 구축에 힘 들일 필요 없이 서비스나 SW 개발에 집중할 수 있게 됨.<br><br>

  - 아마존 웹서비스(AWS), MS 애저(Azure) 등

  - 업체가 클수록 가격은 저렴해짐. ∴AWS가 상대적으로 저렴하다 

  - 부하시 Scale-Out, 서버 여유시 Scale-In ⇒ 유연한 증감(클라우드의 최장점)<br><br>![image](https://user-images.githubusercontent.com/78994909/129821341-d8478515-95f8-4ced-8537-6bfc38bd5c8c.png)<br><br>

  - Scale-Out, Scale-In시 연결하는 스위치(L4)만 알면 됨.
  
    <br><br>

### 6. ETC

- Cloud 환경에서 Linux 필수 공부할 것

  - Unix-AIX, Sun-Soaris, HP-UX
  - Vi, Shell script
    <br><br>

- #### Docker

  - Linux 컨테이너를 만들고 사용할 수 있도록 하는 컨테이너화 기술
  - 컨테이너를 모듈식 가상 머신처럼 다룰 수 있음
  - 컨테이너를 구축, 배포, 복사하고 다른 환경으로 이동하는 등 유연하게 사용할 수 있음
  - 애플리케이션을 클라우드에 최적화하도록 지원<br><br>![image](https://user-images.githubusercontent.com/78994909/129818944-81eb840d-7d9e-4e2f-b0f2-bc1730bd8099.png)
    (출처 : https://www.redhat.com/ko/topics/containers/whats-a-linux-container)
    <br><br>
  

- #### Kubernetes(K8s)
  
  - 컨테이너화된 서비스를 관리하기 위한 오픈소스 플랫폼
     - 분산 시스템을 탄력적으로 실행하기 위한 프레임 워크를 제공
     - 애플리케이션의 확장과 장애 조치를 처리하고, 배포 패턴 등을 제공.
     - 간단하게 말하면 도커를 관리하는 도구. Scale-out도 도움 주는 툴.
       <br><br>
  
- #### Session Clustering
  
  - 세션은 각각의 서버에서 만들어짐 → 서버 장애시  다른 서버로 take over하는데 그럼 기존의 세션 정보는 잃어버리게 됨
  
  - All-to-all Session Replication
       모든 세션 저장소에 세션 정보 복제<br>
       ∵ 소규모일 땐 효율이 좋지만 Scale-Out 시 무리
  
    ⇒ 클라우드 환경에선 세션 스토리지를 분리하여 별도의 세션 저장소를 사용함
  
    <br><br><br><br><br>

