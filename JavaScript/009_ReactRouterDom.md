# React Router 복습

## React Router 기본

### BrowserRouter

- history API를 이용해 URL과 UI를 동기화

### Route

- 컴포넌트 속성에 설정된 URL과 현재 경로가 일치하면 해당 컴포넌트, 함수를 렌더링

### Link

- to 속성에 설정된 링크로 이동. 이동기록이 history 스택에 저장

### Switch

- 자식 컴포넌트 Route 또는 Redirect 중 첫번째 요소 렌더링.
- Switch를 사용하면 BrowserRouter만 사용할 때와 다르게 하나의 매칭되는 요소만 렌더링 해준다. 사용하지 않을 경우 매칭되는 모두를 렌더링.

### Exact

- 경로가 정확하게 매칭되는 하나의 요소만 렌더링.

### Match

- match는 경로를 통해 매칭되는 정보가 담김
- match.params (JSON Object)
  - 동적인 Url. key와 value 쌍으로 이뤄짐.
  - url path로 전달된 파라미터 객체
- match.isExact
  - 전체 URL과 일치하는지 boolean 값으로 반환.
  - true일 경우 전체 경로가 완전히 일치하는 경우에만 동작 수행
- match.path
  - key값을 포함한 url. 라우터에 정의된 url
- match.url
  - value값을 포함한 url. 실제 클라이언트로부터 요청된 url path

```javascript
{
      path: "/mypage/:userId",
      url:"/mypage/idididid",
      isExact: true,
      params: {
            userId: "idididid"
      }
}
```

### Location

- location 객체는 현재 페이지의 정보를 가지고 있음.
- pathname: [String] 현재 페이지 경로명
- search: [String] 현재 페이지의 query string
- hash : [String] 현재 페이지의 hash

### History

- 객체의 브라우저 history와 유사
- length: [number] 전체 history 스택의 길이
- action: [string] 최근에 수행된 action
- location: [JSON object] 최근 경로 정보
- push: 새로운 경로를 history 스택으로 푸시해 경로 이동
- replace: 최근 경로를 history 스택에서 교체해 경로 이동
- go(n) : history 포인터를 n번째로 이동
- goBack: 이전 페이지로 이동
- goForward: 앞 페이지로 이동
- block: history 스택의 pop/push 제어

## Public Router, Private Router

- Private Router
  - 사용자가 로그인한 경우 해당 구성 요소를 표시
  - 로그인하지 않았을 경우 로그인 화면으로 튕김.
- Public Router
  - 모두에게 공개되는 경로
