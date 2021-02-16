# 재귀와 스택

## 두 가지 사고방식

- 재귀 : 함수가 자기 자신을 호출하는 것

- 구현하는 방법

  - 예시 : x를 n제곱해주는 함수 pow(x, n)을 만들어야 함.
  - 첫 번째 방법 : for 루프
  - 두 번째 방법 : 재귀를 사용한 방법

```javascript
// 1번
function pow(x, n) {
  let result = 1;

  for (let i = 0; i < n; i++) {
    result *= x;
  }
  return result;
}

// 2번
function pow(x, n) {
  return (n == 1) ? : x : (x * pow(x, n-1));
}
```

- 중첩 호출의 최대 갯수는 재귀 깊이. 자바스크립트 엔진은 최대 재귀 깊이를 제한. 대략 만 개정도는 확실히 허용

## 실행 컨텍스트와 스택

- 실행 컨텍스트
  - 실행 컨텍스트 : 실행 중인 함수의 실행 절차에 대한 정보를 저장하는 내부 데이터 구조.
  - 함수 내부에 중첩 호출이 있으면 아래와 같은 절차가 수행됨.
    - 현재 함수 실행 일시 중지
    - 중지된 함수와 연관된 실행 컨텍스는 실행 컨텍스트 스택이라는 특별한 자료구조에 저장됨.
    - 중첩 호출이 실행됨
    - 중첩 호출 실행이 끝난 후 실행 컨텍스트 스택에서 일시 중단한 함수의 실행 컨텍스트를 꺼내오고 중단한 함수를 다시 실행
  - 재귀 깊이는 스택에 들어가는 실행 컨텍스트 수의 최대값과 같음
  - 실행 컨텍스트는 메모리를 차지하므로 재귀를 사용할 땐 메모리 요구사항에 유의.

## 재귀적 순회

- 예시

```javascript
let company = {
  // 동일한 객체(간결성을 위해 약간 압축함)
  sales: [
    { name: "John", salary: 1000 },
    { name: "Alice", salary: 1600 },
  ],
  development: {
    sites: [
      { name: "Peter", salary: 2000 },
      { name: "Alex", salary: 1800 },
    ],
    internals: [{ name: "Jack", salary: 1300 }],
  },
};

// 부서별 전체 급여 합계 구하기
function sumSalaries(department) {
  if (Array.isArray(department)) {
    return department.reduce((prev, current) => prev + current.salary, 0); // 단순한 배열로 이뤄진 부서의 경우 배열의 총합을 구함
  } else {
    let sum = 0;
    for (let subdep of Object.values(department)) {
      sum += sumSalaries(subdep); // 재귀 호출로 각 하위 부서 임직원의 급여를 더한다.
    }
    return sum;
  }
}
```

## 재귀적 자료 구조

- 재귀적 자료 구조 : 자기 자신의 일부를 복제하는 형태의 자료 구조

### 연결리스트

- 빠르게 삽입 또는 삭제할 때 사용하는 자료구조
- 연결 리스트의 요소는 객체와 아래 프로퍼티를 조합해 정의할 수 있다
  - value
  - next: 다음 연결 리스트 요소를 참조하는 프로퍼티. 다음 요소가 없으면 Null

## 과제

- 주어진 숫자까지 모든 숫자 더하기

```javascript
function sumTo(num) {
  if (num === 1) {
    return 1;
  } else {
    return num + sumTo(n - 1);
  }
}
```

- 팩토리얼 계산하기

```javascript
function factorial(n) {
  return n === 1 ? 1 : n * factorial(n - 1);
}
```

- 피보나치 수 계산하기

```javascript
function fib(n) {
  let a = 1;
  let b = 1;
  for (let i = 3; i <= n; i++) {
    let c = a + b;
    a = b;
    b = c;
  }
  return b;
}
```

- 단일 연결 리스트 출력하기

```javascript
let list = {
  value: 1,
  next: {
    value: 2,
    next: {
      value: 3,
      next: {
        value: 4,
        next: null,
      },
    },
  },
};

// 재귀를 기반으로
function printList(list) {
  alert(list.value); // 현재 요소를 출력한다
  if (list.next) {
    printList(list.next);
  }
}
```
