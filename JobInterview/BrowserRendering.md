# 브라우저의 렌더링 과정

### 브라우저 렌더링 과정

    1. HTML, CSS 다운로드
    2. 다운로드받은 HTML, CSS를 → Object model (DOM, CSSOM)으로 만듦
    3. DOM과 CSSOM을 이용해 렌더 트리를 생성
        - 렌더트리에서는 화면에 표현되는 노드 요소로만 구성됨
        - display: none 속성이 설정된 요소 → 렌더 트리에서 제외 / visiblity: invisible 속성이 설정된 요소 → 렌더트리에 포함
    4. 레이아웃. 뷰포트 내에서 각 노드들의 정확한 위치와 크기 계산
        - 브라우저 화면의 어떤 위치에 어떤 크기로 출력되는지 계산하는 단계
        - 모바일은 디스플레이의 크기, PC의 경우 브라우저의 크기
        - %, vh, vw와 같이 상대적인 위치와 크기는 실제 화면에 그려지는 pixel 단위로 변환됨
    5. 페인트. 레이아웃 계산이 완료되면 화면에 그린다.
        - 이전 단계에서 이미 요소들의 위치와 크기, 스타일 계산이 완료된 렌더트리를 이용해 실제 픽셀값을 채워넣음
    6. JS 엔진 및 JS 코드 파싱

### 리플로우와 리페인트

- Reflow (Layout 단계)

  - 어떠한 이벤트나 액션에 따라 html 요소의 크기나 위치 등을 레이아웃 수치를 조정하면 그에 영향을 받는 자식 노드, 부모 노드 등을 포함하여 layout을 다시 수행. render tree와 각 요소들의 크기와 위치를 다시 계산하는 것을 리플로우라고 함.
  - reflow가 일어나는 대표적 예시
    - 페이지 초기 렌더링, 윈도우 리사이징, 노드 추가 제거, 요소의 위치 크기 변경 등
    - 폰트 변경 과(텍스트 내용) 이미지 크기 변경(크기가 다른 이미지로 변경 시)
  - reflow가 일어나는 속성 : position, width, height, left, top, right, bottom, margin, padding, border, display, font-size, font-weight, align, overflow...

- Repaint (paint 단계)

  - Reflow만 수행되면 실제 화면에 반영되지 않음. Paint 단계도 다시 수행됨.
  - 무조건 Reflow가 일어나야 Repain가 일어나는 건 아님. background-color, visiblitiy와 같이 레이아웃에 영향을 주지 않는 스타일 속성이 변경됐을 땐 Reflow를 수행할 필요가 없기 때문에 Repaint가 수행됨
  - repaint가 일어나는 속성 : background, border, color, outline, text-decoration, visibility

---

참고

- [https://velog.io/@st2702/브라우저의-렌더링-과정](https://velog.io/@st2702/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EC%9D%98-%EB%A0%8C%EB%8D%94%EB%A7%81-%EA%B3%BC%EC%A0%95)
- [https://boxfoxs.tistory.com/408#recentComments](https://boxfoxs.tistory.com/408#recentComments)
- [https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-tree-construction?hl=ko](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-tree-construction?hl=ko)
