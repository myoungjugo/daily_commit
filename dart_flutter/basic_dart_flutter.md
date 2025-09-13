# dart flutter

flutter 윈도우용 zip파일을 다운받고 환경변수도 편집함.

왜?

### 환경변수란

운영체제가 프로그램을 실행할 때 참고하는 전역 설정 값.

→ 어떤 프로그램을 어디서 찾을지

→ 어떤 설정을 기본으로 쓸지

- PATH

실행 파일을 찾는 경로 목록

### 환경변수 PATH에 등록해야 하는 이유

cmd에 flutter —version같은 명령을 치면

OS는 PATH 환경변수에 등록된 폴더들을 뒤져서 실행 파일(flutter.bat)를 찾음.

- 등록하지 않으면

어디서 찾아야 할지 모름.

- 등록하면

어느 위치에서는 cmd를 켜고 flutter라고만 쳐도 실행 가능!

### dart/flutter란

- dart

구글이 개발한 프로그래밍 언어

문법은 java, c#, javascript와 비슷

```dart
void main() {
  var name = "ChatGPT";
  int age = 3;

  if (age > 1) {
    print("Hello, $name! You are $age years old.");
  }
}
```

클래스/객체 지향 지원

비동기 처리. async/await 내장

컴파일 방식

-JIT →개발 중 빠른 실행

-aot(not attack if titan, yes ahead of time) →배포 시 네이티브 코드로 컴파일해서 빠름

- flutter

dart를 기반으로 동작하는 ui 프레임워크

***크로스 플랫폼***

⇒ ios, android, web, desktop을 한 번에 개발 가능.

리액트와 비슷하지만 자체 렌더링 엔진 덕분에 성능이 더 안정적이라는 평가.

ui 위젯 시스템이 잘 되어 있어서 화면 구성에 강점.

### 백엔드 개발 가능?

dart의 백엔드 프레임워크

- aqueduct(지금은 개발 중단
- angel, alfred, shelf 경량 서버 프레임워크

⇒ rest api(웹에서 가장 널리 쓰이는 데이터통신규칙 api방식. 보통 url + http 메소드로 동작. 서버가 정해준 엔드포인트마다 요청을 보내고 json과 같은 형식으로 응답을 받음. 단순하지만 원하는 데이터만 딱 집어서 가져오기 힘듦.)

, graphQL( 클라이언트가 원하는 데이터만 정확히 요청가능한 api 방식. url 여러개 x. /graphql 하나만 있음. 쿼리 문법으로 어떤 필드가 필요한지 직접 지정. 그러나 서버 구현 복잡함.)

서버 정도는 충분히 가능.

다만 생태계가 파이썬 자바만큼 크지는 않아서 실무에서 dart로 백엔드하는 경우는 드묾.
