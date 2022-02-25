# 정적(Static), 동적(Dynamic Page)

## ![image](https://user-images.githubusercontent.com/71022555/140637192-c6536d0c-5132-471f-a4ad-6f81be8877c3.png)

## 1. 정적 페이지(Static Pages)

- ### Web Server는 파일 경로 이름을 받아 경로와 일치하는 file contents를 반환한다.
- ### 항상 동일한 페이지를 반환한다.
- ### Ex) image, html, css, javascript 파일과 같이 웹 서버에 미리 저장된 파일이 (HTML, 이미지, CSS, JavaScript) 그대로 전달

### 장점

- 빠르다, 비용이 적다.

### 단점

- 서비스가 한정적이다. 관리,유지보수의 불편함

---

<br>

## 2. 동적 페이지(Dynamic Page)

- ### 서버(Web Server)에 있는 데이터들을 스크립트에 의해 가공처리한 후 생성되어 전달되는 웹페이지
- ### 사용자의 요청을 해석하여 데이터를 가공한 후 생성된 웹 페이지를 전송
- ### 상황, 시간, 요청에 따라 달라지는 웹 페이지 제공 ex(SNS)

### 장점

- 다양한 정보를 조합하여 다양한 서비스 제공 가능
- 유지 보수의 편리함

### 단점

- 상대적으로 느린 속도
- 추가적인(Web Application Server(WAS)) 설치를 위한 추가 자원 필요

---

<br>

# Web Server

![image](https://user-images.githubusercontent.com/71022555/140637417-dfdbf0a5-18eb-4b1d-a7ce-ee8823489940.png)
<br>

### 웹 서버란 클라이언트(사용자)가 웹 브라우저에서 어떠한 요청을 하면 웹 서버에서 그 요청을 받아 정적 컨텐츠를 제공하는 서버이다. 정적 컨텐츠란 단순 HTML 문서, CSS, JavaScript, 이미지, 파일 등 즉시 응답가능한 컨텐츠이다. (웹 서버가 동적 컨텐츠를 요청 받으면 WAS에게 해당 요청을 넘겨주고 WAS에서 처리한 결과를 클라이언트 사용자에게 전달해주는 역할도 한다.)

<br>

### Web Server의 예

- Apache Server, Nginx, IIS(Windows 전용 Web 서버) 등

---

<br>

# Web Application Server(WAS)

![image](https://user-images.githubusercontent.com/71022555/140637383-28642d4d-1368-4c9e-b836-69b84ee576ce.png)
<br>

- ### 인터넷 상에서 HTTP 프로토콜을 통해 사용자 컴퓨터나 장치에 애플리케이션을 수행해주는 미들웨어로서, 주로 동적 서버 컨텐츠를 수행하는 것으로 웹 서버와 구별의 되며, 주로 데이터베이스 서버와 같이 수행

- ### WAS는 웹 서버와 웹 컨테이너가 합쳐진 형태로서, 웹 서버 단독으로는 처리할 수 없는 데이터베이스의 조회나 다양한 로직 처리가 필요한 동적 컨텐츠를 제공한다. 덕분에 사용자의 다양한 요구에 맞춰 웹 서비스를 제공할 수 있다. WAS는 JSP, Servlet 구동환경을 제공해주기 때문에 웹 컨 테이너 혹은 서블릿 컨테이너라고 불린다.
  ![image](https://user-images.githubusercontent.com/71022555/140641192-195f5337-c7b2-47c7-81e8-12d6565fdf00.png)
  <br>

---

## Servlet(서블릿)

- ### 클라이언트의 요청을 처리하고, 그 결과를 반환하는 Servlet 클래스의 구현 규칙을 지킨 자바 웹 프로그래밍 기술
- ### 클라이언트의 Request에 대해 동적으로 작동하는 웹 애플리케이션 컴포넌트
- ### MVC 패턴에서의 컨트롤러로 이용된다.
  ![image](https://user-images.githubusercontent.com/71022555/140641285-ca1d0b24-4ff9-4e69-87f2-5ba0de410519.png)
  <br>

---

## 웹 컨테이너(Container)

![image](https://user-images.githubusercontent.com/71022555/140641119-b97219a7-81b4-460d-b7f9-950ba95392ad.png)

- ### WAS 내부에서 개발자 대신 서블릿을 관리
- ### WAS 별로 다양한 종류의 컨테이너를 내장하고 있으며, 이들 중 서블릿에 관련된 기능들을 모아 놓은 것을 서블릿 컨테이너라 부른다.
- ### 서블릿 컨테이너는 클라이언트의 요청(Request)을 받아주고 응답(Response)할 수 있게, 웹서버와 소켓으로 통신하며 대표적인 예로 톰캣(Tomcat)이 있습니다. 톰캣은 실제로 웹 서버와 통신하여 JSP(자바 서버 페이지)와 Servlet이 작동하는 환경을 제공해줍니다.

---

<br>

### 참고문헌

<br>

https://codechasseur.tistory.com/25
<br>

https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html
<br>

https://www.educative.io/edpresso/
