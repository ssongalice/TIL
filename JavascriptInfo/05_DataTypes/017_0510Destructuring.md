# 구조분해할당

## 배열 분해하기

- 예제

```javascript
let arr = ["Bora", "Lee"];
let [firstName, surname] = arr;
alert(firstName); // Bora
alert(surname); // Lee
```

- 할당 연산자 우측엔 모든 이터러블이 올 수 있다.

```javascript
let [a, b, c] = "abc"; // ["a","b","c"];
let [one, two, three] = new Set([1, 2, 3]);
```

- 할당 연산자 좌측엔 뭐든지 올 수 있다.

```javascript
let user = {};
[user.name, user.surname] = "Bora Lee".split(" ");

alert(user.name); // Bora
```

- ...로 나머지 요소 가져오기

```javascript
let [name1, name2, ...rest] = [
  "Julius",
  "Caesar",
  "Consul",
  "of the Roman Republic",
];

alert(name1); // Julius
alert(name2); // Caesar

// `rest`는 배열입니다.
alert(rest[0]); // Consul
alert(rest[1]); // of the Roman Republic
alert(rest.length); // 2
```

- 할당할 값이 없으면 Undefined로 취급.

## 객체 분해하기

```javascript
let { var1, var2 } = {var1: ..., var2: ...}
```

- 할당 연산자 우측엔 분해하고자 하는 객체를, 좌측엔 상응하는 객체 프로퍼티의 패턴을 넣는다.

```javascript
let options = {
  title: "Menu",
  width: 100,
  height: 200,
};

let { title, width, height } = options;

alert(title); // Menu
alert(width); // 100
alert(height); // 200
```

- 객체 프로퍼티를 프로퍼티 키와 다른 이름을 가진 변수에 저장하기. 좌측 패턴에 : 을 사용하면 가능.

```javascript
let options = {
  title: "Menu",
  width: 100,
  height: 200,
};

// { 객체 프로퍼티: 목표 변수 }
let { width: w, height: h, title } = options;

// width -> w
// height -> h
// title -> title

alert(title); // Menu
alert(w); // 100
alert(h); // 200
```

- 나머지 패턴

```javascript
let options = {
  title: "Menu",
  height: 200,
  width: 100,
};

// title = 이름이 title인 프로퍼티
// rest = 나머지 프로퍼티들
let { title, ...rest } = options;

// title엔 "Menu", rest엔 {height: 200, width: 100}이 할당됩니다.
alert(rest.height); // 200
alert(rest.width); // 100
```

## 구조분해할당

```javascript
let user = {
  name: "John",
  years: 30,
};

let { name, years: age, isAdmin = false } = user;
```

## 똑똑한 함수 매개변수

```javascript
// 함수에 전달할 객체
let options = {
  title: "My menu",
  items: ["Item1", "Item2"],
};

// 똑똑한 함수는 전달받은 객체를 분해해 변수에 즉시 할당함
function showMenu({
  title = "Untitled",
  width = 200,
  height = 100,
  items = [],
}) {
  // title, items – 객체 options에서 가져옴
  // width, height – 기본값
  alert(`${title} ${width} ${height}`); // My Menu 200 100
  alert(items); // Item1, Item2
}

showMenu(options);
```
