# 22가지 코드 스니펫

## 1. 삼항 조건 연산자 (The Ternary Operator)

```javascript
let someThingTrue = true;
if (someThingTrue) {
  handleTrue();
} else {
  handleFalse();
}

/// after
someThingTrue ? handleTrue() : handleFalse();
```

## 2. Short-Circuit Evaluation

```javascript
const defaultValue = "SomeDefaultValue";
const someValueNotSureOfItsExistance = null;

const expectingSomeValue = someValueNotSureOfItsEixstance || defaultValue;

console.log(expectingSomeValue);
// output: SomeDefaultValue
```

참고]

- 자바스크립트의 논리 연산은 왼쪽에서 오른쪽으로 이뤄짐.
- 앞의 비교에서 명확한 결과가 예측돼 뒤에서 나오는 비교를 더이상 할 필요가 없을 때 비교 중지 & 답 도출
- (거짓표현식) && expr -> 거짓표현식.
- (참표현식) || expr -> 참표현식.

`||` 와 `&&` 연산자

- 논리 AND ` expr1 && expr2` : expr1을 true로 변환할 수 있는 경우 expr2 반환. 그렇지 않으면 expr1 반환.
- 논리 OR `expr1 || expr2` : exp1을 true로 반환할 수 있는 경우 expr1 반환. 그렇지 않으면 expr2 반환.
- 논리 NOT `!expr` : 연산자를 true로 반환할 수 있으면 false 반환. 그렇지 않으면 true 반환.
- 연산자 `&&`는 `||` 이전에 실행된다.

- 거짓으로 반환할 수 있는 표현식

```javascript
null, NaN, 0, "", "", ``, undefined;
```

## 3. 기본 변수 설정하기

```javascript
// Before
function createMicrobrewery(name) {
  const breweryName = name || "Hipster Brew Co.";
}

// After
function createMicrobrewery(name = "Hipster Brew Co.") {
  //... using default arguments
}
```

## 4. If문

```javascript
const someValue = true;
if (someValue) {
  console.log("Its exist");
}
```

## 5. For문

```javascript
for (let i = 0; i < 1e2; i++) {
  // i <100 대신
}
```

## 6. 객체 키값으로 반복문

```javascript
const someValues = [1, 2, 4];
for (let val in someValues) {
  console.log(val);
}

const obj = {
  key1: "value1",
  key2: "value2",
  key3: "value3",
};

for (let key in obj) {
  console.log(key);
}
// output: key1, key2, key3
```

## 7. 값 객체로 맵핑

```javascript
const x = "x";
const y = "y";
const obj = { x, y };

console.log(obj);
// output: {x: "x", y:"y"}
```

## 8. Object.entries()

```javascript
const credits = {
  producer: "HBO",
  name: "Game of thrones",
  rating: 9,
};

const arr = Object.entries(credits);
console.log(arr);

/* output 
[
	['producer', 'HBO'],
    ['name', 'Game of thrones'],
    ['rating', 9]
] */
```

## 9. Object.values()

```javascript
const credits = {
  producer: "HBO",
  name: "Game of thrones",
  rating: 9,
};

const arr = Object.values(credits);
console.log(arr);

/* output 
['HBO', 'Game of thrones', 9] */
```

## 10. Template Literals

```javascript
var name = "John",
  age = 20;
var someStringConcatenateSomeVariable = `My Name is ${name} and my age is ${age}`;
console.log(someStringConcatenateSomeVariable);

// output: My Name is John and my age is 20
```

## 11. 구조분해할당(Destructuring Assignments)

- 객체와 배열의 값 일부를 변수로 가져올 수 있는 문법
- 값을 복사해 가져오기 때문에 분해 대상은 수정되지 않는다.

```javascript
import { objervable, action, runInAction } from "mobx";
```

## 12. 문자열 줄바꿈

```javascript
const multiLineString = `some string\n
with multi-line of\n
characters\n`;

console.log(multiLineString);
/* output
some string

with multi-line of

characters
*/
```

## 13. 스프레드 연산자

```javascript
const odd = [1,3,5];
const nums = [2,4,6 ...odd];
console.log(nums);
// output: 2,4,6,1,3,5
```

## 14. Array.find 단축작성

```javascript
const pets = [
  { type: "Dog", name: "Max" },
  { type: "Cat", name: "Karl" },
  { type: "Dog", name: "Tommy" },
];

pet = pets.find((pet) => pet.type === "Dog" && pet.name === "Tommy");
console.log(pet);

// output: {type: 'Dog', name: 'Tommy'}
```

## 15. 기본 함수 값 설정

```javascript
// Before
function area(h, w) {
  if (!h) {
    h = 1;
  }
  if (!w) {
    w = 1;
  }
  return h * w;
}

// After
function area(h = 1, w = 1) {
  return h * w;
}
```

## 16. 화살표 함수 단축

```javascript
// Before
const sayHello = (name) => {
  return "Hello " + name;
};

// After
const sayHello = (name) => "Hello " + name;
```

## 17. Implicit Return

- 화살표 함수를 사용할 때 단일 표현식만 포함된 경우 전통적으로 함수를 감싸는 {}를 생략해 값을 반환할 수 있다.

```javascript
// Before
const someFuncThatReturnSomeValue = (value) => {
  return value + value;
};

// After
const someFuncThatReturnSomeValue = (value) => value + value;
```

```javascript
const func = (x) => x * x;
// concise body syntax, implied "return"

const funcB = (x, y) => {
  return x + y;
};
// with block body, explicit "return" needed
```

## 18. 반드시 파라미터 값을 가져야 할 때

```javascript
// Before
function mustHaveParamMethod(param) {
  if (param === undefined) {
    throw new Error("Hey You must Put some param!");
  }
  return param;
}

// After
const mustHaveCheck = () => {
  throw new Error("Missing Parameter");
};

const methodShouldHaveParam = (param = mustHaveCheck()) => {
  return param;
};
```

## 19. charAt() 단축

```javascript
// Before
"SampleString".charAt(0);
// After
"SampleString"[0];
```

## 20. 조건부 함수 호출

```javascript
function fn1() {
  console.log("I'm Function 1");
}
function fn2() {
  console.log("I'm Function 2");
}

// Long Version
const checkValue = 3;
if (checkValue === 3) {
  fn1();
} else {
  fn2();
}

// Short Version
(checkValue === 3 ? fn1 : fn2)();
```

## 21. Math.Floor 단축

```javascript
const val = "123";
console.log(Math.floor(val)); // Long
console.log(~~val); // Short
```

## 22. Math.pow 단축

```javascript
Math.pow(2, 3); // 8
2 ** 3; // 8
```

## 23. 문자열 숫자 변환

```javascript
const num1 = parseInt("100");
// Short
console.log(+"100");
console.log(+"100.2");
```

## 24. && 연산자 조건식으로 사용

```javascript
const value = 1;
if (value === 1) {
  console.log("Value is One");
}
// Short
value && console.log("Value is One");
```

## 25. toString 단축

```javascript
const someNumber = "123";
console.log(someNumber.toString());
console.log(`${someNumber}`);
```

## 26. 키-값 바꾸기

```javascript
const UserRole = {
  ADMIN: "Admin",
  GENERAL_USER: "GeneralUser",
  SUPER_ADMIN: "SuperAdmin",
};
getRoute(userRole){
 const appRoute = {
    [UserRole.ADMIN]: "/admin",
    [UserRole.GENERAL_USER]: "/user",
    [UserRole.SUPER_ADMIN]: "/superadmin"
};
  return appRoute[userRole] ?? "";
}
getRoute("Admin") // return "/admin"
getRoute("Anything") // return "" or default case

```

## 27. 객체 리터럴 함수 바꾸기

```javascript
// Before
var fruit = "banana";
var drink;
switch (fruit) {
  case "banana":
    drink = "banana juice";
    break;
  case "papaya":
    drink = "papaya juice";
    break;
  default:
    drink = "Unknown juice!";
}
console.log(drink); // 'banana juice'

// After
function getDrink(type) {
  const drinks = {
    banana: "banana juice",
    papaya: "papaya juice",
    default: "Just Water!",
  };

  return "The drink I chose" + (drinks[type] || drinks["default"]);
}

const drink = getDrink("papaya");
console.log(drink);
// output: The drink I chose was papaya juice
```

---

원문:
https://medium.com/javascript-in-plain-english/some-js-shortcuts-82bc2f56146e

참고: https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/%EB%85%BC%EB%A6%AC_%EC%97%B0%EC%82%B0%EC%9E%90(Logical_Operators)
https://ko.javascript.info/destructuring-assignment
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions
