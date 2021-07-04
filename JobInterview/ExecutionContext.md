# 실행 컨텍스트

- 전역 컨텍스트 하나 생성 후 함수 호출시마다 컨텍스트가 생김
- 컨텍스트 생성 시 컨텍스트 안에 변수 객체 (arguments, variable), scope chain, this가 생성됨
- 컨텍스트 생성 후 함수가 실행되는데 사용되는 변수들은 변수 객체 안에서 값을 찾고 없다면 스코프 체인을 따라 올라가며 찾음
- 함수 실행이 마무리되면 해당 컨텍스트는 사라짐.

---

참고
[https://www.zerocho.com/category/JavaScript/post/5741d96d094da4986bc950a0](https://www.zerocho.com/category/JavaScript/post/5741d96d094da4986bc950a0)
