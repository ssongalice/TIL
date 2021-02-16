# 나머지 매개변수와 전개 문법

## 나머지 매개변수 ...

- 여분의 매개변수는 그 값을 담을 배열 이름을 마침표 세 개 뒤에 붙여주면 함수 선언부에 포함할 수 있다.
- 나머지 매개변수는 항상 마지막에 있어야 한다.

```javascript
// 모든 인수가 배열 args에 모인다
function sumAll(...args) {
  let sum = 0;
  for (let arg of arges) sum += arg;
  return sum;
}

// 처음 두 인수는 변수에, 나머지 인수는 titles라는 배열에 할당됨.
function showName(firstName, lastName, ...titles) {
  alert(firstName + " " + lastName); // Julius Caesar
  alert(titles); // ["Consul", "Imperator"];
}

showName("Julius", "Caesar", "Consul", "Imperator");
```

## 'arguments' 변수

- arguments라는 특별한 유사 배열 객체를 이용하면 인덱스를 사용해 모든 인수에 접근할 수 있다.
- 유사 배열 객체이기 때문에 배열 메서드를 사용할 수 없다.

```javascript
function showName() {
  alert(arguments.length);
  alert(arguments[0]);
  alert(arguments[1]);

  // arguments는 이터러블 객체이기 때문에
  // for(let arg of arguments) alert(arg); 를 사용해 인수를 나열할 수 있습니다.
}

// 2, Julius, Caesar가 출력됨
showName("Julius", "Caesar");

// 1, Bora, undefined가 출력됨(두 번째 인수는 없음)
showName("Bora");
```

## spread 문법

- 전개 문법(spread syntax)는 나머지 매개변수와 반대의 역할

```javascript
let arr = [3, 5, 1];
alert(Math.max(arr)); // NaN
alert(Math.max(...arr)); // 5
```

- 전개 문법은 for..of와 같은 방식으로 내부에서 iterator(반복자)를 사용해 요소를 수집한다.
- Array.from은 유사배열 객체와 이터러블 객체 둘 다 사용 가능
- 전개문법은 이터러블 객체에만 사용 가능.

- `...`이 함수 매개변수의 끝에 있으면 인수 목록의 나머지를 배열로 모아주는 '나머지 매개변수'
- `...`이 함수 호출 시 사용되면 배열을 목록으로 확장해주는 전개 문법
