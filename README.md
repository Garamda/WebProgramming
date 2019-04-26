# 웹 프로그래밍

- 브라우저

     - Parser : 데이터를 해석

     - Rendering Engine : 데이터를 화면에 표현

     - Parser와 Rendering Engine이 html, css를 처리하는 과정

     
     <img src="https://github.com/Garamda/WebProgramming/blob/master/parsingtree.png" width=60%>
     
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

<br>

요청이 왔을 때 응답을 해야하는 모든 내용이 구현되는 부분

개발자가 service()를 override하지 않았다면, Servlet의 부모 클래스인 HttpServlet의 service()가 실행 됨

<br>

즉, 하나의 서블릿은 메모리에 한 번만 올린다.

<br>

WAS가 종료되거나, 웹 어플리케이션이 새롭게 갱신될 경우 destroy() 메소드를 실행. 즉, 메모리에서 해당 서블릿을 해제함. 그 후 메모리에 reload ->  init()하는 과정을  

<br>

- 요청과 응답 

<img src="https://github.com/Garamda/WebProgramming/blob/master/HttpServletRequestResponse.PNG" width=80%> 

WAS는 웹 브라우저로부터 Servlet 요청을 받으면,

     - 요청할 때 가지고 있는 정보를 HttpServletRequest 객체를 생성하여 저장
     - 웹 브라우저에게 응답을 보낼 때 사용하기 위하여 HttpServletResponse 객체를 생성
     - 생성된 HttpServletRequest, HttpServletResponse 객체를 서블릿에 전달
     - 즉, HttpServletRequest, HttpServletResponse 생성의 주체는 WAS

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

<br>

Session의 저장 방식


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

## 출처

* https://www.edwith.org/boostcourse-web/joinLectures/12952

* https://tech.peoplefund.co.kr/2017/08/02/non-blocking-asynchronous-concurrency.html?utm_source=gaerae.com&utm_campaign=%EA%B0%9C%EB%B0%9C%EC%9E%90%EC%8A%A4%EB%9F%BD%EB%8B%A4&utm_medium=social

* https://devhaks.github.io/2019/04/20/session-strategy/?fbclid=IwAR0Y6_dIH5qy3KAOARe9kGru0XsJFassd1948LW9YLDNQGWulypk9DLK1t0
