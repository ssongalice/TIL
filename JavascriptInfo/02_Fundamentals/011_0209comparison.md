# 2.9 비교연산자

### 불린형 반환

- true가 반환되면 긍정, false가 반환되면 거짓
- 반환된 불린값은 다른 값처럼 변수에 할당할 수 있다.

### 문자열 비교

- 자바스크립트는 유니코드 순으로 문자열을 비교
- 대소문자 구분함. 대문자 A와 소문자 a를 비교했을 때 a가 더 크다

### 다른 형을 가진 값 간의 비교

- 비교하려는 값의 자료형이 다르면 자바스크립트는 이 값을 모두 숫자형으로 바꾼다.
- 불린값의 경우 true = 1, false = 0 으로 변환 후 비교

```javascript
alert("2" > 1); // true, 문자열 2가 숫자형으로 변환 후 비교 -> true
alert("01" == 1); // true 문자열 01이 숫자형 1 로 변환 후 비교 -> true
```

### 일치연산자

- `==`는 0과 false, ''를 구분하지 못한다.
- 일치연산자 `===`를 사용하면 형 변환 없이 갑 비교 가능
- 일치연산자는 자료형의 동등여부까지 비교하기 때문에. ===의 반대는 !==

### null이나 undefined와 비교하기

- ===를 사용해 null과 Undefined비교

```javascript
alert(null === undefined); // false
```

- ==를 사용해 Null과 Undefined 비교

```javascript
alert(null == undefined); // true
```

- 산술연산자나 기타 비교 연산자 < > <= =>를 사용해 Null과 undefined qlry
- null은 0, undefined는 NaN

- null vs 0
  - ==는 undefined나 null일 때 형변환을 하지 않음. undefined와 null을 비교하는 경우에만 true를 반환, 그 이외의 경우는 무조건 false

```javascript
alert(null > 0); // false
alert(null == 0); //false
alert(null >= 0); //true
```

- 비교가 불가능한 undefined

```javascript
alert(undefined > 0); // false
alert(undefined < 0); // false
alert(undefined == 0); // false
```

### 과제

```javascript
5 > 4; // true
"apple" > "pineapple"; // false
"2" > "12"; // false -> true (두 피연산자는 문자열이므로 사전순으로 비교됨. 첫번째 글자인 2가 1보다 크다 )
undefined == null; // false -> true
undefined === null; // false
null == "\n0\n"; // false
null === +"\n0\n"; // true  -> false (형이 다르므로 )
```
