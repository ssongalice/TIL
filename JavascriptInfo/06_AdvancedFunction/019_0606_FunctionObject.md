# 객체로서의 함수와 기명함수 표현식

- 자바스크립트 함수의 자료형은 객체.
- 함수를 호출할 수 있을뿐만 아니라 객체처럼 함수에 프로퍼티를 추가/제거하거나 참조를 통해 전달할 수 있다.

## 'name' 프로퍼티

- 'name' 프로퍼티를 사용하면 함수 이름을 가져올 수 있다.
- 익명함수라도 이름이 자동으로 할당됨.
- contextual name : 이름이 없는 함수의 이름을 지정할 땐 컨텍스트에서 이름을 가져옴

```javascript
function sayHi() {
  alert("Hi!");
}

alert(sayHi.name);
```

## length 프로퍼티

- 내장 프로퍼티 length는 함수 매개변수의 개수를 반환. 나머지 매개변수는 포함하지 않는다.

```javascript
function f1(a) {}
function f2(a,b) {}
function many(a,b, ...more) {}

alert(f1.length); // 1
alert(f2.length); // 2
alert(many.length)l // 2
```

- length 프로퍼티는 다른 함수 안에서 동작하는 함수의 타입을 검사할때도 사용 .
- 인수의 종류에 따라 인수를 다르게 처리하는 방식: 다형성

```javascript
function ask(question, ...handlers) {
  // 질문에 쓰일 question과 질문에 대한 답에 따라 호출할 임의의 함수 handler
  // 인수가 없는 함수로 사용자가 OK 했을 때만 호출됨
  // 인수가 있는 함수로 사용자가 무엇을 클릭하든 호출됨
  const isYes = confirm(question);

  for (let handler of handlers) {
    if (handler.length == 0) {
      if (isYes) handler();
    } else {
      handler(isYes);
    }
  }
}
```

## 커스텀 프로퍼티

- 함수에 자체적으로 만든 프로퍼티도 추가할 수 있다. 프로퍼티는 변수가 아니다.

```javascript
function sayHi() {
  alert("hi!");
  sayHi.counter++;
}
sayHi.counter = 0;
sayHi();
sayHi();
alert(sayHi.counter); // 2
```

- 클로저와 함수 프로퍼티의 차이
  - 클로저는 외부 코드에서 변수에 접근할 수 없고 함수 프로퍼티는 외부에서 접근할 수 있음.

## 기명함수 표현식

- 이름이 있는 함수표현식을 나타내는 용어
- 이름을 붙이면 이름을 사용해 함수 표현식 내부에서 자기 자신을 참조할 수 있다. 기명함수 표현식 바깥에서는 그 이름을 사용할 수 없다.

```javascript
const sayHi = function func(who) {
  if (who) {
    alert(`Hello, ${who}`);
  } else {
    func("Guest"); // func 이름을 호출해 자기 자신을 호출
  }
};
```

- 중첩호출에서 이름이 아닌 변수 이름을 사용하면 외부 코드에 의해 변경될 수 있기 때문에 오류가 발생한다

```javascript
let sayHi = function (who) {
  if (who) {
    alert(`Hello, ${who}`);
  } else {
    sayHi("Guest"); // TypeError: sayHi is not a function
  }
};

let welcome = sayHi;
sayHi = null;

welcome(); // 중첩 sayHi 호출은 더 이상 불가능합니다!
```

## 과제

- 숫자 설정과 감소가 가능한 counter 만들기

```javascript
function makeCounter() {
  let count = 0;
  function counter() {
    return count++;
  }

  counter.set = (value) => (count = value);
  counter.decrease = () => count--;
  return counter;
}
```
