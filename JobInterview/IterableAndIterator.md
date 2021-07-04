# 이터러블과 이터레이터

### 이터러블 (Iterable), 반복 가능한 객체 (iterable object)

- 객체는 반복동작을 정의하는 경우 반복이 가능
- Array, Map과 같은 일부 내장형은 기본 반복 동작이 있지만 Object 같은 형은 없음
- 반복가능하기 위해 객체는 iterator 메서드를 구현해야 함. 즉 객체가 Symbol.iterator 키를 갖는 속성이 있어야 함
- iterable은 단 한 번 또는 여러번 반복 가능.
- 내장 iterable
  - String, Array, TypedArray, Map, set
  - 이들의 프로토타입객체는 모두 Symbol.iterator가 있기 때문.
- 어떤 객체가 Iterable 이라면 그 객체에 대해 아래의 기능을 사용할 수 있음

  - for of 루프
  - spread 연산자
  - 분해대입
  - iterable을 인수로 받는 함수

### 이터레이터 (Iterator) 프로토콜

- Iterable protocol을 만족하려면 Symbol.iterator 속성에 저장된 함수는 iterator 객체를 반환해야 함.
- 두 개의 속성 (value, done)을 반환하는 next() 메소드를 사용해 Iterator protocol을 구현

  - value: 현재 순서의 값
  - done: 반복이 모두 끝났는지를 나타냄

- 주의: iterator 객체와 iterable한 객체는 서로 다른 개념의 객체다!
  - 이터레이터는 next 메서드를 가지는 반면 이터러블한 객체는 Symbo.iterator 메서드를 가지기 때문

[https://helloworldjavascript.net/pages/260-iteration.html](https://helloworldjavascript.net/pages/260-iteration.html)

[https://velog.io/@bigbrothershin/JavaScript-반복-가능한-객체와-forof-문](https://velog.io/@bigbrothershin/JavaScript-%EB%B0%98%EB%B3%B5-%EA%B0%80%EB%8A%A5%ED%95%9C-%EA%B0%9D%EC%B2%B4%EC%99%80-forof-%EB%AC%B8)

[http://hacks.mozilla.or.kr/2015/08/es6-in-depth-iterators-and-the-for-of-loop/](http://hacks.mozilla.or.kr/2015/08/es6-in-depth-iterators-and-the-for-of-loop/)
