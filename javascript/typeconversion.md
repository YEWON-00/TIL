### 형 변환(type conversion)

- 함수와 연산자에 전달되는 값은 대부분 적절한 자료형으로 자동 변환됩니다. 이런 과정을 "형 변환(type conversion)"이라고 합니다.
- `alert`가 전달받은 값의 자료형과 관계없이 이를 문자열로 자동 변환하여 보여주는 것이나, 수학 관련 연산자가 전달받은 값을 숫자로 변환하는 경우가 형 변환의 대표적인 예시입니다.
- 전달받은 값을 의도를 갖고 원하는 타입으로 변환(명시적 변환)해 주는 경우도 형 변환이라고 할 수 있습니다.

### 문자형으로 변환

- `alert`메서드는 매개변수로 문자형을 받기 때문에, `alert(value)`에서 value는 문자형이어야 합니다. 만약, 다른 형의 값을 전달받으면 이 값은 문자형으로 자동 변환됩니다.
- `String(value)` 함수를 호출해 전달받은 값을 문자열로 변환 할 수도 있습니다.
- `false`는 문자열 `"false"`로, `null`은 문자열 `"null"`로 변환되는 것과 같이, 문자형으로의 변환은 대부분 예측 가능한 방식으로 일어납니다.

```jsx
let value = true;
alert(typeof value); // boolean

value = String(value); // 변수 value엔 문자열 "true"가 저장됩니다.
alert(typeof value); // string
```

### 숫자형으로 변환

- 숫자형으로의 변환은 수학과 관련된 함수와 표현식에서 자동으로 일어납니다.
- 예시) 숫자형이 아닌 값에 나누기 `/`를 적용한 경우

```jsx
alert( "6" / "2" ); // 3, 문자열이 숫자형으로 자동변환된 후 연산이 수행됩니다.
```

- `Number(value)` 함수를 사용하면 주어진 값(`value`)을 숫자형으로 명시해서 변환할 수 있습니다.

```jsx
let str = "123";
alert(typeof str); // string

let num = Number(str); // 문자열 "123"이 숫자 123으로 변환됩니다.

alert(typeof num); // number
```

- 숫자형 값를 사용해 무언가를 하려고 하는데 그 값을 문자 기반 폼(form)을 통해 입력받는 경우엔, 이런 명시적 형 변환이 필수입니다.
- 숫자 이외의 글자가 들어가 있는 문자열을 숫자형으로 변환하려고 하면, 그 결과는 `NaN`이 됩니다.

```jsx
let age = Number("임의의 문자열 123");

alert(age); // NaN, 형 변환이 실패합니다.
```

- 숫자형으로 변환 시 적용되는 규칙

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0adcbbb3-5aec-433c-9820-4a6895a73ded/Untitled.png)

```jsx
alert( Number("   123   ") ); // 123
alert( Number("123z") );      // NaN ("z"를 숫자로 변환하는 데 실패함)
alert( Number(true) );        // 1
alert( Number(false) );       // 0
```

### 불린형으로 변환

- 이 형 변환은 논리 연산을 수행할 때 발생합니다
- `Boolean(value)`를 호출하면 명시적으로 불리언으로의 형 변환을 수행할 수 있습니다.
- 숫자 `0`, 빈 문자열, `null`, `undefined`, `NaN`과 같이 직관적으로도 “비어있다고” 느껴지는 값들은 `false`가 됩니다.
- 그 외의 값은 `true`로 변환됩니다.

```jsx
alert( Boolean(1) ); // 숫자 1(true)
alert( Boolean(0) ); // 숫자 0(false)

alert( Boolean("hello") ); // 문자열(true)
alert( Boolean("") ); // 빈 문자열(false)
```

- 문자열 `"0"`은 `true`입니다.
- 자바스크립트에선 비어 있지 않은 문자열은 언제나 `true`입니다.
