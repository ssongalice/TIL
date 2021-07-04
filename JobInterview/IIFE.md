# 즉시 실행 함수

- 즉시실행함수, Immediately-Invoked Function Expression
- 정의되자마자 즉시 실행되는 함수

  - 전역스코프에 불필요한 변수를 추가해 오염시키는 것을 방지할 수 있음.
  - function( ) { } 과 같이 작성되면 자바스크립트 코드 파서는 함수 선언문으로 인식. 값을 남기기 위해서는 ()로 묶어줘 "함수 표현식"이라는 것을 명시적으로 나타내야 함.
    - 문과 식의 차이 → [https://poiemaweb.com/js-syntax-basics](https://poiemaweb.com/js-syntax-basics)
  - IIFE 내부에서 정의된 변수는 외부에서 접근할 수 없다
  - IIFE를 변수에 할당하면 함수 자체는 저장되지 않고 함수가 실행된 결과만 저장된다
  - IIFE의 목적
    - 외부에서 접근할 수 없는 자체 Scope를 형성.
    - 상위 scope에 접근하면서 동시에 내부 변수를 외부로부터 보호해 privacy를 유지할 수 있음.

  ```jsx
  (function () {
    statements;
  })();
  // 화살표 함수를 이용
  (() => {
    statements;
  })();

  // 예시
  const result = (function () {
    const name = "Barry";
    return name;
  })();
  result; // "Barry"
  ```

---

참고

- [https://developer.mozilla.org/ko/docs/Glossary/IIFE](https://developer.mozilla.org/ko/docs/Glossary/IIFE)
- [https://vvkchandra.medium.com/essential-javascript-mastering-immediately-invoked-function-expressions-67791338ddc6](https://vvkchandra.medium.com/essential-javascript-mastering-immediately-invoked-function-expressions-67791338ddc6)
- [https://velog.io/@doondoony/javascript-iife](https://velog.io/@doondoony/javascript-iife)
