# CSS Box Model & Margin Collapsing

## CSS Box Model?

- CSS Box의 구성
  - content box: 콘텐츠 영역. width, height와 같은 속성을 사용해 크기를 설정할 수 있음
  - padding box: 콘텐츠 주변의 공백 영역. padding 속성을 사용해 크기를 설정할 수 있음
  - border box: 콘텐츠와 패딩을 둘러싸는 박스.
  - margin box: 가장 바깥쪽 레이어. 콘텐츠와 패딩, 테투리를 둘러싸면서 해당 박스와 다른 요소 사이 공백 역할을 함.
    - margin은 양수/음수를 가질 수 있고 음수일 경우 다른 부분과 겹칠 수 있다.

## box-sizing

- box-sizing: 요소의 너비와 높이를 계산하는 방법을 지정
  - content-box: 기본 박스 크기 계산법. width와 height 속성이 콘텐츠 영역만 포함하고 padding과 border는 해당되지 않는다.

```css
.box {
  width: 350px;
  border: 10px solid black;
}
/* box의 총 width = 370px */
```

- border-box: width와 height 속성이 안쪽 여백과 테두리까지 포함해서 계산함.
- border-box를 사용하면 요소의 크기 = 테두리 + 안쪽 여백 + 콘텐츠의 너비 또는 높이

```css
.box {
  width: 350px;
  border: 10px solid black;
}
/* box의 총 width = 350px */
```

### border-box 적용 팁

**예시**

- 모든 요소에 `box-sizing: border-box`를 적용하기 위해 \* 로 적용하면 컴포넌트에 적용된 box-sizing 옵션이 꼬일 수 있음.

```css
* {
  box-sizing: border-box;
}
.component {
  /* 해당 컴포넌트와 하위 컴포넌트에 다시 기본 box-sizing 옵션을 적용하고 싶은 경우 */
  box-sizing: content-box;
}
```

```html
<div class="component">
  <!-- box-sizing: content-box-->
  <header></header>
  <!-- box-sizing: border-box -->
</div>
```

- border-box를 모두 적용해야 한다면 이렇게 적용하자
  - [참고 원문](https://css-tricks.com/inheriting-box-sizing-probably-slightly-better-best-practice/)

```css
html {
  box-sizing: border-box;
}
*,
*:before,
*:after {
  box-sizing: inherit;
}
```

## Margin collapsing (마진 병합)

### 마진 병합이란?

- 인접하는 요소의 위아래 마진이 하나의 마진으로 합쳐지는 경우.
- 좌우 여백은 병합되지 않음.
- 병합된 마진은 합쳐진 여백 중 가장 큰 여백으로 결합됨.

### 발생하는 경우

- 인접하는 block 요소의 margin이 겹칠 경우
- 부모와 후손을 구분할 수 없을 경우
  - 테두리, 패딩, 인라인, 블록 컨텍스트 등 부모와 후손을 구분할 수 있는 요소가 없을 경우 margin 병합 발생
- 빈 블록인 경우

  - 테두리, 패딩, 인라인이 없는 경우

- 마진 병합은 여백이 0인 경우에도 적용. 상위 여백이 0인지 관계 없이 하위 항목의 여백은 부모 바깥에서 끝남.
- 마이너스 마진이 포함된 경우 병합된 마진의 크기는 가장 큰 플러스 마진과 가장 작은 마이너스 마진의 합이다.

### 마진 병합이 발생하지 않는 경우

- float, flex, position:absolute가 적용된 요소는 마진 병합이 발생하지 않음.
- [참고: Mastering margin collasping](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing)
- [참고: 마진병합](https://velog.io/@ursr0706/%EB%A7%88%EC%A7%84margin)
