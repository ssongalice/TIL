# let, const, var의 차이

- var, let, const 모두 변수를 선언하는 키워드
- var
  - 함수 스코프
  - 함수 스코프의 최상단으로 호이스팅 되고 선언과 동시에 undefined로 초기화됨.
  - var의 경우 선언 전에 출력하면 undefined로 출력된다.
  - var는 글로벌 스코프로 선언되었을 경우 글로벌 객체(브라우저 환경의 경우 window)에 바인딩된다.
  - var는 재선언 가능
- let, const

  - 블록 스코프
  - 블록 스코프의 최상단으로 호이스팅되고 선언만 되고 값이 할당하기 전까지 어떤 값으로도 초기화되지 않음.
  - 때문에 선언 전에 호출하면 Referrence error 발생. 선언은 되었지만 참조할 수 없는 사각지대 (TDZ, Temporal Dead Zone)을 가짐

    ```jsx
    const x = "outer scope";
    (function () {
      console.log(x); // Reference error
      const x = "inner scope";
    })();
    ```

    - [https://medium.com/korbit-engineering/let과-const는-호이스팅-될까-72fcf2fac365](https://medium.com/korbit-engineering/let%EA%B3%BC-const%EB%8A%94-%ED%98%B8%EC%9D%B4%EC%8A%A4%ED%8C%85-%EB%90%A0%EA%B9%8C-72fcf2fac365)

  - let, const는 글로벌 스코프로 선언되었을 경우 글로벌 객체에 바인딩되지 않는다.
  - let과 const는 재선언 불가능

---

참고
[https://github.com/baeharam/Must-Know-About-Frontend/blob/main/Notes/javascript/var-let-const.md](https://github.com/baeharam/Must-Know-About-Frontend/blob/main/Notes/javascript/var-let-const.md)
