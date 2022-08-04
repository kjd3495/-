## Set과 Map

---

1. Set
2. Map

---

<br/>

### 37.1 Set

<br/>

- Set 객체: 중복되지 않는 유일한 값들의 집합, 요소 순서 의미 X, 인덱스로 요소 접근 불가

- Set 객체의 생성

  - Set 생성자 함수로 생성

    - 이터러블을 인수로 전달받아 Set 객체 생성

  - 배열에서 중복된 요소 쉽게 제거 가능 (filter, indexOf 메서드 사용 안해도 됨)

- 요소 개수 확인

  - Set.prototype.size 프로퍼티

    - setter 함수 없이 getter 함수만 존재하는 접근자 프로퍼티

- 요소 추가

  - Set.prototype.add 메서드

  - 새로운 요소 추가된 Set 객체 반환 => add 메서드 chaining 가능 (연속적 호출)

  - NaN과 NaN, 0과 -0은 같다고 평가하여 중복 추가 허용 X

  - Set 객체에 JS 모든 값을 요소로 저장 가능

- 요소 존재 여부 확인

  - Set.prototype.has 메서드

  - 특정 요소의 존재 여부 나타내는 불리언 값 반환

- 요소 삭제

  - Set.prototype.delete(삭제하려는요소) 메서드

  - 삭제 성공 여부 나타내는 불리언 값 반환 => method chaining 불가

- 요소 일괄 삭제

  - Set.prototype.clear 메서드

  - 언제나 undefined 반환

- 요소 순회

  - Set.prototype.forEach 메서드

    - 첫 번째 인수: 현재 순회 중인 요소값

    - 두 번째 인수: 현재 순회 중인 요소값

    - 세 번째 인수: 현재 순회 중인 Set 객체 자체

    - 첫, 두 번째 인수 같은 이유는 단순히 Array.prototype.forEach 메서드와 인터페이스 통일하기 위함

  - Set 객체는 이터러블임 => for ... of 문 순회 가능, 스프레드 문법/배열 디스트럭처링의 대상

- 집합 연산

  - 교집합

    - for ... of 문과 Set.prototype.has 메서드 이용

    - 또는 스프레드 문법과 filter, has 메서드 이용

  - 합집합

    - for ... of 문과 Set.prototype.add 메서드 이용

    - 스프레드 문법 이용

  - 차집합

    - for ... of 문과 Set.prototype.delete 메서드 이용

    - 스프레드 문법, filter, has 메서드 이용

  - 부분 집합과 상위 집합

    - for ... of 문과 this(Set 객체).has 이용

    - 스프레드 문법, every, includes 메서드 이용

<br/>

### 37.2 Map

<br/>

- Map 객체: 키와 값의 쌍으로 이루어진 컬렉션, 이터러블임, 객체를 포함한 모든 값을 키로 사용 가능

- Map 객체의 생성

  - Map 생성자 함수로 생성

    - 이터러블을 인수로 전달받아 Map 객체 생성

    - 인수로 전달되는 이터러블은 키와 값의 쌍으로 이루어진 요소로 구성됨

  - 중복된 키는 덮어써짐

- 요소 개수 확인

  - Map.prototype.size 프로퍼티

  - getter 함수만 존재하는 접근자 프로퍼티

- 요소 추가

  - Map.prototype.set 메서드

  - 새로운 요소 추가된 Map 객체 반환 => method chaining 가능 (메서드 연속 호출)

  - NaN과 NaN, 0과 -0은 같다고 평가하여 중복 추가 허용 X

  - 객체도 키로 사용 가능 (일반 객체는 문자열, 심벌 값만 키로 사용 가능했음)

- 요소 취득

  - Map.prototype.get 메서드

  - Map 객체에서 인수로 전달한 키를 갖는 값 반환

- 요소 존재 여부 확인

  - Map.prototype.has 메서드

  - 특정 요소의 존재 여부를 나타내는 불리언 값 반환

- 요소 삭제

  - Map.prototype.delete 메서드

  - 삭제 성공 여부를 나타내는 불리언 값 반환 => method chaining 불가

- 요소 일괄 삭제

  - Map.prototype.clear 메서드

  - 언제나 undefined 반환

- 요소 순회

  - Map.prototype.forEach 메서드 사용

    - 첫 번째 인수: 현재 순회 중인 요소값

    - 두 번째 인수: 현재 순회 중인 요소키

    - 세 번째 인수: 현재 순회 중인 Map 객체 자체

  - Map 객체는 이터러블 => for ... of 문 순회 가능, 스프레드/디스트럭처링 할당 대상

  - Map 객체는 이터러블이면서 동시에 이터레이터인 객체를 반환하는 메서드 제공

    - Map.prototype.keys

    - Map.prototype.values

    - Map.prototype.entries
