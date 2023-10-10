---
title: "[6주차] 자바스크립트 웹 개발 기본기"
excerpt: "웹 브라우저와 서버, 비동기 실행에 대해 배워보았습니다."

categories:
  - CodeitSprint
tags:
  - [부트캠프, JavaScript, Web]

permalink: /CodeitSprint/[6주차]-자바스크립트-웹-개발-기본기/

toc: true
toc_sticky: true

date: 2023-10-04
last_modified_at: 2023-10-10
---

# Ch1. 웹 기초 다지기 
## fetch 함수 사용해보기
- 웹브라우저 : 서버로부터 코드를 받고, 코드를 해석해서 화면으로 보여준다.

## fetch 함수 살펴보기
```js
fetch('https://www.google.com') //서버로 요청
  .then((response) => response.text()) //서버의 response가 오면 실행되는 부분
  .then((result) => { console.log(result); }); //이전 then 코드가 실행되야 실행됨
```
- `fetch` : 서버로 리퀘스트를 보내고, 리스폰스를 받는 함수
  - return값은 **Promise 객체**이다.
- `callback` : 어떤 조건을 만족해야지만 실행되는 함수 ⭐
- `then` : **response가 왔을 때 실행**할 callback을 등록해주는 메소드
  - promise 객체의 메소드
  - **1번 콜백의 return값이 다음 콜백의 파라미터로 넘어가게 된다.**
  - 위 코드에서는 `response.text()`가 `result`로 넘어가게 된다!

## response 객체
```js
fetch('https://www.google.com')
  .then((response) => { console.log(response); });
```
- **위의 코드처럼 바로 response값을 출력할 수 없는 이유** ⭐⭐
  - **response 파라미터는 하나의 객체**이기 때문에 여러 정보들을 가지고 있다.
  - 따라서 그 중에 `text`라는 메소드를 호출해야지만 리스폰스의 실제 내용을 return받을 수 있기 때문이다.

## 웹이란?
- Web : 전 세계적인 연결망, 웹 브라우저를 통해 연결되는 가상의 연결망 세계
- 웹 안에 무수히 많은 웹페이지들이 연결되어 있는 것
- HyperText : 다른 텍스트에 대해 **참조**를 가지고 있는 텍스트
  - **H**yper**T**ext **M**arkup **L**anguage : html은 hypertext를 마크업하는 언어다.

## URL이란?
- URL(Uniform Resource Locator) : 웹에 존재하는 특정 데이터를 나타내는 문자열
- https://www.codeitshopping.com/men/shirts?color=blue&size=m
  - `www.codeitshopping.com`
    - Host : 전 세계 서버 중 도메인 주소에 해당하는 하나의 **서버**를 특정
  - `/men/shirts`
    - Path : 서버에 있는 데이터 중 원하는 **데이터**를 특정
    - 서버 안에 존재하는 데이터를 나타내는 부분
  - `color=blue&size=m`
    - Query : 데이터에 관한 **세부적인 요구사항**, `&`로 조건들이 이어진다
    - ? 뒤에 있는 부분

## URL과 리퀘스트 ⭐
- 사용자가 웹 브라우저의 주소창에 URL을 입력하면
  - `웹 브라우저` : 호스트(Domain Name)를 보고 통신할 서버를 찾는다.
  - `웹 브라우저 -> 서버` : path와 query 부분을 담아 **리퀘스트**를 보낸다.
  - `서버` : path와 query를 보고 의미하는 데이터를 찾는다.
  - `서버 -> 웹 브라우저` : 찾은 데이터를 **리스폰스**에 담아 보낸다.
  - `웹 브라우저` : 서버로부터 받은 리스폰스의 내용을 사용자에게 보여준다. 

## HTTP란?
- `Scheme` : 프로토콜의 이름
  - ex. http, https
- `Protocol` : 통신을 하는 두 주체가 지켜야 하는 통신 규약
  - 웹 브라우저와 서버가 서로 통신할 때 지켜야 할 약속
- `http + s` : HyperText Transfer Protocol + Secure
  - http 프로토콜에 보안을 추가한 것

## 한 번의 접속, 여러 번의 Request
- 웹 브라우저로 특정 페이지에 접속할 때, **보통 한 번 이상의 리퀘스트-리스폰스**가 오고간다.
- 웹 페이지를 구성하기 위한 html 파일에 src 속성이 있다면
- 거기에 적힌 url로 접속해서 다시 리퀘스트를 보내고 리스폰스를 받는 과정을 반복하기 때문이다.
- 이런식으로 한번의 리퀘스트로는 온전한 페이지를 구성하기가 어렵다!

---

# Ch2. Web API 배우기 
## JSON이란?
- `JSON`(JS Object Notation) : 정보를 교환할 때 사용하기 위해서 자바스크립트의 문법으로 만들어진 데이터 포맷

## 자바스크립트 객체 표기법과 JSON 문법의 차이
- JSON은 프로퍼티 이름에 반드시 **큰따옴표**를 붙여야 한다.
- 프로퍼티 값이 문자열인 경우에도 반드시 큰따옴표를 사용해야 한다.
- `undefined`, `NaN`, `Infinity` 등은 JSON에서 사용할 수 없다.
- 주석 사용 불가
  - JSON이 코드가 아니라 데이터 포맷이기 때문!

## JSON 데이터를 객체로 변환하기
- **string 타입**의 JSON 데이터는 바로 자바스크립트 객체로 변환 가능
  - JSON 객체의 `parse` 메소드 사용!
```js
fetch('https://jsonplaceholder.typicode.com/users')
  .then((response) => response.text())
  .then((result) => { 
  	const users = JSON.parse(result); //users에 JSON 데이터를 변환한 배열을 저장
  	console.log(users.length);
  	users.forEach( (user) => {
  		console.log(user.name);
  	});
  });
```

## 메소드의 의미
- CRUD : Create-Rred-Update-Delete 의 약자로 데이터베이스 관점에서 데이터에 관한 처리를 나타낸 합성어
- request는 서버의 데이터에 관해 어떤 처리를 요구하냐에 따라 4가지로 나눌 수 있다.
  - 데이터 조회 : `GET` (R)
  - 데이터 추가 : `POST` (C)
  - 데이터 수정 : `PUT` (U)
  - 데이터 삭제 : `DELETE` (D)

## Request의 Head와 Body
- 하나의 request는 head와 body로 이루어져 있다.
- head : request에 대한 부가 정보
  - 메소드 정보도 head에 담겨 있다!
  - header : head 안에 존재하는 하나하나의 **key-value 쌍**을 의미
- body : 실제 데이터를 담는 부분
  - `POST / PUT` 메소드의 경우 데이터를 **body**에 담아서 보내준다.
  - `GET / DELETE` 메소드의 경우에는 body가 필요하지 않다.

## POST request 보내기
```js
fetch('https://learn.codeit.kr/api/members/3') //3번 직원의 정보 조회
  .then((response) => respose.text())
  .then((result) => {console.log(result);});
```
- fetch 함수에 아무런 옵션을 적지 않으면 기본으로 `GET` 리퀘스트를 보낸다.

```js
const newMember = { //새로운 직원 정보
  name : 'Jerry',
  email : 'jerry@codeitmall.kr',
  department : 'engineering',
};

fetch('https://learn.codeit.kr/api/members',{
  // option 객체
  method : 'POST',
  body : JSON.stringify(newMember),
})
  .then((response) => respose.text())
  .then((result) => {console.log(result);});
```
- `stringify` 메소드 : 자바스크립트 객체를 string 타입의 JSON 데이터로 변환

## PUT, DELETE request 보내기
- 직원 Alice의 부서를 수정하는 예시 코드
```js
const member = {
  name : 'Alice',
  email : 'alice.codeitmall.kr',
  department : 'marketing',
};

fetch('https://learn.codeit.kr/api/members/2',{
  method : 'PUT',
  body : JSON.stringify(member),
})
  .then((response) => respose.text())
  .then((result) => {console.log(result);});
```
- 직원 Alice를 삭제하는 예시 코드
```js
fetch('https://learn.codeit.kr/api/members/2',{
  method : 'DELETE',
})
  .then((response) => respose.text())
  .then((result) => {console.log(result);});
```

## 모범적인 Web API, REST API ⭐
- API (Application Programming Interface) : 개발할 때 사용할 수 있도록 특정 라이브러리나 플랫폼 등이 제공하는 데이터나 함수
- Web API : 웹 개발에서 어느 URL로 어떤 리퀘스트를 보냈을 때, 무슨 처리가 수행되고 어떤 리스폰스가 오가는지에 대해 미리 정해둔 규칙(약속)
  - 정리하자면, 프론트랑 백이 서로 이런 URL로 리퀘스트 보내면 서버에서 이런 처리를 하고, 이런 리스폰스 보내주기로 약속한 것!

- REST architecture : 웹이 갖추어야 할 이상적인 아키텍처
  - `Client - Server` : Client-Server 구조로 나누고, 서로가 담당한 역할에만 집중한다.
  - `Stateless` : Server는 Client가 보낸 리퀘스트를 따로 저장하지 않는다.
    - 하나의 리퀘스트에 필요한 모든 정보가 담겨있어야 한다.
  - `Cache` : 캐시를 활용해서 네트워크 비용을 절감해야 한다.
    - Server는 리스폰스에 해당 리스폰스를 **재활용해도 되는지 여부**를 담아서 보내야 함
  - `Uniform Interface`⭐ : client가 server와 통신하는 인터페이스는 다음 4가지 조건을 준수해야 한다.
    1. 리소스(웹 상에 존재하는 데이터)를 URI로 식별할 수 있어야 한다.
    2. 리소스와 리소스의 표현을 엄격하게 구분해야 한다.
        - client와 server 모두 리소스를 직접 다루는 게 아니라 **리소스의 표현**(html, png 파일 등)을 다뤄야 한다.
    3. client의 리퀘스트와 server의 리스폰스는 그 자체에 담긴 정보만으로도 모든 것을 해석할 수 있어야 한다.
    4. server의 리스폰스에는 리소스의 표현, 메타 정보뿐만 아니라 새로운 상태로 넘어갈 수 있도록 해주는 링크들도 포함되어야 한다.
  - `Layered System` : client와 server 사이에는 프록시(proxy), 게이트웨이(gateway)와 같은 중간 매개 요소를 두기 때문에 계층형 층이 형성된다.
  - `Code-On-Demand` : optional한 조건으로, client는 받아서 바로 실행할 수 있는 applet이나 script 파일을 server로부터 받을 수 있어야 한다.
    
- `REST API`⭐ : Web API가 잘 설계되었는지 평가하는 가이드라인, REST 아키텍처에 부합하는 API
  - URL에서 리소스에 대한 처리를 드러내면 안된다.
    - **리소스에 대한 처리는 메소드로!**
  - `도큐먼트`(하나의 파일)는 단수형 명사를
  - `컬렉션`(파일들을 모아놓은 디렉토리)은 복수형 명사를 사용해야 한다.

## JSON 데이터 다루기 종합
- Serialization (직렬화) : 자바스크립트 객체 -> JSON 데이터 (string)
- Deserialization (역직렬화) : JSON 데이터 -> 자바스크립트 객체
  
```js
fetch('https://jsonplaceholder.typicode.com/users')
  .then((response) => response.json())
  .then((result) => { const users = result; });
```
- `json` 메소드를 사용하면 리스폰스의 내용이 json 데이터라면 **바로 deserialization**을 해준다.
- 따로 `parse`를 해줄 필요가 없다!!

## Status Code
- response도 request와 마찬가지로 head와 body로 이루어져 있다.
  - head : response에 대한 부가 정보
  - body : 실제 데이터를 담는 부분
    
- status code : request를 받은 서버가 **작업 결과**를 나타내기 위해 리스폰스의 헤드에 넣는 숫자
  - **200** : 리퀘스트 정상 처리 완료 (OK)
  - **404** : 해당 URL에 해당하는 데이터를 찾을 수 없음 (Not Found)
  - 100 : 계속 리퀘스트를 보내라는 의미 (Countinue)
  - 101 : 프로토콜 이걸로 바꾸자! 라고 서버한테 보냈을 때 -> 그래 그걸로 바꿀게~ 라는 의미
  - 200번대 : 리퀘스트가 성공적으로 처리됨
  - 201 : POST 성공, 리소스 생성 완료 (Created)
  - 202 : 일단은 접수됨. 나중에 처리 될 거임 (Accepted)
  - 300번대 : 리퀘스트 아직 처리 x, 처리하고 싶다면 클라이언트가 추가적인 작업을 해야함
  - 400번대 : 클라이언트 쪽에 문제가 있음

## Content-type이란?
```js
const newMember = {
  name: 'Jerry',
  email: 'jerry@codeit.kr',
  department: 'engineering',
};

fetch('https://learn.codeit.kr/api/members', {
  method: 'POST',
  headers: { // 추가된 부분
    'Content-Type': 'application/json',
  },
  body: JSON.stringify(newMember),
})
  .then((response) => response.text())
  .then((result) => { console.log(result); });
```

- Content-type 헤더 : 리퀘스트 / 리스폰스의 **body에 들어있는 데이터가 어떤 타입인지**를 나타낸다.
- `main type / sub type` 형식으로 값이 구성됨
- Content-type 헤더의 값이 없으면 직접 데이터의 타입을 확인하고, 처리하는 과정이 필요하다.
- json 데이터 : `application/json`

## 알아두면 좋은 Content-type
```js
<?xml version="1.0" encoding="UTF-8" ?>
<person>
    <name>Michael Kim</name>
    <height>180</height>
    <weight>70</weight>
    <hobbies>
        <value>Basketball</value>
        <value>Listening to music</value>
    </hobbies>
</person>
```
- XML(Extensible Markup Language) : 태그를 사용해서 데이터를 나타내는 데이터 포맷
- 이런 식으로 태그로 나타낸다.
- XML의 단점
  - JSON에 비해 많은 용량 차지
  - 가독성 떨어짐
  - 배우기 어려움
  
```js
id=6&name=Jason&age=34&department=engineering
```
- `application/x-www-form-urlencoded` 타입
  - HTML에서 form 태그를 사용할 때, form 태그는 해당 타입의 데이터를 body에 담아서 보낸다.
  - `프로퍼티 이름 = 값` 형식으로 나타내며, `&` 기호로 연결
  - URL에서 query 부분과 유사하다.
  - URL 인코딩 : URL에서 약속한 문자가 아닌 애들은 다른 문자로 변환하는 것
    - `URLSearchParams` 객체를 사용하면 자동으로 URL 인코딩을 적용해준다.
  - Percent 인코딩 
    - 특별한 용도를 가지고 있는 문자들은 원래 용도가 아니라 다른 용도로 사용될 경우 `%숫자` 형식으로 인코딩되는 방식
    - 영어, 숫자를 제외한 다른 언어를 URL에서 나타낼 때에도 사용된다.
    - **Percent 인코딩이 필요한 이유**
      - URL에 대한 해석 오류를 방지하기 위해서!
      - 'Tom&Jerry'가 query를 이어주는 용도인지, 데이터를 나타내는 문자열 &인지를 구분하기 위함이다.

```js
const formData = new FormData();
formData.append('email', email.value);
```
- `multipart/form-data`
  - 실무적으로 중요한 타입이다.
  - **여러 종류의 데이터를 하나로 합친 데이터**를 의미한다.
  - ex. 게시글을 올릴 때, text 정보뿐만 아니라 함께 올린 이미지, 동영상 정보도 함께 보낼 수 있는 Context-type.
  - FormData 객체를 사용한다.

## 그 밖에 알아야 할 내용들
- Ajax (Asynchronous JavaScript And XML)
  - 초반의 웹은 화면의 일부분이 바뀌더라도 매번 아예 새로운 웹 페이지가 로드되는 형식이었다.
  - 현재 페이지를 그대로 유지한 채로 서버에 리퀘스트를 보내고 리스폰스를 받아서 **새로운 페이지를 로드하지 않아도 되는 방식**이다.
  - Asynchronous : 현재 화면에 영향을 미치지 않고 백그라운드에서 작업을 처리하는 것.
  - ex. 구글맵에서 장소를 클릭하면 현재 페이지는 유지되면서 새로운 정보창이 뜨는 방식
  - `XMLHttpRequest` 객체를 이용해서 Ajax 통신을 할 수 있다.
    - 현재 실무에서는 주로 `fetch` 함수 또는 `axios` 패키지를 사용한다.
      
- `PATCH` vs `PUT`
  - PATCH 메소드 : 기존의 데이터의 일부만 수정하고 싶을 때 사용한다.
  - PUT 메소드 : 기존의 데이터를 아예 새로운 데이터로 덮어쓸 때 사용한다.
    
- `HEAD` 메소드
  - GET 메소드와 동일하지만, head 부분만 받아온다.
  - 실제 데이터가 아니라 데이터에 관한 `정보`만 얻고싶을 때 사용한다.

---
# Ch3. 비동기 실행과 Promise 객체
## fetch 함수와 비동기 실행
- `then` 메소드는 콜백을 단지 **등록만 해주는 역할**이지, 바로 실행하지는 않는다.
- 비동기 실행 : 코드를 작성한 순서대로 실행하고, 나중에 콜백이 실행되는 방식

## 동기 실행과 비동기 실행
- 동기 실행 : 한번 시작한 작업은 다 처리하고 나서, 다음 코드로 넘어가는 방식
  - then 메소드로 콜백 함수를 등록한 뒤에 **리스폰스가 올 때까지 코드 실행이 잠시 중지**되는 방식
- 비동기 실행
  - then 메소드로 콜백 함수를 등록해 놓고, **일단 다음 줄을 실행**한 뒤에 **리스폰스가 오면 그때 콜백을 실행**하는 방식
  - 동기 실행 방식보다 작업을 더 `빠른 시간` 내에 처리할 수 있다.

## 알아야하는 비동기 실행 함수들
- **setTimeout 함수**
```js
console.log('a');
setTimeout(() => { console.log('b'); }, 2000);
console.log('c');
```
- 특정 콜의 실행을 `원하는 시간`만큼 미룰 수 있는 함수다.
- `2000ms` 뒤에 `() => console.log('b')` 함수가 실행되는 코드이다.
    
- **setInterval 함수**
```js
console.log('a');
setInterval(() => { console.log('b'); }, 2000);
console.log('c');
```
- 특정 콜백을 `일정한 시간 간격`으로 실행하도록 등록하는 함수다.

- **addEventListener 메소드**
  - 특정 `이벤트가 발생`했을 때 실행할 콜백을 등록하는 메소드이다.

## fetch 함수는 Promise 객체를 리턴합니다
- Promise 객체
  - 어떤 작업에 관한 `상태 정보`를 가지고 있는 객체
- Promise의 3가지 상태
  - `pending` : 진행 중
    - fetch 함수로 콜백이 등록된 후, 리스폰스를 기다리는 상태
  - `fulfilled` : 성공
    - 성공적으로 리스폰스를 받았을 때
  - `rejected` : 실패
    - 네트워크가 끊겼거나 서버 자체와 연결되지 않는 등 리퀘스트/리스폰스를 받지 못한 경우
      
- fulfilled 상태가 되면 Promise 객체는 `작업 성공 결과`도 함께 가진다.
  - fetch 함수의 경우 Promise 객체의 작업 성공 결과는 `리스폰스`가 되는 것이다!
- rejected 상태가 되면 Promise 객체는 `작업 실패 정보(이유)`를 가지게 된다.

## fetch 함수를 사용한 코드, 다시 해석하기
- `then` 메소드
  - 사실 `Promise` 객체의 메소드다.
  - Promise 객체가 fulfilled 상태일 때 실행된다.
- Promise의 작업 성공 결과는 콜백함수의 `첫 번째 파라미터`로 넘어온다.

## Promise Chaining이란?
- Promise Chaining
  - Promise 객체에 then 메소드를 연속적으로 붙이는 것
- Promise Chaining이 가능한 이유
  - then 메소드의 리턴값이 `새로운 Promise 객체`이기 때문이다.
- **then 메소드의 `콜백 함수`의 리턴값** ⭐⭐⭐
  - `Promise 객체`를 return하는 경우
    - then 메소드의 return값은 함수의 return값과 동일한 상태 & 작업 성공 결과를 갖게 된다.
  - `Promise 객체가 아닌 값`을 return하는 경우
    - then 메소드의 return값은 fulfilled 상태
    - 콜백 함수의 return값을 작업 성공 결과로 갖게 된다.
   
## text, json 메소드도 Promise 객체를 리턴해요
- **text 메소드**
  - 상태 : fulfilled
  - 작업 성공 결과 : 리스폰스의 body에 있는 내용을 string으로 변환한 값

- **json 메소드**
  - 상태 : fulfilled
  - 작업 성공 결과 : 리스폰스의 body에 있는 JSON 데이터를 JS 객체로 역직렬화한 객체
  - body에 있는 내용이 JSON 타입이 아닐경우 에러 & rejected
 
## Promise Chaning이 필요한 경우
- 비동기적 작업을 `순차적으로` 하기 위해서 사용한다.
- 콜백 안에 또 then 메소드를 사용하지 않아도 된다.
- 여러 개의 then 메소드를 사용하더라도 코드의 가독성이 좋아진다.

## rejected 상태가 되면 실행할 콜백
```js
fetch('https://jsonplaceholder.typicode.com/users')
  .then((response) => response.text(), (error) => {console.log(error);});
```

- then 메소드의 `두 번째 파라미터`로 넣어주면 된다.
- `error` 파라미터에는 작업 실패 정보가 저장된다.

## then 메소드 완벽하게 이해하기
- **실행된 콜백이 아무 값도 return하지 않는다면?**
  - 함수의 return값이 undefined인 것과 마찬가지이다.
  - Promise 객체의 작업 성공 결과로 `undefined`를 갖게 된다.
  
- **콜백 함수 내에서 에러가 발생한 경우**
  - Promise 객체는 `rejected` 상태가 된다.
  - 작업 실패 정보로 해당 Error 객체를 갖는다.

- **아무런 콜백도 실행되지 않는 경우**
  - ex. fetch함수가 실패해서 error일 때의 콜백함수를 실행해야 하지만 콜백함수가 없을 때
  - 이전 Promise 객체와 동일한 상태 & 결과를 갖게 된다.

## catch 메소드
```js
fetch('https://jsonplaceholder.typicode.com/users')
  .then((response) => response.text())
  .catch((error) => {console.log(error);})
  //.then(undefined, (error) => {console.log(error);})
```

- `에러가 발생`하면 `catch` 메소드로 등록한 콜백 함수를 실행시킨다.
- 사실 catch 메소드는 then 메소드를 변형한 것이다.
- then 메소드에 첫 번째 파라미터에는 `undefined`를 주고 두 번째 파라미터만 넣은 것과 동일한 방식이다.
- 실무에서는 catch 메소드를 주로 사용한다!

## catch 메소드는 마지막에 씁니다
- rejected 상태의 Promise 객체를 아무 처리도 안하고 그냥 남겨두면 웹 브라우저는 에러로 인식한다.
- catch 메소드를 가장 아래로 보내서 **모든 에러에 대응**할 수 있도록 해야한다.

## catch 메소드를 여러 개 쓰는 경우
- **catch 메소드의 return값을 뒤에서 사용할 수 있는 경우**에는 중간에 catch를 작성한다.
- 즉, catch 메소드의 return값을 이용해서 작업을 정상적으로 끝마칠 수 있다면 중간에 사용한다.

## finally 메소드
```js
fetch('https://jsonplaceholder.typicode.com/users')
  .then((response) => response.text())
  .catch((error) => {console.log(error);})
  .finally(() => {console.log('exit');});
```
- Promise의 상태와 상관없이 `항상 실행`하고 싶은 콜백
- 파라미터가 없어도 된다.
- 주로 catch 메소드 바로 뒤에 작성한다.

## Promise 객체는 왜 등장했을까?
- setTimeout, addEeventListener, fetch함수는 직접 콜백 함수를 파라미터로 전달하는 방식
- 콜백 안에 또 콜백을 넣고.. 그 안에 또 콜백을 넣고...
- `콜백 지옥`에 빠질 수 있다.
  - 콜백 지옥에 빠지면 가독성도 지옥으로 간다,,
- 이런 문제를 해결하기 위해 Promise 객체가 등장하게 되었다.

## 직접 만들어보는 Promise 객체
```js
const p = new Promise((resolve, reject) => {
  //setTimeout(() => {resolve('success');}, 2000);
  setTimeout(() => {reject(new Error('fail'));}, 2000);
});
```

- Promise 객체가 fulfilled 상태가 되면 resolve()를 호출한다.
- rejected 상태가 되면 reject()를 호출한다.

## Promisify
```js
function wait(text, milliseconds) {
  const p = new Promise((resolve, reject) => {
    setTimeout(() => { resolve(text); }, 2000);
  });
  return p;
}

fetch('https://jsonplaceholder.typicode.com/users')
  .then((response) => response.text())
  .then((result) => wait(`${result} by Codeit`, 2000)) // 2초 후에 리스폰스의 내용 뒤에 'by Codeit' 추가하고 리턴
  .then((result) => { console.log(result); });
```

- Promise Chaining 안에서 비동기 함수를 사용하면 return값을 사용할 수 없다.
- **Promisify** : 비동기 실행 함수를 Promise 객체로 감싸서 그 객체를 리턴하는 형식
- 콜백을 **한번만 실행**하는 것들에서만 가능하다.
  - ex. setTimeout, readFile 등
- 콜백을 여러번 실행하는 함수들은 불가능하다.
  - ex. setInterval, addEventListener 등
  - Promise 객체는 한번 fulfilled/rejected 상태가 되면 **그 뒤로 상태가 바뀌지 않기 때문**이다.

## 이미 상태가 결정된 Promise 객체
- `fulfilled` 상태로 결정된 Promise 객체 생성
```js
const p = Promise.resolve('success');
```

- `rejected` 상태로 결정된 Promise 객체 생성
```js
const p = Promise.reject(new Error('fail'));
```

- 이외에 `resolve`/`reject` 메소드를 사용하는 경우
  - 함수의 return값을 모두 Promise 객체로 통일하고 싶은 경우

> `Tip!` Promise 객체는 항상 **결과**를 줄 수 있는 Provider(공급자)이고, then 메소드는 그 **결과를 소비하는 콜백**인 Consumer(소비자)를 설정하는 메소드이다!<br> 시점과는 연관 없음!
