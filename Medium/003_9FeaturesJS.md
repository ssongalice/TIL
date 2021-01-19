# 모든 js 개발자가 알아야 하는 9가지 ES6 요소들

## 1. Rest Parameter

- spread 연산자를 함수의 파라미터로 사용한 형태
- rest 파라미터를 사용하면 함수의 인자로 오는 값을 배열로 전달받을 수 있다.
- 마지막 파라미터만 Rest 파라미터가 될 수 있다.

```javascript
function averageOf(...numbers) {
  let sum = 0;

  for (let number of numbers) {
    sum += number;
  }

  return sum / numbers.length;
}

let average = averageOf(5, 6, 2, 1); // 3.5
```

## 2. Promise

- 자바스크립트 비동기 처리에 사용하는 객체
- 콜백지옥: 비동기 프로그래밍시 발생. 함수의 매개변수로 넘어오는 함수가 반복돼 코드의 들여쓰기가 너무 깊어지는 현상
- 여러개의 프로미스 함수를 연결해 사용할 수 있다.

```javascript
/* before */
processStep1(id, function (data1) {
  processStep2(data1, function (data2) {
    processStep3(data2, function (data3) {
      processStep4(data3, function (data4) {
        finish(data4);
      });
    });
  });
});

/* after */
processStep1(id)
  .then((data1) => processStep2(data1))
  .then((data2) => processStep3(data2))
  .then((data3) => processStep4(data3))
  .then((data4) => finish(data4))
  .catch(errorHandler);
```

## 3. Arrow Function

```javascript
/* before */
function sayHello(name) {
  console.log(‘Hello ‘ + name);
}


/* after */
const sayHello = name => console.log('Hello' + name);
```

## 4. Template Literals

- 내장된 표현식을 허용하는 문자열 리터럴. 백틱을 사용한다
- $ {expression} 형식으로 표현식을 추가할 수 있다.

```javascript
const bookTitle = ‘JavaScript’;
console.log(`This ${bookTitle} book is great.
I learned so much from it.`);
// This JavaScript book is great
// I learned so much from it.
```

## 5. const & let

## 6. Default Parameter

- 함수에서 값이 없거나 undefined가 전달될 경우 이름이 붙은 변수를 기본값으로 초기화할 수 있음.
- js 함수의 매개변수는 Undefined가 기본값.
- 여러개의 매개변수가 있을 때, 앞쪽 매개변수는 뒤쪽 매개변수를 정의할 때 사용할 수 있다.

```javascript
/* before */
const welcome = name => {
  name = name || ‘Amy’;
  console.log(‘Welcome ‘ + name);
};
welcome(); // Welcome Amy


/* after */
const welcome = (name = ‘Amy’) => console.log(‘Welcome ‘ + name);
welcome(); // Welcome Amy
```

## 7. Module

- js 함수를 분리해 export/import로 함수의 기능을 외부 파일에서 공유

```javascript
export const moduleName = ‘Calculation’;
export function sum(a, b) {
  return a + b;
}
-----
import { moduleName, sum } from ‘./calculation.js’;
console.log(moduleName); // Calculation
let a = sum(5, 8); // 13
```

## 8. Class

- 자바스크립트 객체를 선언하기 위한 생성자 함수

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
  introduce() {
    console.log(`My name is ${this.name}`);
  }
}
let person = new Person(‘Amy’);
person.introduce(); // My name is Amy
```

## 9. Destructuring

- 구조 분해 할당. 배열이나 객체의 속성을 해체해 그 값을 개별 변수에 담을 수 있게 함.
- 값을 할당할 때 좌변에서 설정해 원래 변수에서 어떤 값을 가져올 지 정의함.

```javascript
let book = {
  title: ‘JavaScript’,
  price: 13,
  author: ‘Amy’
};
let { title, author } = book;
console.log(title, author); // JavaScript Amy
----
var x = [1, 2, 3, 4, 5];
var [y, z] = x;
console.log(y); // 1
console.log(z); // 2
```

---

원문
https://medium.com/javascript-in-plain-english/9-es6-features-every-javascript-developer-should-know-b1f2915e7add

참고

- Rest parameters
  https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/rest_parameters
  https://jeong-pro.tistory.com/117
- Promise
  https://joshua1988.github.io/web-development/javascript/promise-for-beginners/
- Template Literals
  https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals
- Module
  https://ko.javascript.info/modules-intro
- Class
  https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes
  https://www.w3schools.com/js/js_classes.asp
- Destructing
  https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment
