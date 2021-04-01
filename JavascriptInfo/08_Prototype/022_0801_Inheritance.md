# 프로토타입 상속

## [[Prototype]]

- 자바스크립트 객체는 명세서에서 명명한 [[Prototype]]이라는 숨김 프로퍼티를 갖는다.
- 이 숨김프로퍼티 값은 null이거나 다른 객체에 대한 참조가 되는데 다른 객체를 참조하는 경우 참조 대상을 프로토타입이라고 함.
- object에서 프로퍼티를 읽으려고 하는데 해당 프로퍼티가 없으면 자바스크립트는 자동으로 프로토타입에서 프로퍼티를 찾음
- [[Prototype]] 프로퍼티는 내부 프로퍼티이면서 숨김 프로퍼티. 개발자가 값을 설정할 수 있다.

```javascript
let animal = {
  eats: true,
};

let rabbit = {
  jumps: true,
};
rabbit.__proto__ = animal;

// 프로퍼티 eats와 jumps를 rabbit에서도 사용할 수 있게 됨
alert(rabbit.eats); // true
alert(rabbit.jumps); // true
```

- 상속 프로퍼티 : 프로토타입에서 상속받은 프로퍼티
- 프로토타입 체이닝엔 두 가지 제약사항이 있음.
  - 순한참조(circular reference)는 허용되지 않음. **proto**를 이용해 닫힌 형태로 다른 객체를 참조하면 에러 발생
  - **proto**의 값은 객체나 null만 가능. 다른 자료형은 무시된다.
  - 객체엔 오로지 하나의 [[Prototype]]만 가능. 객체는 두 개의 객체를 상속받지 못함.

## 쓸 때는 프로토타입을 사용하지 않는다.

- 프로토타입은 프로퍼티를 읽을 때만 사용. 프로퍼티를 추가, 수정, 삭제하는 연산은 객체에 직접 해야 한다.

```javascript
let animal = {
  eats: true,
  walk() {
    /* rabbit은 이제 이 메서드를 사용하지 않음 */
  },
};

let rabbit = {
  __proto__: animal,
};

rabbit.walk = function () {
  alert("토끼가 깡충깡충 뜁니다");
};

rabbit.walk(); // 토끼가 깡충깡충 뜁니다
```

- 접근자 프로퍼티는 setter 함수를 통해서 프로퍼티에 값을 할당하므로 이 규칙이 적용되지 않음. 접근자 프로퍼티에 값을 할당하는 것은 함수를 호출하는 것과 같기 때문

```javascript
let user = {
  name: "John",
  surname: "Smith",
  set fullName(value) {
    [this.name, this.surname] = value.split(" ");
  },
  get fullName() {
    return `${this.name} ${this.surname}`;
  },
};

let admin = {
  __proto__: user,
  isAdmin: true,
};

alert(admin.fullName); // John Smith
admin.fullName = "Alice Cooper";
alert(admin.fullName); // Alice Cooper
alert(user.fullName); // John Smith
```

## this가 나타내는 것

- 메서드를 객체에서 호출했든 프로토타입에서 호출했든 this는 언제나 . 앞에 있는 객체가 된다.
  - 상속받은 메서드를 사용하더라도 객체는 프로토타입이 아닌 자신의 상태를 수정

```javascript
let animal = {
  walk() {
    if (!this.isSleeping) {
      alert("동물이 걸어갑니다");
    }
  },

  sleep() {
    this.isSleeping = true;
  },
};

let rabbit = {
  name: "하얀토끼",
  __proto__: animal,
};

// rabbit의 프로퍼티 isSleeping을 true로 변경
rabbit.sleep();

alert(rabbit.isSleeping); // true
alert(animal.isSleeping); // undefined. 프로토타입에는 isSleeping이라는 프로퍼티가 없음.
// 이때 상속받은 this는 animal이 아닌 실제 메서드가 호출되는 시점의 . 앞에 있는 객체가 됨.
```

## for..in 반복문

- for..in 은 상속 프로퍼티도 순회대상에 포함시킨다.

```javascript
let animal = {
  eats: true,
};

let rabbit = {
  jumps: true,
  __proto__: animal,
};

// Object.keys는 객체 자신의 키만 반환
alert(Object.keys(rabbit)); // jumps
// for..in은 객체 자신의 키와 상속 프로퍼티의 키 모두를 순환
for (let prop in rabbit) alert(prop); // jumps, ets
```

- obj.hasOwnProperty(key)를 이용하면 상속 프로퍼티를 순회 대상에서 제외할 수 있다. 이 내장 메서드는 key에 대응하는 프로퍼티가 상속 프로퍼티가 아니고 obj에 직접 구현돼있는 프로퍼티일 때 true를 반환

```javascript
let animal = {
  eats: true,
};

let rabbit = {
  jumps: true,
  __proto__: animal,
};

for (let prop in rabbit) {
  let isOwn = rabbit.hasOwnProperty(prop);

  if (isOwn) {
    alert(`객체 자신의 프로퍼티: ${prop}`); // 객체 자신의 프로퍼티: Jumps
  } else {
    alert(`상속 프로퍼티: ${prop}`); // 상속 프로퍼티: eats
  }
}
```

## 과제

- 검색 알고리즘

```javascript
let head = {
  glasses: 1,
};

let table = {
  pen: 3,
  __proto__: head,
};

let bed = {
  sheet: 1,
  pillow: 2,
  __proto__: table,
};

let pockets = {
  money: 2000,
  __proto__: bed,
};
```
