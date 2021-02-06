# 화살표 함수 기본

## 화살표함수란

```javascript
const func = (arg1, arg2, ...argN) => expression;
```

- 인수가 하나밖에 없다면 인수를 감싸는 괄호를 생략할 수 있다.
- 인수가 하나도 없을 땐 괄호를 비울 수 있음. 하지만 괄호를 생략할 수 없다.

## 과제

```javascript
// 문제
function ask(question, yes, no) {
  if (confirm(question)) yes();
  else no();
}

ask(
  "동의하십니까?",
  function () {
    alert("동의하셨습니다.");
  },
  function () {
    alert("취소 버튼을 누르셨습니다.");
  }
);

// 정답
const ask = (question, yes, no) => (confirm(question) ? yes() : no());
```
