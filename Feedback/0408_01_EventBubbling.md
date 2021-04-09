# Event Bubbling and Capturing

## 버블링 (Bubbling)

- 한 요소에 이벤트가 발생하면 요소에 할당된 핸들러가 동작하고, 이어서 부모 요소의 핸들러가 동작. 가장 최상단의 조상 요소를 만날 때 까지 이 과정이 반복되면서 요소 각각의 핸들러가 동작함.
- 몇몇 이벤트를 제외하고 대부분의 이벤트는 버블링됨.

### event.target

- 부모 요소의 핸들러는 이벤트가 정확히 어디서 발생했는지 자세한 정보를 얻을 수 있음
- 이벤트가 발생한 가장 안쪽의 요소는 타겟(target) 요소로 불리고, event.target을 사용해 접근할 수 있다.
- `event.target`과 `this(=event.currentTarget)`의 차이
  - event.target은 실제 이벤트가 시작된 타깃 요소. 버블링이 진행되도 변하지 않는다
  - this는 현재 요소. 현재 실행중인 핸들러가 할당된 요소를 참조

### 버블링 중단하기

- 이벤트 버블링은 타깃 이벤트에서 시작해 html 요소를 거쳐 document 객체를 만날 때까지 각 노드에서 모두 발생.
- `event.stopPropagation()` : 이벤트 버블링 중단 명령
  - event.stopPropagation은 위쪽으로 일어나는 버블링은 막아주지만 다른 핸들러의 동작은 막아주지 못함
  - 버블링을 멈추고 다른 핸들러의 동작을 막으려면 `event.stopImmediatePropagation()`을 사용해야 함.

## 캡쳐링 (Capturing)

- 표준 DOM 이벤트에서 정의한 이벤트 흐름은 3가지가 있다.

  - 캡쳐링 단계 : 이벤트가 하위 요소로 전파되는 단계
  - 타깃 단계 : 이벤트가 실제 타깃 요소에 전달되는 단계
  - 버블링 단계 : 이벤트가 상위 요소로 전파되는 단계

- `on<event>` 프로퍼티나 HTML 속성, `addEventListener(event, handler)`를 이용해 할당된 핸들러는 캡쳐링에 대해 전혀 알 수 없음. 이 핸들러들은 두 번째 혹은 세 번째 단계의 이벤트 흐름에서만 동작
  - 캡쳐링 단계에서 이벤트를 잡아내려면 `addEventListener`의 `capture` 옵션을 true로 설정해야 함

```javascript
elem.addEventListener(..., {capture: true})
// 또는
elem.addEventListener(..., true)
```

- capture 옵션은 두 가지 값을 가짐
  - false : 핸들러는 버블링 단계에서 동작
  - true: 핸들러는 캡쳐링 단계에서 동작
- `event.eventPhase` 프로퍼티를 이용하면 현재 발생중인 이벤트 흐름의 단계를 알 수 있음. 반환되는 정수값에 따라 이벤트 흐름의 현재 실행 단계를 구분할 수 있음.

## 이벤트 위임 (Event delegation)

- 이벤트 위임은 비슷한 방식으로 여러 요소를 다뤄야 할 때 사용.
- 이벤트 위임을 사용하면 요소마다 핸들러를 할당하지 않고 요소의 공통 조상에 이벤트 핸들러를 하나만 할당해도 여러 요소를 한꺼번에 다룰 수 있다.
- 이벤트 위임의 장점

  - 많은 핸들러를 할당하지 않아도 되기 때문에 초기화가 단순해지고 메모리가 절약됨
  - 요소를 추가하거나 제거할 때 해당 요소에 할당된 핸들러를 추가하거나 제거할 필요가 없어 코드가 짧아짐
  - innerHTML이나 유사한 기능을 하는 스크립트로 요소 덩어리를 더하거나 뺄 수 있기 때문에 DOM 수정이 쉬워짐

- 이벤트 위임의 단점

  - 이벤트 위임을 사용하려면 이벤트가 반드시 버블링 돼야 한다. 하지만 몇몇 이벤트는 버블링 되지 않고 낮은 레벨에 할당한 핸들러엔 event.stopPropagation()을 쓸 수 없음.

- 예시
  - 각 버튼마다 독립된 핸들러를 할당하는 게 아니라 메뉴 전체에 핸들러를 추가해주고 각 버튼의 data-action 속성에 호출할 메서드를 할당.

```html
<div id="menu">
  <button data-action="save">저장하기</button>
  <button data-action="load">불러오기</button>
  <button data-action="search">검색하기</button>
</div>
```

```javascript
class Menu {
  constructor(elem) {
    this._elem = elem;
    elem.onclick = this.onClick.bind(this);
  }

  save() {
    alert("저장하기");
  }
  load() {
    alert("불러오기");
  }
  search() {
    alert("검색하기");
  }
  onClick(event) {
    let action = event.target.dataset.action;
    if (action) {
      this[action]();
    }
  }
}

new Menu(menu);
```

### '행동' 패턴

- 이벤트 위임은 요소에 선언적 방식으로 '행동'을 추가할 때 사용할 수 있음.
- 행동 패턴은 두 부분으로 구성됨
  - 요소의 행동을 설명하는 커스텀 속성을 요소에 추가
  - 문서 전체를 감지하는 핸들러가 이벤트를 추적하게 함. 1에서 추가한 속성이 있는 요소에 이벤트가 발생하면 작업을 수행
