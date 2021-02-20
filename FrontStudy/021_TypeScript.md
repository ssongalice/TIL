# 타입스크립트 간단 소개

## 타입스크립트(TypeScript)란?

- MS에서 개발, 관리하는 오픈소스 언어
- 타입 안정성을 보장하는 정적 언어
- 컴파일 단계에서 타입 오류를 Catch, 코드 어시스트 Support
- 크로스플랫폼 지원 : 자바스크립트가 실행되는 모든 플랫폼에서 사용 가능
- 객체 지향 언어 : 클래스, 인터페이스, 모듈 등의 기능을 제공하며 순수한 객체지향 코드를 작성할 수 있음
- 정적 타입 : 정적 타입을 사용하기 때문에 코드를 입력하는 동안 오류를 체크할 수 있음
- DOM 제어 : 자바스크립트와 같이 DOM을 제어해 요소를 추가하거나 삭제 할 수 있다
- 최신 ECMAScript 기능 지원 : ES6 이상의 최신 자바스크립트 문법을 쉽게 지원

## 타입 기본

### 타입 지정

- 타입스크립트는 일반 변수, 매개 변수(Parameter), 객체 속성(Property) 등에 `:TYPE`과 같은 형태로 타입을 지정할 수 있다.

```typescript
function someFunc(a: TYPE_A, b: TYPE_B): TYPE_RETURN {
  return a + b;
}

let some: TYPE_SOME = someFunc(1, 2);
// type이 number가 아니기 때문에 에러 반환
function add(a: number, b: number) {
  return a + b;
}
const sum: string = add(1, 2);
```

### 타입 선언

- Boolean

```typescript
let isBoolean: boolean;
let isDone: boolean = false;
```

- 숫자 : Number
  - 모든 부동 소숫점을 사용할 수 있다.

```typescript
let num: number;
let integer = 6;
```

- 문자열 : String
  - ES6의 템플릿 문자열도 지원

```typescript
let red: string = "Red";
let myColor: string = `My Color is ${red}`;
```

- 배열 : Array
  - 순차적으로 값을 가지는 일반 배열.

```typescript
// 문자열만 가지는 배열
let fruits: string[] = ['Apple', 'Banana', 'Mango']';
// 숫자만 가지는 배열
let oneToSeven: number[] = [1,2,3,4,5,6];
```

- 유니언 타입(다중타입)의 '문자열과 숫자를 동시에 가지는 배열'도 선언할 수 있음.

```typescript
let array: (string | number)[] = ["Apple", 1, 2, "Banana", "Mango", 3];
```

- 배열이 가지는 항목의 값을 단언할 수 없다면 any를 사용할 수 있다.

```typescript
let someArr: any[] = [0, 1, {}, [], false];
```

- 튜플 : Tuple
  - 정해진 타입의 고정된 길이(length) 배열을 표현
  - Tuple 타입의 2차원 배열을 사용할 수 있음.
  - Tuple은 할당에만 국한됨. push나 splice 등을 통해 값을 넣는 행위는 막을 수 없다.

```typescript
let tuple: [string, number];
tuple = ["a", 1];
tuple = ["a", 1, 2]; // Error
```

```javascript
let users: [number, string, boolean][];
// Or
// let users: Array<[number, string, boolean]>;

users = [
  [1, "Neo", true],
  [2, "Evan", false],
  [3, "Lewis", true],
];
```

- 열거형 : Enum
  - 숫자 또는 문자열 값 집합에 이름(Member)을 부여할 수 있는 타입. 종류가 일정한 범위로 정해져 있는 경우 유용.
  - 기본적으로 0부터 시작, 값은 1씩 증가. 수동으로 값을 변경할 수 있으며 값을 변경한 부분부터 다시 1씩 증가.
  - Enum은 역방향 맵핑을 지원. 열거된 멤버로 값에, 값으로 멤버에 접근할 수 있다는 것.
  - 문자열 값으로 초기화할 수 있지만 이 방법은 역방향 맵핑을 지원하지 않는다.

```typescript
enum Week {
  Sun, // 0
  Mon, // 1
  Tue, // 2
  Wed, // 3
  Thu, // 4
  Fri, // 5
  Sat, // 6
}

console.log(Week.Sun); // 0;
console.log(Week[0]); // Sun;
```

```typescript
// 스터디 코드
const status: String = "로딩중";

type Status = "로딩중" | "로딩완료" | "에러발생";
const status1: Status = "로딩중";
const status2: Status = "로딩끝"; // Error

enum EnumStatus {
  loading = "로딩중",
  complete = "로딩완료",
  error = "에러발생",
}

const status3: EnumStatus = EnumStatus.loading;
console.log(status3); // '로딩중'
```

- Void
  - 일반적으로 값을 반환하지 않는 함수. `: void` 위치는 함수가 반환타입을 명시하는 곳
  - 값으르 반환하지 않는 함수는 실제로는 undefined를 반환

```typescript
function hello(msg: string): void {
  console.log(`Hello ${msg}`);
}

const hi: void = hello("world"); // Hello world;
console.log(hi); // undefined
```

- 유니언(Union) : 2개 이상의 타입을 허용하는 경우

```typescript
let union: string | number;
union = "Hellow Type!";
union = 123;
union = false; // Error
```
