### nullish 병합 연산자(nullish coalescing operator)

`??`를 사용하면 짧은 문법으로 여러 피연산자 중 그 값이 ‘확정되어있는’ 변수를 찾을 수 있습니다.

`a ?? b`의 평가 결과는 다음과 같습니다.

- `a`가 `null`도 아니고 `undefined`도 아니면 `a`
- 그 외의 경우는 `b`

nullish 병합 연산자 `??`없이 `x = a ?? b`와 동일한 동작을 하는 코드를 작성하면 다음과 같습니다.

```jsx
x = (a !== null && a !== undefined) ? a : b;
```

또 다른 예시를 살펴봅시다. `firstName`, `lastName`, `nickName`이란 변수에 사용자 이름이나 별명을 저장하는데, 사용자가 아무런 정보도 입력하지 않는 케이스도 허용한다고 해보겠습니다.

화면엔 세 변수 중 실제 값이 있는 변수의 값을 출력하는데, 세 변수 모두 값이 없다면 '익명의 사용자’가 출력되도록 해보죠.

이럴 때 nullish 병합 연산자 `??`를 사용하면 값이 정해진 변수를 간편하게 찾아낼 수 있습니다.

```jsx
let firstName = null;
let lastName = null;
let nickName = "바이올렛";

// null이나 undefined가 아닌 첫 번째 피연산자
alert(firstName ?? lastName ?? nickName ?? "익명의 사용자"); // 바이올렛
```

### ‘??’와 ‘||’의 차이

- `||`는 첫 번째 *truthy* 값을 반환합니다.
- `??`는 첫 번째 *정의된(defined)* 값을 반환합니다.

`null`과 `undefined`, 숫자 `0`을 구분 지어 다뤄야 할 때 이 차이점은 매우 중요한 역할을 합니다.

```jsx
height = height ?? 100;
```

`height`에 값이 정의되지 않은경우 `height`엔 `100`이 할당됩니다.

```jsx
let height = 0;

alert(height || 100); // 100
alert(height ?? 100); // 0
```

- `height || 100`은 `height`에 `0`을 할당했지만 `0`을 falsy 한 값으로 취급했기 때문에 `null`이나 `undefined`를 할당한 것과 동일하게 처리합니다. 따라서 `height || 100`의 평가 결과는 `100` 입니다.
- 반면 `height ?? 100`의 평가 결과는 `height`가 정확하게 `null`이나 `undefined`
일 경우에만 `100`이 됩니다. 예시에선 `height`에 `0`이라는 값을 할당했기 때문에  `0`이 출력됩니다.
- 이런 특징 때문에 높이처럼 `0`이 할당될 수 있는 변수를 사용해 기능을 개발할 땐 `||`보다 `??`가 적합합니다.

### 연산자 우선순위

- `[??](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence#Table)`의 연산자 우선순위는 `5`로 꽤 낮습니다.
- 따라서 `??`는 `=`와 `?`보다는 먼저, 대부분의 연산자보다는 나중에 평가됩니다.
- 그렇기 때문에 복잡한 표현식 안에서 `??`를 사용해 값을 하나 선택할 땐 괄호를 추가하는 게 좋습니다.

### 제약사항

- 안정성 관련 이슈 때문에 `??`는 `&&`나 `||`와 함께 사용하지 못합니다.

```jsx
let x = 1 && 2 ?? 3; // SyntaxError: Unexpected token '??'
```

- 제약을 피하려면 괄호를 사용해주세요.
