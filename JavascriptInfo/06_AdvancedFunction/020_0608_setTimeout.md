# setTimeout과 setInterval을 이용한 호출 스케쥴링

- 호출 스케줄링(scheduling a call) : 일정 시간이 지난 후 원하는 함수를 예약 실행할 수 있게 하는 것
- setTimeout을 이용해 일정 시간이 지난 후 함수를 실행하는 법
- setInterval을 이용해 일정 시간 간격을 두고 함수를 실행하는 법

## setTimeout

```javascript
let timerId = setTimeout(func|code, [delay], [arg1], [arg2], ...)
```

- func|code : 실행하고자 하는 코드. 주로 함수가 들어감
- delay : 실행 전 대기시간. 단위는 밀리초. 기본값 0
- arg1, arg2.. : 함수에 전달할 인수. IE9 이하에선 지원하지 않음.

```javascript
function sayHi() {
  alert("안녕하세요");
}
setTimeout(sayHi, 1000);
// 잘못된 코드
setTimeout(sayHi(), 1000);
```

- setTimeout에 함수를 넘길 때 함수 뒤에 ()를 붙이면 안됨. 이렇게 전달하면 함수 실행결과가 전달됨. sayHi()에는 반환문이 없으므로 호출 결과는 Undefined

## clearTimeout으로 스케줄링 취소하기

- setTimeout을 호출하면 타이머 식별자가 반환됨. 스케줄링을 취소하고 싶을 땐 이 식별자를 사용하면 됨.

```javascript
const timerId = setTimeout(...);
clearTimeout(timerId)
```

## setInterval

```javascript
let timerId = setInterval(func|code, [delay], [arg1], [arg2]...)
```

- setTimeout은 함수를 한번만 실행하지만 setInterval은 함수를 주기적으로 실행
- 함수 호출을 중단하려면 clearInterval(timerId)를 사용하면 됨

```javascript
// 2초 간격으로 메시지를 보여줌
let timerId = setInterval(() => alert("째깍"), 2000);

// 5초 후에 정지
setTimeout(() => {
  clearInterval(timerId);
  alert("정지");
}, 5000);
```

## 중첩 setTimeout

- 중첩 setTimeout을 이용하는 방법은 지연간격을 보장하지만 setInterval은 이를 보장하지 않음
- 중첩 setTimeout을 사용하면 지연간격이 보장되는 이유는 이전 함수의 실행이 종료된 이후에 다음 함수 호출에 대한 계획이 세워지기 때문.

```javascript
const delay = 5000;

let timerId = setTimeout(function request() {
      // 요청 보내기
      if (서버 과부하로 인한 요청 실패) {

            // 요청 간격을 늘림
            delay *=2 ;
      }
      timerId = setTimeout(request, delay);
}, delay);
```

## 대기시간이 0인 setTimeout

- setTimeout(func, 0) 이나 setTimeout(func)를 사용하면 setTimeout의 대기 시간을 0으로 설정할 수 있음.
- 대기시간을 0으로 설정하면 func를 가능한 빨리 실행할 수 있습니다. 다만 스케줄러는 현재 실행중인 스크립트의 처리가 종료된 이후 스케줄링한 함수를 실행.
- 이런 특징을 이용하면 현재 스크립트의 실행이 종료된 직후 원하는 함수가 실행될 수 있게 함.

## 과제

- 일초 간격으로 숫자 출력하기

```javascript
// setInterval을 이용한 방법
function printNumbers(from, to) {
  let current = from;
  let timerId = setInterval(function () {
    alert(current);
    if (current == to) {
      clearInterval(timerId);
    }
    current++;
  }, 1000);
}
```
