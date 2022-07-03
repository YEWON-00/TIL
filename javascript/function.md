### **함수**

- 함수는 프로그램을 구성하는 주요 '구성 요소(building block)'입니다.
- 함수를 이용하면 중복 없이 유사한 동작을 하는 코드를 여러 번 호출할 수 있습니다.

### **함수 선언**

```jsx
function name(parameters) {
  ...함수 본문...
}
```

- `function` 키워드, *함수 이름*, 괄호로 둘러싼 매개변수를 차례로 써주면 함수를 선언할 수 있습니다.
- 위 함수에는 매개변수가 없는데, 만약 매개변수가 여러 개 있다면 각 매개변수를 콤마로 구분해줍니다.
- 이어서 함수를 구성하는 코드의 모임인 '함수 본문(body)'을 중괄호로 감싸 붙여줍시다.

```jsx
function showMessage() {
  alert( '안녕하세요!' );
}

showMessage();
showMessage();
```

- 새롭게 정의한 함수는 함수 이름 옆에 괄호를 붙여 호출할 수 있습니다.

****

### **지역 변수**

- 함수 내에서 선언한 변수인 지역 변수(local variable)는 함수 안에서만 접근할 수 있습니다.

```jsx
function showMessage() {
  *let message = "안녕하세요!"; // 지역 변수*alert( message );
}

showMessage(); // 안녕하세요!

alert( message ); // ReferenceError: message is not defined (message는 함수 내 지역 변수이기 때문에 에러가 발생합니다.)
```

### **외부 변수**

- 함수 내부에서 함수 외부의 변수인 외부 변수(outer variable)에 접근할 수 있습니다.

```jsx
let *userName* = 'John';

function showMessage() {
  let message = 'Hello, ' + *userName*;
  alert(message);
}

showMessage(); // Hello, John
```

- 함수에선 외부 변수에 접근하는 것뿐만 아니라, 수정도 할 수 있습니다.

```jsx
let *userName* = 'John';

function showMessage() {
  *userName* = "Bob"; // (1) 외부 변수를 수정함

  let message = 'Hello, ' + *userName*;
  alert(message);
}

alert( userName ); // 함수 호출 전이므로 *John* 이 출력됨

showMessage();

alert( userName ); // 함수에 의해 *Bob* 으로 값이 바뀜
```

- 외부 변수는 지역 변수가 없는 경우에만 사용할 수 있습니다.
- 함수 내부에 외부 변수와 동일한 이름을 가진 변수가 선언되었다면, 내부 변수는 외부 변수를 *가립니다*.
- 함수 내부에 외부 변수와 동일한 이름을 가진 지역 변수 `userName`가 선언되어 있습니다. 외부 변수는 내부 변수에 가려져 값이 수정되지 않았습니다.

```jsx
let userName = 'John';

function showMessage() {
  *let userName = "Bob"; // 같은 이름을 가진 지역 변수를 선언합니다.*

	let message = 'Hello, ' + userName; // *Bob*
	alert(message);
}

// 함수는 내부 변수인 userName만 사용합니다,
showMessage();

alert( userName ); // 함수는 외부 변수에 접근하지 않습니다. 따라서 값이 변경되지 않고, *John*이 출력됩니다.
```

### **전역 변수**

- 위 예시의 `userName`처럼, 함수 외부에 선언된 변수는 *전역 변수(global variable)* 라고 부릅니다.
- 전역 변수는 같은 이름을 가진 지역 변수에 의해 가려지지만 않는다면 모든 함수에서 접근할 수 있습니다.
- 변수는 연관되는 함수 내에 선언하고, 전역 변수는 되도록 사용하지 않는 것이 좋습니다.
- 비교적 근래에 작성된 코드들은 대부분 전역변수를 사용하지 않거나 최소한으로만 사용합니다. 다만 프로젝트 전반에서 사용되는 데이터는 전역 변수에 저장하는 것이 유용한 경우도 있으니 이 점을 알아두시기 바랍니다.

### **매개변수**

- 매개변수(parameter)를 이용하면 임의의 데이터를 함수 안에 전달할 수 있습니다.
- 매개변수는 *인수(argument)* 라고 불리기도 합니다
- 아래 예시에서 함수 showMessage는 매개변수 `from` 과 `text`를 가집니다.

```jsx
function showMessage(*from, text*) { // 인수: from, text
  alert(from + ': ' + text);
}

*showMessage('Ann', 'Hello!'); // Ann: Hello! (*)
showMessage('Ann', "What's up?"); // Ann: What's up? (**)*
```

- `(*)`, `(**)`로 표시한 줄에서 함수를 호출하면, 함수에 전달된 인자는 지역변수 `from`과 `text`에 복사됩니다.
- 그 후 함수는 지역변수에 복사된 값을 사용합니다.
- 전역 변수 `from`이 있고, 이 변수를 함수에 전달하였습니다.
- 함수가 `from`을 변경하지만, 변경 사항은 외부 변수 `from`에 반영되지 않았습니다. 함수는 언제나 복사된 값을 사용하기 때문입니다.

```jsx
function showMessage(from, text) {

  *from = '*' + from + '*'; // "from"을 좀 더 멋지게 꾸며줍니다.*alert( from + ': ' + text );
}

let from = "Ann";

showMessage(from, "Hello"); // *Ann*: Hello

// 함수는 복사된 값을 사용하기 때문에 바깥의 "from"은 값이 변경되지 않습니다.
alert( from ); // Ann
```

****

### **기본값**

- 매개변수에 값을 전달하지 않으면 그 값은 `undefined`가 됩니다.
- `showMessage(from, text)`는 매개변수가 2개지만, 아래와 같이 인수를 하나만 넣어서 호출할 수 있습니다.

```jsx
showMessage("Ann");
```

- 이렇게 코드를 작성해도 에러가 발생하지 않습니다.
- 두 번째 매개변수에 값을 전달하지 않았기 때문에 `text`엔 `undefiend`가 할당될 뿐입니다.
- 따라서 에러 없이 `"Ann: undefined"`가 출력됩니다.
- 매개변수에 값을 전달하지 않아도 그 값이 `undefined`가 되지 않게 하려면 '기본값(default value)'을 설정해주면 됩니다.
- 매개변수 오른쪽에 `=`을 붙이고 `undefined` 대신 설정하고자 하는 기본값을 써주면 되죠.

```jsx
function showMessage(from, *text = "no text given"*) {
  alert( from + ": " + text );
}

showMessage("Ann"); // Ann: no text given
```

- 이젠 `text`가 값을 전달받지 못해도 `undefined`대신 기본값 `"no text given"`이 할당됩니다.
- 위 예시에선 문자열 `"no text given"`을 기본값으로 설정했습니다. 하지만 아래와 같이 복잡한 표현식도 기본값으로 설정할 수도 있습니다.

```jsx
function showMessage(from, text = anotherFunction()) {
  // anotherFunction()은 text값이 없을 때만 호출됨
  // anotherFunction()의 반환 값이 text의 값이 됨
}
```

### **매개변수 기본값 평가 시점**

- 자바스크립트에선 함수를 호출할 때마다 매개변수 기본값을 평가합니다.
- 물론 해당하는 매개변수가 없을 때만 기본값을 평가하죠.
- 위 예시에선 매개변수 `text`에 값이 없는 경우 `showMessage()`를 호출할 때마다 `anotherFunction()`이 호출됩니다.

### **매개변수 기본값을 설정할 수 있는 또 다른 방법**

- 가끔은 함수 선언부에서 매개변수 기본값을 설정하는 것 대신 함수가 실행되는 도중에 기본값을 설정하는 게 논리에 맞는 경우가 생기기도 합니다.
- 이런 경우엔 일단 매개변수를 `undefined`와 비교하여 함수 호출 시 매개변수가 생략되었는지를 확인합니다.

```jsx
function showMessage(text) {
  *if (text === undefined) {
    text = '빈 문자열';
  }*alert(text);
}

showMessage(); // 빈 문자열
```

- 이렇게 `if`문을 쓰는 것 대신 논리 연산자 `||`를 사용할 수도 있습니다.

```jsx
// 매개변수가 생략되었거나 빈 문자열("")이 넘어오면 변수에 '빈 문자열'이 할당됩니다.
function showMessage(text) {
  text = text || '빈 문자열';
  ...
}
```

- 이 외에도 모던 자바스크립트 엔진이 지원하는 [nullish 병합 연산자(nullish coalescing operator)](https://ko.javascript.info/nullish-coalescing-operator) `??`를 사용하면 `0`처럼 falsy로 평가되는 값들을 일반 값처럼 처리할 수 있어서 좋습니다.

```jsx
// 매개변수 'count'가 넘어오지 않으면 'unknown'을 출력해주는 함수
function showCount(count) {
  alert(count ?? "unknown");
}

showCount(0); // 0
showCount(null); // unknown
showCount(); // unknown
```

****

### 과제

---

**‘?’나 ‘||’를 사용하여 함수 다시 작성하기**

아래 함수는 매개변수 `age`가 `18`보다 큰 경우 `true`를 반환합니다.

그 이외의 경우는 컨펌 대화상자를 통해 사용자에게 질문한 후, 해당 결과를 반환합니다.

```jsx
function checkAge(age) {
  if (age > 18) {
    return true;
  } else {
    return confirm('보호자의 동의를 받으셨나요?');
  }
}
```

`if`문을 사용하지 않고 동일한 동작을 하는 함수를 한 줄에 작성해보세요.

아래 조건을 충족하는 해답 2개를 작성해야 합니다.

1. 물음표 연산자 `?`를 사용하여 본문을 작성

```jsx
function checkAge(age) {
  return (age > 18) ? true : confirm('보호자의 동의를 받으셨나요?');
}
```

1. OR 연산자 `||`를 사용하여 본문을 작성

```jsx
function checkAge(age) {
  return (age > 18) || confirm('보호자의 동의를 받으셨나요?');
}
```

**min(a,b) 함수 만들기**

`a`와 `b` 중 작은 값을 반환해주는 함수, `min(a,b)`을 만들어보세요.

만든 함수는 아래와 같이 동작해야 합니다.

```jsx
min(2, 5) == 2
min(3, -1) == -1
min(1, 1) == 1
```

```jsx
function min(a, b) {
  return a < b ? a : b;
}
```
