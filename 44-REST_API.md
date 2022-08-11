## REST_API

---

1. REST API의 구성
2. REST API 설계 원칙
3. JSON Server를 이용한 REST API 실습

---

<br/>

- REST(REpresentational State Transfer)

  - HTTP를 기반으로 클라이언트가 서버의 리소스에 접근하는 방식을 규정한 아키텍쳐

- REST API: REST 기반으로 서비스 API 구현, self-de-scriptiveness (자체 표현 구조) -> HTTP 요청 내용 이해 가능

<br/>

### 44.1 REST API의 구성

- 자원(resource): 자원, URI(엔드포인트)

- 행위(verb): 자원에 대한 행위, HTTP 요청 메서드

- 표현(representations): 자원에 대한 행위의 구체적 내용, 페이로드

<br/>

### 44.2 REST API 설계 원칙

<br/>

- URI는 리소스를 표현해야 한다.

  - 리소스 식별 가능한 이름은 명사 사용

- 리소스에 대한 행위는 HTTP 요청 메서드로 표현한다.

  - GET, POST, PUT, PATCH, DELETE 요청 메서드를 사용하여 CRUD 구현

  - URI에 표현 X

<br/>

### 44.3 JSON Server를 이용한 REST API 실습

<br/>

- JSON Server 설치

  - JSON Server: json 파일 사용하여 가상 REST API 서버 구축할 수 있는 툴

  - NPM 이용

- db.json 파일 생성

  - 리소스를 제공하는 DB 역할

- JSON Server 실행

- GET 요청

- POST 요청

- PUT 요청

- PATCH 요청

- DELETE 요청
