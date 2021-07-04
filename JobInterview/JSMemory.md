# Javascript의 메모리 구조

- 질문 의도 : 자료구조와 브라우저가 js를 실행시키는 원리를 이해하고 있는지. 얼마나 깊이 공부했니?

- 가비지 컬렉터에 대한 추가 질문 유도
  - 4가지 흔한 메모리 누수법
    - 전역변수 → 선언되지 않은 변수가 참조되면 전역 객체에 새로운 변수를 생성
    - 잊혀진 타이머 혹은 콜백함수
    - 클로져
    - DOM에서 벗어난 요소 참조
- 실행 컨텍스트에 대해 질문 유도

---

참고

- [https://developer.mozilla.org/ko/docs/Web/JavaScript/EventLoop](https://developer.mozilla.org/ko/docs/Web/JavaScript/EventLoop)
- [https://engineering.huiseoul.com/자바스크립트는-어떻게-작동하는가-메모리-관리-4가지-흔한-메모리-누수-대처법-5b0d217d788d](https://engineering.huiseoul.com/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%EC%9E%91%EB%8F%99%ED%95%98%EB%8A%94%EA%B0%80-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EA%B4%80%EB%A6%AC-4%EA%B0%80%EC%A7%80-%ED%9D%94%ED%95%9C-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%88%84%EC%88%98-%EB%8C%80%EC%B2%98%EB%B2%95-5b0d217d788d)
