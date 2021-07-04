# js에서의 This

- 자바스크립트의 경우 함수 호출방식에 의해 함수를 호출할 때 this에 바인딩할 객체가 무엇인지 동적으로 결정됨.

### 1. 함수호출

- 기본적으로 this는 전역객체(Global Object)에 반영된다. 내부함수의 경우, 메소드의 내부함수인 경우, 콜백함수의 경우도 this는 전역객체에 바인딩.

```jsx
var value = 1;

var obj = {
  value: 100,
  foo: function () {
    setTimeout(function () {
      console.log("callback's this: ", this); // window
      console.log("callback's this.value: ", this.value); // 1
    }, 100);
  },
};

obj.foo();
```

### 2. 메소드 호출

- 함수가 객체의 프로퍼티 값이면 메소드로서 호출됨. 이때 메소드의 this는 해당 메소드를 호출한 객체에 바인딩

```jsx
var obj1 = {
  name: "Lee",
  sayName: function () {
    console.log(this.name);
  },
};

var obj2 = {
  name: "Kim",
};

obj2.sayName = obj1.sayName;

obj1.sayName();
obj2.sayName();
```

- 프로토타입 객체 메소드 내부에서 사용된 this도 해당 메소드를 호출한 객체에 바인딩

```jsx
function Person(name) {
  this.name = name;
}

Person.prototype.getName = function () {
  return this.name;
};

var me = new Person("Lee");
console.log(me.getName());

Person.prototype.name = "Kim";
console.log(Person.prototype.getName());
```

### 3. 생성자함수 호출

- 일반적으로 생성자함수는 첫문자를 대문자로 기술하여 혼란을 방지함.

### 4. apply/ call/ bind

- this를 명시적으로 바인딩하는 방법.
- apply 메소드를 호출하는 주체는 함수, apply 메소드는 this를 특정 객체에 바인딩할 뿐 본질적인 기능은 함수호출

```jsx
var Person = function (name) {
  this.name = name;
};

var foo = {};

// apply 메소드는 생성자함수 Person을 호출한다. 이때 this에 객체 foo를 바인딩한다.
Person.apply(foo, ["name"]);

console.log(foo); // { name: 'name' }
```

- bind

  - 함수에 인자로 전달한 this가 바인딩된 새로운 함수를 리턴.

### 화살표함수의 this

- 화살표 함수의 this는 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정됨. 화살표 함수의 this는 언제나 상위 스코프의 this.
- 화살표 함수는 call, apply, bind 메소드를 활용해 this를 변경할 수 없음

```jsx
// 화살표 함수를 사용하지 않은 경우
var prefix = "isGlobal";

function Prefixer(prefix) {
  this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function (arr) {
  // this는 window
  return arr.map(function (x) {
    return `${this.prefix}  ${x}`;
  });
};

const pre = new Prefixer("Hi");
console.log(pre.prefixArray(["Lee", "Kim"]));
//["isGlobal  Lee", "isGlobal  Kim"]

// 화살표 함수를 사용한 경우
function Prefixer(prefix) {
  this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function (arr) {
  // this는 상위 스코프인 prefixArray 메소드 내의 this를 가리킨다.
  return arr.map((x) => `${this.prefix}  ${x}`);
};

const pre = new Prefixer("Hi");
console.log(pre.prefixArray(["Lee", "Kim"]));
// ["Hi  Lee", "Hi  Kim"]

// 화살표 함수를 메소드에 쓰면 안되는 경우
// Bad
const person = {
  name: "Lee",
  sayHi: () => console.log(`Hi ${this.name}`), // window에 붙음
};

person.sayHi(); // Hi undefined

const person = {
  name: "Lee",
  sayHi() {
    // === sayHi: function() {
    console.log(`Hi ${this.name}`);
  },
};

person.sayHi(); // Hi Lee
```

- 화살표 함수를 사용하면 안되는 경우
  - 메소드 정의하기
  - 프로토타입 할당
  - addEventListener 함수의 콜백 내에서 this 사용하는 경우
  - [https://poiemaweb.com/es6-arrow-function](https://poiemaweb.com/es6-arrow-function)
