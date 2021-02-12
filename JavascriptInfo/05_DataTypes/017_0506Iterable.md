# iterable 객체

- 반복 가능한(iterable) 객체는 배열을 일반화한 객체.

## Symbol.iterator

- 예제

```javascript
let range = {
  from: 1,
  to: 5,
};
// 1. for..of 최초 호출 시 Symbol.iterator가 호출
range[Symbol.iterator] = function () {
  // Symbol.iterator는 이터레이터 객체를 반환
  // 2. for..of는 반환된 이터레이터 객체만을 대상으로 동작.
  return {
    current: this.from,
    last: this.to,
    // 3. for..of 반복문에 의해 반복마다 next()가 호출됨
    next() {
      // 4. next()는 값을 객체 형태로 반환해야 함.
      if (this.current <= this.last) {
        return { done: false, value: this.current++ };
      } else {
        return { done: true };
      }
    },
  };
};

for (let num of range) {
  alert(num); // 1,2,3,4,5
}
```

- 이터러블 객체의 핵심은 관심사의 분리
- 예제에서 range엔 메서드 next가 없음. 대신 range[Symbol.iterator]를 호출해서 만든 이터레이터 객체와 이 객체의 메서드 next()에서 반복에 사용될 값을 만듦

## 문자열은 이터러블

- 배열과 문자열은 가장 광범위하게 쓰이는 내장 이터러블

```javascript
for (let char of "test") {
  alert(char); //t,e,s,t
}
```

## 이터러블과 유사배열

- 이터러블은 메서드 Symbol.iterator가 구현된 객체
- 유사배열(array-like)은 인덱스와 length 프로퍼티가 있어서 배열처럼 보이는 객체
- 이터러블과 유사배열은 대개 배열이 아니기 때문에 push, pop 등의 메서드를 지원하지 않음

```javascript
let arrayLike = {
  0: "Hello",
  1: "World",
  length: 2,
};
```

## Array.from

- Array.from은 이터러블이나 유사배열을 받아 진짜 배열을 만들어줌.

```javascript
let arrayLike = {
  0: "Hello",
  1: "World",
  length: 2,
};

let arr = Array.from(arrayLike);
```

- Array.from엔 매핑 함수를 선택적으로 넘겨줄 수 있음.

```javascript
Array.from(obj[, mapFn, thisArg])
```

- mapFn을 두 번째 인수로 넘겨주면 새로운 배열에 obj의 요소를 추가하기 전에 각 요소를 대상으로 mapFn을 적용 가능.

```javascript
let arr = Array.from(range, (num) => num * num);
alert(arr); // 1,4,9,16,25
```
