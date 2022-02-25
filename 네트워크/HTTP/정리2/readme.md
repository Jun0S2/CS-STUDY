# HTTP 정리

## **HTTP**

HyperText : HTML 문서와 문서가 링크로 연결되도록 하는 **태그**로 구성된 언어

Protocol : 물리적으로 떨어진 컴퓨터가 어떻게 데이터를 주고 받는지에 대한 약속, 규칙

<aside>
💡 **물리적으로 떨어진 컴퓨터가 어떻게 HTML 파일을 주고 받는지에 대한 규약**

</aside>

- 어떻게 주고 받을까? → 요청(request)과 응답(response)의 구조로

## 요청 (Request)

<aside>
💡 클라이언트(프론트) 에서 서버(백엔드)에게 이런 작업을 해서 넘겨주라는 요청!

</aside>

- 메세지 구조

![Untitled](HTTP%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5%203fc71/Untitled.png)

요청 메세지 구조는 크게 Start line, Headers, Body로 구성됩니다. 

- Start Line : HTTP 메서드, 목표 url, HTTP 버전 등으로 구성됩니다.

→ 

```
1. HTTP Method: 주로 GET, POST, DELETE가 많이 쓰임
2. Request target
3. HTTP Version: HTTP 버전, 주로 1.1

GET /login HTTP/1.1
해석: GET 메소드로 login 이라는 요청 타겟에 HTTP 1.1 버전으로 요청을 보내겠다.
```

- Headers : 메타 데이터가 키 : 값 쌍의 형태로 구성됩니다. (내용의 크기, charset 등)

→

```

    Headers: {
    	Host: 요청을 보내는 목표(타겟)의 주소. 요청을 보내는 웹사이트의 기본 주소가 된다
    	(ex. www.naver.com)
    	User-Agent: 요청을 보내는 클라이언트의 대한 정보 (ex. chrome, firefox, safari, explorer)
    	Content-Type: 해당 요청이 보내는 메세지 body의 타입 (ex. application/json)
    	Content-Length: body 내용의 길이
    	Authorization: 회원의 인증/인가를 처리하기 위해 로그인 토큰을 Authroization 에 담는다
    }
```

- Body : 요청의 내용이 키 : 값의 쌍의 형태로 구성됩니다. 주로 POST에서 요청 보낼 때 사용

→

```
   로그인 시에 서버에 보낼 요청의 내용
    Body: {
    	"user_email": "inah.choi@gmail.com"
    	"user_password": "wecode"
    }
```

## 응답(Response)

응답의 구조 역시 세 가지인데 Start Line이 Status Line으로 바뀌었다.

- Status Line : 응답의 상태 줄. 현재 받은 요청을 처리하고 있는 상태를 클라이언트에게 알려준다.

```
1. HTTP Version: 요청의 HTTP버전과 동일
    2. Status Code: 응답 메세지의 상태 코드
    3. Status Text: 응답 메세지의 상태를 간략하게 설명해주는 텍스트

    HTTP/1.1 404 Not Found
    HTTP/1.1 200 SUCCESS
    
```

- Header : 요청의 헤더와 동일하다.
- Body : 일반적으로 요청의 바디와 동일하다. 보통 JSON 타입의 데이터 타입이 사용된다.

```
 ex) 로그인 요청에 대해 성공했을 때 응답의 내용
    Body: {
    	"message": "SUCCESS"
    	"token": "kldiduajsadm@9df0asmzm" (암호화된 유저의 정보)
    }
```

## HTTP Request Method

- GET

→ 이름 그대로 데이터를 서버로 부터 받아올 때 사용한다.

→ 가장 간단하다

→ 쿼리 스트링에 데이터를 담는다.

```
GET /shop/bag HTTP/1.1 - 현재 url에서 /shop/bag 페이지 요청한다.
Headers: {
	"HOST": "https://www.apple.com/kr"
	"Authroization": "kldiduajsadm@9df0asmzm" 
}

(축약된 응답 메시지)
HTTP/1.1 200 SUCCESS // 가져오기 성공했다.
Body: { // 이 데이터를 주겠다.
	"message": "SUCCESS"
	"carts": [
		{
			"productId": 10
			"name": "Pro Display XDR - Nano-texture 글래스"
			"price": "₩7,899,000"
			"quantity": 1
		},
		{
			"productId": 20
			"name": "Mac Pro"
			"price": "₩73,376,000"
			"quantity": 2
		}
	]
}
```

- POST

—> 데이터를 생성할 때 주로 사용되는 메서드

—> 바디에 데이터를 담는다.

```
**(축약된 요청 메세지)
POST /shop/bag HTTP/1.1** - 현재 url의 /shop/bag 페이지에서
Headers: {
	"HOST": "https://www.apple.com/kr"
	"Authroization": "kldiduajsadm@9df0asmzm" (유저가 본인임을 증명할 수 있는 인증/인가 토큰)
}
Body: { // 이런 데이터를 요청한다.
	product: {
		"productId": 30
		"name": "12.9형 iPad Pro Wi-Fi + Cellular 128GB"
		"color": "스페이스 그레이"
		"price": "₩1,499,000"
		"quantity": 1
	}
}

**(축약된 응답 메시지)
HTTP/1.1 201 SUCCESS**
Body: {
	"message": "SUCCESSFULLY CARTS UPDATED"
}
```

- DELETE

→ 특정 데이터를 서버에서 삭제 요청 보낼 때 쓰는 메소드

```
**(축약된 요청 메세지)
DELETE /shop/bag HTTP/1.1** 
Headers: {
	"HOST": "https://www.apple.com/kr"
	"Authroization": "kldiduajsadm@9df0asmzm"
}
Body: { // 이 상품을 삭제하고 싶다.
	productId: 30
}

**(축약된 응답 메시지)
HTTP/1.1 201 SUCCESS**
Body: {
	"message": "productId 30 DELETED"
}
```

- put

→ 리소스가 없으면 생성하고 있으면 덮어쓰는 메소드이다. 리소스의 경로를 클라이언트가 알기 때문에 직접 지정해줘야 한다. patch는 이런 리소스의 변경이 가능해집니다.

## POST VS PUT

POST 메소드로 다음과 같이 학생 정보를 생성해보자

```
HttpRequest
POST /student
{
  “name”: “박종대”,
  “grade”: 1
}

HttpResponse
HTTP/1.1 200 OK
{
  “id”: 1,
  “name”: “박종대”,
  “grade”: 1
}
```

그러면 이제, PUT을 통해 박종대의 grade를 2를 변경해보자. PUT은 리소스에 대한 수정이므로 특정 리소스를 구분하는 id값을 넣어줘야 합니다. 아까 설명에서 언급한 PUT은 리소스의 경로를 안다는 것이 이것을 의미합니다.

```
HttpRequest
PUT /student/1 // 1번 id
{
  “grade”: 2
}

HttpResponse
HTTP/1.1 200 OK
{
  “id”: 1,
  “name”: “박종대”,
  “grade”: 2
}
```

POST 메서드로 james 학생을 생성해달라고 2번 요청하면 어떻게 될까?

```
POST /student
{
   “name”: “james”,
   “grade”: 1
}
```

id가 1과 2인 james가 두 개가 생겨버립니다. POST는 리소스를 생성하기 위한 메서드로 요청한 횟수마다 새로운 리소스를 생성합니다. (unique 하게 만들 수도 있긴 하다.)

```
HTTP/1.1 200 OK
{ “id”: 1, “name”: “james”, “grade”: 1 }

HTTP/1.1 200 OK
{ “id”: 2, “name”: "james”, “grade”: 1}
```

반대로 PUT으로 같은 요청을 두번 보내면 어떻게 될까?

```
PUT /student/3
{
  “name”: ”what”
  “grade”: 2
}
```

2번 이상 보내도 아래와 같이 같은 응답이 온다. id를 3을 가진 리소스는 없었으므로, 최소 한번은 생성되고, 그 후에는 생성되지 않습니다. 그러니까 없으면 생성하고 있으면 덮어쓴다는 것이 이것입니다.

```
HTTP/1.1 200 OK
{ “id”: ”3”, “name”: “에디”, “grade”: 2 }
```

다시 정리해보면,

> *POST는 리소스의 생성을 담당한다.* POST는 요청 시 마다, 새로운 리소스가 생성된다.
> 

> *PUT은 리소스의 생성과 수정을 담당한다.*PUT은 요청 시 마다, 같은 리소스를 반환한다물론, 리소스 안에 속성은 변경될 수 있다.
> 

*PUT은 멱등하다*, *POST는 멱등하지 않다.*

## PUT VS PATCH

PUT HTTP 메소드로 gildong 이라는 유저의 나이(age)를 15로 변경하고자 할때

수정된 값만 보낼 경우, 보내지 않은 데이터는 null로 변경되어 버립니다.

```
PUT /users/1
{
    "age": 15
}

HTTP/1.1 200 OK
{
    "name": null,
    "age": 15
}
```

따라서, PUT 요청 시에는 아래와 같이 변경되지 않는 데이터도 모두 전달해야 합니다.

```
PUT /users/1
{
    "name": "gildong"
    "age": 15
}

HTTP/1.1 200 OK
{
    "name": "gildong",
    "age": 15
}
```

그러나 PATCH를 이용하여  ‘age’만 변경하는 요청을 보내면,

새롭게 바뀐 부분만 반영되며 나머지는 기존의 데이터가 유지됩니다.

```
PATCH /users/1
{
	"age": 15
}

HTTP/1.1 200 OK
{
	"name": "gildong",
	"age": 15
}
```

따라서, 자원의 일부를 수정할 때는 PATCH를, 전체적인 수정이 필요할 때는 PUT을 이용하는 것이 적절합니다.

출처: [https://devuna.tistory.com/77](https://devuna.tistory.com/77)

![Untitled](HTTP%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5%203fc71/Untitled%201.png)

## HTTP의 특징

1. Stateless 하다
→ 상태 없음이란 HTTP 통신은 독립적이어서 과거의 통신 내용을 기억하지 못한다는 것입니다. 똑같은 요청을 보내도 이전에 받았던 응답을 기억하지 못하기 때문에 다시 처리해서 보내줘야 합니다. 이 Stateless를 최대한 활용하는 것이 좋은데 수강신청 같이 한번에 대용량 트래픽이 요청되는 상태에서 많은 트래픽을 유지하려고 하면 서버에 무리가 올 수 있기 때문입니다. 서버의 확장성도 좋아집니다. 하지만 login 상태 유지나 유저의 장바구니 데이터 유지 등은 어쩔 수 없이 상태를 유지해야만 하는 기능이니까 쿠키, 세션, 로컬 스토리지 등을 이용해서 유지할 수 있도록 합니다.
2. 비연결적 이다.
→ 연결 유지를 안하기 때문에 서버의 자원을 효율적으로 이용할 수 있습니다. 다만 요청을 보낼때마다 다시 TCP 연결을 해줘야 하고 JS 파일, CSS/HTML 파일을 다시 전송하는 문제가 있어서 최근 HTTP 버전에서는 지속 연결을 지원하여 문제를 해결했습니다.

## 응답 코드

: 클라이언트가 보낸 요청의 처리 상태를 응답에서 알려주는 기능

- 1xx (Informational) : 요청이 수신되어 처리중
- 2xx (Successful) : 요청 정상 처리
- 3xx (Redirection) : 요청을 완료하려면 추가 행동 필요
- 4xx (Client Error) : 클라이언트 오류, 잘못된 문법 등으로 서버가 요청을 수행할 수 없음
- 5xx (Server Error) : 서버 오류, 서버가 정상 요청을 처리하지 못함

## Redirection

![Untitled](HTTP%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5%203fc71/Untitled%202.png)

이미지 출처 : [https://loko1124.tistory.com/m/13](https://loko1124.tistory.com/m/13)

클라이언트는 event 페이지를 요청했는데 event 페이지에 대한 접근 권한이 없거나 그 url을 다른 url로 접속 시키게 하고 싶을 때 서버 측에서 그 주소 말고 이 주소로 접근하라고 Location에 담아 알려줍니다.  그럼 자동으로 다시 요청을 보내는데 이것을 자동 리다이렉션이라고 합니다.

네이버 카페의 게시글을 클릭했을 때 내가 아직 로그인이 안 되어 있고 카페에 가입한 상태가 아니라면 그 게시글에 접근할 수 있는 권한이 없습니다. 그래서 서버는 접근권한이 없으니 로그인 페이지로 이동 시키기 위해 로그인 페이지 주소를 주면서 리다이렉트를 시킵니다.

혹은 내 홈페이지에 접근할 수 있는 url을 여러개 만들어 놓고 실제 주소는 하나로 설정하고 싶을 때도 사용합니다.

자바 스크립트에서 window.location = "url" 이것도 일종의 리다이렉션에 해당합니다.

다음은 Restful API