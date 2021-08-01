# Promise, Async & Await

---

## 자바스크립트의 비동기 처리와 콜백

- 비동기 처리 : 특정 로직의 실행이 끝날때까지 기다려주지 않고 나머지 코드를 먼저 실행하는 것
- 자바스크립트에서 콜백함수를 사용해 비동기처리를 해줌.
- 비동기 처리를 활용하는 예시
  - 사용자 이벤트 처리
  - 네트워크 응답 처리
  - 파일 읽고 쓰는 작업 등
- 콜백함수 정리는 여기 >>

## Promise?

- 프로미스 : 자바스크립트 비동기 처리에 사용하는 객체

### 프로미스의 상태

- 프로미스는 프로미스를 생성하고 종료될 때까지 3가지 상태를 가진다.
  - Pending (대기): 비동기 처리 로직이 아직 완료되지 않은 상태
  - Fulfilled (이행): 비동기 처리가 완료돼 프로미스가 결과값을 반환해준 상태
  - Rejected (실패): 비동기 처리가 실패하거나 오류가 발생한 상태

### Pending

- `new Promise()` 메서드를 호출하면 대기 상태가 된다.
- new Promise를 호출할 때 콜백 함수를 선언할 수 있고 콜백 함수의 인자는 resolve, reject이다.

```js
new Promise(function (resolve, reject) {
  //...
});
```

### Fulfilled

- 여기서 콜백함수의 인자 resolve를 아래와 같이 실행하면 이행 (Fulfilled) 상태가 된다. 이행하면 then을 이용해 처리값을 받을 수 있다.

```js
function getData() {
  return new Promise(function (resolve, reject) {
    const data = 100;
    resolve(data);
  });
}

getData.then(function (resolvedData) {
  console.log(resolvedData); // 100
});
```

### Rejected

- reject를 호출하면 실패 상태가 된다. 실패 이유는 catch로 받을 수 있다.

```js
function getData() {
  return new Promise(function (resolve, reject) {
    reject(new Error("Request is failed"));
  });
}

getData.then().catch(function(err)  {
      console.log(err); // Request is failed
```

### Promise chaining

- 프로미스는 여러개의 프로미스를 연결하여 사용할 수 있다. then 메서드를 호출하고 나면 새로운 프로미스 객체를 반환함.

```js
function getData() {
  return new Promise({
    // ...
  });
}

// then() 으로 여러 개의 프로미스를 연결한 형식
getData()
  .then(function (data) {
    // ...
  })
  .then(function () {
    // ...
  })
  .then(function () {
    // ...
  });
```

### 프로미스의 에러 처리 방법

- 에러 처리 방법은 두가지가 있다.
- 1. then()의 두번째 인자로 처리하는 방법

```js
getData().then(
  function () {
    //resolved
  },
  function (err) {
    //err
  }
);
```

- 2. catch()를 이용하는 방법
- 가급적 catch를 사용해 에러를 처리해야 더 정확한 에러 처리가 가능.

```js
getData()
  .then()
  .catch(function (err) {
    console.log(err); // err
  });
```

## async, await

### async

- function 앞에 async를 붙이면 해당 함수는 항상 프라미스를 반환한다. 프라미스가 아닌 값을 반환하더라도 이행 상태의 프라미스로 값을 감싸 이행된 프라미스가 반환되도록 함.

```js
async function f() {
  return 1;
}

f().then(alert); // 1
```

### await

- await은 async 안에서만 동작한다.
- 자바스크립트는 await 키워드를 만나면 프라미스가 처리될 때까지 기다렸다가 반환됨.
- await은 최상위 레벨 코드에서 작동하지 않는다. 하지만 익명 async 함수로 감싸면 사용 가능.

```js
async function f() {
  let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("완료!"), 1000);
  });

  let result = await promise; // 프라미스가 이행될 때까지 기다림 (*)

  alert(result); // "완료!"
}

f();
// 이렇게 감싸면 사용 가능
(async () => {
  let response = await fetch('/article/promise-chaining/user.json');
  let user = await response.json();
  ...
})();
```

- await는 promise.then()처럼 await에도 thenable 객체를 사용할 수 있다.
  - await는 .then이 구현돼있으면서 프라미스가 아닌 객체를 받으면 내장함수 resolve와 reject를 인수로 제공하는 메서드인 .then을 호출한다. 그리고 나서 await는 resolve와 reject 중 하나가 호출되기를 기다렸다가 호출 결과를 가지고 다음 일을 진행한다.

```js
class Thenable {
  constructor(num) {
    this.num = num;
  }
  then(resolve, reject) {
    alert(resolve);
    // 1000밀리초 후에 이행됨(result는 this.num*2)
    setTimeout(() => resolve(this.num * 2), 1000); // (*)
  }
}

async function f() {
  // 1초 후, 변수 result는 2가 됨
  let result = await new Thenable(1);
  alert(result);
}

f();
```

### async, await 에러 핸들링

- 프라미스가 이행되면 await promise 는 프라미스 객체의 result에 저장된 값을 반환. 반면 프라미스가 거부되면 마치 throw문을 작성한 것처럼 에러를 반환
- await가 던진 에러는 try...catch 문으로 잡을 수 있음.

```js
async function f() {
  try {
    const response = await fetch("url");
  } catch (err) {
    console.err(err);
  }
}
```

- try catch가 없으면 아래 예시의 async 함수 f()를 호출해 만든 프라미스가 거부 상태가 됨. f()에 .catch가 추가되면 거부된 프라미스를 처리할 수 있음.

```js
async function f() {
  let response = await fetch("http://유효하지-않은-url");
}

// f()는 거부 상태의 프라미스가 됩니다.
f().catch(alert); // TypeError: failed to fetch // (*)
```

- 여러개의 프라미스가 모두 처리되기를 기다리는 상황이라면 Promise.all로 감싸고 여기에 await를 붙여 사용할 수 있음.

```js
const result = await Promise.all([
      fetch(url1);
      fetch(url2);
      fetch(url3);
])
```

---

참고링크 -[async/await](https://ko.javascript.info/async-await) -[자바스크립트 async와 await](https://joshua1988.github.io/web-development/javascript/js-async-await/)
