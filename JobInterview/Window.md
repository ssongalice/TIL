# 브라우저 전역객체 window

- 브라우저 전체를 담당하는 객체.
- screen, location, history, document 등의 객체도 window에 포함됨.
- DOM (Document object model)
  - DOM은 HTML, XML 문서의 프로그래밍 인터페이스. DOM은 구조화된 노드와 프로퍼티, 메서드를 가진 object로 문서를 표현. → 쉽게 말하면 html문서의 태그들은 js가 이용할 수 있는 object(객체)로 만듦.
  - DOM은 프로그래밍 언어는 아니지만 DOM이 없다면 자바스크립트 언어는 웹페이지 및 요소와 관련된 개념이나 모델에 대한 정보를 갖지 못하게 됨.
  - DOM의 중요한 데이터 타입들
    - document: 브라우저가 불러온 웹페이지. 페이지 콘텐츠인 DOM 트리의 진입점 역할을 수행.
    - element: DOM 안에서 생성되는 element를 리턴
    - nodeList: elements의 배열
    - attribute: HTML 속성을 나타냄. HTML 속성은 element에 연관돼있다.
    - namedNodeMap: element attribute 노드의 정렬되지 않은 컬렉션을 뜻함.
    - [https://www.w3schools.com/jsref/dom_obj_attributes.asp](https://www.w3schools.com/jsref/dom_obj_attributes.asp)
- BOM (Browser object model)
  - 브라우저와 관련된 객체들의 집합. 최상위객체가 window
  - navigator: 브라우저, 운영체제에 대한 정보가 있음
  - screen: 화면에 대한 정보
  - location: 주소에 대한 정보
  - history: 브라우저의 방문 히스토리
