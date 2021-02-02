# while과 for 반복문

## while 반복문

```javascript
while (condition) {
  // 코드
}
```

- condition(주어진 조건)이 truthy이면 반복문 본문의 코드가 실행됨.

## do...while 반복문

```javascript
do {
  // 본문
} while (condition);
```

- 본문이 먼저 실행되고 condition을 확인 후 조건이 truthy인 동안 본문이 계속 실행됨.
- do..while 문법은 조건이 truthy인지 아닌지에 상관없이 본문을 최소한 한번이라도 실행하고 싶을 때만 사용해야 함.

## for 반복문

```javascript
for (begin; condition; step) {
  // 반복문 본문
}
```

- begin: 반복문에 진입할 때 단 한번 실행
- condition : 반복마다 해당 조건이 확인됨. false면 반복문 멈춤
- body: condition이 truthy일 동안 계속 실행
- step: 각 반복의 body가 실행된 이후에 실행됨.
- for문의 구성요소를 생략하는 것도 가능. 모든 구성요소를 생략하면 무한반복문

```javascript
for (;;) {
  // 무한반복
}
```

## 반복문 빠져나오기

- 반복문의 조건이 falsy가 되면 반복문 종료
- break를 사용하면 빠져나올 수 있음.

```javascript
let sum = 0;

while (true) {
  let value = +prompt("숫자를 입력하세요.", "");

  if (!value) break; // (*)

  sum += value;
}
alert("합계: " + sum);
```

## 다음 반복문으로 넘어가기

- continue의 지시자는 break의 가벼운 버전. continue는 전체 반복문을 멈추지 않고 현재 실행 중인 이터레이션을 멈추고 반복문이 다음을 차례대로 실행하도록 함.

```javascript
for (let i = 0; i < 10; i++) {
  // 조건이 참이라면 실행되지 않음
  if (i % 2 === 0) continue;
  alert(i); // 1,3,5,7,9
}
```

- ? 오른쪽엔 break나 continue가 올 수 없다.
- break 나 continue 같은 지시자는 삼항 연산자에 사용하면 안됨.

## break/continue와 레이블

- 레이블은 반복문 앞에 콜론과 함께 쓰이는 식별자

```javascript
labelName: for (...) {
      // code
}
```

- 반복문 안에서 break labelName 문을 사용하면 레이블에 해당하는 반복문을 빠져나올 수 있음

```javascript
outer: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    let input = prompt(`(${i},${j})의 값`, "");

    // 사용자가 아무것도 입력하지 않거나 Cancel 버튼을 누르면 두 반복문 모두를 빠져나옵니다.
    if (!input) break outer; // (*)

    // 입력받은 값을 가지고 무언가를 함
  }
}
alert("완료!");
```

### 과제

- 반복문의 마지막 값

```javascript
let i = 3;

while (i) {
  alert(i--); // 1
}
```

- while 반복문의 출력값 예상하기

```javascript
// 1.
let i = 0;
while (++i < 5) alert(i); // 1,2,3,4 -> 0,1,2,3,4
// 2.
let i = 0;
while (i++ < 5) alert(i); // 0,1,2,3,4,
```

- 'for' 반복문의 출력값 예상하기

```javascript
// 1.
for (let i = 0; i < 5; i++) alert(i); // 0,1,2,3,4,
// 2.
for (let i = 0; i < 5; ++i) alert(i); // 0,1,2,3,4,
```

- for 반복문을 이용하여 짝수 출력하기 : 2~10까지의 숫자 중 짝수만

```javascript
for (let i = 2; i < 11; i++) {
  if (i % 2 === 1) continue;
  alert(i);
}
```

- 'for' 반복문을 'while' 반복문으로 바꾸기

```javascript
// for문
for (let i = 0; i < 3; i++) {
  alert(`number ${i}!`);
}

// while문
let i = 0;
while (i < 3) {
  alert(`number ${i}!`);
  i++;
}
```

- 소수 출력하기

```javascript
let n = Math.floor(Math.random());

for (i = 2; i < n; i++) {
  if (n % i === 0) continue;
  alert(i);
}
```
