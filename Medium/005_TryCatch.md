# Try/Catch

## try/catch문?

- JS에서 오류를 처리하기 위해 사용하는 구문.
- try문 에서 오류 테스트, catch문에서 예외(오류)를 처리
- try문에서 예외가 발생하지 않으면 catch문은 실행되지 않는다.
- try/catch 문은 실행 가능한 코드에서만 작동한다. 문법적으로 잘못된 코드는 try/catch 문이 작동하지 않는다.

## JS 오류 타입

- EvalError : 전역함수 eval()에서 발생하는 오류
- InternalError: JavaScript 엔진 내부에서 발생한 오류
- RangeError: 숫자변수나 매개변수가 유효한 범위를 벗어났을 때
- ReferenceError: 존재하지 않는 변수를 참조했을 때 발생
- SyntaxError: 문법이 잘못된 경우 발생
- TypeError: 주어진 값이 유효한 자료형이 아닌 경우 발생
- URIError: encodeURI()나 decodeURl() 함수에 부적절한 변수를 제공했을 때
  (encodeURI()?
  URI의 특정한 문자를 UTF-8로 인코딩해 하나, 둘, 셋, 혹은 네 개의 연속된 이스케이프 문자로 나타냄)

## throw문?

- 사용자가 정의하는 예외. 함수의 실행이 중지되고 catch문이 실행됨.

```javascript
function getRectArea(width, height) {
  if (isNaN(width) || isNaN(height)) {
    throw "Parameter is not a number!";
  }
}

try {
  getRectArea(3, "A");
} catch (e) {
  console.error(e);
  // expected output: "Parameter is not a number!"
}
```

## finally문?

- try/catch 문에서 오류의 여부와 관계없이 마지막에 반드시 실행될 함수.
- 오류가 없다면 try 실행이 끝난 후, 오류가 있다면 catch 실행이 끝난 후 실행됨.
- finally문은 try/catch문에서 return을 선언 후에도 실행된다.
- try/catch 문은 총 세가지 형식을 가질 수 있다.
  - try...catch
    - try...finally
    - try...catch...finally

```javascript
let data=prompt("name")

try {
	if (data ==== "") throw new Error("data is empty")
	else alert(`Hi ${data} how do you do today`)
} catch (e) {
	alert(e)
} finally {
	alert("Welcom to the try catch article")
}

```

## 중첩 try/catch문, rethrow

- try/catch문은 중첩해서 사용할 수 있다.
- rethrow란?
  - catch는 알고 있는 에러만 처리하고 나머지는 다시 '던져야' 한다
    1. catch가 모든 에러를 받는다.
    2. catch(err)에서 에러 객체 err를 분석한다
    3. 에러 처리 방법을 알지 못하면 throw err를 한다.
    - 보통 에러 체크를 instanceof 명령어로 체크

```javascript
try {
  user = {
    /*...*/
  };
} catch (err) {
  if (err instanceof ReferenceError) {
    alert("ReferenceError"); //  정의되지 않은 변수에 접근하여 'ReferenceError' 발생
  } else {
    throw err; // catch 에러에서는 알 수 없는 error는 건너뛸 수 있음.
  }
}
```

---

원문
https://www.freecodecamp.org/news/try-catch-in-javascript/

참고
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/try...catch
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/throw
https://ko.javascript.info/try-catch
