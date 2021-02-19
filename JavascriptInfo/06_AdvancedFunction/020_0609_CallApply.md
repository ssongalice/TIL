# call/apply와 데코레이터, 포워딩

## 코드 변경 없이 캐싱 기능 추가하기

```javascript
function slow(x) {
  alert(`slow ${x}를 여기에 호출함`);
  return x;
}

function cachingDecorator(func) {
  let cache = new Map();
  return function (x) {
    if (cache.has(x)) {
      return cache.get(x); // cache에서 해당 키가 있으면 대응하는 값을 읽어옴
    }
    let result = func(x); // 그렇지 않을 경우 func 호출
    cache.set(x, result); // 그 결과를 저장
    return result;
  };
}

slow = cachingDecorator(slow);
```

- 인수로 받은 함수의 행동을 변경시켜주는 함수를 데코레이터라고 한다.
  - 캐싱 관련 코드를 함수 코드와 분리할 수 있기 때문에 함수의 코드가 간결해짐.
  - 원하는 함수 어디에든 데코레이터를 적용할 수 있다.

## func.call 를 사용해 컨텍스트 지정하기

```javascript
func.call(context, arg1, arg2, ...)
```

- 메서드를 호출하면 메서드의 첫번째 인수가 this, 이어지는 인수가 func의 인수가 된 후 func를 호출

```javascript
function say(phrase) {
  alert(this.name + ":" + phrase);
}

const user = { name: "John" };
// this엔 user가 고정되고 "Hello"는 메서드의 첫번째 인수가 된다.
say.call(user, "Hello"); // John : Hello
```

## 여러 인수 전달하기

```javascript
let worker = {
  slow(min, max) {
    alert(`slow ${min}, ${max}를 호출함`);
    return min + max;
  },
};

function cachingDecorator(func, hash) {
  let cache = new Map();
  return function () {
    // hash 가 호출되면서 arguments를 사용한 단일키가 만들어진다.
    let key = hash(arguments);
    if (cache.has(key)) {
      return cache.get(key);
    }
    // func.call를 사용해 컨텍스트와 래퍼가 가진 인수 전부를 기존 함수에 전달
    let result = func.call(this, ...arguments);
    cache.set(key, result);
    return result;
  };
}

function hash(args) {
  return args[0] + "," + args[1];
}

worker.slow = cachingDecorator(worker.slow, hash);
```

## func.apply

```javascript
func.apply(context, args);
```

- apply는 func의 this를 context로 고정해주고 유사 배열 객체인 args를 인수로 사용할 수 있게 해준다.
- call과 apply의 차이 : call이 복수 인수를 따로 받는 대신 apply는 유사 배열 객체로 받음.
- 인수가 이터러블 형태라면 call, 유사 배열 형태라면 apply 사용
- 콜 포워딩 (call forwarding) : 컨텍스트와 함께 인수 전체를 다른 함수에 전달하는 것.
