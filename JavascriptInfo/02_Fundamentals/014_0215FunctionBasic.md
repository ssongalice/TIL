# 함수

## 함수 선언

- 함수 선언문. `function fnName()` 형식으로 써주면 함수를 선언할 수 있음.
- 새롭게 정의한 함수는 함수 이름 옆에 괄호를 붙여 호출할 수 있음.

```javascript
function fnName(parameters) {
      ...함수 본문...
}
```

## 지역 변수, 외부 변수

- 함수 내에서 선언한 변수인 지역 변수는 함수 안에서만 접근 가능.
- 함수 내부에서 함수 외부의 변수인 외부 변수에 접근할 수 있음.
- 함수 내부에 외부 변수와 이름이 동일한 변수가 선언됐다면 내부 변수는 외부 변수를 가림.

## 매개변수

- 매개변수를 이용하면 임의의 데이터를 함수 안에 전달할 수 있음.
- 매개변수에 값을 전달하지 않으면 그 값은 undefined.
- 자바스크립트에선 함수를 호출할 때마다 매개변수 기본값을 평가.

```javascript
function showMessage(from, text) {
      alert(from + ':' + text);
}

// 기본값을 할당한다면
function showMessage(from, text = "no text given") {
      ...fn...
}
```

- 매개변수 기본값을 설정할 수 있는 또 다른 방법.

```javascript
// 매개변수가 생략됐거나 빈 문자열이 넘어오면 변수에 빈 문자열이 할당됨.
function showMessage(text) {
  text = text || "빈 문자열";
}

// 매개변수 count가 넘어오지 않으면 'unknown'을 출력해주는 함수
```

## 반환값

- 함수를 호출했을 때 함수를 호출한 그곳에 특정 값을 반환하게 할 수 있음.
- 지시자 return은 함수 내 어디서든 사용 가능. 실행 흐름이 return을 만나면 함수 실행은 즉시 중단되고 함수를 호출한 곳에 값을 반환.

```javascript
function checkAge(age) {
  if (age >= 18) {
    return true;
  } else {
    return confirm("보호자 동의를 받으셨나요?");
  }
}

let age = prompt("나이를 알려주세요", 18);
if (checkAge(age)) {
  alert("접속허용");
} else {
  alert("접속차단");
}
```

- return 문이 없거나 return 지시자만 있는 함수는 undefined를 반환. return은 return undefined와 동일하게 작동.

## 함수 이름짓기

- 함수가 어떤 동작을 하는지 축약해서 설명해주는 동사를 접두어로 붙여 함수 이름을 붙인다.
- 예시
- show: 무언가를 보여줌
- get : 값을 반환
- calc: 값을 계산
- create: 무언가를 생성
- check: 무언가를 확인하고 불린값 반환

- 함수는 함수 이름에 언급된 동작을 정확히 수행해야 함. 그 외의 동작은 수행해선 안된다.

## 과제

- '?'나 '||'를 사용하여 함수 다시 작성하기

```javascript
// 문제
function checkAge(age) {
  if (age > 18) {
    return true;
  } else {
    return confirm("보호자의 동의를 받으셨나요?");
  }
}
// 답
function checkAge(age) {
  return age > 18 ? true : confirm("보호자의 동의를 받으셨나요");
}

function checkAge(age) {
  return age > 18 || confirm("보호자의 동의를 받으셨나요?");
}
```

- min(a, b) 함수 만들기

```javascript
function min(a, b) {
  return a - b < 0 ? a : b;
}
min(2, 5) == 2;
min(3, -1) == -1;
min(1, 1) == 1;
```

- pow(x,n) 함수 만들기

```javascript
function pow(x,n) {
      if ( x <= 1) {
            return alert("자연수를 입력하세요")
      }

      let xpow= x;
      for ( let x = 1; x < n+1; x++) {
            xpow = xpow * x
      }
      return xpow;
}

pow(3, 2) = 3 * 3 = 9
pow(3, 3) = 3 * 3 * 3 = 27
pow(1, 100) = 1 * 1 * ...* 1 = 1
```
