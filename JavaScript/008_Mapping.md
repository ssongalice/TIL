# 객체 Mappping

## 객체(Object)의 특징

- 객체엔 Array method인 map, filter를 사용할 수 없다.

* 일반 객체엔 다음과 같은 메서드를 사용할 수 있다.

## Object.keys, values, entries

- Object.keys(obj) - 키가 담긴 배열 반환
- Object.values(obj) - 값이 담긴 배열 반환
- Object.entries(obj) - [key, value]가 담긴 배열 반환
- 문법에 차이가 있는 이유: 자바스크립트에선 복잡한 자료구조 전체가 객체에 기반합니다. 때문에 객체 data에 자체적으로 메서드 data.values()를 구현해 사용하는 경우가 있을 수 있음. 이렇게 커스텀 메서드를 구현한 상태라도 Object.values(data)같이 다른 형태로 메서드를 호출할 수 있으면 커스텀 메서드와 내장 메서드 둘 다 사용 가능.

```javascript
let user = {
  name: "John",
  age: 30,
};

Object.keys(user); // ["name", "age"]
Object.values(user); // ["John", 30]
Object.entries(user); // [(["name", "John"], ["age", 30])];
```

### 객체 변환하기

- 객체엔 map, filter 같은 배열 전용 메서드를 사용할 수 없다. 하지만 Object.entries와 Object.fromEntries를 순차적으로 적용하면 사용 가능.

1. Object.entries(obj)를 사용해 객체의 키-값을 쌍으로 가지는 요소 반환
2. 1에서 만든 배열에 map 등 배열 전용 메서드 적용
3. 2에서 만든 배열에 Object.fromEntries(array)를 적용해 배열을 다시 객체로 돌림.

```javascript
let prices = {
      banana: 1,
      orange: 2,
      meat: 4
};

let doublePrices = Object.fromEntries(
      Object.entries(prices).map([key, value] => [key, value*2])
);

// output
/*
doublePrices = {
      banana: 2,
      orange: 4,
      meat: 8
}
*/

```

---

- 참고: https://ko.javascript.info/keys-values-entries
