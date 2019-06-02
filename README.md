# 웹 프로그래밍

[WAS](#was)

[웹 서버 vs WAS](#웹-서버-vs-was)

[자바 웹 어플리케이션(Java Web Application)](#java-web-application)

[Servlet](#servlet)

[Servlet의 생명 주기](#servlet의-생명-주기)

[요청과 응답](#요청과-응답)

[HttpServletRequest](#HttpServletRequest)

[HttpServletResponse](#HttpServletResponse)

[Redirect](#Redirect)

[Forward](#Forward)

[Servlet과 JSP 연동](#servlet과-jsp-연동)

[Redirect & Forward 비교](#redirect-&-forward-비교)

[Scope](#scope)

[Page scope](#page-scope)

[Request scope](#request-scope)

[Session scope](#session-scope)

[Application Scope](#application-scope)

[Maven](#maven)

[JDBC (Java Database Connectivity)](#jdbc-(java-database-connectivity))

[Web API](#web-api)

[HTTP Status Code](#http-status-code)

[Spring Framework](#)

[Container](#)

[IoC (Inversion of Control)](#)

[DI (Dependency Injection)](#)

[Bean](#)

[Java Config를 이용한 설정](#)

[Spring JDBC](#)

[DTO (Data Transfer Object)](#)

[DAO (Data Access Object)](#)

[Connection Pool](#)

[DataSource](#)

[MVC(Model-View-Controller)](#)

[Spring MVC](#)

[DispatcherServlet](#)

[DispatcherServlet의 각 요소](#)

[HandlerMapping](#)

[HandlerAdpater](#)

[ViewResolver](#)

[@EnableWebMvc](#)

[Interceptor](#)

[Argument Resolver](#)

[Hibernate VS Mybatis](#)

[@RestController](#)

[MessageConvertor](#)

[@Transactional](#)

[Servlet의 생명 주기](#)



# BackEnd

<br>

### WAS
- Web Application Server의 줄임말
     
     <img src="https://github.com/Garamda/WebProgramming/blob/master/images/was.PNG" width=60%>
     
<br>
 
### 웹 서버 vs WAS
- WAS도 보통 자체적으로 웹 서버 기능을 내장하고 있다.

- 현재는 WAS가 가지고 있는 웹 서버도 정적인 콘텐츠를 처리하는 데 있어서 성능상 큰 차이가 없다.

- 규모가 커질수록 웹 서버와 WAS를 분리한다.

- 자원 이용의 효율성, 장애 극복, 배포와 유지보수의 편의성을 위해 웹 서버와 WAS를 대체로 분리한다.

<br>

### Java Web Application
- WAS에 설치(deploy)되어 동작하는 어플리케이션

- HTML, CSS, 이미지, Java Class(Servlet, Package, Interface 등), 각종 설정 파일 등이 포함

<br>

### Servlet
- 자바 웹 어플리케이션의 구성요소 중 동적인 처리를 하는 프로그램의 역할

- 요청이 왔을 때 응답을 해야하는 모든 내용이 구현되는 부분

- Annotation과 함께 사용하는 URL Mapping을 통해 URL 요청을 처리할 수 있다.

- 하나의 서블릿이 여러 개의 URL 요청을 처리할 수 있다. (/*)

- WAS에 동작하는 Java 클래스

- Servlet은 HttpServlet 클래스를 상속받아야 함

- Servlet과 JSP로부터 최상의 결과를 얻으려면, 두 가지를 조화롭게 사용해야 함

- ex) 웹 페이지를 구성 화면(html)은 JSP로, 복잡한 프로그래밍은 서블릿으로 구현

<br>

### Servlet의 생명 주기
- init()
- service(request, response)
- destroy()

<br>

<img src="https://github.com/Garamda/WebProgramming/blob/master/images/servlet_lifecycle.PNG" width=40%>

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

### 요청과 응답 

<img src="https://github.com/Garamda/WebProgramming/blob/master/images/HttpServletRequestResponse.PNG" width=80%> 

WAS는 웹 브라우저로부터 Servlet 요청을 받으면,

- 요청할 때 가지고 있는 정보를 HttpServletRequest 객체를 생성하여 저장

- 웹 브라우저에게 응답을 보낼 때 사용하기 위하여 HttpServletResponse 객체를 생성

- 생성된 HttpServletRequest, HttpServletResponse 객체를 서블릿에 전달

- 즉, WAS는 HttpServletRequest, HttpServletResponse 생성의 주체

<br> 

### HttpServletRequest
- http 프로토콜의 request 정보를 서블릿에 전달

- 헤더정보, 파라미터, 쿠키, URI, URL 등의 정보를 읽어 들이는 메소드를 가지고 있음

- Body의 Stream을 읽어 들이는 메소드를 가지고 있음 -> *** Body의 Stream이라는 것은 정확히 무슨 뜻일까?


<br>

### HttpServletResponse


     - WAS는 어떤 클라이언트가 요청을 보냈는지 알고 있고, 해당 클라이언트에게 응답을 보내기 위한 HttpServleResponse 객체를 생성하여 서블릿에 전달

     - 서블릿은 이 객체를 통해 content type, 응답 코드, 응답 메시지 등을 전송

<br>


### Redirect

- 서버가 클라이언트의 요청에 대해, 특정 URL로 이동을 요청하는 것
- 동작 과정
     - HTTP Response Code : 302
     
     - Header : Location 값에 redirect URL을 추가
     
     - 클라이언트는 리다이렉션 응답을 받게 되면 헤더(Location)에 포함된 URL로 재요청
     
     - 즉, redirect 시 클라이언트는 2번의 요청을 보내게 됨
     
     - 때문에 첫 요청과 두 번째 요청의 Request, Response는 다른 객체 
     
     - 클라이언트는 서버로부터 받은 상태 값이 302이면 Location 헤더값으로 재요청
     
     - 서블릿은 HttpServletResponse 클래스의 sendRedirect() 메소드를 사용함
          
     - 예제 코드
     
redirect01.jsp

```response.sendRedirect("redirect02.jsp");```


<img src="https://github.com/Garamda/WebProgramming/blob/master/images/redirect2.PNG" width=80%>


<br>

### Forward
- 요청을 처리하던 한 서블릿이 추가적인 처리를 (같은 웹 어플리케이션의) 다른 서블릿에게 위임하는 것

- 동작 과정
     - 웹 브라우저에서 Servlet 1에게 요청을 보냄
     - Servlet1은 요청을 처리한 후, 그 결과를 HttpServletRequest에 저장
     - Servlet1은 결과가 저장된 HttpServletRequest와 응답을 위한 HttpServletResponse를 같은 웹 어플리케이션 안에 있는 Servlet2에게 전송(forward)
     - Servlet2는 Servlet1으로 부터 받은 HttpServletRequest와 HttpServletResponse를 이용하여 요청을 처리한 후 웹 브라우저에게 결과를 전송


     - 예제 코드
     
FrontServlet.java
     
```
protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            
     // forward로 보내고자 하는 값을 HttpServletRequest 객체에 설정
     request.setAttribute("key", value);
            
     // RequestDispatcher : 1) 클라이언트로부터 최초로 들어온 요청을 JSP/Servlet 내에서 원하는 자원으로 요청을 넘기는 역할을 수행
     //                     2) 특정 자원에 처리를 요청하고 처리 결과를 얻어오는 기능을 수행하는 클래스
     // RequestDispatcher 객체에 forward url mapping을 함
     RequestDispatcher requestDispatcher = request.getRequestDispatcher("/next");
            
     // request, response 객체 모두 forward를 통해 다음 Servlet으로 전달
     requestDispatcher.forward(request, response);
}
```


NextServlet.java

 
```
protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
     // request 내 attribute들은 Object로 저장되기 때문에, 형 변환을 거쳐야 한다. 
     int takenValue = (Integer)request.getAttribute("key");
}
```
<img src="https://github.com/Garamda/WebProgramming/blob/master/images/forward.png" width=80%>


<br>

### Servlet과 JSP 연동
- Servlet은 프로그램 로직을 수행하기에 유리
- JSP는 결과를 출력하기에 유리(html)
- Servlet에서 프로그램 로직을 수행
- 그 결과를 JSP에 포워딩
- 예제 코드
     ```
        request.setAttribute("key", value);
        RequestDispatcher requestDispatcher = request.getRequestDispatcher("/result.jsp");
        requestDispatcher.forward(request, response);
     ```
     
<br>

### Redirect & Forward 비교

비교 | Redirect | Forward
:---: | :---: | :---:
URL 주소 변경 | O | X
요청 | 2번 (서로 다른 요청/응답 객체) | 1번

<br>

### Scope
- Page : 페이지 0내에서 지역변수처럼 사용

- Request : http 요청을 WAS가 받아서 웹 브라우저에게 응답할 때까지 변수가 유지 되는 경우 사용

- Session : 웹 브라우저별로 변수가 관리되는 경우 사용, 상태 유지 시 사용

- Application : 웹 어플리케이션이 시작되고 종료될 때까지 변수가 유지 되는 경우 사용

<img src="https://github.com/Garamda/WebProgramming/blob/master/images/scope.jpg" width=40%>

<br>

### Page scope
- 특정 서블릿이나 JSP가 실행되는 동안에만 정보를 유지 하고 싶은 경우 사용

- PageContext 추상 클래스를 사용

- JSP 페이지에서 pageContext라는 내장 객체로 사용 가능

- forward가 될 경우 해당 Page scope에 지정된 변수는 사용할 수 없음 (서블릿이 바뀌므로 page scope도 전환 됨)

- 다른 Scope들과 달리, 마치 지역변수처럼 사용 됨. 즉, 해당 JSP나 서블릿이 실행되는 동안에만 정보를 유지하고자 할 때 사용 됨

- JSP에서 pageScope에 값을 저장한 후 해당 값을 EL표기법 등에서 사용할 때 사용 됨

<br>

### Request scope
- http 요청을 WAS가 받아서 웹 브라우저에게 응답할 때까지 변수값을 유지하고자 할 경우 사용

- HttpServletRequest 객체를 사용

- JSP에서는 request 내장 변수를 사용

- 서블릿에서는 HttpServletRequest 객체를 사용

- 값을 저장하고 읽어 들일 때는 request 객체의 setAttribute(), getAttribute() 메소드를 사용

- forward 시 값을 유지하고자 사용 (Request scope를 사용한 것 : forward 되는 동안 값이 유지되는 것)
    
 <br>  
 
### Session scope
- 웹 브라우저별로(하나의 클라이언트 마다) 변수를 관리할 경우 사용

- 웹 브라우저 간의 탭 간에는 세션정보가 공유되기 때문에, 각각의 탭에서는 같은 세션정보를 사용할 수 있음

- HttpSession 인터페이스를 구현한 객체를 사용

- JSP에서는 session 내장 변수를 사용

- 서블릿에서는 HttpServletRequest의 getSession()메소드를 이용하여 session 객체를 얻음

- 값을 저장하고 읽어 들일 때는 session 객체의 setAttribute(), getAttribute() 메소드를 사용

- 여러 요청들을 거쳐도 유지되는 scope

- 사용자마다 유지가 되어야 할 정보가 있을 때 사용 ( ex) 장바구니) 

<br>

### Application Scope
- 웹 어플리케이션이 시작되고 종료될 때까지 변수를 사용할 수 있음

- 하나의 서버에는 여러 개의 Web Application이 있을 수 있으므로, 하나의 서버에 여러 개의 Application Scope이 있을 수 있음

- ServletContext 인터페이스를 구현한 객체를 사용

- JSP에서는 application 내장 객체를 사용

- 서블릿은 getServletContext() 메소드를 사용하여 application 객체를 사용

- 하나의 웹 어플리케이션 당 하나의 application 객체가 사용됨

- 값을 저장하고 읽어 들일 때는 application 객체의 setAttribute(), getAttribute() 메소드를 사용

- 모든 클라이언트가 공통으로 사용해야 할 값들이 있을 때 사용

- 예제 코드
     
ApplicationScope01.java
``` 
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
     ServletContext application = getServletContext();
     int value = 1;
     application.setAttribute("value", value);  
}     
```
<br>

ApplicationScope02.java

```
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
     response.setContentType("text/html; charset=UTF-8");    
     PrintWriter out = response.getWriter();
        
     ServletContext application = getServletContext();
                
     try {
          int value = (int)application.getAttribute("key");
          value++;
          application.setAttribute("value", value);
     }catch(NullPointerException ex) {
          out.println("value가 설정되지 않습니다.")
     }
}
        
// 1. Application scope에 저장된 value는 2가 되었다.
// 2. ApplicationScope01.java에서 먼저 setAttribute()가 되지 않았을 경우를 대비해 try catch로 예외를 처리한다.
```
<br>


applicationscope01.jsp

```
<body>
<%
    try{
        int value = (int)application.getAttribute("value");
        value += 2;
        application.setAttribute("value", value);
%>
        <h1><%=value %></h1>
<%        
    }catch(NullPointerException ex){
%>
        <h1>설정된 값이 없습니다.</h1>
<%        
    }
%>

</body>

// 1. JSP에선 내장 객체 application을 바로 사용할 수 있다.
// 2. 이전 ApplicationScope에서 setAttribute()가 되지 않았을 경우를 대비해 try catch로 예외를 처리한다.
```

<br>

### Maven
- 빌드(Build), 패키징, 문서화, 테스트, 테스트 리포팅, git, 의존성 관리, 형상관리서버와 연동(SCMs), 배포 등의 작업을 손쉽게 할 수 있음

- CoC(Convention over Configuration)를 따라 많은 반복 작업들을 자동화 함 

- ex) 프로그램의 소스 파일 위치, 컴파일 된 파일의 위치 등

- 편리하게 의존성 라이브러리를 관리할 수 있음

- 모든 개발자가 Maven의 설정을 따라 일관된 방식으로 빌드를 수행 함

- 추가 설명
     - scope 
          * compile : scope를 따로 설정하지 않는 경우 기본값. 컴파일 할 때 필요. 테스트 및 런타임에도 클래스 패스에 포함 됨. 
          * runtime : 런타임에 필요. 컴파일 시에는 필요하지 않지만, 실행 시에 필요한 경우입니다.  ex) JDBC 드라이버
          * provided : 컴파일 시에 필요하지만, 실제 런타임 때에는 컨테이너 같은 것에서 제공되는 모듈. 배포 시 제외 됨.  ex) Servlet, JSP API 등. 
          * test : 테스트 코드를 컴파일 할 때 필요. 테스트 시 클래스 패스에 포함되며, 배포 시 제외 됨.
          * 예시
                    ```
                    <dependency>
                         <groupId>javax.servlet</groupId>
                         <artifactId>javax.servlet-api</artifactId>
                         <version>3.1.0</version>
                         <scope>provided</scope> // <- 여기
                    </dependency>
                    ```

<br>

### JDBC (Java Database Connectivity)
- 자바를 통한 DB 접속, SQL query 실행, 실행 결과로 얻어진 데이터를 핸들링하는 방법 제공

- 자바 프로그램 내에서 SQL문을 실행하기 위한 자바 API

- Java는 표준 인터페이스인 JDBC API를 제공

- DB 벤더, 기타 써드파티에서는 JDBC 인터페이스를 구현한 드라이버(driver)를 제공

- 실행 단계
     - import java.sql.*;
     
     - 드라이버 로드 : 사용하는 DB에 맞는 객체 제공
          
     - Connection 객체 생성 : DB에 접속
          
     - Statement 객체 생성 및 질의 수행 : query를 생성하고 수행
          
     - ResultSet 객체 생성 (SQL문에 결과물이 있다면)
               - SELECT : row들을 return
               - INSERT, UPDATE, DELETE : 성공/실패 여부를 return
          
     - 모든 객체를 닫는다 :  객체를 생성한 반대의 순서로 접속을 끊는다
          
          <br>
          <img src="https://github.com/Garamda/WebProgramming/blob/master/images/jdbc.PNG" width=70%>

<br>

### Web API
     - REST API의 모든 규칙을 준수하지는 못하는 API
     

<br>


### HTTP Status Code
- 100 (조건부 응답)

- 200 (성공)
     - 200 : 클라이언트의 요청을 성공적으로 수행 함
     - 201 : 클라이언트가 요청한 리소스가 성공적으로 생성 됨 (POST 요청에 대한 응답)
- 300 (리다이렉션 완료)

- 400 (요청 오류)
     - 401 : 클라이언트가 인증되지 않은 상태에서 보호된 리소스를 요청함.  ex) 로그인 하지 않고 특정 정보를 요청하는 경우
     - 404(Not Found): 서버가 요청한 페이지(Resource)를 찾을 수 없음.  ex) 서버에 존재하지 않는 페이지에 대해 요청을 보낸 경우
     - 405 : 클라이언트의 요청에 사용 불가능한 method가 있음.  ex) GET만을 처리할 수 있지만 POST 요청을 보낸 경우
     
- 500 (서버 오류)
     
<br> <br> 

### Spring Framework
- 약 20개의 모듈로 구성되어 있으며, 필요한 모듈만 가져다 사용할 수 있음
- Core 계층은 알고 있어야 함
     
<img src="https://github.com/Garamda/WebProgramming/blob/master/images/springframework.png" width=70%>



### Container
- 인스턴스의 life cycle을 관리

- WAS가 Servlet의 컨테이너를 가지고 있음

- 개발자는 Servlet 코드를 작성, (Servlet URL에 해당하는 요청을 받으면) WAS의 Servlet 컨테이너가 메모리에 올린 후 실행

- cf) Servlet 컨테이너는 동일한 서블릿에 대한 요청을 받을 시, 또 메모리에 올리지 않고 기존에 메모리에 올라간 서블릿을 실행, 웹 브라우저에게 전달

- 생성된 인스턴스에 추가적인 기능을 제공

<br> 

### IoC (Inversion of Control)
- 컨테이너가 코드 대신 오브젝트의 제어권을 갖고 있음 

- 개발자가 만든 클래스, 메소드를 다른 프로그램이 대신 실행해주는 것

- ex) Servlet : 개발자가 만들지만, 서블릿의 메소드를 알맞게 호출하는 것은 WAS

### DI (Dependency Injection)
- 의존성 주입 : 클래스 사이의 의존 관계를 빈(Bean) 설정 정보를 바탕으로 컨테이너가 자동으로 연결해주는 것

<br>
DI가 적용되지 않은 예 : 개발자가 직접 인스턴스를 생성

```
class Engine {

}

class Car {
     Engine v5 = new Engine();
}
```

<br>
DI가 적용된 예 : 컨테이너가 v5 변수에 인스턴스를 할당

```
@Component
class Engine {

}

@Component
class Car {
     @Autowired
     Engine v5;
}
```

<br>

### Bean
- 일반적인 Java 클래스를 Bean 클래스라고 일컫는다

- 3가지 특징
     - 기본생성자를 가진다
     - 필드는 private하게 선언함
     - getter, setter 메소드를 가진다. 이 메소드들을 property라고 한다.
     
- 싱글턴 패턴
    
    
<br>

### Java Config를 이용한 설정
- @Configuration : 스프링 설정 클래스를 선언하는 어노테이션

- @Bean : bean을 정의하는 어노테이션

- @ComponentScan : @Controller, @Service, @Repository, @Component 어노테이션이 붙은 클래스를 찾아 컨테이너에 등록 (메모리에 올림)

- @Component : 컴포넌트 스캔의 대상이 되는 어노테이션 중 하나로써, 주로 유틸이나 기타 지원 클래스에 붙임

- @Autowired : 주입 대상이되는 bean을 컨테이너에 찾아 주입하는 어노테이션

- Tip : @Controller, @Service, @Repository, @Component 어노테이션이 붙어 있는 객체들은 @ComponentScan을 이용해서 읽어들여 메모리에 올리고 DI를 주입, 이러한 어노테이션이 붙어 있지 않은 객체는 @Bean 어노테이션을 이용하여 직접 생성해주는 방식으로 클래스들을 관리하면 편리

<br>

### Spring JDBC
- org.springframework.jdbc.core
     - JdbcTemplate 및 관련 Helper 객체 제공
     
- JDBC Template
     - org.springframework.jdbc.core에서 가장 중요한 클래스
     
     - Statement의 생성과 실행을 처리
     
     - 리소스 생성, 해지를 처리해서 연결을 닫는 것을 잊어 발생하는 문제 등을 피할 수 있도록 함
     
     - SQL 조회, 업데이트, 저장 프로시저 호출, ResultSet 반복호출 등을 실행
     
     - JDBC 예외가 발생할 경우 org.springframework.dao 패키지에 정의되어 있는 일반적인 예외로 변환


<br>

### DTO (Data Transfer Object)
- 계층 간 데이터 교환을 위한 Java Bean

- 계층이란 컨트롤러 뷰, 비지니스 계층, 퍼시스턴스 계층을 의미합니다.

- 로직을 가지고 있지 않은 순수한 데이터 객체

- 필드, getter, setter를 가짐. 추가적으로 toString(), equals(), hashCode()등의 Object 메소드를 오버라이딩 할 수 있음
    
<br>

### DAO (Data Access Object)
- 데이터를 조회하거나 조작하는 기능을 전담하도록 만든 객체

- 보통 데이터베이스를 조작하는 기능을 전담하는 목적으로 만들어 짐
     
### Connection Pool    
- DB 연결에는 많은 비용이 들어가므로, 미리 Connection 여러 개 맺어 둔다.
     - Connection이 필요하면 Connection Pool에게 빌려서 사용한 후 반납한다.
     
     - Connection 사용 후 이를 반납하지 않으면, 속도가 느려진다.
     
     - 아래 그림은 여러 클라이언트가 Connection Pool에서 Connection을 사용하고 반납하는 예를 보여준다.
<br>

<img src="https://github.com/Garamda/WebProgramming/blob/master/images/connectionpool.jpg" width=40%>

<br>

### DataSource
- Connection Pool을 관리하는 목적으로 사용되는 객체
- DataSource를 이용해 커넥션을 얻어오고 반납하는 등의 작업을 수행 함
     
<br>

### MVC(Model-View-Controller)
- Model : View가 렌더링하는데 필요한 데이터.  ex)사용자가 요청한 상품 목록
- View : 실제로 보이는 부분이며, Model을 사용해 렌더링을 함. 뷰는 JSP, JSF, PDF, XML 등으로 결과를 표현.
- Controller : 사용자의 액션에 응답하는 컴포넌트. Controller는 Model을 업데이트하고, 다른 액션을 수행 함.
     
<br>

<img src="https://github.com/Garamda/WebProgramming/blob/master/images/MVC.png" width=60%>

<br>

이 MVC 구조가 Spring Framework에 구현되어 있음

<img src="https://github.com/Garamda/WebProgramming/blob/master/images/springWebModule.png" width=60%>

<br>

### Spring MVC 
<img src="https://github.com/Garamda/WebProgramming/blob/master/images/SpringMVC.png" width=60%>

<br>

### DispatcherServlet
- SpringMVC 이해의 핵심
- 프론트 컨트롤러 : 요청을 처리하지 않고 넘겨주기만 함
- 클라이언트의 모든 요청을 받은 후, 요청을 처리할 컨트롤러와 메소드가 무엇인지 HandlerMapping에게 물어 봄(그 정보는 개발자가 설정한 xml 파일이나 Annotation에 들어있다). 그 후 이를 처리할 핸들러(HandlerAdapter)에게 넘김
     - 핸들러가 처리한 결과를 받아 사용자에게 응답 결과를 보여줌(ViewResolver)
     - 이처럼 여러 컴포넌트를 이용해 작업을 처리함
     
<br>

<img src="https://github.com/Garamda/WebProgramming/blob/master/images/DispatcherServlet.png " width=60%>    

<br>

### DispatcherServlet의 각 요소
### HandlerMapping
### HandlerAdpater
### ViewResolver

-> 이 4가지는 추후에 깊히 익힐 것. Spring Framework의 동작 과정을 익히는 데 필수.

참고 보강 자료 : http://blog.naver.com/duco777/220605479481

<br>

### @EnableWebMvc
- DispatcherServlet의 RequestMappingHandlerMapping, RequestMappingHandlerAdapter, ExceptionHandlerExceptionResolver, MessageConverter 등 Web에 필요한 빈들을 대부분 자동으로 설정해준다.

- cf) 기본 설정 이외의 설정이 필요하다면 WebMvcConfigurerAdapter를 상속받도록 Java config class를 작성한 후, 필요한 메소드를 오버라이딩 하도록 한다.

<br>

### Interceptor
- Dispatcher servlet에서 Handler(Controller)로 요청을 보낼 때, Handler에서 Dispathcer servlet으로 응답을 보낼 때 동작합니다.
     
     <img src="https://github.com/Garamda/WebProgramming/blob/master/images/interceptor.jpg " width=70%> 
<br>

### Argument Resolver

<br>

### Hibernate VS Mybatis

<br>

### @RestController
- Spring 4 에서 Rest API, Web API를 개발하기 위해 등장한 Annotation

- 이전 버전의 @Controller와 @ResponseBody를 포함
     
<br>

### MessageConvertor
- @RestController를 이해하는 데 중요함

- HTTP Request를 자바 객체로 변환하는 역할

- Response Body를 클라이언트에게 전달할 수 있도록 JSON으로 변환하는 역할

- @ResponseBody, @RequestBody

- @EnableWebMvc로 인한 기본 설정
    
<br>  

### @Transactional


# FrontEnd

### 브라우저
- Parser : 데이터를 해석

- Rendering Engine : 데이터를 화면에 표현

- Parser와 Rendering Engine이 html, css를 처리하는 과정

     
     <img src="https://github.com/Garamda/WebProgramming/blob/master/images/parsingtree.png" width=60%>

<br> 
     
### DOM tree (Document Object Model tree)

     <img src="https://github.com/Garamda/WebProgramming/blob/master/images/domtree.png" width=40%> 

- 브라우저에서는 html element를 DOM tree로 저장합니다.

- 복잡한 DOM Tree를 탐색하기 위해 다양한 DOM API를 활용합니다.
     
     
### Event


### Ajax


### JSP (Java Server Page)
- JSP는 WAS에 의해 서블릿으로 바뀌어 동작함 (<% %>에 해당하는 부분)
- JSP Life Cycle
     
     <img src="https://github.com/Garamda/WebProgramming/blob/master/images/jspLifecycle.png" width=40%> 
     
     - 서블릿과 유사한 라이프 사이클로 이해할 수 있다.
     
     - 실행 순서
          * 브라우저가 웹서버에 JSP에 대한 요청 정보를 전달한다.
          * 브라우저가 요청한 JSP가 최초로 요청했을 경우만 JSP로 작성된 코드가 서블릿으로 코드로 변환한다. (java 파일 생성)
          * 서블릿 코드를 컴파일해서 실행가능한 bytecode로 변환한다. (class 파일 생성)
          * 서블릿 클래스를 로딩하고 인스턴스를 생성한다.
          * 서블릿이 실행되어 요청을 처리하고 응답 정보를 생성한다.
<br>

## 웹 프로그래밍과 관련이 있는 지식

### Non-blocking

- Non-blocking algorithm : 어떤 쓰레드에서 오류가 발생하거나 멈추었을 때 다른 쓰레드에게 영향을 끼치지 않도록 만드는 방법

- ex) Wait-freedom, Lock-freedom

<br>

### Non-blocking I/O : 입출력 처리는 시작만 해둔 채 완료되지 않은 상태에서, 다른 처리 작업을 계속 진행할 수 있도록 멈추지 않고 입출력 처리를 기다리는 방법.

- cf) I/O 작업이 완료된 이후에 처리해야하는 후속 작업이 있다면, I/O 작업이 완료될 때까지 기다려야 한다. 이 후속 작업이 프로세스를 멈추지 않아야 하므로, I/O 작업이 완료된 이후 후속 작업을 이어서 진행할 수 있도록 별도의 약속(Polling, Callback function 등)을 함.

<br>

### Concurrency VS Parallelism

- Concurrency : 각 프로그램의 부분들이 실행 순서와 무관하게 동작할 수 있도록 만들어, 한 번에 여러 개의 작업을 처리할 수 있도록 만든 구조. 즉, 하나의 작업자가 여러 개의 작업을 번갈아가며 수행할 수 있도록 만드는 것.
     
- Parallelism : 많은 작업을 물리적으로 동시에 수행하는 것으로써, 작업자를 물리적으로 여럿 둠으로써 같은 작업을 동시에 수행할 수 있도록 만드는 것.

<br>

cf) 두 개념은 서로 의존관계가 없이 분리되어 있는 개념. (Parallelism은 한 개의 프로세서에서는 확보할 수 없는 개념)

<br>

### Asynchronous Programming

<br>

### Cookie VS Session

- Stateless Protocol(http)을 극복하고자 클라이언트 / 서버에 상태를 저장하는 것
     
- Cookie : 유저의 상태를 클라이언트에 저장
     <img src="https://github.com/Garamda/WebProgramming/blob/master/images/cookie1.png" width=40%> 
     <img src="https://github.com/Garamda/WebProgramming/blob/master/images/cookie2.png" width=40%> 
     
- Session : 유저의 상태를 서버에 저장
     <img src="https://github.com/Garamda/WebProgramming/blob/master/images/session1.png" width=40%> 
     <img src="https://github.com/Garamda/WebProgramming/blob/master/images/session2.png" width=40%> 
     
- Session의 저장 방식


저장 방식 | 단점
:---: | :---:
In memory | 서버 중단 시 이전 세션의 정보 저장 불가능
File storage | 서버 증설 및 다른 기기를 통한 동일 클라이언트의 접속 시 같은 유저임을 판별하기 어려움

Database storage : DB 상의 유저 정보와 함께 저장되므로 위 단점들을 모두 극복할 수 있음

<br>


### 일급 컬렉션 (First Class Collection)

<br>

### SOLID : 객체 지향 개발의 5대 원리

- http://www.nextree.co.kr/p6960/?fbclid=IwAR0uL_OPI5kAx8r1yH6bObZ3MpfyckHkqWaEZ1gLwI-M-tU1KvuUuQ7D-1A

<br>

### 좋은 Git 커밋 메시지를 작성하는 방법
    
- 제목과 본문을 한 줄 띄워 분리하기
     - 커밋 메시지 : 50자 이내의 요약문장 + 빈 줄 하나 + 설명문
     - ```git log --oneline``` 명령어 사용시 제목만 출력하여 보여줌
- 제목은 영문 기준 50자 이내로
- 제목 첫글자를 대문자로
- 제목 끝에 . 금지
- 제목은 명령조로
     - git 자동 커밋 시 명령문을 사용하기 때문 ex) ```git merge``` == ```Merge branch 'myfeature'```
     - 커밋 메시지를 명령문으로 작성한다는 것은, git의 빌트-인 컨벤션(Built-in Convention)을 그대로 따른다는 것을 의미함
- 본문은 영문 기준 72자마다 줄 바꾸기
     - git은 자동으로 커밋 메시지 줄바꿈을 하지 않는다. 단순 git log 명령어 입력만으로도 보기 좋은 메시지를 만들고자 한다면 적당한 위치(72자)에서 엔터키를 눌러 줄바꿈을 하자.
- 본문은 어떻게보다 무엇을, 왜에 맞춰 작성하기

<br>

### RequestBody VS RequestParam

- RequestBody
     - Body 자체를 가져오므로 POST 에서만 사용 가능함
     - 주로 객체 단위로 받아 사용
- RequestParam
     - GET 에서 넘긴 파라미터를 메서드의 인자로 매칭하는 식으로 사용

<br>

### Micro Service Architecture (MSA)
- 각 서비스는 독립적으로 배치 가능, 확장 가능

- 각 서비스는 서로 다른 프로그래밍 언어로 개발 가능
- 각 서비스는 그것을 만든 팀들이 직접 관리할 수 있음
     
- cf) Monolithic Architecture의 문제점
          - 배포 주기를 늘리는 것이 점점 어려워짐
          - 작은 부분에 대한 변경으로 인해 모드 빌드 후 다시 배포해야 함 
          - 각 모듈의 변경 사항을 그 모듈에만 한정하는 것도 어려움
     
### MSA의 특징

- 서비스를 컴포넌트 단위로 정의함 
     - 각 서비스가 독립적으로 배치 가능하기 때문 
     
     - 응용 프로그램에 변경사항이 있을 경우, 해당 서비스의 재배포만 필요
          
     - 각 구성 요소의 인터페이스가 보다 명시적임
          
     - 각 서비스는 명시적인 원격 호출 메커니즘을 이용하기 때문에, 구성 요소 간의 결합도를 지나치게 높이지 않게 됨
          
     - cf) 부정적인 측면 : 원격 호출(RPC)은 프로세스 내부 호출보다 비용이 높기 때문에 원격 API는 각 구성 요소를 크게 나누는(coarse-grained) 경향이 있음. 구성 요소 간의 책임 할당을 변경할 필요가 있는 경우 어려움을 겪을 수 있음
     

- 비즈니스 수행에 따른 컴포넌트 구성
     - 즉, 소프트웨어 계층 별(UI, 서버, DB)로 팀을 나누지 않음
          
     - 각 팀은 상호 기능적(cross-functional)임. 즉, UI, UX, DB, PM 등 개발을 위해 필요한 모든 범위의 기술 스택과 직군을 포함 할 수 있음
         
### Redis (REmote DIctionary Server)

- 디스크가 아닌 메모리 기반의 데이터 저장소
- NoSQL & Cache 솔루션
- 명시적으로 삭제, Expire를 설정하지 않으면 데이터는 삭제되지 않는다. 즉, 영구적으로 보존된다.
- 데이터베이스로도 사용될 수 있는 기술이다.
- NoSQL 중에서도 Redis가 주목 받는 이유
     - 데이터 저장소로 입출력이 가장 빠른 메모리를 채택
     - 단순한 구조인 Key-Value 방식을 통해 빠른 속도를 보장
     - 캐시 및 데이터 스토어에 유리
     - 다양한 API 지원
     - 메모리를 활용하면서 영속적인 데이터 보존이 가능하다.
- 단점
     - 메모리 파편화가 발생하기 쉽다
          - 메모리를 2배로 사용한다.
          - Copy-on-Write 방식으로 인한 문제점
               - Redis를 사용할 때는 데이터 변경이 잦기 때문에, 실제 메모리 크기만큼 자식 프로세스가 복사하게 된다.
               - 그래서 실제로 필요한 메모리 양보다 더 많은 메모리를 사용하게 된다.
               - 추후 이 문제의 원인에 대한 자세한 정리 : http://redisgate.kr/redis/configuration/copy-on-write.php 

 

### Nginx

- 리버스 프록시(reverse proxy)
     - 클라이언트가 가짜 서버에 요청(request)하면, 프록시 서버가 배후 서버(reverse server)로부터 데이터를 가져오는 역할
     - 여기서 프록시 서버가 Nginx, 리버스 서버가 응용 프로그램 서버를 의미
     - 리버스 프록시(Nginx)를 두는 이유는 요청(request)에 대한 버퍼링이 있기 때문이다. 
     - 클라이언트가 직접 App 서버에 직접 요청하는 경우, 프로세스 1개가 응답 대기 상태가 되어야만 한다. 
     - 따라서 프록시 서버를 둠으로써 요청을 배분하는 역할을 한다.
     - 보안을 향상시킨다. WAS는 보통 DB 서버와 연결되므로 WAS가 최전방에 있으면 WAS가 침입당할 경우 DB서버까지 같이 침입당하는 심각한 문제가 발생할 수 있다.


<img src="https://raw.githubusercontent.com/Garamda/WebProgramming/master/images/Nginx.png">

<br>

### 예외 처리

- https://okky.kr/article/362305

<br>

### https

<br>

### JVM Garbage Collection 

<br>

### 웹 아키텍처
- https://blog.rhostem.com/posts/2018-07-22-web-architecture-101
- AOMC에 적용하면서 (코드 상으로 반영할 수 없다면 개념 상으로라도) 하나씩 정리해볼 것

<br>

## 출처

* Web Programming : https://www.edwith.org/boostcourse-web/joinLectures/12952

* Non-blocking, Asynchronous, and Concurrency : https://tech.peoplefund.co.kr/2017/08/02/non-blocking-asynchronous-concurrency.html?utm_source=gaerae.com&utm_campaign=%EA%B0%9C%EB%B0%9C%EC%9E%90%EC%8A%A4%EB%9F%BD%EB%8B%A4&utm_medium=social

* [Session] 웹 서버 개발의 Session 전략 : https://devhaks.github.io/2019/04/20/session-strategy/?fbclid=IwAR0Y6_dIH5qy3KAOARe9kGru0XsJFassd1948LW9YLDNQGWulypk9DLK1t0

* [Spring] RequestParam과 RequestBody의 차이 : https://github.com/occidere/notepad/issues/41

* [Micro Service Architecture] : http://channy.creation.net/articles/microservices-by-james_lewes-martin_fowler

* [Redis] 개념과 특징 : https://goodgid.github.io/Redis/

* [Redis] Copy on Write로 인한 메모리 사용량 증가 문제 진단: http://redisgate.kr/redis/configuration/copy-on-write.php

* [SOLID] 객체지향 개발 5대 원리 : http://www.nextree.co.kr/p6960/?fbclid=IwAR0uL_OPI5kAx8r1yH6bObZ3MpfyckHkqWaEZ1gLwI-M-tU1KvuUuQ7D-1A

* [Git] 좋은 Git 커밋 메시지를 작성하는 방법 : https://meetup.toast.com/posts/106

* [https] https://webactually.com/2018/11/http%EC%97%90%EC%84%9C-https%EB%A1%9C-%EC%A0%84%ED%99%98%ED%95%98%EA%B8%B0-%EC%9C%84%ED%95%9C-%EC%99%84%EB%B2%BD-%EA%B0%80%EC%9D%B4%EB%93%9C/

* [RequestDispatcher] https://dololak.tistory.com/502

* [HTTP Status Code] https://ko.wikipedia.org/wiki/HTTP_%EC%83%81%ED%83%9C_%EC%BD%94%EB%93%9C

* [Hibernate VS Mybatis 1] https://stackoverflow.com/questions/1984548/hibernate-vs-ibatis

* [Hibernate VS Mybatis 2] https://okky.kr/article/286812

* [Spring 요청 처리 과정] http://blog.naver.com/duco777/220605479481

* [예외 처리에 대한 6 가지 화두] https://okky.kr/article/362305

* [자바에서 null을 안전하게 다루는 방법] https://www.slideshare.net/gyumee/null-142590829?fbclid=IwAR2NvlfYGCfYZ7COqvTYQPbenIS8pMlIaS_yNmni0PeWTZLQ-pZts9saZBQ

* [Spring Test] https://www.slideshare.net/ssuser59a869/ksug-2019?fbclid=IwAR2UcYpT58l7AUEPj8vAXIUpllk4meCTlLk4aGDZJSnaECgMwpRR1sVkYAc

* [자바에서 final 멤버 변수에 관례적으로 static을 붙이는 이유] https://djkeh.github.io/articles/Why-should-final-member-variables-be-conventionally-static-in-Java-kor/

* [@Transactional 꼭 설정해야 하는건가요?] https://okky.kr/article/437870

* [JVM Garbage Collection] https://perfectacle.github.io/2019/05/07/jvm-gc-basic/

* [Stack Trace 읽는 법 1] https://okky.kr/article/338405

* [Stack Trace 읽는 법 2] https://hashcode.co.kr/questions/2162/stack-trace%EA%B0%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80%EC%9A%94-%EC%95%A0%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98-%EC%97%90%EB%9F%AC%EB%A5%BC-%EB%94%94%EB%B2%84%EA%B9%85%ED%95%A0-%EB%95%8C-%EA%B7%B8%EA%B2%83%EC%9D%84-%EC%96%B4%EB%96%BB%EA%B2%8C-%ED%99%9C%EC%9A%A9%ED%95%B4%EC%95%BC-%ED%95%98%EB%82%98%EC%9A%94

* [에러 대처 방법] https://okky.kr/article/311337

* [Nginx 1] https://whatisthenext.tistory.com/123

* [Nginx 2] https://www.lesstif.com/pages/viewpage.action?pageId=21430345
