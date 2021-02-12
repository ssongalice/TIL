# 메서드와 this

## 메서드와 this

- 메서드 내부에서 this 키워드를 사용하면 객체에 접근할 수 있다.

```javascript
let user = {
  name: "John",
  age: 30,

  sayHi() {
    // this는 현재 객체 = user를 가리킴.
    alert(this.name);
  },
};
```

## 자유로운 this

- 자바스크립트에선 모든 함수에 this를 사용할 수 있다.
- this값은 런타임에 결정됨. 동일한 함수라도 다른 객체에서 호출했다면 this가 참조하는 값이 달라짐.

```javascript
let user = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
  alert(this.name);
}

user.f = sayHi;
admin.f = sayHi;

user.f(); // John
admin.fn(); // Admin
```

## this가 없는 화살표 함수

- 화살표 함수는 일반 함수와 달리 고유한 this를 가지지 않음. 화살표 함수에서 this를 참조하면 평범한 외부함수에서 this를 가져옴.

```javascript
let user = {
  firstName: "보라",
  sayHi() {
    let arrow = () => alert(this.firstname);
    arrow();
  },
};

user.sayHi(); // 보라
```

## 과제

- 객체 리터럴에서 'this' 사용하기

```javascript
function makeUser() {
  return {
    name: "John",
    ref: this,
  };
}

let user = makeUser();

alert(user.ref.name); // 결과가 어떻게 될까요? -- John
```

- 계산기 만들기

```javascript
let calculator = {
   sum() {
         return this.a + this.b;
   },
   mul() {
         return this.a * this.b;
   }
   read() {
         this.a = +prompt('첫번째', 0);
         this.b = +prompt('두번째', 0);
   }
};

calculator.read();
alert( calculator.sum() );
alert( calculator.mul() );
```
