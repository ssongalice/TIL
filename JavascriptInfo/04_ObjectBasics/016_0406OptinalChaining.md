# 옵셔널체이닝 '?.'

## 옵셔널 체이닝의 등장

- `?.`는 앞의 평가 대상이 undefined나 null이면 평가를 멈추고 undefined를 반환.

```javascript
let user = {};
alert(user?.address?.street); // undefined 반환
```

- 옵셔널 체이닝은 ?. 존재하지 않아도 괜찮은 대상에만 사용해야 함.

## 단락평가

- ?.는 왼쪽 평가대상에 값이 없으면 즉시 평가를 멈춤. 그렇기 때문에 함수 호출을 비롯한 ?. 오른쪽에 있는 부가 동작은 ?.의 평가가 멈췄을 때 더는 일어나지 않음

```javascript
let user = null;
let x = 0;

user?.sayHi(x++); // 아무일도 일어나지 않음
alert(x); // 0
```

## ?.()와 ?.[]

- ?.는 연산자가 아님.

```javascript
let user1 = {
  firstName: "Violet",
};

let user2 = null;

let key = "firstName";

alert(user1?.[key]); // Violet
alert(user2?.[key]); // undefined
```
