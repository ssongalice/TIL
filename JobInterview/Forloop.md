# for in, for of, forEach문의 차이

- [ for in ]
  - 열거 가능한 속성(non-Symbol 속성)에 대해서만 사용
    - Symbol로 선언된 속성은 무시
  - for...in은 특정 순서에 따라 인덱스를 반환하는 것을 보장할 수 없음. 반복 순서가 구현에 따라 다르기 때문.
  - for...in은 정수가 아닌 이름을 가진 속성, 상속된 모든 열거 가능한 속성들을 반환. 객체의 속성을 확인할 수 있기 때문에 디버깅을 위해 사용할 수 있음. → 일반 Object의 key를 순회하기 위한 문법
  - for...in은 iterable object면 모두 반복할 수 있는 대상이 됨. prototype chain에 따라 상속받은 값도 반복에 포함.
  - [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...in](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...in)
- [ for of ]

  - 이터러블 객체 반복일 때 사용.
  - for...of는 [Symbol.iterator] 속성이 있는 모든 컬렉션 요소에 대해 반복함
  - for...of는 prototype chain에 따라 상속받은 값은 반복에 포함하지 않음. [(링크)](https://victorydntmd.tistory.com/89)

  ```jsx
  Object.prototype.objCustom = function () {};
  Array.prototype.arrCustom = function () {};

  let iterable = [3, 5, 7];
  iterable.foo = "hello";

  for (let i in iterable) {
    console.log(i); // logs 0, 1, 2, "foo", "arrCustom", "objCustom"
  }

  for (let i of iterable) {
    console.log(i); // logs 3, 5, 7
  }
  ```

  [https://n-log.tistory.com/39](https://n-log.tistory.com/39)

- [ forEach ]

  - 주어진 함수를 배열 요소 각각에 대해 실행. 배열만 실행할 수 있음.
  - 주어진 콜백을 주어진 배열에 있는 각 요소에 대해 오름차순으로 한번씩 실행.
  - forEach는 예외를 던지지 않고는 중간에 종료할 수 없음. 중간종료가 필요할 경우 for, for of, for in이 더 적합할 수 있음.

  ```jsx
  const items = ["item1", "item2", "item3"];
  const copy = [];

  // for loop
  for (let i = 0; i < items.length; i++) {
    copy.push(items[i]);
  }

  // forEach
  items.forEach(function (item) {
    copy.push(item);
  });
  ```
