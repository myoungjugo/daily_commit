## 개요

js기반인 리액트로 안드로이드, ios 다 짤 수 있음

웹/앱/pc 개발까지 다 할 수 있음

마크업     *논리설계가능

실습- 크롬브라우저(js가 잘돌아감)

마우스우클릭→검사→개발자도구창에서 콘솔

REPL :입력하고 바로 결과나옴

호이스팅:변수나 함수를 스코프 상단으로 끌어올림 → 버그의 원인이 될 수 있음

## 기초문법

- 출력

```python
console.log();
```

- 변수

var, let(한 번 할당한 것을 바꿀 수 있음)    const(바뀔 수 없음, 상수)

기본적으로는 let a = 1

- 함수

```jsx
function myFunction(x) {

let temp = 2*x + 3

return temp

}
```

또는

- 화살표함수

함수 선언 방식. 

(매개변수) ⇒ {…} 

```jsx
add = (x,y) ⇒ {

let temp  = x+y;

return temp;

}
```

익명함수(바로실행)

((매개변수) ⇒ {실행내용})(인자)

```jsx
((x,y) ⇒ {return x+y})(1,2)
```

- 조건문

```jsx
if(money > 5000){

rideTaxi();

} else if(money > 2000) {

rideBus();

} else {

walk();

}
```

- 반복문

```jsx
for (let i = 0; i<10; i++){
	  console.log("나무찍기" + i);
}
```

```jsx
myArray = [1,2,3,4,5]
myArray.forEach(element => { //.foreach로 하나씩 빼서 중괄호 안에 있는 식을 실행
		console.log("나무 찍기" + element);
});
```

## 특징

- 숫자 자료형+문자 자료형이 가능
- 문법 널널 → 자체논리 강함
- 브라우저 위에서 돌아가므로 따로 설치하지 않아도 실행가능

## 비동기

- 비동기:  특정 작업의 완료를 기다리지 않고 다른 작업을 동시에 수행함

setTimeout() 함수나 fetch() 함수.

메인 스레드가 작업을 다른 곳에 인가하여 처리 → 작업 완료 시 콜백 함수를 받아 실행

비동기 함수의 콜백 함수가 이벤트 루프에 의해 콜백 큐에 담김

→ 다시 싱글 스레드인 콜스택에 담겨 콜백 함수가 실행됨

![image.png](attachment:d5366e15-1866-4835-9356-c14bbf397c7b:image.png)

자바스크립트를 실행하는 콜 스택 자체는 싱글 스레드(한 번에 하나의 작업만 수행)

but Web APIs 는 멀티스레드 (각 api마다 스레드들이 할당되어 있고, 이들이 모여 멀티 스레드로)

```jsx
setTimeout(()=>{   //WebAPIs들 중 TimerAPI에 넘어가 3000ms를 병렬로 처리됨
	console.log('5초 대기 완료')
}, 3000);
Task1();
Task2();
Task3();
//동시에 메인 콜 스택의 Task1,2,3을 처리
```

## 모듈

- 파일 하나 = 모듈 하나

```jsx
function add(a,b){
		return a + b;
}
module.exports = {add};  //내보내기

const {add} = require("./math"); //불러오기
console.log(add(2,3));
```

## 콜백

비동기 코드는 실행 순서 예측 불가 (언제 결과값 받아올지 모름)

```jsx
function first() {
  let value;

  setTimeout(() => {
    value = { name: "MaxlChan", age: 18 };
  }, 3000);  // 서버에서 데이터를 가지고 오는 과정이라 가정(몇초가 걸리는 지 실제로는 모름)

  return value;
}

console.log(first()); // undefined
```

여기서 변수에 할당하기 전에 반환했기 때문에 undefined 나옴. 

가져온 값을 활용해야 하는데 이러면 안되잖아.

⇒이걸 해결하기 위한 방법 중 하나가 콜백.

콜백 함수는 다른 함수에 인수로 전달된 함수.

*“작업 끝나면 이 전화번호(콜백함수)로 전화 줘(call me back)”*

콜백 내부에서 리턴하는 값이 항상 외부로 돌아가지는 않는다.

node.js는 파일 읽기, 네트워크 요청 같은 작업을 비동기로 함

→ 결과를 처리할 때 콜백을 자주 사용.

```jsx
function fetchData(callback){
	console.log("데이터 가져오는 중...");
	setTimeout(()=>{
		const data = { name :"Alice", age:25};
		callback(data);  // 다 끝나고 호출
	}, 1000);
}

//사용
fetchData(function(result){   //콜백 함수
	console.log("콜백으로 받은 데이터:", result);
});
//fetchData가 데이터를 다 불러오면 콜백함수를 실행하면서 result에 값 전달해 줌
```

```jsx
//2초 후 함수를 실행해 달라. setTimeout(함수, 지연시간)
setTimeout(() => {
	console.log("2초 후 실행!");  // 안에 실행할 함수를 인자로 넘김
}, 2000);

//파일 읽기 콜백
const fs = require("fs");

fs.readFile("hello.txt", "utf8", (err,data) => {
	if (err) {
		console.error("에러 발생:",err);
	}else{
		console.log("파일 내용:", data);
	}
});
```

단점: 콜백 안에 콜백이 계속 들어가면 콜백 지옥 발생

## 프로미스

비동기 작업의 결과를 담는 객체

*”택배 배송조회 번호(promise)를 주고,  나중에 택배가 오면 알려줄게.”*

(성공: resolve

실패: reject)

```jsx
//promise 직접 만들기
let myPromise = new Promise((resolve, reject) => {
	let success = true;
	if (success){
		resolve("성공!"); //성공했을 때 결과 전달
	}else {
		reject("실패...");  //실패했을 때 에러 전달
	}
});

//사용
myPromise
	.then(result => console.log(result)) //성공:"성공!"  //성공시 실행
	.catch(error => console.error(error))//실패:"실패..."   //에러 발생 시 실행
```

```jsx
//자주 쓰는 형태
const fs = require("fs").promises;

fs.readFile("hello.txt", "utf8")
	.then(data => console.log("읽은 내용:", data))
	.catch(err => console.error("에러:", err));
```

## 프론트에서

<script>태그

html 메소드

- getElementById()    괄호 안에 있는걸 찾고 = 뒤에 오는걸로 바꿈
- onclick=    클릭하면
- document.getElementById("demo").style.display = "none";  숨

css 메소드

- document.getElementById("demo").style.fontSize = "35px";

이벤트가 발생하면 함수 실행됨 

외부 파일

- <script src="myScript.js"></script>

이때 외부 파일은 script 태그를 포함할 수 없음. 이미 불러오면서 썼잖아.

src 뒤 “ 안에는 전체 url을 넣을 수도 있고 파일경로를 넣을 수도 있음. 파일 이름을 넣을수도.

body에 쓸 땐 함수 먼저 쓰고 script  태그 뒤에 함수 정의 해도 동작
