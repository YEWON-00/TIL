### 변수(variable)

- 데이터를 저장할 때 쓰이는 ‘이름이 붙은 저장소’
- let 키워드를 사용해 변수 생성

```jsx
//'message'라는 이름을 가진 변수를 생성(선언)
let message;

//할당 연산자를 사용해 변수 안에 데이터 저장
message = 'Hello'; 

//문자열이 변수와 연결된 메모리 영역에 저장되었기 때문에, 변수명을 이용해 문자열에 접근 가능
alert(message); 
```

- 변수 선언과 값 할당을 한 줄에 작성할 수도 있음

```jsx
let message = 'Hello!';
```

- 한 줄에 여러 변수를 선언하는 것도 가능(가독성을 위해 권장하는 방법은 아님)

```jsx
let user = 'John', age = 25, message = 'Hello';
```

- 값이 변경되면 이전 데이터는 변수에서 제거됨

```jsx
let message;

message = 'Hello!';

message = 'World!'; // 값이 변경되었습니다.

alert(message);
```

- 변수 두 개를 선언하고, 한 변수의 데이터를 다른 변수에 복사할 수도 있음

```jsx
let Hello = 'Hello world!';

let message;

// Hello의 'Hello world' 값을 message에 복사합니다.
message = Hello;

// 이제 두 변수는 같은 데이터를 가집니다.
alert(Hello); // Hello world!
alert(message); // Hello world!
```

- 변수를 두 번 선언하면 에러 발생
- 따라서 변수는 딱 한 번만 선언하고, 선언한 변수를 참조할 때는 `let`없이 변수명만 사용해 참조

```jsx
let message = "This";

// 'let'을 반복하면 에러가 발생합니다.
let message = "That"; // SyntaxError: 'message' has already been declared
```

### 변수 명명 규칙

**자바스크립트에서의 변수 명명 시 두 가지 제약 사항**

1. 변수명에는 오직 문자와 숫자, 그리고 기호 `$`와 `_`만 들어갈 수 있음
2. 첫 글자는 숫자가 될 수 없음

```jsx
//유효한 변수명의 예시
let userName;
let test123;
let $ = 1; // '$'라는 이름의 변수를 선언합니다.
let _ = 2; // '_'라는 이름의 변수를 선언합니다.

//유효하지 않은 변수명의 예시
let 1a; // 변수명은 숫자로 시작해선 안 됩니다.
let my-name; // 하이픈 '-'은 변수명에 올 수 없습니다.
```

- 대소문자를 구별함
- 비 라틴계 언어도 변수명에 사용할 수 있지만 권장하진 않음
- 예약어는 변수명으로 사용할 수 없음

### use strict 없이 할당하기

- 변수는 대개 정의되어 있어야 사용할 수 있음
- 그러나 예전에는 `let` 없이도 단순하게 값을 할당해 변수를 생성하는 것이 가능했음
- `use strict`를 쓰지 않으면 과거 스크립트와의 호환성을 유지할 수 있기 때문에 여전히 이 방식을 사용 할 수 있음

```jsx
// 참고: 이 예제에는 "use strict"가 없습니다.

num = 5; // 변수 'num'이 정의되어있지 않더라도, 단순 할당만으로 변수가 생성됩니다.

alert(num); // 5
```

- 이렇게 변수를 생성하는 것은 엄격 모드에서 에러를 발생시키기 때문에 나쁜 관습

```jsx
"use strict";

num = 5; // error: num is not defined
```

### 상수

- 변화하지 않는 변수를 선언할 땐, `let` 대신 `const`를 사용
- `const`로 선언한 변수를 '상수(constant)'라고 부름
- 상수는 재할당할 수 없으므로 상수를 변경하려고 하면 에러가 발생
- 변숫값이 절대 변경되지 않을 것이라 확신하면, 값이 변경되는 것을 방지하면서 다른 개발자들에게 이 변수는 상수라는 것을 알리기 위해 `const`를 사용해 변수를 선언하도록 함

```jsx
const myBirthday = '18.04.1982';

myBirthday = '01.01.2001'; // error, can't reassign the constant!
```

### 바람직한 변수명

- `userName` 이나 `shoppingCart`처럼 사람이 읽을 수 있는 이름을 사용하기
- 무엇을 하고 있는지 명확히 알고 있지 않을 경우 외에는 줄임말이나 `a`, `b`, `c`와 같은 짧은 이름은 피하기
- 최대한 서술적이고 간결하게 명명하기. `data`와 `value`는 나쁜 이름의 예시.
- 자신만의 규칙이나 소속된 팀의 규칙을 따르기. 만약 사이트 방문객을 'user’라고 부르기로 했다면, 이와 관련된 변수를 `currentVisitor`나 `newManInTown`이 아닌 `currentUser`나 `newUser`라는 이름으로 지어야 함.

### 과제

---

****변수 가지고 놀기****

1. `admin`과 `name`이라는 변수를 선언하세요.
2. `name`에 값으로 `"John"`을 할당해 보세요.
3. `name`의 값을 `admin`에 복사해 보세요.
4. `admin`의 값을 `alert` 창에 띄워보세요. "John"이 출력되어야 합니다.

```jsx
//variable.js
let admin, name;

name = "John";
admin = name;

alert(admin);
```

**올바른 이름 선택하기**

1. 현재 우리가 살고있는 행성(planet)의 이름을 값으로 가진 변수를 만들어보세요. 변수 이름은 어떻게 지어야 할까요?
2. 웹사이트를 개발 중이라고 가정하고, 현재 접속 중인 사용자(user)의 이름(name)을 저장하는 변수를 만들어보세요. 변수 이름은 어떻게 지어야 할까요?

```jsx
let ourPlanetName = "Earth";

let currentUserName = "John";
```
