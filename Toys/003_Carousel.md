# Carousel 구현하기

- 원리
  - carousel 카드를 감싸고 있는 wrapper를 만들고 넘길 때마다 css로 위치를 계산해 해당 카드만 보여준다.
    ![Carousel](./Toys/images/Carousel.PNG)

### 코드

- 기본 구조

```jsx
// startIndex : carousel이 시작하는 시점
// count: 화면에 보여질 카드의 수
// Carousel 컴포넌트를 만들어서 작성
<Carousel startIndex="0" count="3">
  {data.map((item) => {
    return <CarouselCard key={item.key}></CarouselCard>;
  })}
</Carousel>

// 실제 화면에서는 이런 구조로 나온다.
<div className="carousel__area">
      <div className="carousel__wrapper">
            // cards...
      </div>
</div>
```

```css
/* carousel__area는 움직이지 않는다 */
.carousel__area {
  max-width: 100%;
  overflow: hidden;
}
/* carousel__area의 자식 요소인 wrapper가 움직이면서 card를 보여준다 */
.carousel__wrapper {
  display: flex;
  flex-flow: row;
  transition: transform 0.3s;
}
```

- 카드 넓이는 flex로 지정한다. carousel 카드의 크기는 한 화면에 들어가는 갯수를 퍼센트로 계산해 %로 지정

```jsx
const viewPer = 100 / count;

// card를 렌더링 할 때 style.flex로 넓이를 다시 한 번 지정해준다.
card.style.flex = `0 0 ${viewPer}%`;
```

- carousel 버튼을 클릭 해 카드를 넘길 때마다 css translateX를 적용해 움직이도록 한다.
  - 보여주는 영역(`carousel__area`)과 카드들은 고정이고, 안의 wrapper가 움직인다.

```jsx
// prev, next에 따라 currentX를 다시 계산한다
// prev는 이전 카드를 보여줘야 하기 때문에 오른쪽으로 이동해야 하므로 +, next는 다음 카드를 보여줘야 하기 때문에 왼쪽으로 이동해야 하므로 -.
const onPrev = () => {
  const calcCurrentX = currentX + viewPer;
};
const onNext = () => {
  const calcCurrentX = currentX - viewPer;
};
// translateX로 wrapper를 움직인다.
wrapperRef.current.style.transform = `translateX(${currentX}%)`;
```
