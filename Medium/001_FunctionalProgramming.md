# 함수형 프로그래밍에 대한 적당한 고찰

## 값으로서의 함수

```javascript
/* Before */
const formatUsers = (users) => {
  if (!(users instanceof Array)) {
    return [];
  }
  return users.map(
    (user) => `
    Name: ${user.first} ${user.last},
    Age: ${user.age}
  `
  );
};

/* After */
const userF = (user) => {
  return `
    	Name: ${user.first} ${user.last},
        Age: ${user.age}
    `;
};

const formatUsers = (users) => {
  if (!(users instanceof Array)) {
    return [];
  }
  return users.map(userF);
};
```

### 고차함수(High-Order Function, HOF)?

- 함수에 함수를 파라미터로 전달할 수 있다.
- 함수의 반환값으로 함수를 사용할 수 있다.

### 함수 컴포지션 (Function composition)

- 함수를 조합해 새로운 함수로 만드는 것. 개별 함수는 단일 기능만 가진다.
- 함수들을 연쇄적 또는 병렬로 호출해 더 큰 함수를 만든다.

```javascript
/* Before */
const users = [
  {id: 1, name: "Mark", registered: true, money: 46},
  {id: 2, name: "Bill", registered: false, money: 22},
  {id: 3, name: "Steve", registered: true, money: 71}
]

const isArray = v => v instanceof Array
const getUserMoney = get('money')
const add = (x1, x2) => x1 + x2

const isValidPayer = user =>
	get('registered')(user) &&
    get('money')(user) > 40

export const sumMoneyOfRegUsers = users => {
	if(!isArray(users)) {
    	return 0
    }
    return users
    	.filter(isValidPayer)
        .map(getUserMoney)
        .reduce(add, 0)
}

sumMoneyOfRegUsers(users)

/* After */
const money = sumMoneyOfRegUsers(users)
const pipe = (...funcs) => {
	return (firstVal) => {
    	return funcs.reduce((partial, func) => 				func(partial), firstVal
    }
}

const arrify = x => x instanceof Array ? x : [x]
const getUserMoney = get('money')
const getUserReg = get('registered')

const filterValidPayers = users => users.filter (user => getUserReg(user) && getUserMoney(user) > 40)

const getUsersMoney = users => users.map(getUserMoney)
const sumUsersMoney = moneyArray => moneyArray.reduce((x,y) => x+y, 0)

export const sumMoneyOfRegUsers = pipe(
	arrify,
    filterValidPayers,
    getUsersMoney,
    sumUsersMoney
)

sumMoneyOfRegUsers(users)

```

## 자바스크립트 함수형 얕은/깊은 복사 (Shallow/Deep Copy)

```javascript
const subscribers = [
  { id: 1, name: "Tyler", registered: true, money: 36 },
  { id: 2, name: "Donald", registered: true, money: 26 },
  { id: 3, name: "William", registered: true, money: 61 },
];

// Shallow copy
const newSubscribers1 = [...subscribers];

// Deep copy
const newSubscribers2 = subscribers.map((sub) => ({ ...sub }));
```

- Shallow copy
  - 단순히 변수에 다른 변수를 할당하는 행위
    - 레퍼런스를 복제해서 값을 바꿀 경우 원본도 같이 바뀜
- Deep copy
  - 객체값 자체를 복사해 할당
    - Object.assign(), Spread 연산자

---

원문: https://dev.to/mr_bertoli/an-adequate-introduction-to-functional-programming-1gcl

참고

- https://www.linkedin.com/pulse/compose-me-function-composition-javascript-kevin-greene/
- https://brunch.co.kr/@kd4/87
- https://velog.io/@kyusung/%ED%95%A8%EC%88%98%ED%98%95-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%9A%94%EC%95%BD
