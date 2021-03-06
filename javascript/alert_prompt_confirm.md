### alert

- alert 함수가 실행되면 사용자가 ‘확인(OK)’ 버튼을 누를 때까지 메시지를 보여주는 창이 계속 떠있게 됩니다.
- 메시지가 있는 작은 창은 *모달 창(modal window)*이라고 부릅니다.
- '모달’이란 단어엔 페이지의 나머지 부분과 상호 작용이 불가능하다는 의미가 내포되어 있습니다.
- 따라서 사용자는 확인 버튼을 누르기 전까지 모달 창 바깥에 있는 버튼을 누른다든가 하는 행동을 할 수 없습니다.

```jsx
alert("Hello");
```

### prompt

- 브라우저에서 제공하는 `prompt` 함수는 두 개의 인수를 받습니다.
- 함수가 실행되면 텍스트 메시지와 입력 필드(input field), 확인(OK) 및 취소(Cancel) 버튼이 있는 모달 창을 띄워줍니다.
- 사용자는 프롬프트 대화상자의 입력 필드에 원하는 값을 입력하고 확인을 누를 수 있습니다.
- 값을 입력하길 원하지 않는 경우는 취소(Cancel) 버튼을 누르거나 Esc를 눌러 대화상자를 빠져나가면 됩니다.

```jsx
result = prompt(title, [default]);
```

- title: 사용자에게 보여줄 문자열
- default: 입력 필드의 초깃값(선택값)

예시

```jsx
let age = prompt('나이를 입력해주세요.', 100);

alert(`당신의 나이는 ${age}살 입니다.`); // 당신의 나이는 100살입니다.
```

### 컨펌 대화상자

```jsx
result = confirm(question);
```

- `confirm` 함수는 매개변수로 받은 `question(질문)`과 확인 및 취소 버튼이 있는 모달 창을 보여줍니다.
- 사용자가 확인버튼를 누르면 `true`, 그 외의 경우는 `false`를 반환합니다.

예시

```jsx
let isBoss = confirm("당신이 주인인가요?");

alert( isBoss ); // 확인 버튼을 눌렀다면 true가 출력됩니다.
```


### 과제

---

사용자에게 이름을 물어보고, 입력받은 이름을 그대로 출력해주는 페이지를 만들어 보세요.

```jsx
let name = prompt("이름을 입력해 주세요.", "");
alert(name);
```
