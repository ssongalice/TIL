# `[[prototype]]` vs proto

- 자바스크립트에서는 객체의 숨김 프로퍼티로 `[[prototype]]` 을 가지고 있다.
- 자바스크립트에서는 객체의 숨김 프로퍼티로 만약 해당 객체에 이 프로퍼티가 존재하지 않는다면 [[prototype]] 프로퍼티가 참조하는 다른 객체에서 이를 찾으려고 시도.
- **proto**?
  - 프로토타입의 getter와 setter
  - obj.**proto**를 사용하면 프로토타입에 접근할 수 있음.
- Object.keys, Object.values와 같이 키-값을 순회하는 메서드 대부분은 상속 프로퍼티를 제외하고 동작함.

  - 프로토타입에서 상속받은 프로퍼티는 제외하고 해당 객체에서 정의한 프로퍼티만 연산대상에 정의

  ```jsx
  const animal = { eats: true };
  Object.setPrototypeOf(animal, { pet: true });
  animal;
  // {eats: true}
  // __proto__:
  //          pet: true
  ```

- 프로토타입에 접근할 때 사용할 수 있는 모던 메서드
  - Object.create(proto, [descriptors]) - [[Prototype]]이 proto인 객체를 만듬.
  - Object.getPrototypeOf(obj) - obj의 [[Prototype]]을 반환.
  - Object.setPrototypeOf(obj, proto) - obj의 [[prototype]]을 proto로 설정함
- `Object.getPrototypeOf(obj),` Object.setPrototypeOf(obj, proto)와`__proto__`의 차이

  - `__proto__`는 읽기와 쓰기가 모두 가능하기 때문에 의도치 않게 값을 쓸 수 있게 됨.

---

참고
[https://ko.javascript.info/prototype-methods](https://ko.javascript.info/prototype-methods)

- https://www.nextree.co.kr/p7323/
