# 프로퍼티 getter와 setter

- 객체의 프로퍼티는 두 종류로 나뉜다.
  - 데이터 프로퍼티 : 지금까지 사용한 모든 프로퍼티
  - 접근자 프로퍼티 : 접근자 프로퍼티의 본질은 함수. 값을 획득하고(get) 설정(set)하는 역할 담당. 외부 코드에서는 함수가 아닌 일반적인 프로퍼티로 보인다.

## getter와 setter

- 접근자 프로퍼티는 getter(획득자)와 setter(설정자) 메서드로 표현됨.

```javascript
let obj = {
  get propName() {
    // getter, obj.propName을 실행할 때 실행되는 코드
  },
  set propName(value) {
    // setter, obj.propName = value를 실행할 때 실행되는 코드
  },
};
```

- getter는 obj.propName을 사용해 프로퍼티를 읽으려고 할 때 실행되고 setter는 obj.propName = value로 프로퍼티에 값을 할당할 때 실행됨.

```javascript
let user = {
  name: "John",
  surname: "Smith",
  get fullName() {
    return `${this.name} ${this.surname}`;
  },
};

alert(user.fullName); // John Smith
```

- 바깥 코드에선 접근자 프로퍼티를 일반 프로퍼티처럼 사용할 수 있음. 접근자 프로퍼티를 사용하면 일반 프로퍼티에서 값에 접근하는 것처럼 평범하게 user.fullName을 사용해 값을 얻을 수 있음.
- setter를 추가한 예제

```javascript
let user = {
  name: "John",
  surname: "Smith",
  get fullName() {
    return `${this.name} ${this.surname}`;
  },
  set fullName(value) {
    [this.name, this.surname] = value.split(" ");
  },
};
// 주어진 값을 사용해 set fullName이 실행됩니다.
user.fullName = "Alice Cooper";

alert(user.name); // Alice
alert(user.surname); // Cooper
```

## 접근자 프로퍼티 설명자

- 접근자 프로퍼티에는 value와 writable이 없는 대신에 get과 set 함수가 있다.
- get: 인수가 없는 함수. 프로퍼티를 읽을 때 동작
- set: 인수가 하나인 함수. 프로퍼티에 값을 쓸 때 호출
- enumerable, configurable : 데이터 프로퍼티와 동일.

* 프로퍼티는 접근자 프로퍼티(get/set) 또는 데이터 프로퍼티(value) 중 한 종류에만 속하고 둘 다 속할 수 없다.

```javascript
// Error: Invalid property descriptor.
Object.defineProperty({}, "prop", {
  get() {
    return 1;
  },

  value: 2,
});
```

## getter와 setter 똑똑하게 활용하기

- getter와 setter를 실제 프로퍼티 값을 감싸는 래퍼로 활용하면 프로퍼티 값을 원하는대로 통제할 수 있다.
- 아래 예시에서는 name을 위한 setter를 만들어 user의 이름이 너무 짧아지는걸 방지. 실제 값은 별도의 프로퍼티 \_name에 저장됨

```javascript
let user = {
  get name() {
    return this._name;
  },

  set name(value) {
    if (value.length < 4) {
      alert(
        "입력하신 값이 너무 짧습니다. 네 글자 이상으로 구성된 이름을 입력하세요."
      );
      return;
    }
    this._name = value;
  },
};

user.name = "Pete";
alert(user.name); // Pete

user.name = ""; // 너무 짧은 이름을 할당하려 함
```
