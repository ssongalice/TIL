# JSON과 메서드

## JSON.stringfy

- JSON.stringfy - 객체를 JSON으로 바꿔줌.
- JSON.parse - JSON을 객체로 바꿔줌.
- 객체에서 변경된 문자열은 JSON으로 인코딩된 객체로 불림. 객체는 이렇게 문자열로 변환된 후에야 네트워크를 통해 전송하거나 저장소에 저장할 수 있음
- JSON으로 인코딩된 객체는 일반 객체와 다른 특징을 보임
  - 문자열은 큰따옴표로 감싸야 함. 작은따옴표나 백틱을 사용할 수 없음
  - 객체 프로퍼티는 큰따옴표로 감싸야 함.
- JSON.stringfy는 객체뿐 아니라 원시값에도 적용 가능.
  - 객체, 배열, 원시형 (문자형, 숫자형, 불린형, null)
- 자바스크립트 특유의 객체 프로퍼티는 JSON.stringfy가 처리할 수 없음
  - 함수 프로퍼티 (메서드)
  - 심볼형 프로퍼티 (키가 심볼인 프로퍼티)
  - 값이 undefined인 프로퍼티
- 순환 참조가 있으면 객체를 문자열로 바꾸는게 불가능

```javascript
let room = { number: 23 };
let meetup = {
  title: "Conference",
  participants: ["john", "ann"],
};

meetup.place = room;
room.occupiedBy = meetup;

JSON.stringify(meetup); // ERROR
```

## replace로 원하는 프로퍼티만 직렬화하기

```javascript
const json = JSON.stringify(value[, replacer, space])
```

- value: 인코딩하려는 값
- replacer: JSON으로 인코딩하길 원하는 프로퍼티가 담긴 배열
- space: 서식 변경 목적으로 사용할 공백 문자 수
- 대부분 JSON.stringify엔 인수를 하나만 넘겨서 사용. 순환참조를 다뤄야 하는 경우 두번째 인수를 사용해야 함.

```javascript
let room = {
  number: 23,
};

let meetup = {
  title: "Conference",
  participants: [{ name: "John" }, { name: "Alice" }],
  place: room,
};

room.occupiedBy = meetup; // room은 meetup을 참조
alert(
  JSON.stringify(meetup, function replacer(key, value) {
    alert(`${key} : ${value}`);
    return key == "occupiedBy" ? undefined : value;
  })
);
```

## space로 가독성 높이기

- space는 가독성을 높이기 위해 중간에 삽입해 줄 공백 문자 수
- 가독성을 높이기 위한 용도이기 때문에 단순 전달 목적이면 space 없이 직렬화 한다.

## toJSON

- 객체에 toJSON이라는 메서드가 구현돼있으면 객체를 JSON으로 바꿀 수 있다. JSON.stringify는 이런 경우를 감지하고 toJSON을 자동으로 호출

## JSON.parse

- JSON.parse를 사용하면 JSON으로 인코딩된 객체를 다시 객체로 디코딩할 수 있다.

```javascript
let value = JSON.parse(str, [reviver]);
```

- str: JSON 형식의 문자열
- reviver: 모든 Key,value 쌍을 대상으로 호출되는 function 형태의 함수로 값을 변경시킬 수 있음.
