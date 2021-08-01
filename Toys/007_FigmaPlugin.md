# 피그마 플러그인 만들기

## 피그마 플러그인?

- 회사 내부에서 사용하기 위한 다양한 플러그인 제작
- 플러그인 기획 관련 내용은 배제하고 리서치한 내용만 여기에 기록.

## 문제 해결을 위한 기술 리서치

### React MemoryRouter

**문제**

- React router - BrowserRouter를 썼을 때 작동하지 않음.

**해결**

- Figma plugin은 iframe으로 띄워지기 때문에 브라우저의 URL과 무관한 MemoryRouter를 사용.
- MemoryRouter는 브라우저가 아닌 환경에서 사용하기 좋음.
- [https://reactrouter.com/web/api/MemoryRouter](https://reactrouter.com/web/api/MemoryRouter)

### Figma - Color 시스템

**문제**

- Figma의 컬러시스템은 RGB를 사용하는데 rgb의 값이 0-255 사이값이 아닌 0-1사이의 값이어야 한다.

```tsx
interface RGB {
  readonly r: number;
  readonly g: number;
  readonly b: number;
}
```

**해결**

- Hex 형식의 컬러값을 RGB로 변환 후 다시 그 값을 255로 나눠서 0-1 사이의 값으로 치환

```tsx
export function convertHex(hex: string) {
  const r = parseInt(hex.slice(1, 3), 16),
    g = parseInt(hex.slice(3, 5), 16),
    b = parseInt(hex.slice(5, 7), 16);

  return { r: r, g: g, b: b };
}

export function getFigmaRGB(color: FigmaColor) {
  const rgbColorArray = Object["values"](color).map(
    (channel: number) => channel / 255
  );
  const rgbColor = {
    r: rgbColorArray[0],
    g: rgbColorArray[1],
    b: rgbColorArray[2],
  };
  return rgbColor;
}
```

### Figma - Font Family 사용하기

**문제**

- 텍스트 요소를 생성하면 기본 폰트가 Roboto 인데 변경하고 싶음

**해결**

- figma 요소의 폰트를 변경하기 위해서는 먼저 폰트를 불러온 후 요소를 생성해야 한다.

```tsx
export const FONT = {
  BOLD: {
    family: "Apple SD Gothic Neo",
    style: "Bold",
  },
};

// code.ts
figma.ui.onmessage = async (msg) => {
  await figma.loadFontAsync(FONT.BOLD);
...
}
```

### Figma - 자식 요소 크기에 맞춰 frame 크기 자동 설정하기

**문제**

- 자식 요소에 따라 frame의 크기가 늘어나야 함.
- 기본 width/height를 지정해주면 해당 크기로 고정됨. 하지만 자식 요소가 많거나 텍스트가 길어질 경우 요소를 감싸는 frame의 크기가 그에 맞게 늘어나야 함.

**해결**

- frame 컴포넌트의 layout mode를 'HORIZONTAL' 또는 'VERTICAL'로 설정
  - HORIZONTAL → 가로로 늘어남
  - VERTICAL → 세로로 늘어남

```jsx
const frame = figma.createFrame();
frame.layoutMode = "HORIZONTAL";
```

- (+) 텍스트를 frame 가로에 맞추고 넘치는 텍스트는 자동으로 내려가게 하려면 → text를 frame으로 한번 감싼뒤 text의 layoutAlign을 다음과 같이 설정.

```jsx
const text = figma.createText();
text.layoutAlign = "STRETCH";
```

### Figma - 요소 생성 후 요소가 생성된 위치로 view 이동하기

**문제**

- 요소를 생성할 때 x,y를 지정해주지 않으면 (0,0)에 생성되는 문제 발생

**해결**

- 요소를 생성할 때 x,y 위치를 viewport 기준으로 잡는다.

```jsx
frame.x = figma.viewport.center.x;
```

- 요소 생성 후 figma에서 제공하는 함수를 사용해 view를 이동시킨다.

```jsx
figma.viewport.scrollAndZoomIntoView(nodes);
```
