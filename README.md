# 웹 프로그래밍

1. 브라우저

- Parser : 데이터를 해석
- Rendering Engine : 데이터를 화면에 표현
- Parser와 Rendering Engine이 html, css를 처리하는 과정

     
     <img src="https://github.com/Garamda/WebProgramming/blob/master/parsingtree.png" width=60%>
     
<br>

2. WAS

     Web Application Server의 줄임말
     
     <img src="https://github.com/Garamda/WebProgramming/blob/master/was.PNG" width=60%>
     
<br>
 
3. 웹 서버 vs WAS

- WAS도 보통 자체적으로 웹 서버 기능을 내장하고 있다.
- 현재는 WAS가 가지고 있는 웹 서버도 정적인 콘텐츠를 처리하는 데 있어서 성능상 큰 차이가 없다.
- 규모가 커질수록 웹 서버와 WAS를 분리한다.
- 자원 이용의 효율성, 장애 극복, 배포와 유지보수의 편의성을 위해 웹 서버와 WAS를 대체로 분리한다.

<br>

4. 자바 웹 어플리케이션(Java Web Application)

- WAS에 설치(deploy)되어 동작하는 어플리케이션
- HTML, CSS, 이미지, Java Class(Servlet, Package, Interface 등), 각종 설정 파일 등이 포함

<br>

5. Servlet

- 자바 웹 어플리케이션의 구성요소 중 동적인 처리를 하는 프로그램의 역할
- WAS에 동작하는 Java 클래스
- Servlet은 HttpServlet 클래스를 상속받아야 함


# 웹 프로그래밍과 관련이 있는 전공 지식

1. Non-blocking

- Non-blocking algorithm
- Non-blocking I/O

2. Concurrency VS Parallelism

3. Asynchronous Programming


## 출처

* https://www.edwith.org/boostcourse-web/joinLectures/12952

* https://tech.peoplefund.co.kr/2017/08/02/non-blocking-asynchronous-concurrency.html?utm_source=gaerae.com&utm_campaign=%EA%B0%9C%EB%B0%9C%EC%9E%90%EC%8A%A4%EB%9F%BD%EB%8B%A4&utm_medium=social
