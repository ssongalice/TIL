# API 데이터 파싱하기

## 문제 1. to_id가 같은 from_id 들을 어떻게 찾아내지?

- 조건

  - to_id가 같은 from 상품들은 하나의 데이터 묶음으로 묶어준다.
  - 데이터의 순서는 연관성이 가장 높은 순서.

- 문제 해결의 순서

1. if랑 for문을 중첩해서 사용해볼까?

```javascript
for (let i = 0; i < data.length; i++) {
  if (i === 0) {
    parsedData.push({ to: data[0].to, from: [data[0].from] });
  } else {
    if (data[i - 1].to.item_id === data[i].to.item_id) {
      const currentIndex = parsedData.length - 1;
      parsedData[currentIndex].from.push(data[i].from);
    } else {
      parsedData.push({ to: data[i].to, from: [data[i].from] });
    }
  }
}
```

- 발생하는 문제

* 인덱스가 서로 붙어있는 요소가 아니면 to_id가 같은지 판별할 수 없음.
* for문, if/else 중첩 등 무한루프가 걸려서 화면이 동작하지 않음.
* 순서를 sort 함수를 활용해 이름순으로 정렬도 해봤지만 그럴경우 상위 순으로 이미 정렬된 데이터기 때문에 정렬 함수를 사용하면 데이터가 망가짐.

```javascript
for (let i = 0; i < data.length; i++) {
  const checkExistToItem = parsedData.find(
    (item) => item.to.item_id === data[i].to_item_id
  );

  let fromIntoNew; // 데이터 생략

  let toIntoNew; // 데이터 생략

  if (!checkExistToItem) {
    parsedData.push({ to: toIntoNew, from: [fromIntoNew] });
  } else {
    const currentIdx = parsedData.length - 1;
    parsedData[currentIdx].from.push(fromIntoNew);
  }
}
return parsedData;
```

2. 해결

- 새로운 배열을 하나 만들고, 새로운 배열에 for문 해당 인덱스 item의 to_id가 있는지 find로 찾음
- 만약 find가 undefined(=일치하는 to_id 없음 )라면 새로운 데이터 추가, 이미 해당 to_id가 배열에 있다면 해당 배열의 from배열에 요소를 추가.
- find를 사용한 이유 - find는 일치하는 첫번째 요소를 반환하는데, 현재 조건은 일치하는 to_id가 하나만 존재하기 때문에 find로 판별.

## 문제 2. Object에 새로운 key, value 추가하기

- 문제
  _ 상품 연관성 API랑 상품 정보 API가 달라서 각각 정보를 받아온 후 item_id를 기준으로 상품 정보를 매칭 해야 함
  _ 상품 정보 API와 상품 연관성 API에서 중복되는 정보 (item_id)도 있고 필요 없는 정보도 있어서 일부만 선택해서 Object에 추가해야 함.

* 첫번째

```javascript
refinedData[i]["from_item_name"] = getFromImgUrl.item_name;
refinedData[i]["from_item_img"] = getFromImgUrl.item_img;
refinedData[i]["from_item_cate"] =
  getFromImgUrl.cate_name || getFromImgUrl.cate_id;
refinedData[i]["to_item_name"] = getFromImgUrl.item_name;
refinedData[i]["to_item_img"] = getFromImgUrl.item_img;
refinedData[i]["to_item_cate"] = getToImgUrl.cate_name || getToImgUrl.cate_id;
```

- 코드가 너무 지저분
- spread 연산자를 활용해 값을 갱신

```javascript
refinedData[i] = {
  ...refinedData[i],
  from_item_name: getFromImgUrl.item_name,
  from_item_img: getFromImgUrl.item_img,
  from_item_cate: getFromImgUrl.cate_name || getFromImgUrl.cate_id,
  to_item_name: getToImgUrl.item_name,
  to_item_img: getToImgUrl.item_img,
  to_item_cate: getToImgUrl.cate_name || getToImgUrl.cate_id,
};
```

## 문제 3. store 액션 중첩

- 내일 다시 확인해보기
