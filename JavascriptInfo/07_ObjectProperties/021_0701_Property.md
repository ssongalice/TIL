# 프로퍼티 플래그와 설명자

## 프로퍼티 프래그

- 객체 프로퍼티는 값과 함께 플래그라고 불리는 특별한 속성 세 가지를 가진다.
- writable : true면 값을 수정할 수 있음. 그렇지 않으면 읽기만 가능
- emumerable : true면 반복문을 사용해 나열할 수 있음. 그렇지 않으면 반복문을 사용해 나열할 수 없음
- configurable : true면 프로퍼티 삭제나 플래그 수정이 가능. 그렇지 않다면 프로퍼티 삭제와 플래그 수정이 불가능.
- Object.getOwnPropertyDescriptor 메서드를 사용하면 특정 프로퍼티에 대한 정보를 얻을 수 있음

```javascript
let descriptor = Object.getOwnPropertyDescriptor(obj, propertyName);
```

- obj: 정보를 얻고자 하는 객체
- propertyName: 정보를 얻고자 하는 객체 내 프로퍼티

```javascript
let user = {
  name: "John",
};

let descriptor = Object.getOwnPropertyDescriptor(user, "name");

alert(JSON.stringify(descriptor, null, 2));
/* property descriptor:
{
  "value": "John",
  "writable": true,
  "enumerable": true,
  "configurable": true
}
*/
```

- 메서드 Object.defineProperty를 사용하면 플래그를 변경할 수 있다.

```javascript
Object.defineProperty(obj, propertyName, descriptor);
```

- obj, propertyName: 실명자를 적용하고 싶은 객체와 객체 프로퍼티
- descriptor : 적용하고자 하는 프로퍼티 설명자
- defineProperty를 이용해 프로퍼티를 만들 경우 descriptor에 플래그 값을 명시하지 않으면 플래그 값이 false가 된다

## writable 플래그

```javascript
let user = {
  name: "John",
};

Object.defineProperty(user, "name", {
  writable: false,
});
user.name = "Pete"; // Error
```

- 이제 defineProperty를 사용해 writable 플래그를 true로 변경하지 않는 한 누구도 객체의 이름을 변경할 수 없음.
- defineProperty 메서드를 사용해 프로퍼티를 밑바닥에서 만들기

```javascript
let user = {};

Object.defineProperty(user, "name", {
      value: "John:,
      // defineProperty를 사용해 새로운 프로퍼티를 만들 때 어떤 플래그를 true로 할지 명시해야 함
      enumerable: true,
      configurable: true
});
alert(user.name); // John
user.name = "Pete"; // Error
```

## enumerable 플래그

- 객체 내장 메서드 toString은 열거가 불가능(non-enumerable)하기 때문에 for..in 사용 시 나타나지 않는다. 하지만 커스텀 toString()을 추가하지 않으면 아래와 같이 for..in에 toString이 나타남
- 열거가 불가능한 프로퍼티는 Object.keys에도 배제됨

```javascript
let user = {
  name: "John",
  toString() {
    return this.name;
  },
};

//커스텀 toString은 for...in을 사용해 열거할 수 있습니다.
for (let key in user) alert(key); // name, toString
```

## configurable 플래그

- 구성 가능하지 않음을 나타내는 플래그(non-configurable flag)인 configurable: false는 몇몇 내장객체나 프로퍼티에 기본으로 설정됨.
- 어떤 프로퍼티의 configurable 플래그가 false로 설정돼있다면 해당 프로퍼티는 객체에서 지울 수 없다.
- 대표적으로 Math의 PI 프로퍼티는 쓰기, 열거, 구성이 불가능
- configurable 플래그를 false로 설정하면 돌이킬 방법이 없음. defineProperty를 써도 true로 돌릴 수 없다.

```javascript
let user = {};

Object.defineProperty(user, "name", {
  value: "John",
  writable: false,
  configurable: false,
});

// user.name 프로퍼티의 값이나 플래그를 변경할 수 없습니다.
// 아래와 같이 변경하려고 하면 에러가 발생합니다.
//   user.name = "Pete"
//   delete user.name
//   Object.defineProperty(user, "name", { value: "Pete" })
Object.defineProperty(user, "name", { writable: true }); // Error
```

- non-configurable과 non-writable은 다름. configurable 플래그가 false여도 writable 플래그가 true이면 프로퍼티 값을 변경할 수 있다.

## Object.defineProperties

- Object.defineProperties(obj, descriptor) 메서드를 사용하면 프로퍼티 여러개를 한 번에 정의할 수 있음

## Object.getOwnPropertyDescriptors

- Object.getOwnPropertyDescriptors(obj) 메서드를 사용하면 프로퍼티 설명자를 전부 한꺼번에 가져올 수 있음.
- 이 메서드를 Object.defineProperties와 함께 사용하면 객체 복사 시 플래그도 함께 복사할 수 있다.

```javascript
let clone = Object.defineProperties({}, Object.getOwnPropertyDescriptors(obj));
```

- for문을 사용해 객체를 복사하면 플래그나 심볼형 프로퍼티도 놓치게 됨. 하지만 Object.getOwnPropertyDescriptors는 심볼형 프로퍼티를 포함한 프로퍼티 설명자 전체를 반환.
