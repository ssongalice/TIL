# 함수 호이스팅

- 함수를 정의하는 세 가지 방식

  - 함수 선언문

  ```jsx
  function fn(num) {
    return num * num;
  }
  ```

  - 함수 표현식
    - 함수 선언문, 함수 표현식 모두 함수 리터럴 방식으로 함수를 정의함. 이것은 결국 function 생성자 함수로 함수를 생성하는 것을 단순화시킨 것.

  ```jsx
  const fn = function (num) {
    return num * num;
  };

  // 함수 선언문으로 선언한 함수도 자바스크립트 엔진에 의해 다음과 같이 변형됨
  const fn = function fn(num) {
    return num * num;
  };
  ```

  - function 생성자로 선언한 함수

    ```jsx
    const fn = new Function("number", "return num * num");
    ```

- 함수 호이스팅이란?

  - 함수 선언문의 경우 함수 선언의 위치와 관계없이 코드 내에서 어디서나 호출이 가능한 것.

    - 함수 선언문으로 정의된 함수는 자바스크립트 엔진이 스크립트가 로딩되는 시점에 바로 초기화하고 이를 VO(variable object)에 저장. 함수 선언, 초기화, 할당이 한번에 이뤄짐. 때문에 위치에 관계없이 어디서나 사용할 수 있다.

    ```jsx
    const res = square(5);

    function square(number) {
      return number * number;
    }
    ```

  - 함수 표현식의 경우 함수가 아니라 변수가 호이스팅 된다. 함수 표현식은 함수 선언문과는 달리 스크립트 로딩 시점에 변수 객체(VO)에 함수를 할당하지 않고 runtime에 해석되고 실행된다.

  ```jsx
  //===== var 로 선언할 경우
  var varTest = fnNumB(5);
  var fnNumB = function (number) {
    return console.log(number);
  };
  // fnNumB is not a function

  //===== const로 선언할 경우
  const constTest = fnNum(5);
  const fnNum = function (number) {
    return console.log(number);
  };
  // Uncaught ReferenceError: Cannot access 'fnNum' before initialization
  ```

  ```jsx
  //===== var로 선언한 경우
  console.log(fnNumB); // undefined
  var fnNumB = function (number) {
    return console.log(number);
  };

  //===== const로 선언한 경우
  console.log(fnNum);
  // Uncaught ReferenceError: Cannot access 'fnNum' before initialization
  const fnNum = function (number) {
    return console.log(number);
  };
  ```

---

참고

- [https://poiemaweb.com/js-function](https://poiemaweb.com/js-function)
