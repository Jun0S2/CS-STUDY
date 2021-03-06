# HTTP GET/POST

![Untitled](HTTP%20GET%20P%20506c9/Untitled.png)

# **HTTP**

웹상에서 클라이언트 - 서버 간에 요청과 응답으로 데이터를 주고 받을 때 규칙(프로토콜)을 의미합니다. 클라이언트가 서버에 request를 보내면 서버는 response하는 구조에서 HTTP 요청에 포함되는 HTTP 메서드는 서버가 어떤 response를 하면 되는지를 알려줍니다. 이 HTTP 메서드는 GET, POST, PUT, PATCH, DELETE 등이 있습니다. 이 중에 가장 중요한 get과 post에 대해 알아봅니다.

## **GET**

GET은 **서버로부터 정보를 조회하기 위해** 설계된 메소드 입니다. GET은 요청을 전송할 때 필요한 데이터를 Body에 담지 않고, **쿼리 스트링**을 통해 전송합니다. URL의 끝에 '?이름=값'으로 쌍을 이루는 요청 파라미터를 쿼리 스트링이라고 부릅니다. 만약, 요청 파라미터가 여러 개이면 &로 연결합니다. 쿼리스트링을 사용하게 되면 URL에 조회 조건을 url에 표시하기 때문에 특정 페이지를 쉽게 링크하거나 북마크를 쉽게 설정할 수 있습니다.

> www.example-url.com/resources?name1=value1&name2=value2
> 

그리고 GET은 반복적인 request를 제한하기 위해 요청을 캐싱할 수 있습니다. 자바스크립트, CSS, 이미지 같은 정적 컨텐츠는 데이터양이 크고, 변경될 일이 거의 없기 때문에 반복해서 동일한 요청을 보낼 필요가 없습니다. 정적 컨텐츠를 한 번 요청하고 나면 브라우저에서는 요청을 캐시해두고, 동일한 요청이 발생할 때 서버로 요청을 보내지 않고 캐시된 데이터를 사용하는 것입니다. 만약 정적 컨텐츠를 변경하고 싶다면 브라우저의 캐시를 지워주어야 다시 컨텐츠를 조회하기 위해 서버로 요청을 보내게 됩니다.

또 get 방식은 url에 정보가 노출 됩니다. 로그인 같은 창을 생각해 보면 아이디와 비밀번호가 url에 노출되기 때문에 그런 곳에서는 단순하게 get 방식만을 적용하면 안되고 암호화 등의 기법을 적용해야 할 것입니다.

**POST**

POST는 **리소스를 생성/변경하기 위해 설계**되었고 GET과 달리
전송해야될 데이터를 HTTP 메세지의 Body에 담아서 전송합니다. HTTP 메세지의 Body는 길이의 제한없이 데이터를 전송할 수 있습니다. 그래서 POST 요청은 GET과 달리 대용량 데이터를 전송할 수 있다는 장점이 존재합니다. 이처럼 POST는 데이터가 Body로 전송되고 내용이 눈에 보이지 않아 GET보다 보안적인 면에서 안전하긴 하지만, POST 요청도 개발자 도구, Fiddler와 같은 툴로 내용을 확인할 수 있기 때문에 아까와 같은 패스워드 같은 경우에는 반드시 암호화의 과정을 거쳐 전송해야 합니다.

그리고 POST로 요청을 보낼 때는 요청 헤더의 Content-Type에 요청 데이터의 타입을 표시해야 합니다. 데이터 타입을 표시하지 않으면 서버는 내용이나 URL에 포함된 리소스의 확장자명 등으로 데이터 타입을 유추합니다. 만약, 알 수 없는 경우에는 application/octet-stream로 요청을 처리합니다.

**GET과 POST의 차이**

GET은 Idempotent,
POST는 Non-idempotent하게 설계되었습니다. 멱등은 수학적 개념으로 다음과 같이 나타낼 수 있습니다. 수학이나 전산학에서 연산의 한 성질을 나타내는 것으로, 연산을 여러 번 적용하더라도 결과가 달라지지 않는 성질, 멱등이라는 것은 **동일한 연산을 여러 번 수행하더라도 동일한 결과**가 나타나야 합니다. 식으로 나타내면 다음과 같습니다. 'f(f(x)) = f(x)'

여기서 GET이 멱등하도록 설계되었다는 것은 GET으로 서버에게 동일한 요청을 여러 번 전송하더라도 동일한 응답이 돌아와야 한다는 것을 의미합니다. 이에 따라 GET은 설계원칙에 따라 서버의 데이터나 상태를 변경시키지 않아야 Idempotent하기 때문에 주로 조회를 할 때에 사용해야합니다. 예를 들어, 브라우저에서 웹페이지를 열어보거나 게시글을 읽는 등 조회를 하는 행위는 GET으로 요청하게 됩니다.

반대로 POST는 비멱등 하기 때문에 서버에게 동일한 요청을 여러 번 전송해도 응답은 항상 다를 수 있습니다. 이에 따라 POST는 서버의 상태나 데이터를 변경시킬 때 사용됩니다. 게시글을 쓰면 서버에 게시글이 저장이 되고, 게시글을 삭제하면 해당 데이터가 없어지는 등 POST로 요청을 하게 되면 서버의 무언가는 변경되도록 사용합니다. 이처럼 POST는 생성, 수정, 삭제에 사용할 수 있습니다. 그런데 정확히는 생성에는 POST, 수정은 PUT 또는 PATCH, 삭제는 DELETE가 더 용도에 맞는 메소드입니다. 이러한 메소드들은 다음에 더 자세히 다루겠습니다.

- GET 요청은 캐시가 가능하다.
- GET 요청은 브라우저 히스토리에 남는다.
- GET 요청은 북마크 될 수 있다.
- GET 요청은 길이 제한이 있다. - 브라우저마다 제한이 다르다고 한다.
- GET 요청은 중요한 정보를 다루면 안된다. ( 보안 ) : GET 요청은 파라미터에 다 노출되어 버리기 때문에 최소한의 보안 의식이라 생각하자.
- GET은 데이터를 요청할때만 사용 된다.

- POST 요청은 캐시되지 않는다.
- POST 요청은 브라우저 히스토리에 남지 않는다.
- POST 요청은 북마크 되지 않는다.
- POST 요청은 데이터 길이에 제한이 없다.