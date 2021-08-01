# Callback 함수

## 콜백함수란?

- 다른 함수의 인자로써 이용되는 함수
- 어떤 이벤트에 의해 호출되는 함수
- 자바스크립트에서 함수는 객체다. 그래서 함수를 변수처럼 함수의 인자로 전달하거나 다른 함수의 리턴값으로 사용할 수 있다.
- 콜백함수는 콜백함수를 포함한 함수 내부 인자에 접근이 가능하고 전역변수에도 접근이 가능한 상태.

## 콜백함수의 적용 원칙

- 콜백함수를 사용할 땐 이름이나 익명함수로 사용한다.
- 콜백함수로 파라미터를 전달.
  - 콜백함수는 실행될 때 일반함수와 동일하게 전달됨. 그래서 콜백함수에 파라미터를 전달할 수 있다.

```js
const data = [];
const name = "ona";

function getInput(options, callback) {
  data.push(options);
  callback(name, options);
}
```

- 콜백함수에 this를 사용할 경우 this 객체의 컨텍스트를 보호하기 위해 콜백함수를 수정해야 함.
  - call, apply 메서드를 사용해 this를 보호한다.

```js
const clientData = {
  id: 094545,
  fullName: "Not Set",
  // setUserName clientData의 메서드입니다.
  setUserName: function (firstName, lastName) {
    // this는 clientData라는 객체를 지칭하고 있습니다.
    this.fullName = firstName + " " + lastName;
  },
};

function getUserInput(firstName, lastName, callback) {
  callback(firstName, lastName);
}
getUserInput("Barack", "Obama", clientData.setUserName);
console.log(clientData.fullName); // 값에 설정되지 않음
console.log(window.fullName); // Barack Obama

function getUserInputApply(firstName, lastName, callback, callbackObj) {
  callback.apply(callbackObj, [firstName, lastName]);
}

getUserInput("Barack", "Obama", clientData.setUserName, clientData);
console.log(clientData.fullName); // Barack Obama
```

---

참고

- [자바스크립트의 콜백함수 이해하기](https://yubylab.tistory.com/entry/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%9D%98-%EC%BD%9C%EB%B0%B1%ED%95%A8%EC%88%98-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)
