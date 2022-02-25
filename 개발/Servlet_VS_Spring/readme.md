# servlet vs spring

## Servlet

동적인 페이지를 만드는데 사용되는 웹서버의 프로그램

![Servlet을 사용할 경우, 비즈니스 로직(처리 로직)에 집중할 수 있게 됨](servlet%20vs%200fa94/Untitled.png)

Servlet을 사용할 경우, 비즈니스 로직(처리 로직)에 집중할 수 있게 됨

### http 요청

- 직접 파싱:

```visual-basic
GET /api/products HTTP/1.1
Content-Type : application/json
User-Agent: PostmanRuntime/7.28.0
Accept: */*
Postman-Token : abfcbcf8-9317-430c-86b9-c00020eb736e
Host : localhost:8080
Accept-Encoding: gzip, deflate, br
Connection : keep-alive
```

- servlet을 사용할 경우

```java
HttpServletRequest.getMethod();
```

→  서비스 메서드만 재정의해서  처리 방법을 지정

### Servlet Container

서블릿을 담고 관리하는 컨테이너

![사용자 요청이 들어오면 서블릿 컨테이너가 해당 요청과 매핑된 서블릿을 찾는다](servlet%20vs%200fa94/Untitled%201.png)

사용자 요청이 들어오면 서블릿 컨테이너가 해당 요청과 매핑된 서블릿을 찾는다

1. Servlet Request/Servlet Response 객체 생성

    
    ```java
    public class MyServlet extends HttpServlet{
    	@Override
    	protected void doGet(HttpServletRequest req,HttpServletResponse resp)
    	throws IOException{
    		PrintWriter w=resp.getWriter();
    		w.println("Hello");
    	}//end of doGet
    }//end of class
    ```
    
2. 설정 파일을 참고하여 매핑할 Servlet 확인 → 설정 파일에 정의되어있음

    
    ```xml
    <servlet>
    	<servlet-name>HelloServlet</servlet-name>
    	<servlet-class>servlet.HelloServlet</servlet-class>
    </servlet>
    <servlet-mapping>
    	<servlet-name>HelloServlet</servlet-name>
    	<url-pattern>/hello</url-pattern>
    </servlet-mapping>
    ```
    
3. 해당 서블릿 인스턴스 존재 유무를 확인하여 없으면 생성 `init()`
4. Servlet container에 스레드를 생성하고 앞서만든 res,req를 인자로 service 호출
5. 응답 처리 후 response 와 request 객체 소멸
→ 서블릿은 생성만 하고 소멸시키지 않음 : `singleton pattern`
소멸되지 않고 있다가 다음번 같은 요청이 들어왔을 때, 서블릿 컨테이너에 의해 재호출되어 사용됨. 즉, Servlet Container는 서블릿의 생명주기를 관리하는 객체임 (서블릿 생성, 필요시 호출, 적절한 시점에 소멸)

### 여러 요청

한 요청을 처리하는 도중 여러 요청이 들어오면 멀티스레드로 요청을 처리하게 된다

멀티 스레드 사용 시 주의점 : 

스레드 생성 비용이 크고, 다른 스레드로 전환하는 context switch가 많은 오버헤드를 야기함. 또, 스레드 생성에 제한이 없으면 많은 요청을 처리하기 위해 그많금 많은 스레드를 생성하다가 서버의 하드웨어 한계를 넘으면 서버가 터짐

이 때, 요청을 받고 응답을 만들고, 요청에 맞는 서블릿을 찾는 과정(Handler)이 매번 중복되며, 이 **공통 로직을 한번에 처리할 수 있는 방법이** `Dispatcher Servlet` 이다

<aside>
✔️ `Dispatcher Servlet`
Dispatcher Servlet 하나로 모든 요청을 수행
요청이 들어오면 서블릿 컨테이너의 제일 앞에서 모든 요청을 받아 적절한 하위 서블릿으로 작업을 위임함
`Dispatcher Servlet`은 `Spring` 에서 **웹 요청을 처리**할 때 사용됨
→ 개발자는 컨트롤러(Handler)에만 집중하면 됨
→ 나머지 요청 처리 핸들러 검색, 핸들로 호출, 뷰 검색 또는 생성 기능은 스프링의 IOC 컨테이너로 부터 주입받아 사용하고 동작됨

</aside>

## Spring

**따라서, Spring을 사용함으로써 개발자는 웹 요청을 처리하는 로직에만 집중할 수 있음**

### 스프링의 웹 요청 처리 흐름

Dispatcher를 사용함

![Untitled](servlet%20vs%200fa94/Untitled%202.png)

---

1. 클라이언트로 부터 들어오는 **모든 요청을 Dispatcher Servlet이 받는다**.
2. Dispatcher Servlet은 Handler Mapping을 통해 요청을 **처리할 Controller를 검색**한다.
3. Dispatcher Servlet은 검색된 Controller를 실행하여 클라이언트의 요청을 처리한다.
4. Controller는 비즈니스 로직의 수행 결과로 얻어낸 Model 정보와 Model을 보여줄 View 정보를 ModelAndView 객체에 저장하여 리턴한다.
5. Dispatcher Servlet은 전달받은 View이름과 매칭되는 실제 View를 찾기 위해 ViewResolver에게 요청하고ViewResolver는 결과를 보여줄 View를 찾아서 Dispatcher Servlet에게 전달한다.
6. Dispatcher Servlet은 ViewResolver를 통해 찾아낸 View를 실행하여 **사용자에게 응답을 전송**한다.

---

Reference :

[https://www.youtube.com/watch?v=calGCwG_B4Y&t=14s](https://www.youtube.com/watch?v=calGCwG_B4Y&t=14s)

[https://moonsbeen.tistory.com/321](https://moonsbeen.tistory.com/321)