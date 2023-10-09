---
title: "[1주차] 웹 퍼블리싱 시작하기"
excerpt: "HTML & CSS를 처음 배워보았습니다."

categories:
  - CodeitSprint
tags:
  - [부트캠프, HTML, CSS]

permalink: /CodeitSprint/[1주차]-웹-퍼블리싱-시작하기/

toc: true
toc_sticky: true

date: 2022-07-24
last_modified_at: 2022-07-24
---

# Ch1. 수업 소개
- html : 사이트의 `내용`을 작성하는 언어
- css : 페이지의 `스타일`을 작성하는 언어 (디자인을 담당한다.)

## 나의 첫 웹사이트
```html
<!DOCTYPE html> <!-- DOCUMENT 타입이 HTML이라는 것 -->
<html>
    안녕 HTML!
</html> 
```
- 맨 처음에는 `<!DOCTYPE html>`를 반드시 써준다. #include<stdio.h> 와 같은 개념인 것 같다,, 손에 익혀야지
- <html></html> : html 태그
  - html 코드는 html 태그로 크게 감싸진다.
- <> 안에 써지는 것들을 태그라고 하고, 시작 & 종료 태그로 이루어져 있다.
  - 종료 태그 앞에는 /가 붙는다.
> 내가 처음으로 만든 페이지!<br>
netlify에서 배포도 하고, site name도 바꿔봤다. 

https://first-page-of-hw.netlify.app/

# Ch2. HTML 시작하기
```html
<!DOCTYPE html>
<html>
    <head>
        <title>Weekly Codeit</title> <!-- title : 페이지의 제목 -->
        <meta charset="utf-8"> <!-- 안에 내용이 없으므로 시작 태그만 존재, 한글 안깨지려면 무조건 써줘야하는 코드 -->
    </head>
    <body>
        <!-- body tag는 페이지의 내용 
        글은 늘 이어져 있다. 단락 구분은 p tag로 !-->
        <h1>Weekly Codeit</h1> <!-- h1 : heading 1(숫자 커질수록 글씨 작아짐, h6까지 있음), 제목 -->
        <h2>생산성을 높여줄 유닉스 커맨드 꿀팁</h2>
        <h2>머신 러닝을 통한 추천 시스템(내용 기반, 협업 필터)</h2>
        <h2>Tips & Tricks: HTML 코드 편하게 입력하는 법</h2>
        <h2>코둥이 퀴즈</h2>
    </body>
</html>
```
- html은 크게 head 태그, body 태그로 이루어져 있다.
- `<head>` 태그 : 페이지에 직접적으로 보이지 않는 내용을 작성한다.
  - `<title>` 태그 : 탭 부분에 나타나는 페이지의 제목을 의미한다.
- `<body>` 태그 : 실제로 페이지에 보이는 내용을 작성한다.
  - `<h1~6>` 태그 : 글의 제목을 의미하는 태그
  - `<p>` : 단락을 나타내는 태그
    - 주로 세부 내용을 작성할 때 사용된다.

## 줄 바꿈
- html에서는 줄 바꿈이 없는 게 디폴트다.
  - 그래야 페이지 크기를 늘렸을 때에도 자동으로 여백이 채워지기 때문이다.
- `<br>` : 줄 바꿈 태그

## 이미지와 링크
- `<img>` 태그 : 이미지를 넣을 수 있다.
- `<a>` 태그 : 하이퍼링크를 걸 수 있다.

## 속성 이름 = "속성 값"
- <a `href="주소"`>자세히 보기</a>
- <img `src="이미지 주소"`>

## 💻 위키 페이지 만들기
`실습 결과`

![image](https://github.com/naya-h2/naya-h2.github.io/assets/103186362/58fb9018-2cf0-44d3-bbfc-8589789b6dc5)

`실습 코드`

```html
<!DOCTYPE html>
<html>
  <head>
    <title>DK</title>
    <meta charset="utf-8">
  </head>
  <body>
    <h1>
      도겸<br>
      (DK)
    </h1>
    <img src = "https://i.namu.wiki/i/i7arK6D44GJDJtO0RVDKIcqALwnN02kY8eN8IdclXAiPsqYS_Toq0zS8pqW8feMUr5trPVt1vRSdS8031pC_Zim80YDC02oY-YxGcjyBLi1Ga0I5LzyBIjqkTFE86AlvcT_5x6SYW7wZhQ1zqfkVkw.webp">
    <p>
      플레디스 엔터테인먼트 소속 13인조 보이그룹 <a href = "https://namu.wiki/w/%EB%B6%84%EB%A5%98:%EC%84%B8%EB%B8%90%ED%8B%B4">세븐틴</a>[보컬팀]과 믹스 유닛 부석순의 멤버.
      팀 내 메인보컬을 맡고 있으며 부석순에서는 리더를 겸하고 있다.
    </p>
  </body>
</html>
```

> 뚝딱이면서 만들어봤는데,, 도겸 사진이 너무 커버림 ,, 밑에 설명도 있고 페이지 링크도 달았는데ㅜ
사진 크기 조절하는 건 css에서 하는 건가?<br>
사진 출처는 나무위키 ..

## 꺾쇠 기호 넣는 법
- html에서 `<>`는 태그를 의미하기 때문에 일반적인 텍스트로 사용할 수 없다.
- 페이지 내용에 <> 넣는 법 : `&lt; 페이지내용 &gt;`

## 영역 나누기
- `<div>` 태그 : 눈에 보이지 않는 영역을 `박스`처럼 지정
- `<span>` 태그 : 제목이나 단락에서 `일부분`만 영역 지정
  - ex. "weekly codeit"에서 'codeit'만 굵게 하고 싶을 때 사용한다.

## 꿀팁
- vs code에서 `!`를 입력한 상태에서 `tab`을 누르면 html 기본 코드를 완성해준다 !!

# Ch3. CSS 시작하기
## 배경색
```html
<div style = "background-color: purple">
```
- purple 대신 색상 코드를 직접 넣어줘도 된다.
- css에서는 **"속성 이름 : 속성값"** 이다.

## 💻 구독 페이지: 배경색 넣기
`실습 결과`

![image](https://github.com/naya-h2/naya-h2.github.io/assets/103186362/0cc0c1fb-8036-4d1f-9b35-04b50097d9e2)

`실습 코드`  
```html
<!DOCTYPE html>
<html>
  <head>
    <title>Weekly Codeit 구독하기</title>
    <meta charset="utf-8">
  </head>
  <body>
    <div style = "background-color : #703fda">
      <h1>Weekly Codeit</h1>
      <p>
        금요일에 만나는<br>
        코딩 한 스푼
      </p>
    </div>
    <div>
      <h2>
        코드잇이 엄선한<br>
        프로그래밍 꿀팁
      </h2>
      <img src="banner-programming.png">
      <p>
        컴퓨터 개론, 프로그래밍 기초, 업무 자동화 ...<br>
        인기 코드잇 강의를 뉴스레터로 만나보세요.
      </p>
      <p>
        유용한 팁과 개발 지식을 매주 금요일 여러분의 메일함으로 보내드려요.
      </p>
      <p>
        <a href="https://codeit.kr/catalog">
          수업 살펴보기
        </a>
      </p>
    </div>
    <div style = "background-color : #f6f6fb">
      <h2>
        배움의 기쁨을 세상 모두에게.<br>
        많은 코둥이들이 구독하고 있어요!
      </h2>
      <img src="banner-students.png">
      <p style = "background-color : #ffffff">
        iloveprincess 님<br>
        안녕하세요, 5년차 코둥이입니다! 제가 구독 중인 뉴스레터 중 가장 읽기 편하고 재밌어요.
        매주 금요일이 기다려지네요 :) 
      </p>
      <p style = "background-color : #ffffff">
        코드냠냠 님<br>
        뉴스레터 정말 잘 보고 있습니다. 다양한 주제에 대한 소개 덕분에 기술 면접에서도 당황하지 않을 수 있었어요!
        항상 감사드립니다.
      </p>
      <p style = "background-color : #ffffff">
        냐리 님<br>
        덕분에 프로그래밍 상식이 풍부해지는 느낌임. 깊이있는 내용을 알기 쉽게 소개해줘서 더 좋은듯.
        초보 코둥이들에게 추천해요.
      </p>
      <p style = "background-color : #ffffff">
        <a href="https://codeit.kr/reviews">
          후기 더 보기
        </a>
      </p>
    </div>
    <div style = "background-color : #7844e8">
      <h2>
        코딩이 즐거워지는 뉴스레터,<br>
        Weekly Codeit
      </h2>
    </div>
    <div style = "background-color : #5b2eb0">
      <p>
        Weekly Codeit
      </p>
      <p>
        Weekly Codeit 을 아직 구독하지 않으셨다면? 구독 신청 Subscribe<br>
        최신 뉴스레터들을 놓치지 않기 위해 weekly@codeit.kr을 메일 주소록에 추가해주세요
      </p>
      <p>
        (주)코드잇 | 서울 중구 청계천로 100 시그니쳐타워 동관 10층 | 수신 거부 Unsubscribe
      </p>
    </div>
  </body>
</html>
```

## 글자색
```html
<h1 style = "color : #ffffff"></h1>
```
- body tag에 color를 지정하면 기본 지정색을 정할 수 있다.
```html
<div style = "background-color : purple ; color : #ffffff"></div>
```
- 여러 개의 CSS 속성을 사용하고 싶으면 `;` 을 사용한다.

## 글꼴
```html
<body style="color: #737373 ; font-family : Arial, AppleGothic, 돋움">
```
- `font-family`라고 지정하면 **여러 개의 글꼴**을 지정할 수 있다.
- 위의 코드 뜻은 Arial로 설정되지 않는 부분은 AppleGothic, 얘도 없으면 돋움으로 설정하라는 뜻이다.

## 웹 폰트 사용 방법 (구글 폰트)
- `<link>` : 외부에서 데이터를 가져오는 태그
  - head 태그에 작성하는 태그다.
- 구글 폰트에서 원하는 폰트의 <link> 코드를 복사하고, head에 붙여넣는다.
- 원하는 영역에 CSS 속성 코드로 font-family를 추가하면 끝!

## 글자 크기와 굵기
- `font-size : 20px` : 글자 크기를 20px로 설정
- `font-weight : 300` : 글자 굵기를 300으로 설정
  - 굵기는 100단위로 설정
  - 100 ~ 900까지

## 글 정렬
- `text-align : center/right/left` : 중앙/우측/좌측 정렬

## 크기 고정
- `width : 700px ; height = 375px` : 700px, 375px로 크기 고정
- `width : 100%` : 화면 넓이의 100%를 채우도록 설정

## 여백
- padding : 영역 안쪽 여백
  - `padding : 40px 20px` : 영역에 여백 설정
  - <div>에 추가하면 된다.

- margin : 영역 바깥쪽 여백
  - `margin : 32px` : 상자 바깥에 여백 설정
  - 기본적으로 body에는 margin이 설정되어 있다.
  - `margin : 0 auto` : 세로는 0, 가로는 자동으로 바깥여백 설정(== 가운데 정렬)
 
# Ch4. 완성하기
## 오픈그래프로 소셜 공유 미리보기 만들기
```html
<head>
<title>The Rock (1996)</title>
<meta property="og:title" content="The Rock" />
<meta property="og:type" content="video.movie" />
<meta property="og:url" content="https://www.imdb.com/title/tt0117500/" />
<meta property="og:image" content="https://ia.media-imdb.com/images/rock.jpg" />
</head>
```
- 페이지 링크를 복붙하면 자동으로 미리보기 창이 생성되는 방법
- head 태그 부분에 `<meta property = "~" content = "~">`를 추가하면 된다.

## 구글 애널리틱스로 방문자 수 확인하기
- [🔎 이 강의를 참고해주세요](https://www.codeit.kr/topics/intro-to-web-publishing/lessons/5353)

# Ch5. 꿀팁
## 개발자 도구 사용하기
- `f12` : 개발자 도구 열기
> 우와 개발자 도구로 선택해서 그 부분에 해당하는 코드 읽을 수 있는거 짱신기,, 거기다 내가 배운 내용들로 구현됐다는게 더 신기하다 !!

## HTML/CSS 공부하는 법
- MDN 사이트를 이용하자
- div 태그가 궁금할땐?
  - `MDN div` 라고 구글에 검색해보기

---
# 공부 후기
`23.09.05`

html 아예 첨배웠는데 재밌잖아 ,,?  
아직까진 오류도 없고, 한줄 작성하면 바로 웹페이지에 결과로 나타나는게 넘 짜릿 ,,,✨  
아무튼 도겸 페이지 만들기 잼썼다.
