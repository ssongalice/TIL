# 유사 배열 객체 (Array like Object);

[https://dev.to/capscode/what-is-array-like-object-in-javascript-3f5m](https://dev.to/capscode/what-is-array-like-object-in-javascript-3f5m)

- 배열과 유사한 형태의 객체

```jsx
const arr_like_obj = {
  0: "we",
  1: "are",
  2: "capscode",
  length: 3,
};
```

- 배열과 유사하지만 키가 숫자고 length 속성을 가짐 [(링크)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Indexed_collections#배열_객체의_메서드)
- 유사배열객체는 배열의 메서드(forEach, map, pop, push) 등을 사용할 수 없다.
- 유사배열객체에서는 object의 key값을 이용해 프로퍼티에 접근하는 방식을 사용할 수 없음

```jsx
arr_like_obj.0 // SyntaxError: Unexpected number
arr_like_obj[0] // "we"
arr_like_obj.length // 3
```

- 유사배열객체를 Array.isArray(인자가 array인지 확인하는 메서드) 로 체크하면 false를 뱉음

```jsx
Array.isArray(arr_like_obj); // returns false
```

- 대표적인 유사배열객체: 함수 argument 객체, HTMLCollection, NodeList
  - argument 객체 [(링크)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/arguments)
    - 함수에 전달된 인수에 해당하는 Array 형태의 객체
    - 모든 함수에 사용할 수 있는 인수. arguments객체를 사용해 함수 내에서 모든 인수를 참조할 수 있음. 호출할 때 제공한 인수 각각에 대한 항목을 가짐.
    - 함수에서 선언할 때 받기로 선언한 것보다 많은 인수로 함수를 호출하는 경우 arguments 객체를 사용할 수 있음.
  - HTMLCollection?
    - 문서 내에 순서대로 정렬된 노드의 컬렉션.
    - HtmlCollection은 구성요소를 이름과 인덱스를 동시에 노출
  - NodeList
    - element.childNodes 프로퍼티나 document.querySelectorAll() 메서드로 반환되는 노드의 모음
    - childNodes는 변경사항을 바로 반영. querySelector는 정적으로 변경사항이 생겨도 반영되지 않음
