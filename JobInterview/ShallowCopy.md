# 얕은 복사와 깊은 복사

- 얕은 복사

  - 새로운 객체에 원본 객체의 각 속성과 값을 그대로 생성.
  - 원본 객체와 동일한 프로퍼티와 값을 새롭게 가지지만 주소가 복사된 프로퍼티는 같은 것을 공유함. → 해당 데이터의 참조값을 전달해 하나의 데이터를 공유하는 것 → 서로 공유하는 객체가 존재하게 됨.
  - 얕은 복사의 이슈

    - Property Descriptors가 복사되지 않음

    ```jsx
    const car = {
      name: "sonata",
      maker: "hyundai",
      engine: "1300cc",
    };

    Object.defineProperty(car, "engine", { writable: false });
    Object.getOwnPropertyDescriptor(car, "engine");
    // {value: "1300cc", writable: false, enumerable: true, configurable: true}

    const copyCar = Object.assign({}, car);
    Object.getOwnPropertyDescriptor(copyCar, "engine");
    // {value: "1300cc", writable: true, enumerable: true, configurable: true}configurable: trueenumerable: truevalue: "1300cc"writable: true__proto__: Object
    ```

    - 프로토타입 체인 또는 열거 가능하지 않은 프로퍼티는 복사되지 않음

    ```jsx
    const chainObj = {
      a: 1,
    };

    const newObj = Object.create(chainObj, {
      b: { value: 2 },
      c: { value: 3, enumerable: true },
    });

    console.log(newObj);
    // { c: 3, b: 2 }
    // __proto__: a: 1
    console.log(newObj.a); // 1

    const copyObj = Object.assign({}, newObj);
    console.log(copyObj);
    // { c: 3 }
    ```

    - 공유하고 있는 객체는 변경할 경우 영향을 끼침

  - Object.assign

    - 원본 객체의 열거 가능한 모든 프로퍼티를 복사해줌

    ```jsx
    const mainObj = {
      a: 1,
      b: 2,
      c: {
        x: 3,
        y: 4,
      },
    };

    const copyObj = Object.assign({}, mainObj);
    ```

  - Spread 연산자 사용

    ```jsx
    const cat = {
      name: "Ona",
      city: "Seoul",
    };

    const catClone = { ...cat };
    console.log(catClone); // {name: 'Ona', city: 'Seoul};
    cat === catClone; // false

    const hero = {
      name: "Batman",
      city: "Gotham",
    };

    const { ...heroClone } = hero;

    heroClone; // { name: 'Batman', city: 'Gotham' }

    hero === heroClone; // => false
    ```

- 깊은 복사

  - 값 자체의 복사. 독립적인 메모리에 값 자체를 할당해 생성하는 것.
  - JSON.stringify

  ```jsx
  function cloneObj(obj) {
    return JSON.parse(JSON.stringify(obj));
  }
  ```

  - 재귀 함수

  ```jsx
  function cloneObj(obj) {
    let clone = {};
    for (const i in obj) {
      if (typeof obj[i] === "object" && obj[i] !== null)
        clone[i] = cloneObj(obj[i]);
      else clone[i] = obj[i];
    }
    return clone;
  }
  ```

---

참고
[https://velog.io/@ddalpange/자바스크립트-객체-복사하기](https://velog.io/@ddalpange/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EA%B0%9D%EC%B2%B4-%EB%B3%B5%EC%82%AC%ED%95%98%EA%B8%B0)
[https://mygumi.tistory.com/322](https://mygumi.tistory.com/322)
