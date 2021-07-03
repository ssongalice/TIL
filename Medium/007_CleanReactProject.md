# 21 Best Practices for a Clean React Project

### 1. JSX ShortHand 사용하기

```javascript
// Bad
return <Navbar showTitle={true} />;

// Good
return <Navbar showTitle />;
```

### 2. 삼항 연산자 사용하기

```javascript
// Bad
const { role } = user;
if (role === ADMIN) {
  return <AdminUser />;
} else {
  return <NormalUser />;
}

// Good
const { role } = user;
return role === ADMIN ? <AdminUser /> : <NormalUser />;
```

### 3. Object Literals의 장점 취하기

```javascript
// Bad
const { role } = user;

switch (role) {
  case ADMIN:
    return <AdminUser />;
  case EMPLOYEE:
    return <EmployeeUser />;
  case USER:
    return <NormalUser />;
}

// Good
const { role } = user;

const components = {
  ADMIN: AdminUser,
  EMPLOYEE: EmployeeUser,
  USER: NormalUser,
};

const Component = components[role];

return <Component />;
```

### 4. Fragment 사용하기

```javascript
// Bad
return (
  <div>
    <Component1 />
    <Component2 />
    <Component3 />
  </div>
);

// Good
return (
  <>
    <Component1 />
    <Component2 />
    <Component3 />
  </>
);
```

### 5. Render 안에 함수 선언 하지 않기

```javascript
// Bad
return (
  <button onClick={() => dispatch(ACTION_TO_SEND_DATA)}>
    This is a bad example
  </button>
);

// Good
const submitData = () => dispatch(ACTION_TO_SEND_DATA);

return <button onClick={submitData}>This is a good example</button>;
```

### 6. Memo 사용하기

- memo를 사용하면 불필요한 렌더링을 줄일 수 있음

```javascript
// Bad
import React, { useState } from "react";

export const TestMemo = () => {
  const [userName, setUserName] = useState("faisal");
  const [count, setCount] = useState(0);
  const increment = () => setCount((count) => count + 1);
  return (
    <>
      <ChildrenComponent userName={userName} />
      <button onClick={increment}>Increment</button>
    </>
  );
};

const ChildrenComponent = ({ userName }) => {
  console.log("rendered", userName);
  return <div>{userName} </div>;
};

// 이렇게 코드를 짜면 userName이 변하지 않더라도 버튼을 클릭할 때마다 ChildrenComponent가 렌더링된다
```

```javascript
// Good
import React, { useState } from "react";

const ChildrenComponent = React.memo(({ userName }) => {
  console.log("rendered", userName);
  return <div>{userName} </div>;
});
```

### 7. CSS 를 JS에 넣기

- 리액트 앱을 만들 때 깡으로 자바스크립트를 쓰지 않는다. CSS를 구성하는 게 JS를 구성하는 것보다 어렵기 때문

```javascript
// Bad
/// CSS
.body {
      height: 10px;
}

/// jsx
return <div className="body"></div>

// Good
const bodyStyle = {
      height: "10px"
};

return <div style={bodyStyle}></div>
```

### 8. Object Destructuring 활용하기

```javascript
// Bad
return (
  <>
    <div>{user.name}</div>
    <div>{user.age}</div>
    <div>{user.profession}</div>
  </>
);

// Good
const { name, age, profession } = user;
return (
  <>
    <div>{name}</div>
    <div>{age}</div>
    <div>{profession}</div>
  </>
);
```

### 9. 문자열 {}로 감싸지 않기

```javascript
// Bad
return <Navbar title={"My app"} />;
// Good
return <Navbar title="My App" />;
```

### 10. JSX에 이유없는 JS 코드 제거하기

```javascript
// Bad
return (
  <ul>
    {posts.map((post) => (
      <li
        onClick={(event) => {
          console.log(event.target, "clicked!");
        }}
        key={post.id}
      >
        {post.title}
      </li>
    ))}
  </ul>
);

// Good
const onClickHandler = (event) => {
  console.log(event.target, "clicked!");
};

return (
  <ul>
    {posts.map((post) => (
      <li onClick={onClickHandler} key={post.id}>
        {post.title}
      </li>
    ))}
  </ul>
);
```

### 11. 템플릿 리터럴 사용하기

```javascript
// Bad
const userDetails = user.name + "'s profession is" + user.profession;
return <div>{userDetails}</div>;

// Good
const userDetails = `${user.name}'s profession is ${user.profession}`;

return <div>{userDetails}</div>;
```

### 12. 순서에 맞는 Import

- Import할 때 순서는 다음과 같이 하는게 좋다
  - Built-in
  - External
  - Internal

```javascript
// Bad
import React from "react";
import ErrorImg from "../../assets/images/error.png";
import styled from "styled-components/native";
import colors from "../../styles/colors";
import { PropTypes } from "prop-types";

// Good
import React from "react";

import { PropTypes } from "prop-types";
import styled from "styled-components/native";

import ErrorImg from "../../assets/images/error.png";
import colors from "../../styles/colors";
```

### 13. return 함축하기

```javascript
// Bad
const add = (a, b) => {
  return a + b;
};

// Good
const add = (a, b) => a + b;
```

### 14. 컴포넌트 이름에는 PascalCase 쓰기

```javascript
// Bad
import reservationCard from './ReservationCard';

// Good
import ReservationCard from './ReservationCard';

const reservationItem = <ReservationCard>;
```

### 15. Prop 이름 전달하기

- Props를 전달할 때 DOM 컴포넌트를 구성하는 props는 사용하지 않는다

```javascript
// Bad
<MyComponent style="dark"/>
<MyComponent className="dark"/>

// Good
<MyComponent variant="fancy"/>
```

### 16. 따옴표

- JSX 속성에만 쌍따옴표를 사용하고 나머지에서는 전부 홑따옴표를 쓴다

```javascript
// Bad
<Foo bar='bar' />
<Foo style={{ left: "20px" }} />

// Good
<Foo bar="bar" />
<Foo style={{ left: '20px';}} />
```

### 17. Prop 이름

- Prop 이름으로는 camelCase를 쓰거나 prop 값이 리액트 컴포넌트일 경우 PascalCase를 쓴다

```javascript
// Bad
<Component UserName="hello" phone_number={1234567} />

// Good
<MyComponent
  userName="hello"
  phoneNumber={1234567}
  Component={SomeComponent}>
```

### 18. 괄호 감싸기

- 컴포넌트가 1줄 이상일 경우 항상 괄호로 감싼다

```javascript
// Bad
return (
  <MyComponent variant="long">
    <MyChild />
  </MyComponent>
);

// Good
return (
  <MyComponent variant="long">
    <MyChild />
  </MyComponent>
);
```

### 19. Self-Closing Tags

- 컴포넌트가 자식 요소를 가지고 있지 않을 경우 셀프 클로징 태그를 사용한다.

```javascript
// Bad
<SomeComponent variant="stuff"></SomeComponent>

// Good
<SomeComponent variant="stuff" />
```

### 20. 함수명에 \_ 사용 금지

```javascript
// Bad
const _onClickHandler = () => {};

// Good
const onClickHandler = () => {};
```

### 21. Alt 포함하기

- img 태그에 alt를 포함하고 alt를 적을 때에는 이미지나 사진 같은 단어를 사용하지 않는다.

```javascript
// Bad
<img src="hello.jpg" alt="Picture of me rowing a boat" />
// Good
<img src="hello.jpg" alt="Me waving hello" />
```

---

- [원문링크](https://betterprogramming.pub/21-best-practices-for-a-clean-react-project-df788a682fb)
