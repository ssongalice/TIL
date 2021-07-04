# React 렌더링 과정

- 질문 의도 : 리액트 라이프사이클을 이해하고 있는가?

- 리액트 가상돔: 리엑트에서 데이터 변경에 의한 화면 업데이트는 렌더 단계와 커밋 단계를 거침

  - 렌더 단계 : 실제 돔에 반영할 변경 사항을 파악하는 단계
  - 커밋 단계 : 파악된 변경사항을 실제 돔에 반영
  - 리액트는 렌더링 할 때마다 가상 돔을 만들고 이전의 가상돔과 비교하면서 변경사항이 있으면 해당 사항을 실제 돔에 반영

- 생명주기(lifecycle) 메소드는 무엇인가요?

  클래스 기반 컴포넌트는 그들이 mount(DOM에 렌더링)되었을 때, unmount될 때 등과 같이 그들의 생명주기 중 특정한 시점에 호출되는 특별한 메소드를 선언할 수 있음. 이는 예를 들면 컴포넌트가 필요로 하는 것을 셋팅 및 해제하거나, 타이머를 설정하거나 브라우저 이벤트에 바인딩하는 데 유용.

  componentWillMount: 컴포넌트가 생성된 후 DOM에 렌더링되기 전에 호출됩니다.
  componentDidMount: 처음으로 렌더링이 끝나고 컴포넌트의 DOM 엘리먼트가 사용 가능할 때 호출됩니다.
  componentWillReceiveProps: props가 업데이트 될 때 호출됩니다.
  shouldComponentUpdate: 새로운 props를 받았을 때 호출되며, 성능 최적화를 위해 리랜더링을 막을 수 있습니다.
  componentWillUpdate: 새로운 props를 받았고 shouldComponentUpdate가 true를 리턴할 때 호출됩니다.
  componentDidUpdate: 컴포넌트가 업데이트된 후에 호출됩니다.
  componentWillUnmount: 컴포넌트가 DOM에서 제거되기 전에 호출되어 이벤트리스너 등을 정리할 수 있게 해줍니다.

---

참고

- [https://imkev.dev/react-rendering-order](https://imkev.dev/react-rendering-order)
- [https://it-eldorado.tistory.com/83](https://it-eldorado.tistory.com/83)
- [https://www.zerocho.com/category/React/post/579b5ec26958781500ed9955](https://www.zerocho.com/category/React/post/579b5ec26958781500ed9955)
- [https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)
- [https://ooeunz.tistory.com/138](https://ooeunz.tistory.com/138)
