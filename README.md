# 웹 프로그래밍

# BackEnd

<br>

- WAS
     - Web Application Server의 줄임말
     
     <img src="https://github.com/Garamda/WebProgramming/blob/master/was.PNG" width=60%>
     
<br>
 
- 웹 서버 vs WAS

     - WAS도 보통 자체적으로 웹 서버 기능을 내장하고 있다.

     - 현재는 WAS가 가지고 있는 웹 서버도 정적인 콘텐츠를 처리하는 데 있어서 성능상 큰 차이가 없다.

     - 규모가 커질수록 웹 서버와 WAS를 분리한다.

     - 자원 이용의 효율성, 장애 극복, 배포와 유지보수의 편의성을 위해 웹 서버와 WAS를 대체로 분리한다.

<br>

- 자바 웹 어플리케이션(Java Web Application)

     - WAS에 설치(deploy)되어 동작하는 어플리케이션

     - HTML, CSS, 이미지, Java Class(Servlet, Package, Interface 등), 각종 설정 파일 등이 포함

<br>

- Servlet

     - 자바 웹 어플리케이션의 구성요소 중 동적인 처리를 하는 프로그램의 역할
     
     - 요청이 왔을 때 응답을 해야하는 모든 내용이 구현되는 부분

     - Annotation과 함께 사용하는 URL Mapping을 통해 URL 요청을 처리할 수 있다.

     - WAS에 동작하는 Java 클래스

     - Servlet은 HttpServlet 클래스를 상속받아야 함

<br>

- Servlet의 생명 주기
     - init()
     - service(request, response)
     - destroy()

<br>

<img src="https://github.com/Garamda/WebProgramming/blob/master/servlet_lifecycle.PNG" width=40%>

<br>

WAS는 서블릿 요청을 받으면 해당 서블릿이 메모리에 있는지 확인함.
메모리에 없다면, 해당 서블릿 클래스를 메모리에 올린 후

- init() 실행
- service() 실행

<br>

메모리에 있다면,

- service() 실행

즉, 하나의 서블릿은 메모리에 한 번만 올린다.

<br>

cf) 개발자가 service()를 override하지 않았다면, Servlet의 부모 클래스인 HttpServlet의 service()가 실행 됨

<br>

WAS가 종료되거나, 웹 어플리케이션이 새롭게 갱신될 경우 destroy() 메소드를 실행. 즉, 메모리에서 해당 서블릿을 해제함. 그 후 메모리에 reload ->  init()하는 과정을 거친다.

<br>

- 요청과 응답 

<img src="https://github.com/Garamda/WebProgramming/blob/master/HttpServletRequestResponse.PNG" width=80%> 

WAS는 웹 브라우저로부터 Servlet 요청을 받으면,

- 요청할 때 가지고 있는 정보를 HttpServletRequest 객체를 생성하여 저장
- 웹 브라우저에게 응답을 보낼 때 사용하기 위하여 HttpServletResponse 객체를 생성
- 생성된 HttpServletRequest, HttpServletResponse 객체를 서블릿에 전달
- 즉, WAS는 HttpServletRequest, HttpServletResponse 생성의 주체

<br> 

- HttpServletRequest

     - http 프로토콜의 request 정보를 서블릿에 전달

     - 헤더정보, 파라미터, 쿠키, URI, URL 등의 정보를 읽어 들이는 메소드를 가지고 있음

     - Body의 Stream을 읽어 들이는 메소드를 가지고 있음 -> *** Body의 Stream이라는 것은 정확히 무슨 뜻일까?


<br>

- HttpServletResponse


     - WAS는 어떤 클라이언트가 요청을 보냈는지 알고 있고, 해당 클라이언트에게 응답을 보내기 위한 HttpServleResponse 객체를 생성하여 서블릿에 전달

     - 서블릿은 이 객체를 통해 content type, 응답 코드, 응답 메시지 등을 전송

<br>


- Redirect

     - 서버가 클라이언트의 요청에 대해, 특정 URL로 이동을 요청하는 것
     - 동작 과정
          - HTTP Response Code : 302
          - Header : Location 값에 redirect URL을 추가
          - 클라이언트는 리다이렉션 응답을 받게 되면 헤더(Location)에 포함된 URL로 재요청
          - 즉, redirect 시 클라이언트는 2번의 요청을 보내게 됨
          - 때문에 첫 요청과 두 번째 요청의 Request, Response는 다른 객체 
          - 클라이언트는 서버로부터 받은 상태 값이 302이면 Location 헤더값으로 재요청
          - 서블릿은 HttpServletResponse 클래스의 sendRedirect() 메소드를 사용함
     
<img src="https://github.com/Garamda/WebProgramming/blob/master/redirect.PNG" width=80%>


<br>

- Forward

     - 요청을 처리하던 한 서블릿이 추가적인 처리를 (같은 웹 어플리케이션의) 다른 서블릿에게 위임하는 것
     - 동작 과정
          - 웹 브라우저에서 Servlet 1에게 요청을 보냄
          - Servlet1은 요청을 처리한 후, 그 결과를 HttpServletRequest에 저장
          - Servlet1은 결과가 저장된 HttpServletRequest와 응답을 위한 HttpServletResponse를 같은 웹 어플리케이션 안에 있는 Servlet2에게 전송(forward)
          - Servlet2는 Servlet1으로 부터 받은 HttpServletRequest와 HttpServletResponse를 이용하여 요청을 처리한 후 웹 브라우저에게 결과를 전송


<img src="https://github.com/Garamda/WebProgramming/blob/master/forward.png" width=80%>

<br>

- Redirect & Forward 비교

비교 | Redirect | Forward
:---: | :---: | :---:
URL 주소 | O | X
요청 | 2번 (서로 다른 요청/응답 객체) | 1번

<br>

- Scope

     - Application : 웹 어플리케이션이 시작되고 종료될 때까지 변수가 유지 되는 경우 사용
     - Session : 웹 브라우저별로 변수가 관리되는 경우 사용
     - Request : http 요청을 WAS가 받아서 웹 브라우저에게 응답할 때까지 변수가 유지 되는 경우 사용
     - Page : 페이지 내에서 지역변수처럼 사용
    
<br>

- Maven

<br>

- JDBC

<br>

- Web API

<br>

# FrontEnd

- 브라우저

     - Parser : 데이터를 해석

     - Rendering Engine : 데이터를 화면에 표현

     - Parser와 Rendering Engine이 html, css를 처리하는 과정

     
     <img src="https://github.com/Garamda/WebProgramming/blob/master/parsingtree.png" width=60%>

<br> 
     
- DOM tree (Document Object Model tree)

     <img src="https://github.com/Garamda/WebProgramming/blob/master/domtree.png" width=40%> 

     - 브라우저에서는 html element를 DOM tree로 저장합니다.

     - 복잡한 DOM Tree를 탐색하기 위해 다양한 DOM API를 활용합니다.
     
     
- Event


- Ajax


- JSP (Java Server Page)
     - JSP는 WAS에 의해 서블릿으로 바뀌어 동작함 (<% %>에 해당하는 부분)
     - JSP Life Cycle
     
     <img src="https://github.com/Garamda/WebProgramming/blob/master/jspLifecycle.png" width=40%> 
     
     - 서블릿과 유사한 라이프 사이클로 이해할 수 있다.
     
     - 실행 순서
          * 브라우저가 웹서버에 JSP에 대한 요청 정보를 전달한다.
          * 브라우저가 요청한 JSP가 최초로 요청했을 경우만 JSP로 작성된 코드가 서블릿으로 코드로 변환한다. (java 파일 생성)
          * 서블릿 코드를 컴파일해서 실행가능한 bytecode로 변환한다. (class 파일 생성)
          * 서블릿 클래스를 로딩하고 인스턴스를 생성한다.
          * 서블릿이 실행되어 요청을 처리하고 응답 정보를 생성한다.
<br>

## 웹 프로그래밍과 관련이 있는 지식

- Non-blocking

     - Non-blocking algorithm : 어떤 쓰레드에서 오류가 발생하거나 멈추었을 때 다른 쓰레드에게 영향을 끼치지 않도록 만드는 방법
     - ex) Wait-freedom, Lock-freedom

<br>

- Non-blocking I/O : 입출력 처리는 시작만 해둔 채 완료되지 않은 상태에서, 다른 처리 작업을 계속 진행할 수 있도록 멈추지 않고 입출력 처리를 기다리는 방법.

     - cf) I/O 작업이 완료된 이후에 처리해야하는 후속 작업이 있다면, I/O 작업이 완료될 때까지 기다려야 한다. 이 후속 작업이 프로세스를 멈추지 않아야 하므로, I/O 작업이 완료된 이후 후속 작업을 이어서 진행할 수 있도록 별도의 약속(Polling, Callback function 등)을 함.

<br>

- Concurrency VS Parallelism

     - Concurrency : 각 프로그램의 부분들이 실행 순서와 무관하게 동작할 수 있도록 만들어, 한 번에 여러 개의 작업을 처리할 수 있도록 만든 구조. 즉, 하나의 작업자가 여러 개의 작업을 번갈아가며 수행할 수 있도록 만드는 것.
     
     - Parallelism : 많은 작업을 물리적으로 동시에 수행하는 것으로써, 작업자를 물리적으로 여럿 둠으로써 같은 작업을 동시에 수행할 수 있도록 만드는 것.

<br>

cf) 두 개념은 서로 의존관계가 없이 분리되어 있는 개념. (Parallelism은 한 개의 프로세서에서는 확보할 수 없는 개념)

<br>

- Asynchronous Programming

<br>

- Cookie VS Session

     - Stateless Protocol(http)을 극복하고자 클라이언트 / 서버에 상태를 저장하는 것
     
     - Cookie : 유저의 상태를 클라이언트에 저장
     
     - Session : 유저의 상태를 서버에 저장

     - Session의 저장 방식


저장 방식 | 단점
:---: | :---:
In memory | 서버 중단 시 이전 세션의 정보 저장 불가능
File storage | 서버 증설 및 다른 기기를 통한 동일 클라이언트의 접속 시 같은 유저임을 판별하기 어려움

Database storage : DB 상의 유저 정보와 함께 저장되므로 위 단점들을 모두 극복할 수 있음

<br>


- 일급 컬렉션 (First Class Collection)

<br>

- SOLID : 객체 지향 개발의 5대 원리

     - http://www.nextree.co.kr/p6960/?fbclid=IwAR0uL_OPI5kAx8r1yH6bObZ3MpfyckHkqWaEZ1gLwI-M-tU1KvuUuQ7D-1A

<br>

- 좋은 Git 커밋 메시지를 작성하는 방법
    
     - https://meetup.toast.com/posts/106

<br>

- RequestBody VS RequestParam

     - RequestBody
          - Body 자체를 가져오므로 POST 에서만 사용 가능함
          - 주로 객체 단위로 받아 사용
     - RequestParam
          - GET 에서 넘긴 파라미터를 메서드의 인자로 매칭하는 식으로 사용

<br>

- Micro Service Architecture (MSA)

     - 각 서비스는 독립적으로 배치 가능, 확장 가능
     - 각 서비스는 서로 다른 프로그래밍 언어로 개발 가능 
     - 각 서비스는 그것을 만든 팀들이 직접 관리할 수 있음
     
     - cf) Monolithic Architecture의 문제점
          - 배포 주기를 늘리는 것이 점점 어려워짐
          - 작은 부분에 대한 변경으로 인해 모드 빌드 후 다시 배포해야 함 
          - 각 모듈의 변경 사항을 그 모듈에만 한정하는 것도 어려움
     
- MSA의 특징
     
     - 서비스를 컴포넌트 단위로 정의함 
          - 각 서비스가 독립적으로 배치 가능하기 때문 
          - 응용 프로그램에 변경사항이 있을 경우, 해당 서비스의 재배포만 필요
          - 각 구성 요소의 인터페이스가 보다 명시적임
          - 각 서비스는 명시적인 원격 호출 메커니즘을 이용하기 때문에, 구성 요소 간의 결합도를 지나치게 높이지 않게 됨
          - cf) 부정적인 측면 : 원격 호출(RPC)은 프로세스 내부 호출보다 비용이 높기 때문에 원격 API는 각 구성 요소를 크게 나누는(coarse-grained) 경향이 있음. 구성 요소 간의 책임 할당을 변경할 필요가 있는 경우 어려움을 겪을 수 있음
     

     - 비즈니스 수행에 따른 컴포넌트 구성
     
          - 즉, 소프트웨어 계층 별(UI, 서버, DB)로 팀을 나누지 않음
          - 각 팀은 상호 기능적(cross-functional)임. 즉, UI, UX, DB, PM 등 개발을 위해 필요한 모든 범위의 기술 스택과 직군을 포함 할 수 있음
         
- Redis

     - https://goodgid.github.io/Redis/
<br>

- https

<br>

## 출처

* Web Programming : https://www.edwith.org/boostcourse-web/joinLectures/12952

* Non-blocking, Asynchronous, and Concurrency : https://tech.peoplefund.co.kr/2017/08/02/non-blocking-asynchronous-concurrency.html?utm_source=gaerae.com&utm_campaign=%EA%B0%9C%EB%B0%9C%EC%9E%90%EC%8A%A4%EB%9F%BD%EB%8B%A4&utm_medium=social

* [Session] 웹 서버 개발의 Session 전략 : https://devhaks.github.io/2019/04/20/session-strategy/?fbclid=IwAR0Y6_dIH5qy3KAOARe9kGru0XsJFassd1948LW9YLDNQGWulypk9DLK1t0

* [Spring] RequestParam과 RequestBody의 차이 : https://github.com/occidere/notepad/issues/41

* [Micro Service Architecture] : http://channy.creation.net/articles/microservices-by-james_lewes-martin_fowler

* [Redis] 개념과 특징 : https://goodgid.github.io/Redis/

* [SOLID] 객체지향 개발 5대 원리 : http://www.nextree.co.kr/p6960/?fbclid=IwAR0uL_OPI5kAx8r1yH6bObZ3MpfyckHkqWaEZ1gLwI-M-tU1KvuUuQ7D-1A

* [Git] 좋은 Git 커밋 메시지를 작성하는 방법 : https://meetup.toast.com/posts/106

* [https] https://webactually.com/2018/11/http%EC%97%90%EC%84%9C-https%EB%A1%9C-%EC%A0%84%ED%99%98%ED%95%98%EA%B8%B0-%EC%9C%84%ED%95%9C-%EC%99%84%EB%B2%BD-%EA%B0%80%EC%9D%B4%EB%93%9C/
