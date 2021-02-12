# 'new' 연산자와 생성자 함수

## 생성자 함수

- 함수 이름의 첫글자는 대문자로 시작
- 반드시 new 연산자를 붙여 실행함

```javascript
function User(name) {
  this.name = name;
  this.isAdmin = false;
}

let user = new User("Jack");

alert(user.name); // Jack
alert(user.isAdmin); // false
```

## 생성자와 return 문

- 생성자 함수엔 보통 return 문이 없다. 반환할 것들은 모두 this에 저장되고 this는 자동으로 반환되기 때문에.
- 객체를 return 한다면 this 대신 객체 반환
- 원시형을 return 한다면 return 문 무시

## 생성자 내 메서드

- this에 메서드를 더해주는 것도 가능.

```javascript
function User(name) {
  this.name = name;
  this.sayHi = function () {
    alert("My name is " + this.name);
  };
}

let john = new User("John");
john.sayHi(); // My name is John.
```

## 과제

- 누산기 만들기

```javascript
function Accumulator(startingValue) {
  this.value = startingValue;

  this.read = function () {
    this.value += +prompt("더할 값을 입력해주세요.", 0);
  };
}

let accumulator = new Accumulator(1);
accumulator.read();
accumulator.read();
alert(accumulator.value);
```
