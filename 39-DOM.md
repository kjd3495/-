## DOM

---

1. 노드
2. 요소 노드 취득
3. 노드 탐색
4. 노드 정보 취득
5. 요소 노드의 텍스트 조작
6. DOM 조작
7. 어트리뷰트
8. 스타일
9. DOM 표준

---

<br/>

- DOM: HTML 문서의 계층적인 구조와 정보를 표현, 이를 제어할 수 있는 API, 즉 프로퍼티와 메서드를 제공하는 트리 자료구조

<br/>

### 39.1 노드

<br/>

- HTML 요소와 노드 객체

  - 트리 자료구조

    - 노드들의 계층 구조

    - 비선형 자료구조

    - DOM(Document Object Model): 노드 객체들로 구성된 트리 자료구조

- 노드 객체의 타입 (총 12개 종류)

  - 문서 노드

    - DOM 트리 최상위에 존재하는 루트 노드, document 객체 가리킴

    - 모든 JS 코드는 전역 객체 window의 document 프로퍼티에 바인딩 되어 있는 하나의 document 객체 공유

    - HTML 문서당 document 객체는 유일

    - DOM 트리 노드 진입 위한 엔트리 포인트 역할

  - 요소 노드

    - HTML 요소 가리키는 객체

    - 문서의 구조 표현

  - 어트리뷰트 노드

    - HTML 요소의 어트리뷰트를 가리키는 객체

    - 어트리뷰트 노드는 부모 노드가 없고 요소 노드에만 연결되어 있음

  - 텍스트 노드

    - HTML 요소의 텍스트를 가리키는 객체

    - 요소 노드의 자식 노드, 자식 노드 가질 수 없는 리프 노드

    - 문서의 정보 표현

- 노드 객체의 상속 구조

  - DOM 구성하는 노드 객체는 표준 빌트인 객체가 아니라 브라우저 환경 호스트 객체임

  - 노드 객체도 JS 객체이므로 프로토타입에 의한 상속 구조 가짐

  - 모든 노드 객체는 Object, EventTarget, Node 인터페이스 상속 받음

  - EventTarget 인터페이스; 모든 노드 객체는 이벤트 발생시킬 수 있음

    (EventTarget.addEventListener, EventTarget.removeEventListener, ...)

  - Node 인터페이스; 모든 노드 객체는 트리 자료구조의 노드로서 트리 탐색 기능이나 노드 정보 제공 기능 필요

    (Node.parentNode, Node.childNodes, Node.previousSibling, Node.nextSibling, Node.nodeType, ...)

  - HTMLElement 인터페이스; HTML 요소가 갖는 공통적 기능

    (HTML 요소 스타일 나타내는 style 프로퍼티, ...)

  - Object (객체)

    - EventTarget (이벤트 발생시키는 객체)

      - Node (트리 자료구조의 노드 객체)

        - Document

          - HTMLDocument

        - Element (브라우저가 렌더링할 수 있는 웹 문서의 요소를 표현하는 객체 ex. HTML, XML, SVG)

          - HTMLElement (웹 문서의 요소 중에서 HTML 요소를 표현하는 객체)

            - HTMLHtmlElement

            - HTMLHeadElement

            - HTMLMetaElement

            - HTMLLinkElement

            - HTMLScriptElement

            - HTMLBodyElement

            - HTMLUListElement

            - HTMLLIElement ...

        - Attr

        - CharacterData

          - Text

          - Comment

<br/>

### 39.2 요소 노드 취득

<br/>

- id를 이용한 요소 노드 취득

  - Document.prototype.getElementById 메서드

    - 인수로 전달한 id 어트리뷰트 값을 갖는 하나의 요소 노드 탐색하여 반환 (첫 번째 요소 노드만 반환)

    - id 값 갖는 HTML 요소 존재하지 않으면 null 반환

  - 반드시 문서 노드인 document를 통해 호출

  - HTML 요소에 id 어트리뷰트 부여 시 id 값과 동일한 이름의 전역 변수가 암묵적으로 선언되고

    해당 노드 객체가 할당됨

    - delete 연산자로 삭제 시 암묵적 전역으로 생성된 전역 프로퍼티는 삭제되지만 전역 변수는 그대로 있음

    - id 값과 동일한 이름의 전역 변수 이미 선언되어 있으면 전역 변수에 노드 객체 재할당되지 않음

- 태그 이름을 이용한 요소 노드 취득

  - Document.prototype/Element.prototype.getElementsByTagName 메서드

    - 인수로 전달한 태그 이름 갖는 모든 요소 노드 탐색하여 반환

    - 여러 개의 요소 노드 객체 갖는 DOM 컬렉션 객체인 HTMLCollection 객체 반환 (유사배열, 이터러블)

    - 인수로 전달된 태그 이름 갖는 요소 존재하지 않으면 빈 HTMLCollection 객체 반환

    - Document.prototype.getElementsByTagName 메서드

      - document를 통해 호출하며 DOM 전체에서 요소 노드 탐색해서 반환

    - Element.prototype.getElementsByTagName 메서드

      - 특정 요소 노드 통해 호출하며 특정 요소 노드의 자손 노드 중에서 요소 노드 탐색해서 반환

- class를 이용한 요소 노드 취득

  - Document.prototype/Element.prototype.getElementsByClassName 메서드

    - 인수로 전달한 class 어트리뷰트 값을 갖는 모든 요소 노드 탐색해서 반환

    - 여러 개의 요소 노드 객체 갖는 HTMLCollection 객체 반환

    - 인수로 전달된 class 값을 갖는 요소 존재하지 않으면 빈 HTMLCollection 객체 반환

    - Document.prototype.getElementsByClassName 메서드

      - document를 통해 호출하며 DOM 전체에서 요소 노드 탐색하여 반환

    - Element.prototype.getElementsByClassName 메서드

      - 특정 요소 노드 통해 호출하며 특정 요소 노드의 자손 노드 중에서 요소 노드 탐색하여 반환

- CSS 선택자를 이용한 요소 노드 취득

  - Document.prototype/Element.prototype.querySelector 메서드

    - 인수로 전달한 CSS 선택자를 만족시키는 하나의 요소 노드 탐색하여 반환

  - Document.prototype/Element.prototype.querySelectorAll 메서드

    - 인수로 전달한 CSS 선택자를 만족시키는 모든 요소 노드 탐색하여 반환

    - 여러 개의 요소 노드 객체 갖는 DOM 컬렉션 객체인 NodeList 객체 반환 (유사배열, 이터러블)

      - NodeList는 forEach 메서드 제공함

  - Document.prototype.querySelectorAll 메서드

    - DOM의 루트 노드인 문서 노드, 즉 document를 통해 호출하며 DOM 전체에서 요소 노드 탐색하여 반환

  - Element.prototype.querySelectorAll 메서드

    - 특정 요소 노드 통해 호출하며 특정 요소의 자손 노드 중에서 요소 노드 탐색하여 반환

- 특정 요소 노드를 취득할 수 있는지 확인

  - Element.prototype.matches 메서드

    - 인수로 전달한 CSS 선택자를 통해 특정 요소 노드 취득할 수 있는지 확인

    - 이벤트 위임을 사용할 때 유용

- HTMLCollection과 NodeList

  - HTMLCollection

    - ex. getElementsByTagName, getElementsByClassName, ...

    - 노드 객체의 상태 변화를 실시간으로 반영하는 live DOM 컬렉션 객체

    - for문으로 순회하면서 노드 객체 상태 변경 시 주의 필요

      - for문을 역방향으로 순회하기

      - while문을 사용하여 노드 객체 남아있지 않을 때까지 무한 반복하기

      - 유사 배열 객체이면서 이터러블인 HTMLCollection 객체를 배열로 변환하여 순회하기 (권장)

  - NodeList

    - ex. querySelectorAll, ...

    - 대부분 실시간으로 노드 객체의 상태 변경을 반영하지 않는 non-live 객체 (과거의 정적 상태 유지)

      - childNodes 프로퍼티가 반환하는 NodeList 객체는 live 객체로 동작하므로 주의 필요!

    - NodeList 객체는 NodeList.prototype.forEach/items/entries/keys/values 등 메서드 상속받아 사용 가능

    - 노드 객체 상태 변경 상관없이 안전하게 DOM 컬렉션 사용하려면 모두 배열로 변환하여 사용 권장

      - 스프레드 문법이나 Array.from 메서드 사용하면 간단히 배열로 변환 가능

      - 배열의 유용한 고차 함수 사용 가능

<br/>

### 39.3 노드 탐색

<br/>

- 공백 텍스트 노드

  - HTML 요소 사이의 스페이스, 탭, 개행 등 공백 (white space) 문자는 공백 텍스트 노드 생성

  - 노드 탐색 시 공백 문자가 생성한 공백 텍스트 노드 주의

- 자식 노드 탐색

  - 자식 노드 탐색 위해 노드 탐색 프로퍼티 사용

  - Node.prototype.childNodes 프로퍼티

    - 자식 노드 모두 탐색하여 NodeList에 담아 반환

    - 요소 노드뿐만 아니라 텍스트 노드도 포함 가능

  - Element.prototype.children 프로퍼티

    - 자식 노드중에서 요소 노드만 모두 탐색하여 HTMLCollection에 담아 반환

    - 텍스트 노드 포함 X

  - Node.prototype.firstChild 프로퍼티

    - 첫 번째 자식 노드 반환

    - 텍스트 노드 or 요소 노드

  - Node.prototype.lastChild 프로퍼티

    - 마지막 자식 노드 반환

    - 텍스트 노드 or 요소 노드

  - Element.prototype.firstElementChild 프로퍼티

    - 첫 번째 자식 요소 노드 반환

    - 요소 노드만 반환

  - Element.prototype.lastElementChild 프로퍼티

    - 마지막 자식 요노 노드 반환

    - 요소 노드만 반환

- 자식 노드 존재 확인

  - Node.prototype.hasChildNodes 메서드

    - 자식 노드 존재하면 true, 존재하지 않으면 false 반환

    - 텍스트 노드 포함하여 자식 노드의 존재 확인

  - 자식 노드 중에 텍스트 노드 아닌 요소 노드 존재하는지 확인하려면

    children.length 프로퍼티 또는 Element 인터페이스의 childElementCount 프로퍼티 사용

- 요소 노드의 텍스트 노드 탐색

  - 요소 노드의 텍스트 노드는 요소 노드의 자식 노드임

    - firstChild 프로퍼티로 접근 가능

      - 텍스트 노드 또는 요소 노드

- 부모 노드 탐색

  - Node.prototype.parentNode 프로퍼티

  - 부모 노드가 텍스트 노드인 경우는 없음 (텍스트 노드는 DOM 트리의 리프 노드)

- 형제 노드 탐색

  - 부모 노드 같은 형제 노드 탐색하기 위해 노드 탐색 프로퍼티 사용

    - 텍스트 노드 또는 요소 노드만 반환 (어트리뷰트 노드는 반환 X)

  - Node.prototype.previousSibling 프로퍼티

    - 부모 노드 같은 형제 노드 중에서 자신의 이전 형제 노드 탐색하여 반환

    - 요소 노드 or 텍스트 노드

  - Node.prototype.nextSibling 프로퍼티

    - 부모 노드 같은 형제 노드 중에서 자신의 다음 형제 노드 탐색하여 반환

    - 요소 노드 or 텍스트 노드

  - Element.prototype.previousElementSibling 프로퍼티

    - 부모 노드 같은 형제 노드 중에서 자신의 이전 형제 요소 노드 탐색하여 반환

    - 요소 노드만 반환

  - Element.prototype.nextElementSibling 프로퍼티

    - 부모 노드 같은 형제 노드 중에서 자신의 다음 형제 요소 노드 탐색하여 반환

    - 요소 노드만 반환

<br/>

### 39.4 노드 정보 취득

<br/>

- 노드 객체에 대한 정보 취득 위해 노드 정보 프로퍼티 사용

- Node.prototype.nodeType 프로퍼티

  - 노드 객체의 종류, 즉 노드 타입을 나타내는 상수 반환

    - Node.ELEMENT_NODE: 요소 노드 타입, 상수 1 반환

    - Node.TEXT_NODE: 텍스트 노드 타입, 상수 3 반환

    - Node.DOCUMENT_NODE: 문서 노드 타입, 상수 9 반환

- Node.prototype.nodeName 프로퍼티

  - 노드의 이름을 문자열로 반환

    - 요소 노드: 대문자 문자열로 태그 이름 반환

    - 텍스트 노드: 문자열 "#text" 반환

    - 문서 노드: 문자열 "#document" 반환

<br/>

### 39.5 요소 노드의 텍스트 조작

<br/>

- nodeValue

  - Node.prototype.nodeValue 프로퍼티

    - setter, getter 모두 존재하는 접근자 프로퍼티

    - 노드 객체의 값 반환 (텍스트 노드의 텍스트)

    - 텍스트 노드가 아닌 노드 (문서 노드나 요소 노드)의 nodeValue 프로퍼티 참조 시 null 반환

- textContent

  - Node.prototype.textContent 프로퍼티

    - setter, getter 모두 존재하는 접근자 프로퍼티

    - 요소 노드의 텍스트와 모든 자손 노드의 텍스트를 모두 취득하거나 변경

    - 요소 노드의 textContent 프로퍼티 참조 시 요소 노드의 콘텐츠 영역 내의 텍스트 모두 반환

    - 요소 노드의 textContent 프로퍼티에 문자열 할당 시 요소 노드의 모든 자식 노드가 제거되고,

      할당한 문자열이 텍스트로 추가됨

      - 할당한 문자열에 HTML 마크업이 포함되어 있어도 문자열로 인식되어 텍스트로 취급됨

      - HTML 마크업 파싱되지 않음

    - innerText 프로퍼티 사용 권장 X

      - CSS에 종속적임

      - CSS 고려해야 하므로 textContent 프로퍼티보다 느림

<br/>

### 39.6 DOM 조작

<br/>

- innerHTML

  - Element.prototype.innerHTML 프로퍼티

    - setter와 getter 모두 존재하는 접근자 프로퍼티

    - 요소 노드의 HTML 마크업을 취득하거나 변경

    - HTML 마크업이 포함된 문자열 그대로 반환

    - 요소 노드의 innerHTML 프로퍼티에 문자열 할당 시 할당한 문자열에 포함되어 있는

      HTML 마크업이 파싱되어 요소 노드의 자식 노드로 DOM에 반영됨

    - 사용자로부터 입력받은 데이터 (untrusted input data)를 그대로 innerHTML 프로퍼티에 할당하는 것은

      크로스 사이트 스크립팅 공격 (XSS: Cross-Site Scripting Attacks)에 취약하므로 위험

      - HTML 마크업 내에 JS 악성 코드 포함되어 있으면 파싱 과정에서 그대로 실행될 가능성 있음

      - HTML sanitization: DOMPurify 라이브러리 사용 권장

    - 요소 노드의 innerHTML 프로퍼티에 HTML 마크업 문자열 할당하면

      요소 노드의 모든 자식 노드를 제거하고 할당한 HTML 마크업 문자열을 파싱하여 DOM을 변경하는 단점

    - 새로운 요소 삽입 시 삽입될 위치 지정 못하는 단점

- insertAdjacentHTML 메서드

  - Element.insertAdjacentHTML(position, DOMString 메서드

    - 기존 요소 제거하지 않으면서 위치 지정해 새로운 요소 삽입

    - position(문자열): 'beforebegin', 'afterbegin', 'beforeend', 'afterend'

    - innerHTML 프로퍼티보다 효율적이고 빠름 (모든 요소 제거 이후 생성해서 추가하지 않음)

    - HTML 마크업 문자열 파싱하므로 크로스 사이트 스크립팅 공격에 취약함

- 노드 생성과 추가

  - 요소 노드 생성

    - Document.prototype.createElement(tagName) 메서드

      - 요소 노드 생성하여 반환

      - 생성된 요소 노드는 아무런 자식 노드 없음

      - tagName: 태그 이름 나타내는 문자열을 인수로 전달

  - 텍스트 노드 생성

    - Document.prototype.createTextNode(text) 메서드

      - 텍스트 노드 생성하여 반환

      - text: 텍스트 노드의 값으로 사용할 문자열을 인수로 전달

  - 텍스트 노드를 요소 노드의 자식 노드로 추가

    - Node.prototype.appendChild(childNode) 메서드

      - childNode를 메서드를 호출한 노드의 마지막 자식 노드로 추가

    - textContent 프로퍼티 사용하는 것이 더 간편함 (자식 노드 있으면 다 제거되므로 주의 필요)

  - 요소 노드를 DOM에 추가

    - Node.prototype.appendChild 메서드

    - 단 하나의 요소 노드 생성하여 DOM에 한번 추가하면 DOM은 한 번 변경됨

      - 리플로우와 리페인트 1번 실행됨

- 복수의 노드 생성과 추가

  - 배열의 forEach 메서드 이용

  - DOM 변경하는 것은 높은 비용이 드는 처리이므로 가급적 횟수 줄이는 것이 성능에 유리

    - 컨테이너 요소 사용

      - DOM을 한 번만 변경하므로 성능에 유리하지만 불필요한 컨테이너 요소 추가되는 부작용

    - DocumentFragment 노드 사용!

      - 자식 노드들의 부모 노드로서 별도의 sub DOM을 구성하여 기존 DOM에 추가하기 위한 용도로 사용

      - Document.prototype.createDocumentFragment 메서드

        - 비어있는 DocumentFragment 노드 생성하여 반환

- 노드 삽입

  - 마지막 노드로 추가

    - Node.prototype.appendChild 메서드

      - 항상 마지막 자식 노드로 추가

  - 지정한 위치에 노드 삽입

    - Node.prototype.insertBefore(newNode, childNode) 메서드

      - 첫 번째로 전달받은 노드를 두 번째 인수로 전달받은 노드 앞에 삽입

      - 두 번째 인수로 전달받은 노드는 반드시 insertBefore 메서드를 호출한 노드의 자식 노드여야 함

      - 두 번째 인수로 전달받은 노드가 null이면 첫 번째 인수로 전달받은 노드를 마지막 자식 노드로 추가

- 노드 이동

  - DOM에 이미 존재하는 노드를 appendChild/insertBefore 메서드를 사용하여 DOM에 다시 추가하면,

    현재 위치에서 노드를 제거하고 새로운 위치에 노드를 추가함 (노드가 이동함)

- 노드 복사

  - Node.prototype.cloneNode([deep: true | false]) 메서드

    - 노드의 사본을 생성하여 반환

    - deep에 true로 인수 전달 시, 노드 깊은 복사하여 모든 자손 노드 포함된 사본 생성

      - false로 인수 전달 시, 노드 얕은 복사 하여 노드 자신만의 사본 생성

      - 얕은 복사로 생성된 요소 노드는 자손 노드를 복사하지 않으므로 텍스트 노드도 없음

- 노드 교체

  - Node.prototype.replaceChild(newChild, oldChild) 메서드

    - 자신을 호출한 노드의 자식 노드인 oldChild를 newChild 노드로 교체

    - oldChild 노드는 DOM에서 제거됨

- 노드 삭제

  - Node.prototype.removeChild(child) 메서드

    - child 매개변수에 인수로 전달한 노드를 DOM에서 삭제

<br/>

### 39.7 어트리뷰트

<br/>

- 어트리뷰트 노드와 attributes 프로퍼티

  - HTML 문서 파싱될 때 HTML 요소의 어트리뷰트는 어트리뷰트 노드로 변환되어 요소 노드와 연결됨

  - 모든 어트리뷰트 노드의 참조는 유사 배열 객체, 이터러블인 NamedNodeMap 객체에 담겨서

    요소 노드의 attritbutes 프로퍼티에 저장됨

  - Element.prototype.attributes 프로퍼티

    - 요소 노드의 모든 어트리뷰트 노드 취득 가능

    - getter만 존재하는 읽기 전용 접근자 프로퍼티

    - HTML 요소 초기 상태는 변하지 않음

- HTML 어트리뷰트 조작

  - Element.prototype.getAttribute/setAttribute 메서드

    - 요소 노드에서 메서드 통해 직접 HTML 어트리뷰트 값 취득하거나 변경 가능해서 편리함

  - Element.prototype.getAttribute(attributeName) 메서드

    - HTML 어트리뷰트 값 참조

  - Element.prototype.setAttribute(attributeName, attributeValue) 메서드

    - HTML 어트리뷰트 값 변경

  - Element.prototytpe.hasAttribute(attributeName) 메서드

    - 특정 HTML 어트리뷰트 존재하는지 확인

  - Element.prototype.removeAttribute(attributeName) 메서드

    - 특정 HTML 어트리뷰트 삭제

- HTML 어트리뷰트 vs. DOM 프로퍼티

  - 요소 노드는 2개의 상태, 즉 초기 상태와 최신 상태 관리해야 함

    - 요소 노드의 초기 상태는 어트리뷰트 노드가 관리

    - 요소 노드의 최신 상태는 DOM 프로퍼티가 관리

  - 어트리뷰트 노드

    - HTML 어트리뷰트로 지정한 HTML 요소의 초기 상태는 어트리뷰트 노드에서 관리함

    - HTML 요소 초기 상태 그대로 유지

    - 초기 상태 값 취득하거나 변경 위해 getAttribute/setAttribute 메서드 사용

  - DOM 프로퍼티

    - 사용자가 입력한 최신 상태는 HTML 어트리뷰트에 대응하는 요소 노드의 DOM 프로퍼티가 관리함

    - 사용자의 입력에 의한 상태 변화에 반응하여 언제나 최신 상태 유지

    - HTML 요소에 지정한 어트리뷰트 값에는 어떠한 영향도 주지 않음

    - 모든 DOM 프로퍼티가 사용자의 입력에 의해 변경되 최신 상태 관리하는 것은 아님

      - ex. id 어트리뷰트와 id 프로퍼티는 사용자 입력과 관계없이 항상 동일한 값 유지/연동

  - HTML 어트리뷰트와 DOM 프로퍼티의 대응 관계

    - 대부분은 1:1 대응

    - 예외사항

      - class 어트리뷰트는 className, classList 프로퍼티와 대응

      - for 어트리뷰트는 htmlFor 프로퍼티와 1:1 대응

      - td 요소의 colspan 어트리뷰트에 대응하는 프로퍼티 존재 X

      - textContent 프로퍼티에 대응하는 어트리뷰트 존재 X

      - 어트리뷰트 이름은 대소문자 구별 X, 대응하는 프로퍼티 키는 카멜 케이스 따름

  - DOM 프로퍼티 값의 타입

    - getAttribute 메서드로 취득한 어트리뷰트 값은 항상 문자열 타입

    - DOM 프로퍼티로 취득한 최신 상태 값은 문자열 타입이 아닐 수 있음

- data 어트리뷰트와 dataset 프로퍼티

  - HTML 요소에 정의한 사용자 정의 어트리뷰트와 JS 간에 데이터 교환 가능

  - data 어트리뷰트 값은 HTMLElement.dataset 프로퍼티로 취득 가능

    - dataset 프로퍼티는 HTML 요소의 모든 data 어트리뷰트 정보 제공하는 DOMStringMap 객체 반환

    - DOMStringMap 객체에 data- 접두사 다음에 카멜 케이스로 변환한 프로퍼티 가지고 있음

    - 반대로 동적으로 HTML 요소에 data 어트리뷰트 추가하면 케밥 케이스로 자동 변경되어 추가됨

<br/>

### 39.8 스타일

<br/>

- 인라인 스타일 조작

  - HTMLElement.prototype.style 프로퍼티

    - setter, getter 모두 존재하는 접근자 프로퍼티

    - 요소 노드의 인라인 스타일을 취득하거나 추가/변경 가능

    - style 프로퍼티 참조 시 CSSStyleDeclaration 타입의 객체 반환

      - CSS 프로퍼티는 케밥 케이스 따름

      - CSSStyleDeclaration 객체의 프로퍼티는 카멜 케이스 따름

- 클래스 조작

  - className

    - Element.prototype.className 프로퍼티

      - setter, getter 모두 존재하는 접근자 프로퍼티

      - HTML 요소의 class 어트리뷰트 값을 취득하거나 변경

  - classList

    - Element.prototype.classList 프로퍼티

      - class 어트리뷰트의 정보를 담은 DOMTokenList 객체 반환

      - DOMTokenList; 노드 객체의 상태 변화를 실시간으로 반영하는 live 객체,

        class 어트리뷰트의 정보를 나타내는 컬렉션 객체로서 유사 배열, 이러터블

        - add(...className)

          - 인수로 전달한 1개 이상의 문자열을 class 어트리뷰트 값으로 추가

        - remove(...className)

          - 인수로 전달한 1개 이상의 문자열과 일치하는 클래스를 class 어트리뷰트에서 삭제

        - item(index)

          - 인수로 전달한 index에 해당하는 클래스를 class 어트리뷰트에서 반환

        - contains(className)

          - 인수로 전달한 문자열과 일치하는 클래스가 class 어트리뷰트에 포함되어 있는지 확인

        - replace(oldClassName, newClassName)

          - class 어트리뷰트에서 첫 번째 인수로 전달한 문자열을 두 번째 인수로 전달한 문자열로 변경

        - toggle(className[, force])

          - class 어트리뷰트에 인수로 전달한 문자열과 일치하는 클래스가 존재하면 제거하고, 존재하지 않으면 추가

          - 두 번째 인수로 불리언 값으로 평가되는 조건식 전달 가능,

            true => 강제로 첫 번째 인수로 전달받은 문자열 추가, false => 강제로 제거

- 요소에 적용되어 있는 CSS 스타일 참조

  - window.getComputedStyle(element, pseudo]) 메서드

    - HTML 요소에 적용되어 있는 모든 CSS 스타일 참조

    - 첫 번째 인수로 전달한 요소 노드에 적용되어 있는 computed 스타일을 CSSStyleDeclaration 객체에 담아 반환

    - 두 번째 인수로 :after, :before 와 같은 pseudo element를 지정하는 문자열 전달 가능

<br/>

### 39.9 DOM 표준

<br/>

- HTML과 DOM 표준은 W3C와 WHATWG 두 단체가 협력하면서 공통 표준 만들어 왔음

- 최근에 두 단체 서로 다른 표준 결과물 내놓음

- WHATWG이 단일 표준 내놓기로 두 단체가 합의함
