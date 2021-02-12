# 배열과 메서드

## 요소 추가. 제거 메서드

### splice

- splice를 사용해 요소 추가, 삭제, 교체 모두 가능

```javascript
arr.splice(index[, deleteCount, elem1, ..., elemN])
```

- index: 조작을 가할 첫 번째 요소의 index. 음수를 인덱스로 사용하면 배열 끝에서부터 센 요소의 위치
- deleteCount: 제거하고자 하는 요소의 갯수. 0으로 설정하면 요소를 제거하지 않으면서 새로운 요소를 추가할 수 있음.
- elem1, ..., elemN : 배열에 추가할 요소

```javascript
let arr = ["I", "study", "JavaScript", "right", "now"];
arr.splice(0, 3, "Let's", "dance");
alert(arr); // ["Let's", "dance", "right", "now"];
```

### slice

```javascript
arr.slice([start], [end]);
```

- start 인덱스부터 end를 제외한 end인덱스까지 복사한 새로운 배열을 반환.

### concat

```javascript
arr.concat(arg1, arge2...)
```

- 기존 배열의 요소를 사용해 새로운 배열을 만들거나 기존 배열에 요소를 추가하고자 할 때 사용
- 객체가 인자로 넘어오면 객체는 통으로 복사됨.

## forEach로 반복작업하기

- arr.forEach는 주어진 함수를 배열 요소 각각에 대해 실행할 수 있게 해줌

```javascript
arr.forEach(function (item, index, array) {
  // 본문
});
```

## 배열 탐색하기

### indexOf, lastIndexOf, includes

- arr.indexOf(item, from) : from 부터 시작해 item을 찾습니다. 요소를 발견하면 해당 요소의 인덱스를 반환하고 발견하지 못하면 -1을 반환
- arr.lastIndexOf(item, from) : indexOf와 동일. 인덱스를 끝에서부터 시작함
- arr.includes(item, from) : from 부터 시작해 item이 있는지 검색. 요소를 발견하면 true, 없으면 false 반환

### find와 findIndex

- arr.find

```javascript
const result = arr.find(function (item, index, array) {
  // true가 반환되면 반복이 멈추고 해당 요소 반환.
  // 조건에 해당하는 요소가 없으면 undefined 반환
});
```

- arr.findIndex : find와 동일하나 조건에 맞는 요소 대신 해당 요소의 index를 반환. 조건에 맞는 요소가 없으면 -1을 반환

### filter

- 조건을 충족하는 요소를 모두 반환.

```javascript
const results = arr.filter(function (item, index, array) {
  // 조건을 충족하는 요소는 results에 순차적으로 더해짐
  // 조건을 충족하는 요소가 하나도 없으면 빈 배열 반환
});
```

## 배열을 변형하는 메서드

### map

- 배열 전체를 대상으로 함수를 호출하고, 함수 호출 결과를 배열로 반환해줌.

```javascript
const result = arr.map(function (item, index, array) {
  // 요소 대신 새로운 값을 반환
});
```

### sort

- 배열의 요소를 정렬해줌. 배열 자체가 변경된다. 요소는 문자열로 취급되서 재정렬되기 때문에 새로운 정렬 기준을 만드려면 arr.sort에 새로운 함수를 넘겨줘야 함.

```javascript
function compareNumeric(a, b) {
  if (a > b) return 1;
  if (a == b) return 0;
  if (a < b) return -1;
}

let arr = [1, 2, 15];
arr.sort(compareNumeric);
alert(arr); // 1, 2, 15
// 더 간단하게
arr.sort((a, b) => a - b);
```

### reverse

- arr의 요소를 역순으로 정렬
- 반환값은 재정렬된 배열

### split, join

- str.split(delim)은 구분자 delim을 기준으로 문자열을 쪼개줌
- delim을 빈 문자열로 지정하면 문자열을 글자 단위로 분리할 수 있음

```javascript
const arr = "Bilbo, Gandalf, Nazgul, Saruman".split(",", 2);
alert(arr); // Bilbo, Gandalf
```

- arr.join(glue)는 split와 반대. 배열 요소를 모두 합친 후 하나의 문자열을 만든다

```javascript
const arr = ["Bilbo", "Gandalf", "Nazgul"];
const str = arr.join(";");
alert(str); // Bilbo;Gandalf;Nazgul
```

### reduce와 reduceRight

- reduce와 reduceRight는 배열을 기반으로 값 하나를 도출할 때 사용
- reduceRight는 reduce와 동일하지만 배열의 오른쪽부터 연산을 수행한다.

```javascript
const value = arr.reduce(
  function (accumlator, item, index, array) {
    ///
  },
  [initial]
);
```

- accumulator: 이전 함수의 호출 결과. initial은 함수 최초 호출 시 사용되는 초깃값. 마지막 함수까지 호출되면 이 값은 reduce의 반환값이된다.
- item: 현재 배열 요소
- index: 요소의 위치
- array: 배열
- 초깃값이 없으면 reduce는 배열의 첫번째 요소를 초깃값으로 사용하고 두번째 요소부터 함수를 호출한다. 하지만 배열이 비어있을 경우 오류가 발생하기 때문에 초깃값은 명시해주는 것을 권장.

## Array.isArray로 배열 여부 알아내기

- 배열은 독립된 자료형으로 취급되지 않고 객체형에 속함. typeof로는 일반 객체와 배열을 구분할 수 없다.
- value가 배열이라면 true를, 배열이 아니라면 false를 반환

```javascript
alert(Array.isArray({})); // false
alert(Array.isArray([])); // true
```

## 과제

- border-left-width를 borderLeftWidth로 변경하기

```javascript
function camelize(str) {
  const splited = str.split("-");
  const joined = splited.map((item, idx) => {
    return idx !== 0 ? item.toUpperCase() : item;
  });
  return joined.join();
}
```

- 특정 범위에 속하는 요소 찾기

```javascript
function filterRange(arr, a, b) {
  const filtered = arr.filter((item) => (a <= item) & (item <= b));
  return filtered;
}
```

- 특정 범위에 속하는 요소 찾기

```javascript
function filterRangeInPlace(arr, a, b) {
      for (let i = 0; i<arr.length; i++) {
            let val = arr[i];

            if (val <a || val >b) {
                  arr.splice(i,1);
                  i==;
            }
      }
}
```
