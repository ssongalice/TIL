# 코드 분할 (Code Spliting)

## 코드 분할이란?

- 번들링은 훌륭하지만 앱의 번들도 커짐. 큰 규모의 서드파티 라이브러리를 사용할수록 앱이 커짐.
- 코드 분할은 번들이 거대해지는 것을 방지하기 위한 해결방법. 런타임에 여러 번들을 동적으로 만들고 불러오는 것.
- 코드 분할은 앱을 지연 로딩하게 도와주고 앱 사용자에게 획기적인 성능 향상을 하게 함.
- 앱의 코드 양을 줄이지 않고도 사용자가 필요하지 않은 코드를 불러오지 않으며 앱의 초기화 로딩에 필요한 비용을 줄여줌.

## import()

- 앱에 코드 분할을 도입하는 가장 좋은 방법. 동적 import()문 사용하기

```javascript
// before
import { add } from "./math";
console.log(add(16, 26));
// after
import("./math").then((math) => {
  consoel.log(math.add(16, 26));
});
```

## React.lazy()

- `React.lazy()` 함수를 사용하면 동적 import를 사용해서 컴포넌트를 렌더링할 수 있다.
- React.lazy는 아직 서버사이드 렌더링은 지원하지 않음.

```javascript
// before
import OtherCompnent from "./OtherComponent";
// after
const OtherComponent = React.lazy(() => import("./OtherComponent"));
```

- MyComponent가 처음 렌더링 될 때 OtherComponent를 포함한 번들을 자동으로 불러옴.
- React.lazy는 동적 import()를 호출하는 함수를 인자로 가진다. 이 함수는 React Component를 포함해야 하며 default export로 결정되는 모듈을 Promise로 반환해야 함.
- lazy 컴포넌트는 Suspense 컴포넌트 하위에서 렌더링 되야 하며 Suspense는 lazy가 로딩되기를 기다리는 동안 로딩 화면과 같은 예비 화면을 보여준다.

```javascript
import React, { Suspense } from "react";
const OtherComponent = React.lazy(() => import("./OtherComponent"));
const AnotherComponent = React.lazy(() => import("./AnotherComponent"));

function MyComponent() {
  return (
    <div>
      <Suspense fallback={<div>Loading...</div>}>
        <OtherComponent />
        <AnotherComponent />
      </Suspense>
    </div>
  );
}
```

- fallback prop는 컴포넌트가 로드될 때까지 기다리는 동안 렌더링하려는 react 앨리먼트를 보여줌.
- Suspense 컴포넌트는 lazy 컴포넌트를 감싸고 하나의 Suspense 컴포넌트로 여러 lazy 컴포넌트를 감쌀 수 있다.

## Route-based code spliting

- 앱 코드분할을 시작하기 좋은 장소는 라우팅. 웹페이지를 불러오는 시간은 페이지 전환에 어느정도 발생하며 대부분 페이지를 한번에 렌더링하기 때문에 사용자가 페이지를 렌더링하는 동안 다른 요소와 상호작용하지 않는다.

```javascript
import React, { Suspense, lazy } from "react";
import { BrowserRouter as Router, Route, Switch } from "react-router-dom";

const Home = lazy(() => import("./route/Home"));
const About = lazy(() => import("./route/About"));

const App = () => (
  <Router>
    <Suspense fallback={<div>Loading...</div>}>
      <Switch>
        <Route exact path="/" component={Home} />
        <Route path="/about" component={About} />
      </Switch>
    </Suspense>
  </Router>
);
```

## Named Exports

- React.lazy는 현재 default export만 지원. named export를 사용하고자 한다면 default로 이름을 재정의한 중간 모듈을 생성할 수 있음.

```javascript
// ManyComponents.js
export const MyComponent = /*...*/;
export const MyUnUsedComponent = /*...*/;
```

```javascript
// MyComponent.js
export { MyComponent as default } from "./ManyComponents.js";
```

```javascript
// MyApp.js
import React, { lazy } from "react";
const MyComponent = lazy(() => import("./MyComponent.js"));
```
