# 참조에 의한 객체 복사

- 객체와 원시 타입의 근본적인 차이 중 하나는 객체는 '참조에 의해' (by reference) 저장되고 복사된다.
- 원시값(문자열, 불린, 숫자)은 값 그대로 할당, 저장, 복사됨.
- 변수에 객체가 그대로 저장되는 것이 아니라 객체가 저장된 메모리 주소인 객체에 대한 참조값이 저장됨.

### 참조에 의한 비교

- 객체 비교 시 동등 연산자 ==와 일치 연산자 ===는 동일하게 동작.
- 비교 시 피연산자인 두 객체가 동일한 객체인 경우 참을 반환.

```javascript
// 첫번째 예시
let a = {};
let b = a; // 참조에 의한 복사

alert(a == b); // true
alert(a === b);

// 두번째 예시
let a = {};
let b = {};
alert(a == b); // false
```

## 객체 복사, 병합과 Object.assign

- Object.assign

```javascript
Object.assign(dest, [src1, src2, src3...])
```

- 첫 번째 dest는 목표로 하는 객체
- 이어지는 인수 src, ... srcN은 복사하고자 하는 객체.
- 객체 src1, ..., srcN의 프로퍼티를 dest에 복사. dest를 제외한 인수 전부가 첫번째 인수로 복사됨. 마지막으로 dest를 반환.
