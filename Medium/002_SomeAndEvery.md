# some, every의 차이

- some과 every는 모두 고차함수(Higher Order Function).

## some()

- some은 주어진 **callback함수가 true을 반환하는 요소를 찾을 때까지** 배열에 있는 각 요소에 대해 한 번씩 callback 함수를 실행.
- 적어도 한가지 요소가 조건을 만족하면 true를 return.
- 빈 배열에서 호출하면 false 반환

```javascript
let marks = [4, 5, 7, 9, 10, 3];

const lessThanFive = marks.some((element) => element < 5);
// true

const lessThanThree = marks.some((element) => element < 3);
// false
```

## every()

- every는 **주어진 callback함수가 false을 반환하는 요소를 찾을 때까지** 배열에 있는 각 요소에 대해 한 번씩 callback 함수를 실행합니다.
- 해당하는 요소를 발견한 경우 every는 즉시 false를 반환합니다.
- 빈 배열에서 호출하면 true 반환

```javascript
let number = [1, 3, 5];

let biggerThanZero = number.every((element) => element > 0);
// true

let biggerThanTwo = number.every((element) => element > 2);
// false
```

---

원문
https://medium.com/javascript-in-plain-english/the-methods-some-and-every-in-javascript-8b303a36eaae

참고
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/some
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/every
