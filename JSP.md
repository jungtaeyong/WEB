# JSP(Java Server Page)

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

JSP는 실행시 java소스 코드로 변환한 다음 컴파일되어 실행된다. 이 JSP 파일을 Servlet 클래스로 변환하고 실행시켜 주는 역할을 하는 프로그램을 서블릿 컨테이너라고 부른다. 서블릿 컨테이너의 대표적인 예로 톰캣이 있다. 서블릿 컨테이너도 java 프로그램이며, Java Virtual Machine 위에서 실행된다. 이 부분이 조금 헷갈리는데, JSP 컨테이너라는 것이 실제로 존재하지 않는다고 한다. 서블릿 컨테이너의 대표적인 예가 톰켓인데, 이 톰캣 안에 JSP파일을 서블릿 파일로 변환해주는 JSP엔진(JSPServlet)이 존재한다. 그러니까 서블릿 컨테이너(=톰캣)은 JSP 컨테이너이기도 한 것이다. (톰캣 내부에 JSP엔진이 있으니까.)

 ![jsp1](https://user-images.githubusercontent.com/52786355/84742749-e60cdf00-afeb-11ea-85ba-0d5d4f8ec949.PNG)

위 그림에서 Java파일은 Servlet이라고 할 수 있다. Java파일로 변환하는 과정은 서블릿 컨테이너에서 하고, 그 예로 톰캣이 있는데, 톰캣 폴더의 해당 프로젝트 경로에 들어가보면 실제로 .java 파일이 있다. java파일을 확인해보면 위에 소스코드 처럼 servlet 형대로 변환되어 있다. 따라서 **JSP를 쓴다는 것은 Servlet을 쓴다는 의미**이다. 따라서 Servlet에 대해 자세히 알고 있어야한다.



## Index

- [Servlet](#Servlet)

- [JSP](#JSP)


## Servlet

### 서블릿 컨테이너 동작방식

서블릿은 도움이 필요하다. 요청이 들어오면 누군가 요청을 처리할 새로운 스레드를 만들거나 서블릿에서 필요한 메서드를 호출해야 한다. (새로운 스레드를 만든다는 것이지 새로운 인스턴스를 생성한다는 뜻이 아니다. 인스턴스는 최초시작시 한 번만 생성해 계속 재활용한다. 또한, 무제한 쓰레드를 생성하는 것이 아니라 활용가능 한 쓰레드는 쓰레드 풀에 저장했다가 다시 꺼내 쓴다. ) 이 역할을 하는 것이 바로 컨테이너이다. 웹 서버가 클라이언트로부터 서블릿에 대한 요청을 받으면 컨테이너에게 이 요청을 넘긴다. 요청을 넘겨받은 컨테이너는 서블릿을 찾아 필요한 메소드를 호출하게 된다. 그럼 컨테이너의 동작 방식을 살펴보자.

![servlet1](https://user-images.githubusercontent.com/52786355/84839245-9247d780-b077-11ea-81e7-f1ba7f5518dc.PNG)

<p align="center">[서블릿 컨테이너의 동작방식 구조도]</p>



1. 클라이언트가 url을 통해 요청을 보내면 HTTP Request를 Servlet Container로 전송한다.
2. HTTP Request를 전송받은 Servlet Container는 `HttpServletRequest`, `HttpServletResponse` 두 객체를 생성한다.
3. 그다음에는 요청한 url을 분석하여 어느 서블릿에 대해 요청을 한 것인지 찾는다. (web.xml에서 진행하며, 개발자가 매핑한다.)
4. 해당 서블릿에서 service메소드를 호출한 후 POST, GET 여부에 따라 `doGet()` 또는 `doPost()`를 호출한다.
5. `doGet()` or `doPost()` 메소드는 동적 페이지를 생성한 후 `HttpServletRespons` 객체에 응답을 보낸다.
6. 응답이 끝나면 `HttpServletRequest`, `HttpServletResponse` 두 객체를 소멸시킨다.

여기서 `HttpServletRequest`, `HttpServletResponse` 객체를 생성한 컨테이너는 요청에 알맞은 서블릿을 찾게 되는데 이 서블릿을 찾기 위해서는 개발자가 서블릿을 매핑해줘야 한다. 그렇지 않으면 적절한 서블릿을 찾을 수 있는 정보가 없기 때문에 컨테이너는 서블릿을 찾지 못한다.

![servlet2](https://user-images.githubusercontent.com/52786355/84840249-f9668b80-b079-11ea-91a7-59c267298db0.PNG)

<p align="center">[서블릿 매핑 구조도]</p>



### Servlet 라이프 사이클 (생명주기) 
어떤 기술이든 라이프 사이클은 중요하다. 생명주기를 정확하게 알고 있어야 필요한 시점에 필요한 기능(메소드)을 사용할 수 있기 때문이다.

<p align="center"><img src="https://user-images.githubusercontent.com/52786355/84840735-60387480-b07b-11ea-99d7-b44016b02020.PNG"></p>

Servlet의 사용도가 높은 이유는 빠른 응답 속도 때문이다. Servlet은 한 번(최초 요청 시)만 객체가 생성되어 메모리에 로딩되고, 이후 요청 시에는 기존의 객체를 그대로 재활용한다. 여러 번 객체를 생성할 필요가 없기 때문에 속도가 빠르다. 이후 클라이언트가 요청 할 때마다 요청에 따라 doGet(), doPost() 메소드가 호출된다. 이후 서버를 종료하거나 중단했을 시 자원을 한 번 해제한다.


### 선처리, 후처리

- @PostConstruct : Servlet 객체생성과 Init()호출 사이에 실행되는 메소드 (선처리)
- @PreDestroy : destroy() 호출 이후 실행되는 메소드 (후처리)
  

### ServletConfig 
**특정 Servlet**이 생성될 때, 초기에 필요한 데이터들이 있다. 예를 들어 경로 및 아이디 정보 등이다. 이러한 데이터들을 초기화 파라미터라고 하며, web.xml에 기술하고 Servlet파일에서는 ServletConfig 클래스를 이용해서 접근(사용)한다. 2가지 방법이 있다.

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
         <!-- 사용할 특정 클래스명 -->
     	<servlet-name>InitParam</servlet-name>
         <!-- 사용할 특정 클래스의 정확한 경로 -->
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

   이후 `InitParam`.class (서블릿 파일)에서 호출한다.

   ```java
   protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
   		String id = getInitParameter("id");
   		String pw = getInitParameter("pw");
       	System.out.println("id : "+id);
   		System.out.println("pw : "+pw);
   					...
   ```

   

2. @Webvlet 어노테이션에 데이터를 직접 기술

   ```java
   @WebServlet(urlPatterns={"/InitP"}, initParams={@WebInitParam(name="id2",value="aaaaa"), @WebInitParam(name="pw2", value="9999")})
   public class InitParam extends HttpServlet { 
       		...
   ```

   

### ServletContext

**모든 Servlet**에서 특정 데이터를 공유해야 할 경우, context parameter를 이용해서 web.xml에 데이터를 기술하고, Servlet에서 공유하면서 사용 할 수 있다.

모든 servlet에서 사용할 데이터를 `web.xml`에 key, value로 기술

```xml
<web-app>
    ...
    
<context-param>
  	<param-name>allId</param-name>
  	<param-value>all ID</param-value>
  </context-param>
  <context-param>
  	<param-name>allPw</param-name>
  	<param-value>all PW</param-value>
  </context-param>
</web-app>
```

이후 어떤 서블릿(class)에서도 key를 참조해 `getServletContext().getInitParameter("key")`로 불러올 수 있다.

```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
String allId = getServletContext().getInitParameter("allId");
		String allPw = getServletContext().getInitParameter("allPw");
		
		System.out.println("allId : "+allId);
		System.out.println("allPw : "+allPw);
    				...
```



### ServletContextListener 
**웹 어플리케이션의 생명주기를 감시하는 리스너**이다. (서블릿이 아닌 클래스이다.) 리스너의 해당 메소드가 웹 어플리케이션의 시작(`contextInitialized(ServletContextEvent arg()){ ... }`)과 종료시(`contextDestroted(ServletContextEvent arg()){ ... })`) 호출 된다. 
먼저 리스너 클래스를 생성하고, ServletContextListener의 인터페이스를 implements한다. 이후 해당 메소드들을 오버라이딩해 기능을 구현한다.

```java
// @WebListener 사용시 web.xml에 등록안해도 됨 
public class ServletL implements ServletContextListener {
	@Override
	public void contextDestroyed(ServletContextEvent sce) {
		System.out.println("contextDestroyed");
	}

	@Override
	public void contextInitialized(ServletContextEvent sce) {
		System.out.println("contextInitialized");
	}

}
```

web.xml에 리스너로 등록을 해주거나, 해당 클래스에 `@WebListene` 어노테이션을 이용해 등록한다.

```xml
<web-app>
    ...
    
  <listener>
  	<listener-class>com.javalec.ex.ServletL</listener-class>
  </listener>
</web-app>
```



## JSP

## Index

- [태그](#태그)
- [내부 객체](#내부-객체)


### 태그

- 지시자 : `<%@  %>` -> 페이지 속성
  - page : 해당 페이지의 전체적인 속성 지정 (설정, java 클래스 import 등)
  - include : 별도의 페이지를 현재 페이지에 삽입
  - taglib : 태그라이브러리의 태그 사용
- 주석 : `<%-- %>` -> HTML에서 주석처리할 경우 브라우저에서 페이지 소스를 보면 주석이 그대로 출력되지만, JSP는 서버단의 언어이기 때문에 주석이 출력되지 않는다.

- 선언 : `<%! %>` -> 변수, 메소드 선언

- 표현식 : `<%= %>` -> 결과값 출력

- 스크립트릿 : `<% %>` -> Java 코드 (제일 많이 쓰게 될 태그)

- 액션태그 : `<jsp:action> </jsp:action>` -> Java Bean 연결

  - `<jsp:forward page="sub.jsp"/>` : forward를 이용하면 다른 페이지로 연결한다. 리다이렉트와 다른 점은 리다이렉트는 아예 다른 url로 이동시키지만, forward는 현재 url을 유지하면서 페이지 내용만 sub.jsp를 출력한다. 다른 페이지로 연결할 때, `jsp:param`을 이용해 name, value로 값을 넘겨줄 수 있다.

    ```jsp
    <jsp:forward page="sub.jsp">
    	<jsp:param name="id" value="ckck5050" />
        <jsp:param name="pw" value="1234"/>
    </jsp:forward>
    <%-- 받는 쪽에선 request.getParameter("id")로 받는다. -->
    ```

    

  - `<jsp:include page="include02.jsp" flush="true"/>` : include를 이용해서 현재 페이지에서 다른 페이지를 추가해 보여준다.

```jsp
<%@ page language="java" contentType="text/html; charset=EUC-KR"
    pageEncoding="EUC-KR"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>Insert title here</title>
</head>
<body>
	<%
		int i=0;
		while(true){
			i++;
            <%-- 입출력 내부객체인 out이용해 출력 --%>
			out.println("2 * "+i+" = "+2*i+"<br>");
	%>
	<%-- 블록 단위로 하지 않아도 된다. 스크립트릿을 끊고 연결하면서 이어쓸 수 있다. --%>
	===================<br>
	<%		
			if(i>9) break;
		}
	%>
    <%= i%><br>
</body>
</html>
```

<p align="center">[태그를 사용한 JSP 예시코드]</p>



### 내부 객체

개발자가 객체를 생성하지 않고 바로 사용할 수 있는 객체가 내부객체 이다. JSP에서 제공되는 내부객체는 JSP 컨테이너에 의해 Servlet으로 변환될 때 자동으로 객체가 생성된다. 내부객체의 종류는 아래와 같다.

- 입출력 객체

  - out : `out.println()`메소드를 이용해 자바의 변수나, 메소드 리턴 값 등을 html상에서 표현 할 수 있다.

  - request : 웹 브라우저를 통해 서버에 어떤 정보를 요청하는 것을 request라고 한다. 그리고 이러한 요청 정보는 request객체가 관리한다.

    ```jsp
    <%@ page language="java" contentType="text/html; charset=EUC-KR"
        pageEncoding="EUC-KR"%>
    <!DOCTYPE html>
    <html>
    <head>
    <meta charset="EUC-KR">
    <title>Insert title here</title>
    </head>
    <body>
        <%--http://localhost:8181/jspEx/ex.jsp 로 요청했을 경우--%>
    	<%
    		out.println("서버 : "+request.getServerName()+"<br />");
    		out.println("포트 번호 : "+request.getServerPort()+"<br />");
    		out.println("요청 방식 : "+request.getMethod()+"<br />");
    		out.println("프로토콜 : "+request.getProtocol()+"<br />");
    		out.println("URL : "+request.getRequestURL()+"<br />");
    		out.println("URI : "+request.getRequestURI()+"<br />");
    	%>
        <%-- 
            서버 : localhost
            포트 번호 : 8181
            요청 방식 : GET
            프로토콜 : HTTP/1.1
            URL : http://localhost:8181/jspEx/ex.jsp
            URI : /jspEx/ex.jsp  
        --%>
    </body>
    </html>
    ```

    GET방식이 아닌 POST방식으로 왔을 때는 무엇이 더 필요할까? 예를들어 회원가입을 할 때, 해당 정보를 입력하고 전송버튼을 누르면 서버, 포트번호 등의 정보 외에도 회원 정보에 대한 데이터들도 추가로 넘어올 것이다. 이러한 정보들을 받는 메서드를 살펴보자

    1. `getParameter(String name)` : name에 해당하는 파라미터 값을 구한다. (단일 값)
    2. `getParameterNames()` : 모든 파라미터 이름을 구한다.
    3. `getParameterValues(String name)` : name에 해당하는 파라미터 값들을 구한다. (배열 값)

    아래의 예제를 살펴보자.

    ```jsp
    <%--Java Arrays 클래스를 쓰기위해 지시자를 이용해 import한다.--%>
    <%@ page import="java.util.Arrays" %>
    <%@ page language="java" contentType="text/html; charset=EUC-KR"
        pageEncoding="EUC-KR"%>
    <!DOCTYPE html>
    <html>
    <head>
    <meta charset="EUC-KR">
    <title>Insert title here</title>
    </head>
    <body>
        <%-- 선언 --%>
    	<%!
    		String name, id, pw, major, protocol;
    		String[] hobbys;
    	%>
        <%-- post로 보낸 값들을 실제 string에 매핑시킨다.
        	 예를 들면 id는 <input type="text" name="id">
        	 태그 요소의 값을 매핑한다.
        --%>
    	<%
    		request.setCharacterEncoding("EUC-KR");
    		
    		name = request.getParameter("name");
    		id = request.getParameter("id");
    		pw = request.getParameter("pw");
    		major = request.getParameter("protocol");
    		<%-- request.getParameterValues메소드로 여러 값을 배열에 매핑한다. --%>
    		hobbys = request.getParameterValues("hobby");
    	%>
        <%-- 첫 줄에 java.util.Arrays를 import시켰기 때문에 사용가능 --%>
        <%= Arrays.toString(hobbys)%><br />
    </body>
    </html>
    ```

  - response : 브라우저의 요청에 응답하는 것을 response라고 하며, 이러한 응답의 정보를 가지고 있는 객체를 response라고 한다.

    1. `getCharacterEncoding()` : 응답할 때 문자의 인코딩 형태를 구한다.
    2. `addCookie(Cookie)` : 쿠키를 지정한다.
    3. `sendRedirect(URL)` : 지정한 URL로 이동한다.

- 서블릿 객체 : page, config

- 세션 객체: session

- 예외 객체 : exception





#### 참고자료 : [배움이 즐거운 개발자님 블로그](https://galid1.tistory.com/488), [나무위키](https://namu.wiki/w/JSP), [Seoul Wiz 블스님 JSP 유튜브 강의](https://www.youtube.com/watch?v=dWkKwWDQxio&list=PLieE0qnqO2kTyzAlsvxzoulHVISvO8zA9&index=35)

