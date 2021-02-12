# 객체를 원시형으로 변환하기

- 객체는 논리평가시 true를 반환. 객체는 숫자형이나 문자형으로만 형 변환이 일어남
- 숫자형으로의 형 변환은 객체끼리 빼는 연산을 할 때나 수학 관련 함수를 적용할 때. 객체 Date끼리 차감하면 (date1 - date2) 두 날짜의 시간 차이가 반환됨.
- 문자형으로의 형 변환은 대게 alert(obj)와 같이 객체를 출력하려고 할 때 일어남

## ToPrimitive

- 특수 객체 매서드를 사용하면 숫자형이나 문자형으로의 형 변환을 원하는대로 조절할 수 있음. 객체형 변환은 세 종류로 구분되는데, 'hint'로 불리는 값이 구분 기준. hint는 목표로 하는 자료형 과 비슷한 개념
- "string" : alert함수같이 문자열을 기대하는 연산을 수행할 때

```javascript
alert(obj);
```

- "number" : 수학 연산을 적용할 때

```javascript
// 명시적 형 변환
let num = Number(obj);
// 수학 연산
let n = +obj;
let delta = date1 - date2;
```

- "default" : 연산자가 기대하는 자료형이 확실하지 않을 때 hint는 default. 드물게 발생
- 이항 덧셈연산자 +는 피연산자의 자료형에 따라 문자열을 합치는 연산을 할수도, 숫자를 더하는 연산을 할 수도 있다. + 의 인수가 객체일 때 hint는 default.
- 동등연산자 == 를 사용해 객체-문자, 객체-숫자, 객체-심볼형으로 비교할 때도 객체를 어떤 자료형으로 바꿔야할 지 확신이 안 서므로 hint는 defaul.t
- boolean hint는 없다. 모든 객체는 그냥 true로 평가됨

- 자바스크립트는 형변환이 필요할 때 아래와 같은 알고리즘에 따라 원하는 메서드를 찾고 호출.
- 1. 객체에 `obj[Symbol.toPrimitive](hint)` 메서드가 있는지 찾고, 있다면 메서드를 호출.
- 2. 1에 해당하지 않고 hint가 string이라면, obj.toString()이나 obj.valueOf()를 호출.
- 3. 1,2에 해당하지 않고 hint가 number나 default라면 obj.valueOf()나 obj.toString()을 호출.

## Symbol.toPrimitive

- 자바스크립트엔 Symbol.toPrimitive라는 내장 심볼이 존재하는데, 이 심볼은 목표로 하는 자료형(hint)를 명명하는데 사용.

```javascript
let user = {
  name: "John",
  money: 1000,
  [Symbol.toPrimitive](hint) {
    alert(`hint: ${hint}`);
    return hint == "string" ? `{name: "${this.name}"` : this.money;
  },
};

// 데모:
alert(user); // hint: string -> {name: "John"}
alert(+user); // hint: number -> 1000
alert(user + 500); // hint: default -> 1500
```

## toString과 valueOf

- hint가 string인 경우 : toString -> valueOf순.
- 그 외 : valueOf -> toString순
- 이 메서드들은 반드시 원시값을 반환해야 함. toString이나 valueOf가 객체를 반환하면 그 결과는 무시됨. 일반 객체는 기본적으로 toString과 valueOf에 적용되는 규칙을 따름
- toString은 문자열 "[object object]"를 반환.
- valueOf는 객체 자신을 반환.

## 반환타입

- 위 세개의 메서드는 hint에 명시된 자료형으로의 형 변환을 보장해주지 않음.
- toStirng()이 항상 문자열을 반환하리라는 보장이 없고, Symbol.toPrimitive의 hint가 number일 때 항상 숫자형 자료가 반환된다는 보장 없음.

## 추가형 변환

- 곱셈을 해주는 `*`는 피연산자를 숫자형으로 반환시킴.
- 객체가 피연산자일 때는 다음과 같은 단계를 거쳐 형 변환이 일어남
- 1. 객체는 원시형으로 변화. 변환 후 원시값이 원하는 형이 아닌 경우 또 다시 형 변환이 일어남.
