# 함수의 프로토타입 프로퍼티

- `new F()`와 같은 생성자 함수를 사용하면 새로운 객체를 만들 수 있다. 그런데 F.prototype이 객체면 new 연산자는 F.prototype을 사용해 새롭게 생성된 객체의 [[Prototype]]을 생성.

```javascript
let animal = {
  eats: true,
};

function Rabbit(name) {
  this.name = name;
}

Rabbit.prototype = animal;

let rabbit = new Rabbit("White Rabbit"); //  rabbit.__proto__ == animal

alert(rabbit.eats); // true
```

## 함수의 prototype 프로퍼티와 constructor 프로퍼티

- 모든 함수는 기본적으로 "prototype" 프로퍼티를 갖는다.
- 기본 프로퍼티인 "prototype"은 constructor 프로퍼티 하나만 있는 객체를 가리키는데, 이 constructor는 자기 자신.

```javascript
function Rabbit() {}

/* 기본 프로토타입
Rabbit.prototype = {
      constructor: Rabbit;
}

```

- 자바스크립트는 알맞은 "constructor"값을 보장하지 않는다.
  - 함수에 기본으로 prototype이 지정되지만 그게 전부. constructor에서 벌어지는 일은 개발자의 책임

```javascript
// before
function Rabbit() {}
Rabbit.prototype = {
  jumps: true,
};

let rabbit = new Rabbit();
alert(rabbit.constructor === Rabbit); // false

// after
// prototype을 덮어쓰지말고 값을 추가한다.
Rabbit.prototype.jumps = true;
```

### 요약

- `F.prototype` 프로퍼티는 `[[Prototype]]`과는 다릅니다. `F.prototype`은 `new F()`를 호출할 때 만들어지는 새로운 객체의 `[[Prototype]]`을 설정함.
- `F.prototype`의 값은 객체 또는 null만 가능
- 모든 함수는 기본적으로 `F.prototype = { constructor: F }`를 가지고 있으므로 함수의 "constructor"프로퍼티를 사용하면 객체의 생성자를 얻을 수 있다

### 문제

- 각 번호대로 코드를 수정하면 어떤 결과값이 출력될까?

```javascript
function Rabbit() {}
Rabbit.prototype = {
  eats: true,
};

let rabbit = new Rabbit();

// 문제
// 1. Rabbit.prototype = {};
// 2. Rabbit.prototype.eats = false;
// 3. delete rabbit.eats;
// 4. delete Rabbit.prototype.eats;
alert(rabbit.eats);
```

- 정답
- 1. `true`
  - Rabbit.prototype에 무언가를 할당하면 그 값이 새로운 프로토타입이 된다. 하지만 rabbit은 이미 객체가 만들어져있기 때문에 수정되지 않음.
- 2. `false`
  - 객체는 참조에 의해 할당됨. Rabbit.prototype이 참조하는 객체는 하나, 이 객체는 Rabbit.prototype과 rabbit의 [[prototype]]을 사용해 참조할 수 있다. 따라서 둘 중 하나의 참조를 이용해 값을 변경하면 다른 참조를 통해서도 그 값을 볼 수 있다.
- 3. `true`
  - delete 연산은 객체에 직접 적용됨. `delete rabbit.eats`는 rabbit에서 eats를 제거하는데 rabbit엔 eats가 없으므로 아무런 영향을 주지 않음.
- 4. undefined
  - 프로퍼티 eats가 프로토타입에서 삭제됐기 때문에 더이상 존재하지 않음.
