# Redux Toolkit 기본

## Redux란?

- Redux의 공식 개발도구.

## 리덕스에 포함되는것

### `configureStore()`

### `createReducer()`

- switch문을 작성하지 않고 reducer 함수 작성을 할 수 있게 해줌.
- 간단하게 불변성을 유지하면서 상태를 업데이트 할 수 있다.

### `createAction()`

- 주어진 action type에 따라 action create 함수를 반환.
- 함수 자체에 `toString()`이 정의돼있어 별도의 상수를 선언할 필요 없이 함수 이름 사용 가능

### `createSlice()`

- 리듀서 함수 세트. 슬라이스 이름 및 초기 상태값을 받아서 자동으로 slice reducer, action creator, action types 생성

```javascript
import { createSlice } from "@reduxjs/toolkit";

const initialState = { value: 0 };

const counterSlice = createSlice({
  name: "counter",
  initialState,
  reducers: {
    increment(state) {
      state.value++;
    },
    decrement(state) {
      state.value--;
    },
    incrementByAmount(state, action) {
      state.value += action.payload;
    },
  },
});

// 액션
export const { increment, decrement, incrementByAmount } = counterSlice.actions;
// 리듀서
export default counterSlice.reducer;
```

- 선언한 action 이 dispatch 되면 바로 state를 가지고 해당 action을 처리함.

### `createSelector()`

- Reselect 라이브러리를 사용하기 쉽도록 re-export 한것.

## 리덕스와 관련된 대략적인 개념

### 액션 (Action)

- 상태에 어떤 변화가 필요할 때 발생시키는 것. 액션 객체는 반드시 type을 가지고 있어야 함.

### 리듀서 (Reducer)

- 현재의 상태와 전달받은 액션을 참고해 새로운 상태를 만들어서 반환.

### 스토어 (Store)

- 현재의 앱 상태, 리듀서가 들어가 있는 곳

### 디스패치 (Dispatch)

- 스토어 내장함수. 액션을 발생시킨다. 액션을 파라미터로 전달. `dispatch(action)`
- 호출하면 스토어가 리듀서 함수를 실행시킴. 해당 액션을 참고해 새로운 상태를 생성.

### 구독 (Subscribe)

- 스토어 내장함수. 함수 형태의 값을 파라미터로 받아옴.
- subscribe에 특정 함수를 전달하면 액션이 디스패치 될 때마다 전달해준 함수가 호출된다.
