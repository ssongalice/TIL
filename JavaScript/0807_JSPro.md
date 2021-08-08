# 자바스크립트 프로처럼 쓰는 팁

## Nullish coalescing operator ??

- 왼쪽 표현식이 null이거나 undefined 일 경우에만 오른쪽 표현식을 실행

```js
leftExpr ?? rightExpr;
```

- 비교하기 ||
  - 왼쪽 표현식이 falsy일 경우에만 오른쪽 표현식을 실행
  - falsy: false, undefined, null, "", 0, NaN...

```js
leftExpr || rightExpr;
```

- 함수를 실행해서 값이 null인 경우 ?? 옆의 함수를 실행한다

```js
const result = getInitialState() ?? fetchFromServer();

function getInitialState() {
  return null;
}
function fetchFromServer() {
  return "hi";
}

console.log(result); // "hi"
```

## Object Destructuring

```js
// Bad
function display(person) {
  displayName(person.name);
  displayProfile(person.name, person.age);
}

// Good
function display(person) {
  const { name, age } = person;
  displayName(name);
  displayProfile(name, age);
}
```

## Optional Chaining

```js
const bob = {
  name: "julia",
  age: 20,
};

const anna = {
  name: "julia",
  age: 20,
  job: {
    title: "Software Engineer",
  },
};

// Bad
function displayJobTitle(person) {
  if (person.job && person.job.title) {
    console.log(person.job.title);
  }
}

// Good
function displayJobTitle(person) {
      if(person.job?.title) {
            console.log(person.job?title);
      }
}
// Good
function displayJobTitle(person) {
      const title  = person.job?.title ?? 'No job';
      console.log(title);
}
```

---

[자바스크립트 프로처럼 쓰는법](https://www.youtube.com/watch?v=BUAhpB3FmS4&t=985s)
