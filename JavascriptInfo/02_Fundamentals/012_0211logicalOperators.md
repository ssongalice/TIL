# 논리 연산자

## || (OR)

- 인수 중에 하나라도 true면 true 반환
- || 연산자는 주로 if문에서 사용. 주어진 값 중 하나라도 true라면 true 실행

### 첫 번째 truthy를 찾는 연산자 OR '||'

```javascript
result = value1 || value2 || value3;
```

- OR 연산자는 다음 순서에 따라 연산 수행
- 가장 왼쪽부터 순서대로 피연산자를 평가.
- 각 피연산자를 불린형으로 반환해 변환 후 그 값이 true이면 연산을 멈추고 해당 피연산자의 변환 전 원래값을 반환.
- 피연산자를 모두 평가한 경우 모두 false 일 경우 마지막 피연산자를 반환

- 단락평가 : 왼쪽부터 오른쪽으로 차례대로 진행하는데 truthy를 만나면 나머지 값들은 건드리지 않고 평가를 멈춤.
- 단락평가는 왼쪽 명령어가 falsy일 때만 명령어를 실행할 때 자주 사용

## && (AND)

- 두 연산자가 모두 참일 때 true 반환. 그 외라면 false

### 첫 번째 falsy를 찾는 연산자 '&&'

```javascript
result = value1 && value2 && value3;
```

- 가장 왼쪽부터 순서대로 피연산자를 평가.
- 각 피연산자는 불린형으로 반환. 변환 후 값이 false이면 연산을 멈추고 피연산자의 변환 전 원래 값을 반환.
- 피연산자를 모두 평가한 경우 모두 true일 경우 마지막 피연산자를 반환
- &&의 우선순위가 ||보다 높다.

## ! (NOT)

- 피연산자를 불린형으로 반환. 반환된 값의 반대를 반환
- NOT을 !! 연속으로 쓰면 값을 불린형으로 반환 가능.

### 과제

- 다음 OR 연산의 결과는 무엇일까요?

```javascript
alert(null || 2 || undefined); // 2
```

- OR 연산자의 피연산자가 alert 라면??

```javascript
alert(alert(1) || 2 || alert(3)); // 1,2
```

- 다음 AND 연산의 결과는 무엇일까요?

```javascript
alert(1 && null && 2); // null
```

- AND 연산자의 피연산자가 alert 라면?

```javascript
alert(alert(1) && alert(2)); // alert(true) -> 1, undefined alert는 undefined를 반환
```

- OR AND OR 연산자로 구성된 표현식

```javascript
alert(null || (2 && 3) || 4); // 4 -> 3: &&의 우선순위는 || 보다 높다.
```

- 사이 범위 확인하기

```javascript
/* age(나이)가 14세 이상 90세 이하에 속하는지를 확인하는 if문을 작성하세요.

"이상과 이하"는 age(나이) 범위에 14나 90이 포함된다는 의미입니다.*/

if (age >= 14 && age <= 90) {
}
```

- 바깥 범위 확인하기

```javascript
/* age(나이)가 14세 이상 90세 이하에 속하지 않는지를 확인하는 if문을 작성하세요.

답안은 NOT ! 연산자를 사용한 답안과 사용하지 않은 답안 2가지를 제출해 주세요. */

if (age < 14 && age > 90) {
}
if (!(age >= 14) && !(age <= 90)) {
} // -> !(age>=14 && age <=90)
```

- "if"에 관한 고찰

```javascript
if (-1 || 0) alert("first"); // X 둘다 거짓이므로 아무일도 일어나지 않음 -> -1 과 0은 -1이므로 truthy
if (-1 && 0) alert("second"); // 0이므로 falsy
if (null || (-1 && 1)) alert("third"); // null || 1  ->  1 -> true
```
