# js 요소 Dom 선택자

### queryselector와 getElementbyId의 차이

- getElementById

  - ID를 통해 element 반환
  - 일치하는 값이 없다면 Null 반환
  - 리턴값: HTMLCollection
  - 오로지 element DOM ID로만 선택해야 함.
  - 매우 오래된 브라우저까지 지원하려면 getElementById 사용이 좋음.
  - 성능은 querySelector보다 getElement가 더 빠르다.

- querySelector

  - css seletor와 일치하는 첫 번째 element 반환
  - 일치하는 값이 없다면 Null 반환
  - 리턴값: NodeList
  - querySelector는 element name, dom ID, css selector 등 다양한 선택자를 사용해 선택할 수 있다.

  ```jsx
  const elemId = document.querySelector("#unique_id");
  const elemClass = document.querySelector(".element_class");
  ```

- querySelectorAll
  - sector와 일치하는 모든 요소 반환
  - getElementsByClassName과의 차이
    - querySelectorAll은 element 이름뿐만 아니라 클래스 이름도 검색에 사용 가능. getElementsByClassName은 클래스 네임만 가능.
    - 하위 지원을 위해서는 getElementByClassName 사용이 좋음.

---

참고
[https://careerkarma.com/blog/javascript-queryselector-vs-getelementbyid/](https://careerkarma.com/blog/javascript-queryselector-vs-getelementbyid/)

[https://developer.mozilla.org/ko/docs/Web/API/Document/querySelector](https://developer.mozilla.org/ko/docs/Web/API/Document/querySelector)
[https://developer.mozilla.org/ko/docs/Web/API/Document/getElementById](https://developer.mozilla.org/ko/docs/Web/API/Document/getElementById)

[https://truecode-95.tistory.com/41](https://truecode-95.tistory.com/41)

[https://gomakethings.com/javascript-selector-performance/](https://gomakethings.com/javascript-selector-performance/)
