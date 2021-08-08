# 구조분해할당 (Destructuring assignment)

- 구조분해할당이라는 명칭은 어떤 것을 복사 후에 변수로 분해해준다는 의미로 붙여짐. 이 과정에서 분해 대상은 수정 또는 파괴되지 않는다.

## 배열 분해하기

```js
const arr = ["Songyi", "Lim"];

const [firstName, surName] = arr;
console.log(firstName); // Songyi
console.log(surName); // Lim
```

- 쉼표를 사용해 필요하지 않은 요소를 버릴 수 있다.

```js
const [firstName, , title] = [
  "Julius",
  "Caesar",
  "Consul",
  "of the Roman Republic",
];
console.log(title); // Consul
```

- .entries()로 반복하기

```js
let user = {
  name: "John",
  age: 30,
};

for (let [key, value] of Object.entries(user)) {
  console.log(`${key}: ${value}`);
}
```

- 두 변수에 저장된 값을 교환할 때 구조분해할당을 사용할 수 있다.

```js
const guest = "Jane";
const admin = "Pete";

// 변수 guest엔 admin, admin엔 guest가 저장되도록 변경
[guest, admin] = [admin, guest];
console.log(guest, admin); // Pete, Jane
```

- ...로 나머지 요소 가져오기

```js
const [name1, name2, ...rest] = [
  "Julius",
  "Caesar",
  "Consul",
  "of the Roman Republic",
];
console.log(name1); // Julius
console.log(name2); // Caesar
console.log(rest); // ["Consul", "of the Roman Republic"]
```

- 기본값

  - 할당하고자 하는 변수의 개수가 분해하고자 하는 배열의 길이보다 크더라도 에러가 발생하지 않음. 할당할 값이 없으면 undefined 취급

  ```js
  const [firstName, surName] = [];
  console.log(firstName); // undefined;
  console.log(surName); // undefined
  ```

  - =를 이용하면 할당할 값이 없을 때 기본값을 설정해줄 수 있음.

  ```js
  // 기본값
  let [name = "Guest", surname = "Anonymous"] = ["Julius"];
  alert(name); // Julius (배열에서 받아온 값)
  alert(surname); // Anonymous (기본값)
  ```

## 객체 분해 할당

- 할당 연산자 우측엔 분해하고자 하는 객체를, 좌측엔 상응하는 객체의 패턴을 넣는다.

```js
const options = {
  title: "menu",
  width: 100,
  height: 200,
};

const { title, width, height } = options;
console.log(title); // menu
```

- 할당 연산자 좌측엔 좀 더 복잡한 패턴이 올 수 있다. 분해하려는 객체의 프로퍼티와 변수의 연결을 원하는대로 조정할 수 있다.

```js
const options = {
  title: "menu",
  width: 100,
  height: 200,
};

// { 객체 프로퍼티 : 목표 변수 }
// width -> w, height -> h
const { width: w, height: h, title } = options;
console.log(w); // 100
```

- 배열 혹은 함수 매개변수에서 했던 것처럼 객체에도 표현식이나 함수 호출을 기본값으로 할당할 수 있음.

```js
const options = {
  title: "Menu",
};

// 아래 예시를 실행하면 width값만 물어보고 title은 물어보지 않는다
const { width = prompt("Width"), title = prompt("title") } = options;
```

- 나머지 패턴 `...`
- 분해하려는 객체의 프로퍼티 개수가 할당하려는 변수의 개수보다 많다면 나머지 패턴을 사용해 나머지 프로퍼티를 할당하는 게 가능.

```js
const options = {
  title: "Menu",
  height: 200,
  width: 100,
};

// title = 이름이 title인 프로퍼티
// rest = 나머지 프로퍼티들
const { title, ...rest } = options;
```

## 중첩구조분해

- 객체나 배열이 다른 객체나 배열을 포함하는 경우, 좀 더 복잡한 패턴을 사용해 중첩 배열이나 객체의 정보를 추출할 수 있다.

```js
const options = {
  size: {
    width: 100,
    height: 200,
  },
  items: ["Cake", "Donut"],
  extra: true,
};

// 코드를 여러 줄에 걸쳐 작성해 의도하는 바를 명확히 드러냄
const {
  size: {
    // size는 여기,
    width,
    height,
  },
  items: [item1, item2], // items는 여기에 할당함
  title = "Menu", // 분해하려는 객체에 title 프로퍼티가 없으므로 기본값을 사용함
} = options;

alert(title); // Menu
alert(width); // 100
alert(height); // 200
alert(item1); // Cake
alert(item2); // Donut
```
