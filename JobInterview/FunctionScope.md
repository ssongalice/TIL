# 함수 스코프

### 함수 스코프

- 함수 내에서 정의된 변수는 함수의 범위에서만 정의돼있기 때문에 함수 외부 어느곳에서도 접근할 수 없다.
- 다른 함수 내에서 정의된 함수는 부모 함수와 부모함수가 액세스할 수 있는 다른 변수에 정의된 모든 변수를 액세스할 수 있음.
- 스코프 체인 : 변수를 찾기 위해 자기 자신의 스코프를 찾고 없다면 한 단계 올라가 부모의 스코프에서 찾는 것. 전역 스코프에도 없다면 변수를 찾지 못했다는 에러가 발생.
- 스코프는 함수를 선언할 때 생김.

### 렉시컬 스코핑(lexical scoping)

- 함수를 처음 선언하는 순간 함수 내부의 변수는 자기 자신의 스코프로부터 가장 가까운곳(상위 범위)에서 있는 변수를 계속 참조하게 됨.
- 함수를 어디서 선언하였는지에 따라 상위 스코프를 결정.
- [https://poiemaweb.com/js-scope](https://poiemaweb.com/js-scope)

```jsx
var name = "zero";
function log() {
  console.log(name);
}

function wrapper() {
  name = "nero";
  log();
}
wrapper(); // nero
//----------------------------
var name = "zero";
function log() {
  console.log(name);
}

function wrapper() {
  var name = "nero";
  log();
}
wrapper(); // zero
```

- 렉시컬 스코핑을 방지하기 위한 방법

```jsx
var another = function () {
  var x = "local";
  function y() {
    alert(x);
  }
  return { y: y };
};
var newScope = another();
console.log(newScope); // {y: f y()}

//------ 간단하게 바꾸면
var newScope = (function () {
  var x = "local";
  return {
    y: function () {
      alert(x);
    },
  };
})();
```
