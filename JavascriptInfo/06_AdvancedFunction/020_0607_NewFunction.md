# new Function

## 문법

```javascript
let func = new Function([arg1, arge2, ...argN], functionBody);
```

- new function 문법을 사용하면 함수를 만들 수 있음
- 런타임에 받은 문자열을 사용해 함수를 만들 수 있음.
- 서버에서 코드를 받거나 템플릿을 사용해 함수를 동적으로 컴파일해야 하는 경우, 복잡한 웹 애플리케이션을 구현할 때와 같이 특별한 경우에 new function 사용

## 클로저

- new Function을 이용해 함수를 만들면 함수의 [[Environment]] 프로퍼티가 전역 렉시컬 환경을 참조하게 됨. new Function을 이용해 만든 함수는 외부 변수에 접근할 수 없고 오직 전역 변수에만 접근할 수 있다.

```javascript
function getFunc() {
      let value = "test";
      let func = new Function('alert(value'));
      return func
}
```
