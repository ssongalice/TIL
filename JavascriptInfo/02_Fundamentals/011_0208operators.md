# 2.8 기본 연산자와 수학

### 나머지 연산자 %

- 나머지 연산자를 사용한 표현식 `a % b`는 a를 b로 나눈 후 그 나머지를 정수로 반환.

### 거듭제곱 연산자

- `a ** b`는 a를 b번 곱한 값을 반환.

### 단항 연산자 +와 숫자형으로의 반환

- 피연산자가 숫자가 아닌 경우 +가 붙으면 숫자로 바뀐다.

```javascript
alert(+true); // 1
alert(+""); // 0

let apples = "2";
let oranges = "3";

alert(apples + oranges); // "23" 문자형
alert(+apples + +oranges); // 5  숫자형
```

### 연산자 우선순위

- 하나의 표현식에 둘 이상의 연산자가 있는 경우 실행 순서는 연산자의 우선순위에 의해 결정됨.
- 괄호를 사용하면 괄호가 제일 먼저 수행됨.

### 할당연산자 =

- 값을 반환하는 할당 연산자

```javascript
let a = 1;
let b = 2;
let c = 3 - (a = b + 1);
alert(a); // 3
alert(c); // 0
```

- 할당 연산자는 여러개를 연결할 수 있다. (체이닝)

```javascript
let a, b, c;
a = b = c = 2 + 2;
alert(a); // 4
alert(b); // 4
alert(c); // 4
```

### 복합 할당 연산자

- 변수에 연산자를 적용하고 그 결과를 같은 변수에 저장할 때 사용

```javascript
let n = 2;
n += 5; // n = 7
n *= 2; // n = 14
```

### 증가.감소 연산자

- 숫자를 하나 늘리거나 줄여주는 연산
- 증가/감소 연산자는 변수에만 쓸 수 있다. 값에 쓸 수 없다.
- 증가 연산자 ++ : 변수를 1 증가

```javascript
let counter = 2;
counter++;
alert(counter); // 3
```

- 감소 연산자 -- : 변수를 1 감소

```javascript
let counter = 2;
counter--;
alert(counter); // 1
```

- ++ 와 -- 연산자는 변수 앞이나 뒤에 올 수 있다.
- 피연산자 앞에 붙으면 prefix, 뒤에 붙으면 postfix

```javascript
let counter = 1;
let a = ++counter;
alert(a); // 2
```

- ++counter는 counter를 증가시키고 새로운 값 2를 반환

```javascript
let counter = 1;
let a = counter++;
alert(a); // 1
```

- counter++ 는 counter를 증가시키지만 처음값 1을 반환.
- 값을 증가시키고 난 뒤 증가한 값을 바로 사용하려면 앞에 붙인다 `++counter`
- 값을 증가시키지만 증가 전의 기존값을 사용하려면 뒤에 붙인다 `counter++`

### 과제

- 전위형과 후위형

```javascript
let a = 1,
  b = 1;

let c = ++a; // 2
let d = b++; // 1
```

- 할당 후 결과 예측

```javascript
let a = 2;

let x = 1 + (a *= 2);
// a=4, x=5
```

- 형 변환

```javascript
"" + 1 + 0; // 1 -> 10 : ""+1 = 문자열 "1" + 0 = "10"
"" - 1 + 0; // -1
true + false; // false -> 1
6 / "3"; // 2
"2" * "3"; // 23 -> 6
4 + 5 + "px"; // 45px -> 9px
"$" + 4 + 5; // $45
"4" - 2; // 2
"4px" - 2; // error -> NaN
7 / 0; // 0  -> Infinity
"  -9  " + 5; // 4 -> " -9 5"
"  -9  " - 5; // error -> -14
null + 1; // 1 -> 숫자형으로 변환시 Null은 0
undefined + 1; // 1 -> NaN -> 숫자형으로 변환시 undefined는 NaN
" \t \n" - 2; // eeror -> -2
```

- 덧셈고치기

```javascript
let a = +prompt("덧셈할 첫 번째 숫자를 입력해주세요.", 1);
let b = +prompt("덧셈할 두 번째 숫자를 입력해주세요.", 2);

alert(a + b); // 12
```
