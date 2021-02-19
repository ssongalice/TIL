# 화살표함수 다시 살펴보기

## 화살표 함수에는 this가 없다.

- 화살표 함수 본문에서 this에 접근을 하면 외부에서 값을 가져옴

```javascript
const group = {
  title: "1모둠",
  students: ["a", "b", "c"],
  showList() {
    // forEach에서 화살표 함수를 사용했기 때문에 함수 본문에 있는 this.title은 화살표 함수 바깥에 있는 메서드인 showList가 가리키는 대상, group.title과 동일하다
    this.students.forEach((student) => alert(this.title + ":" + student));
  },
};
```

- 화살표함수와 bind의 차이
  - bind는 함수의 한정된 버전을 만듦.
  - 화살표 함수는 어떤것도 바인딩시키지 않고 단지 this가 없을 뿐. 화살표 함수에서 this를 사용하면 this의 값을 외부 렉시컬 환경에서 찾음

## 화살표 함수에는 argunments가 없음

- 화살표 함수는 일반 함수와 다르게 모든 인수에 접근할 수 있게 해주는 유사배열 객체 arguments를 지원하지 않음.

```javascript
function defer(f, ms) {
  return function () {
    setTimeout(() => f.apply(this, arguments), ms);
  };
}

function sayHi(who) {
  alert("안녕", who);
}

let sayHiDeferred = defer(sayHi, 2000);
```
