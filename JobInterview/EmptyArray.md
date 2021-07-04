# 배열 초기화하는 여러 방법

- 1번
  - A를 새로운 빈 배열로 다시 설정.
  - 다른 곳에서 원래 배열 A에 대한 참조가 없는 경우 가능한 방법. 다른 변수나 속성에서 해당 배열을 참조한 경우 원래 배열이 변경되지 않은 상태를 유지하므로 방법에 주의해야 함.

```jsx
A = [];
// 원본을 참조하는 배열이 있을 경우 발생하는 문제
let arr1 = ["a", "b", "c", "d", "e", "f"];
let arr2 = arr1;
arr1 = [];
console.log(arr2); // ['a','b','c','d','e','f']
```

- 2번
  - 배열의 길이를 0으로 설정해 배열을 지움.
  - 원본 배열을 참조하고 있는 배열도 초기화 됨.

```jsx
A.length = 0;
// 예시
let arr1 = ["a", "b", "c", "d", "e", "f"];
let arr2 = arr1;
arr1.length = 0;
console.log(arr1); // []
console.log(arr2); // []
```

- 3번
  - 실제로는 원래 배열을 복사 후 모든 값을 제거한 배열의 복사본을 반환함.
  - 원본 배열을 참조하고 있는 배열도 초기화 됨.

```jsx
A.splice(0, A.length)
// 예시
let arr1 = ['a','b','c','d','e','f']'
let arr2 = arr1;
arr1.splice(0, arr1.length)
console.log(arr1); // []
console.log(arr2); // []
```

- 4번 (비권장 방법)

```jsx
while (A.length > 0) {
  A.pop();
}
```

---

- 참고
  [https://stackoverflow.com/questions/1232040/how-do-i-empty-an-array-in-javascript](https://stackoverflow.com/questions/1232040/how-do-i-empty-an-array-in-javascript)

[https://jsben.ch/hyj65](https://jsben.ch/hyj65)
