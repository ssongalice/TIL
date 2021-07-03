# RequestAnimationFrame

## window.requestAnimationFrame()

- 브라우저에게 수행하기를 원하는 이벤트를 알리고 다음 리페인트가 진행되기 전 해당 애니메이션을 업데이트하는 함수를 호출하게 된다.
  - 리페인팅? HTML 문서의 전체 또는 일부 영역의 스타일이 변경됐을 때 브라우저가 변경된 스타일을 다시 적용하는 작업
- window.requestAnimationFrame함수는 비동기 함수. 스스로를 반복호출하지 않기 때문에 함수를 반복하려면 재귀적으로 자신을 스스로 다시 호출해야 함.
- requestAnimationFrame은 애니메이션을 위한 함수로 기본적으로 1초당 60번, 보통 모니터의 주사율에 맞춰 함수를 실행한다.
- 애니메이션을 종료할 때는 cancelAnimationFrame 함수를 사용한다.

## requestAnimationFrame과 setInterval의 차이

- setTimeout, setInterval을 이용해서도 animation 구현이 가능하다. 하지만 이벤트 콜벡의 지연으로 정해진 시간에 함수가 실행된다는 것을 보장할 수 없다. setTimeout, setInterval을 사용할 경우 다음과 같은 이슈 발생
  - animation 주기가 짧아 불필요한 프레임 생성
  - 주기가 너무 길어져 매끄럽지 못한 경우
- setTimeout과 다르게 콜백함수는 실행 시점을 timestamp값을 파라미터로 전달받아 애니메이션을 구현할 수 있다.
