# input type = button과 그냥 button의 차이

- <button></button>

  - 버튼 태그는 하위 자식 요소를 가질 수 있다.
  - 버튼 태그는 css pseudo-elements를 허용해서 스타일을 자유롭게 할 수 있음. :after, :before. → input type button은 안됨.
  - button 태그의 type은 기본적으로 submit. 타입이 특정되지 않으면 submit 기능 수행
  - 버튼 태그가 input type button보다 좀 더 시맨틱적. 만약에 클릭 가능한 버튼을 만든다면 button 태그가 더 추천됨.
  - button 태그의 타입
    - submit: form data를 서버로 전송
    - reset: form input들을 초기값으로 되돌림.
    - button: 기본행동이 없으며 클라이언트 스크립트와 연결해서 사용 가능.

- <input type="button" />
    - input type 버튼은 하위 자식 요소를 가질 수 없다.
    - 만약에 input button이 submit 역할을 한다면 type='submit'으로 바꾸는 것이 좋다.

---

참고
[https://www.geeksforgeeks.org/button-tag-vs-input-typebutton-attribute/](https://www.geeksforgeeks.org/button-tag-vs-input-typebutton-attribute/)

[https://www.tutorialspoint.com/What-is-difference-between-button-vs-input-type-button](https://www.tutorialspoint.com/What-is-difference-between-button-vs-input-type-button)

[https://thisthat.dev/button-vs-input-type-button/](https://thisthat.dev/button-vs-input-type-button/)

[https://developer.mozilla.org/ko/docs/Web/HTML/Element/button](https://developer.mozilla.org/ko/docs/Web/HTML/Element/button)
