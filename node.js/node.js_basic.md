# 소개

무료 오픈소스. 자바스크립트를 웹브라우저 밖에서 실행하도록 도와줌.
웹서버, api등 빠른 어플리케이션 만들 수 있음

- api란

응용 프로그램 프로그래밍 인터페이스

두 소프트웨어 구성 요소가 서로 통신할 수 있게 하는 메커니즘.

(ex 날씨 앱이  기상청 시스템과 대화하여 매일 최신 날씨를 표시

- 이벤트 동작
- 높은 트래픽

### vscode에서 사용

.js 파일 생성

자바스크립트는 브라우저에 인터프리터가 있어서 컴퓨터에서 설치하지 않아도 돌아감.

→ 이걸 내 컴퓨터 혹은 서버에서 돌리는 *백엔드*가 목표!

⇒ node.js를 설치해야 실행 가능

node.js에서 npm 사용 

사용가능한 모듈이 많다 

node.js 폴더 안 index.js 파일

```jsx
console.log("hello world")
```

```powershell
node index.js  
```

실행됨.

## npm

node package manager

https://www.npmjs.com/

→ 모듈 다운받을 수 있음

- 설치방법

```powershell
npm install 모듈이름
```

끝에 -g 덧붙이면 해당 프로젝트 뿐만 아니라 다른 곳에서도 사용 가능

```powershell
npm uninstall 모듈이름
```

- npm init 터미널에

package.json 생성됨 : 설치된 모듈들을 정리해주는 메모장과 비슷, 대략적으로 확인하는 용도

package-lock.json : 더 구체적인 정보 기록

*전역으로 설치할 시 충돌이 일어날 수 있기에 프로젝트에서만 설치하는 것을 추천

- express

node.js 기반 웹 프레임워크

- 웹 프레임워크

클라이언트의 요청 → 백엔드에서 응답.

⇒ 요청에 따라 응답하는 게 웹 프레임워크.

## 예제 api

```jsx
import express from 'express'

const app = express()

app.get('/', (req, res) => {
  res.send('Hello World')
})

app.listen(3000) 
```

서버 끄는 명령어 

: ctrl + c

- 포트

*선착장*  ip 주소로 들어올 수 있는 입구. 따라서 포트마다 다른 프로그램 실행 가능.

listen을 하고 있어야 들어왔을 때 수행 가능

localhost: 내 컴퓨터로 접속할 때 내 컴퓨터의 ip주소는 굳이 쓰지 않아도 됨.

```jsx
app.get('/', (req,res) => {
	res.send('Hello World!')   //응답에 hello world 보내겠다. 담겠다.
})
```

## app.get( ‘/’, () ⇒ {} )

    http메소드  라우팅     콜백함수

- http 메소드

요청의 목적, 종류를 알려주기 위해 사용하는 수단. 

이걸 달고 가면 목적에 맞게 요청하고 처리 가능함.

- get

요청 : 주소창에서 데이터 전달.

params 또는 query 이용 가능.

- post

요청: 주소창이 아닌 내부적으로 body에 데이터 전달.

- 라우팅

라우팅에 따라 보여지는 html 페이지가 달라짐.

‘/’ : 기본주소

- 콜백함수

함수 ( 끝나고 실행할 함수 )

다른 코드에 인수로서 넘겨주는 실행 가능한 코드.

setTimeout( 콜백함수, 시간)

실행 순서 조정.

⇒ 순서

항상 3000번 포트 듣고 있음. 

→프론트에서 http 요청을 보냄.

→ app.get 방식의 루트(’/’)로 들어옴.

→res.send로 응답을 프론트로 돌려줌.

- json

자바스크립트 오브젝트.  {’sound’ : ‘멍멍;}

이걸 보낼 때는 res.send  res.json 둘 다 가능

## 파라미터 값으로 라우팅하기

- params이용하기

```jsx
app.get('/user/:id', (req, res) => {  
    const q = req.params
    console.log(q)
    res.send({'userid' : q.id})
})
```

이때 id는  주소창에서 파라미터로 받아옴.

id로 받은 값이 params로 들어옴.

- query 이용

```jsx
app.get('/user/:id', (req, res) => {  
 
    const q = req.query
    console.log(q)

    res.send({'userid' : q.id})
})
```

- 쿼리스트링 asdf?

뒤에오는값 받아서 서버에 전달.

서버는 그냥 /page를 보여줄지, 특정 조건 /page
