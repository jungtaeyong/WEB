# JSP

jsp를 이해하려면 먼저 servlet에 대해 이해해야 한다. servlet은 서버에서 웹페이지 등을 동적으로 생성하거나 데이터 처리를 수행하기 위해 자바로 작성된 프로그램이다. servlet은 Java 코드 안에 HTML태그가 삽입된 형태의 Java 언어이다. 그래서 **servlet을 HTML in Java**라고 표현한다. servlet은 **클라이언트 요청을 처리하고 그 결과를 다시 클라이언트에게 전송하는 servlet클래스의 구현 규칙을 지킨 자바프로그램**이라고 정의할 수 있다. 

**그렇다면 servlet만으로도 웹 프로그래밍이 가능한데, 왜 JSP가 나오게 되었을까?**

servlet은 인터페이스(view)를 구현하기 위해 너무 많은 코드가 필요했다. 아래의 코드를 보면 `HTML`을 작성하기 위해 servlet을 이용하면 너무나도 불편한 것을 알 수 있다.

```java
public class HelloServlet extends HttpServlet{
    public void doGet(HttpServletRequest req, HttpServletResponse res)
        	throws ServletException,IOException{
        res.setContentType("text/html;charset=UTF-8");
        
        PrintWriter out = res.getWriter();
        
        out.println("<HTML>");
        out.println("<BODY>");
        out.println("Hello World!!");
        out.println("</BODY>");
        out.println("</HTML>");
        out.close();
    }
}
```

위의 소스코드에서 `HelloServlet`클래스는 `HttpServlet`클래스를 상속받고 있는데, 구조는 아래와 같다.

<p align="center"><img src="https://user-images.githubusercontent.com/52786355/84744203-e4dcb180-afed-11ea-9686-2f9f6290bdfc.PNG"></p>

Servlet은 기본적으로 Servlet이라는 인터페이스를 GenericServlet이라는 추상클래스가 상속받고 있고, 이 GenericServlet 추상클래스를 다시 HttpServlet이 상속받고 있는 구조이다. 따라서 HttpServlet을 상속받아 사용해 위 그림의 모든 클래스의 기능을 사용할 수 있는 것이다. 

이러한 문제점을 해결하고자 servlet을 작성하지 않고도 간편하게 구현할 수 있도록 만든 것이 jsp이다. 아래와 같이 `HTML`안에 `Java`코드를 삽입하는 형태의 JSP가 등장하게 되었다.

```jsp
<%@page import="java.util.Calendar"%>
<%@ page language="java" contentType="text/html; charset=EUC-KR"
    pageEncoding="EUC-KR"%>
<%
	String day = String.format("%tF", Calendar.getInstance());
%>
<!DOCTYPE html>
<html>
<head>
<meta charsert="EUC-KR">
<title>Insert title here</title>
</head>
<body>
	Hello world~~ (<%=day %>)    
</body>
</html>
```

jsp는 자바코드가 HTML안에 있다고해서 **Java In HTML**이라고 표현한다. jsp의 장점은 다음과 같다.

- Servlet에 비해 매우 편리해 생산성이 높다.

- Java 기반이기 때문에 플랫폼에 독립적이다.
- JSP파일이 Servlet으로 변환되는 과정은 오직 한 번만 수행되므로 같은 페이지에 수 많은 사용자의 요청이 있더라도 처리속도는 거의 유지된다. JSP 페이지의 코드가 변경된다면 Servlet으로의 변환과정을 다시 한 번 진행하게 된다.

JSP는 실행시 java소스 코드로 변환한 다음 컴파일되어 실행된다. 이 JSP 파일을 Servlet 클래스로 변환하고 실행시켜 주는 역할을 하는 프로그램을 서블릿 컨테이너라고 부른다. 서블릿 컨테이너의 대표적인 예로 톰캣이 있다. 서블릿 컨테이너도 java 프로그램이며, Java Virtual Machine 위에서 실행된다.

 ![jsp1](https://user-images.githubusercontent.com/52786355/84742749-e60cdf00-afeb-11ea-85ba-0d5d4f8ec949.PNG)

위 그림에서 Java파일은 Servlet이라고 할 수 있다. Java파일로 변환하는 과정은 서블릿 컨테이너에서 하고, 그 예로 톰캣이 있는데, 톰캣 폴더의 해당 프로젝트 경로에 들어가보면 실제로 .java 파일이 있다. java파일을 확인해보면 위에 소스코드 처럼 servlet 형대로 변환되어 있다. 따라서 **JSP를 쓴다는 것은 Servlet을 쓴다는 의미**이다. 따라서 Servlet에 대해 자세히 알고 있어야한다.



## Index

- [Servlet](#Servlet)



## Servlet

- 서블릿 컨테이너 동작방식 <br>

  서블릿은 도움이 필요하다. 요청이 들어오면 누군가 요청을 처리할 새로운 스레드를 만들거나 서블릿에서 필요한 메서드를 호출해야 한다. (새로운 스레드를 만든다는 것이지 새로운 인스턴스를 생성한다는 뜻이 아니다. 인스턴스는 최초시작시 한 번만 생성해 계속 재활용한다. 또한, 무제한 쓰레드를 생성하는 것이 아니라 활용가능 한 쓰레드는 쓰레드 풀에 저장했다가 다시 꺼내 쓴다. ) 이 역할을 하는 것이 바로 컨테이너이다. 웹 서버가 클라이언트로부터 서블릿에 대한 요청을 받으면 컨테이너에게 이 요청을 넘긴다. 요청을 넘겨받은 컨테이너는 서블릿을 찾아 필요한 메소드를 호출하게 된다. 그럼 컨테이너의 동작 방식을 살펴보자.

  ![servlet1](https://user-images.githubusercontent.com/52786355/84839245-9247d780-b077-11ea-81e7-f1ba7f5518dc.PNG)

  <center>[서블릿 컨테이너의 동작방식 구조도]</center>

  1. 클라이언트가 url을 통해 요청을 보내면 HTTP Request를 Servlet Container로 전송한다.
  2. HTTP Request를 전송받은 Servlet Container는 `HttpServletRequest`, `HttpServletResponse` 두 객체를 생성한다.
  3. (web.xml은 사용자가) 그 다음에는 요청한 url을 분석하여 어느 서블릿에 대해 요청을 한 것인지 찾는다.
  4. 해당 서블릿에서 service메소드를 호출한 후 POST, GET 여부에 따라 `doGet()` 또는 `doPost()`를 호출한다.
  5. `doGet()` or `doPost()` 메소드는 동적 페이지를 생성한 후 `HttpServletRespons` 객체에 응답을 보낸다.
  6. 응답이 끝나면 `HttpServletRequest`, `HttpServletResponse` 두 객체를 소멸시킨다.

  여기서 `HttpServletRequest`, `HttpServletResponse` 객체를 생성한 컨테이너는 요청에 알맞은 서블릿을 찾게 되는데 이 서블릿을 찾기 위해서는 개발자가 서블릿을 매핑해줘야 한다. 그렇지 않으면 적절한 서블릿을 찾을 수 있는 정보가 없기 때문에 컨테이너는 서블릿을 찾지 못한다.

![servlet2](https://user-images.githubusercontent.com/52786355/84840249-f9668b80-b079-11ea-91a7-59c267298db0.PNG)

<center>[서블릿 매핑 구조도]</center>



- Servlet 라이프 사이클 (생명주기)
  어떤 기술이든 라이프 사이클은 중요하다. 생명주기를 정확하게 알고 있어야 필요한 시점에 필요한 기능(메소드)을 사용할 수 있기 때문이다.

![jsp3](https://user-images.githubusercontent.com/52786355/84840735-60387480-b07b-11ea-99d7-b44016b02020.PNG)

Servlet의 사용도가 높은 이유는 빠른 응답 속도 때문이다. Servlet은 한 번(최초 요청 시)만 객체가 생성되어 메모리에 로딩되고, 이후 요청 시에는 기존의 객체를 그대로 재활용한다. 여러 번 객체를 생성할 필요가 없기 때문에 속도가 빠르다. 이후 클라이언트가 요청 할 때마다 요청에 따라 doGet(), doPost() 메소드가 호출된다. 이후 서버를 종료하거나 중단했을 시 자원을 한 번 해제한다.

- 선처리, 후처리
  - @PostConstruct : Servlet 객체생성과 Init()호출 사이에 실행되는 메소드 (선처리)
  - @PreDestroy : destroy() 호출 이후 실행되는 메소드 (후처리)

- ServletConfig
  특정 Servlet이 생성될 때, 초기에 필요한 데이터들이 있다. 예를 들어 경로 및 아이디 정보 등이다. 이러한 데이터들을 초기화 파라미터라고 하며, web.xml에 기술하고 Servlet파일에서는 ServletConfig 클래스를 이용해서 접근(사용)한다. 2가지 방법이 있다.

  1. web.xml파일에 초기화 파라미터를 기술

     ```xml
     <?xml version="1.0" encoding="UTF-8"?>
     <web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd" id="WebApp_ID" version="3.1">
       <display-name>ex</display-name>
       <welcome-file-list>
         <welcome-file>index.html</welcome-file>
         <welcome-file>index.htm</welcome-file>
         <welcome-file>index.jsp</welcome-file>
         <welcome-file>default.html</welcome-file>
         <welcome-file>default.htm</welcome-file>
         <welcome-file>default.jsp</welcome-file>
       </welcome-file-list>
       <!-- 핵심 로직 -->
       <servlet>
       	<servlet-name>InitParam</servlet-name>
           <!-- 설정한 경로 -->
       	<servlet-class>com.javalec.ex.InitParam</servlet-class>
       	<init-param>
       		<param-name>id</param-name>
       		<param-value>abcde</param-value>
       	</init-param>
       	<init-param>
       		<param-name>pw</param-name>
       		<param-value>12345</param-value>
       	</init-param>
       </servlet>
       <servlet-mapping>
       	<servlet-name>InitParam</servlet-name>
       	<url-pattern>/IP</url-pattern>
       </servlet-mapping>
     </web-app>
     ```

     

  2. @Webvlet 어노테이션에 데이터를 직접 기술

     ```java
     @WebServlet(urlPatterns={"/InitP"}, initParams={@WebInitParam(name="id2",value="aaaaa"), @WebInitParam(name="pw2", value="9999")})
     public class InitParam extends HttpServlet { 
         ...
     ```

     

- ServletContext
  

- ServletContextListener







#### 참고자료 : [배움이 즐거운 개발자님 블로그](https://galid1.tistory.com/488), [나무위키](https://namu.wiki/w/JSP), [Seoul Wiz 블스님 JSP 유튜브 강의](https://www.youtube.com/watch?v=dWkKwWDQxio&list=PLieE0qnqO2kTyzAlsvxzoulHVISvO8zA9&index=35)

