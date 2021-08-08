# JS Is Weird

## 링크

- https://jsisweird.com/

## 해답

### 1. true + false

- 정답: 1

```js
Number(true); // 1
Number(false); // 0
1 + 0; // 1
```

### 2. [,,,].length

- 정답: 3
- [,,,] 은 3개의 슬롯을 가진 배열을 반환한다.

### 3. [1,2,3] + [4,5,6]

- 정답: "1,2,34,5,6"
- 각 배열이 string으로 변환된 후 합쳐진다.

### 4. 0.2 + 0.1 === 0.3

- 정답: FALSE (0.30000000000000004)
- 부동 소수점을 비교하는데 JS의 경우 소수점이 완전하게 딱 떨어지지 않음.

```js
0.2 + 0.1; // 0.30000000000000004
0.2 + 0.1 > 0.3; // true
```

### 5. 10,2

- 정답: 2
- 쉼표연산자는 마지막 피연산자의 값만 반환한다.

### 6. !!""

- 정답: false
- ! 은 논리 not 연산자. ""는 빈값으로 falsy한 값이므로 false

### 7. +!![]

- 정답: 1
- 빈값은 falsy한 값이지만 빈 배열은 true임. 때문에 !![]는 true이며 +를 붙이면 숫자로 변환돼 1을 출력

### 8. !!!true

- 정답: false

### 9. true == "true"

- 정답: false
- 형비교에서 다르기 때문. true는 boolean, "TRUE"는 string

### 10. 010 - 03

- 정답: 5
- 010은 자바스크립트에서 8진법으로 취급. 때문에 010 = 8, 03 = 3 이므로 8 -3 = 5이다.
- 8진수 구문은 앞에 0을 사용한다. 0 이후의 숫자가 0에서 7까지 범위 밖에 있는 경우 숫자는 10진수로 해석됨

### 11. "" - - ""

- 정답: 0
- 빈값은 모두 0으로 치환됨.

```js
- - ""; // 0
--""; // SyntaxError: Invalid left-hand side expression in prefix operation
```

### 12. null + 0

- 정답: 0
- null은 숫자 0으로 치환된다.

```js
Number(null); // 0
null === false; // false
+null === +false; // true
```

### 13. 0/0

- 정답: NaN

### 14. 1>0 > Math.pow(10, 1000)

- 정답: false
- 자바스크립트는 1/0과 Math.pow(10,1000)을 무한대 숫자로 취급.
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Infinity

```js
1 / 0; // infinity
Math.pow(10, 1000); // infinity
Infinity > Infinity; // false
```

### 15. true++

- 정답: SyntaxError
- Invalid left-hand side expression in postfix operation

```js
1++ ; // SyntaxError
```

### 16. "" - 1

- 정답: -1
- - 연산자는 숫자와 문자열 모두에 사용되지만 빼기 연산자는 문자열에 사용되지 않는다. 때문에 자바스크립트는 이 연산을 숫자의 연산으로 해석한다.

```js
Number(""); // 0
0 - 1; // -1;
```

### 17. (null - 0) + "0"

- 정답: 00
- 숫자 (null - 0 = 0) + 문자열 0이므로 "00"을 반환한다.

### 18. true + ("true" - 0)

- 정답: NaN

### 19. !5 + !5

- 정답: 0

```js
Boolean(5); // true
!true; // false
!5; // false
```

### 20. [] + []

- 정답: ""
- 배열은 빈 문자열로 변환이 된다.

```js
[].toString(); // ""
"" + ""; // ""
```

### 21. NaN === NaN

- 정답: false
- NaN은 모든 값과 비교했을 때 같지 않으며 NaN과도 같지 않다.
- 때문에 NaN을 판별하려면 isNaN()함수를 사용한다.

### 22. NaN++

- 정답: NaN
- NaN은 증가시켜도 NaN이다.

### 23. undefined + NaN

- 정답: NaN
- false는 숫자로 변환되지만 undefined는 아님.

### 24. +0 === -0

- 정답: TRUE
- 자바스크립트에서 양수 0와 음수 0는 같음.

```js
+0 === -0; // true
Object.is(+0, -0); // false
```

### 25. +!!NaN \* "" - - [,]

- 정답: 0

```js
+!!NaN; // -> 0
Number(""); // -> 0
-[,]; // -> -0
```
