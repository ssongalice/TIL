# 전역 객체

- 전역 객체를 사용하면 어디서나 사용 가능한 변수나 함수를 만들 수 있음.
- 전역 객체엔 Array와 같은 내장 객체, window.innerHeight 같은 브라우저 환경 전용 변수 등이 저장됨.
- 중요한 변수라서 모든 곳에서 사용할 수 있게 하려면 전역 객체에 직접 프로퍼티를 추가할 수 있음.

```javascript
window.currentUser = {
  name: "John",
};
```

- 폴리필 사용하기
  - 전역 객체를 이용해 현재 사용중인 브라우저가 최신 자바스크립트 기능을 지원하는지 여부를 확인할 수 있음.
  - 예시 : 내장 객체 Promise를 지원하는지 테스트하기

```javascript
if (!window.Promise) {
  alert("구식 브라우저 사용중");
}
```