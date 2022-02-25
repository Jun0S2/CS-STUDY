# REST(REpresentational State Transfer)

## HTTP 통신에서 어떤 자원에 대한 CRUD 요청을 Resource와 Method로 표현하여 특정한 형태로 전달하는 방식

<br>

## API

<br>

### API는 프로그램들이 서로 상호작용하는 것을 도와주는 매개체

## API 역할

1. API는 프로그램들이 서로 상호작용하는 것을 도와주는 매개체
2. API는 애플리케이션과 기기가 원활하게 통신할 수 있도록 한다.
3. API는 모든 접속을 표준화한다.
   <br>

## API 유형

1. private API
2. public API
3. partner API

## REST란

- ### 어떤 자원에 대해 CRUD(Create, Read, Update, Delete) 연산을 수행하기 위해 URI(Resource)로 요청을 보내는 것으로
- ### Get, Post 등의 방식(Method)을 사용하여 요청을 보내며, 요청을 위한 자원은 특정한 형태(Representation of Resource)으로 표현됩니다. 그리고 이러한 REST 기반의 API를 웹으로 구현한 것이 RESTful API인데 예를 들어, 우리는 게시글을 작성하기 위해 http://localhost:8080/board 라는 URI에 POST방식을 사용하여 JSON형태의 데이터를 전달할 수 있습니다.
- ### 위와 같이 CRUD 연산에 대한 요청을 할 때, 요청을 위한 Resource(자원, URI)와 이에 대한 Method(행위, POST) 그리고 Representation of Resource(자원의 형태, JSON)을 사용하면 표현이 명확해지므로 이를 REST라 하며
- ### 이러한 규칙을 지켜서 설계된 API를 Rest API 또는 Restful한 API라고 합니다. 그리고 위에서 살짝 언급하였듯이, 이러한 Rest API는 Resource(자원), Method(행위), Representation of Resource(자원의 형태)로 구성됩니다.
<br>

## REST API(REST FUL API)

![image](https://user-images.githubusercontent.com/71022555/138590105-edcd55dd-7bdd-4894-888e-c2600f4d5811.png)

### 애플리케이션이나 디바이스가 서로 간에 연결하여 통신할 수 있는 방법을 정의하는 규칙 세트입니다. REST API는 REST(REpresentational State Transfer) 아키텍처 스타일의 디자인 원칙을 준수하는 API입니다.

<br>

## RESTful API 구성요소

- ## Resource

  - ### 서버는 Unique한 ID를 가지는 Resource를 가지고 있으며, 클라이언트는 이러한 Resource에 요청을 보냅니다. 이러한 Resource는 URI에 해당합니다.
  <br>

- ## Method

  - ### 서버에 요청을 보내기 위한 방식으로 GET, POST, PUT, PATCH, DELETE가 있습니다. CRUD 연산 중에서 처리를 위한 연산에 맞는 Method를 사용하여 서버에 요청을 보내야 합니다.
  - PUT : resource의 업데이트 하거나 resource가 없다면 새로운 resource를 생성해 달라고 요청
  - PATCH : 서버에게resource의 업데이트를 요청합니다. 회원정보 수정 등에 사용됩니다. PUT과 비교해서 부분 데이터를 업데이트하는 차이점
  - DELETE : 서버에게 resource의 삭제를 요청합니다.
  - HEAD : GET과 유사하지만 콘텐츠가 아닌, HTTP 헤더만 리턴한다.(GET 요청으로 대용량 데이터를 조회하기 전에 해당 리소스가 변경되었는지 여무를 확인할 때 사용)  
    <br>

- ## Representation of Resource(표현)
  - ### 클라이언트와 서버가 데이터를 주고받는 형태로 json, xml, text, rss 등이 있습니다. 최근에는 Key, Value를 활용하는 json을 주로 사용합니다.

## URI VS URL

### URL은 Uniform Resource Locator로 인터넷 상 자원의 위치를 의미합니다. 자원의 위치라는 것은 결국 어떤 파일의 위치를 의미합니다.

### URI는 Uniform Resource Identifier로 인터넷 상의 자원을 식별하기 위한 문자열의 구성으로, URI는 URL을 포함하게 됩니다. 그러므로 URI가 보다 포괄적인 범위라고 할 수 있습니다.

<br>

## REST 특징

1.  ### Server-Client(서버-클라이언트 구조)

    - 자원이 있는 쪽이 Server, 자원을 요청하는 쪽이 Client가 된다.
    - REST Server: API를 제공하고 비즈니스 로직 처리 및 저장을 책임진다.
    - Client: 사용자 인증이나 context(세션, 로그인 정보) 등을 직접 관리하고 책임진다.
    - 서로 간 의존성이 줄어든다.  
      <br>

2.  ### Stateless(무상태) (이전, 현재 통신 상태 기록이 남아있지 않음)

    - HTTP 프로토콜은 Stateless Protocol이므로 REST 역시 무상태성을 갖는다.
    - Client의 context를 Server에 저장하지 않는다.
    - 즉, 세션과 쿠키와 같은 context 정보를 신경쓰지 않아도 되므로 구현이 단순해진다.
    - Server는 각각의 요청을 완전히 별개의 것으로 인식하고 처리한다.
    - 각 API 서버는 Client의 요청만을 단순 처리한다.
    - 즉, 이전 요청이 다음 요청의 처리에 연관되어서는 안된다.
    - 물론 이전 요청이 DB를 수정하여 DB에 의해 바뀌는 것은 허용한다.
    - Server의 처리 방식에 일관성을 부여하고 부담이 줄어들며, 서비스의 자유도가 높아진다.  
      <br>

3.  ### Cacheable(캐시 처리 가능)

    - 웹 표준 HTTP 프로토콜을 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용할 수 있다.
    - 즉, HTTP가 가진 가장 강력한 특징 중 하나인 캐싱 기능을 적용할 수 있다.
    - HTTP 프로토콜 표준에서 사용하는 Last-Modified 태그나 E-Tag를 이용하면 캐싱 구현이 가능하다.
    - 대량의 요청을 효율적으로 처리하기 위해 캐시가 요구된다.
    - 캐시 사용을 통해 응답시간이 빨라지고 REST Server 트랜잭션이 발생하지 않기 때문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상시킬 수 있다.  
      <br>

4.  ### Layered System(계층화)

    - Client는 REST API Server만 호출한다.
    - REST Server는 다중 계층으로 구성될 수 있다.
    - API Server는 순수 비즈니스 로직을 수행하고 그 앞단에 보안, 로드밸런싱, 암호화, 사용자 인증 등을 추가하여 구조상의 유연성을 줄 수 있다.
    - 또한 로드밸런싱, 공유 캐시 등을 통해 확장성과 보안성을 향상시킬 수 있다.
    - PROXY, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있다.  
      <br>

5.  ### Code-On-Demand(optional)

        - Server로부터 스크립트를 받아서 Client에서 실행한다.

    반드시 충족할 필요는 없다.  
    <br>

6.  ### Uniform Interface(인터페이스 일관성)
        - URI로 지정한 Resource에 대한 조작을 통일되고 한정적인 인터페이스로 수행한다.
        - HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
    특정 언어나 기술에 종속되지 않는다.

## REST 규칙

1. ### URI는 명사를 사용한다.
2. ### /(슬래시)로 계층 관계를 표현한다.
3. ### URI의 마지막에는 슬래시를 붙이지 않는다.
4. ### URI는 소문자로만 구성한다.
5. ### 가독성이 떨어지는 경우 하이픈(-)을 사용한다.
