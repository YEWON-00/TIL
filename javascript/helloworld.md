### script 태그

script 태그를 이용하면 자바스크립트 프로그램을 HTML 문서 대부분의 위치에 삽입할 수 있습니다.

```html
<!DOCTYPE HTML>
<html>

<body>

  <p>스크립트 전</p>

  <script>
    alert( 'Hello, world!' );
  </script>

  <p>스크립트 후</p>

</body>

</html>
```

### 외부 스크립트

자바스크립트 코드의 양이 많은 경우엔, 파일로 소분하여 저장할 수 있습니다.

이렇게 분해해 놓은 각 파일은 `src` 속성을 사용해 HTML에 삽입합니다.

```html
<script src="/path/to/script.js"></script>
```

**`src` 속성이 있으면 태그 내부의 코드는 무시됩니다.**

`<script>` 태그는 `src` 속성과 내부 코드를 동시에 가지지 못합니다.

다음 코드는 실행되지 않습니다.

```html
<script src="file.js">
  alert(1); // src 속성이 사용되었으므로 이 코드는 무시됩니다.
</script>
```

따라서 `<script src="…">`로 외부 파일을 연결할지 아니면 `<script>` 태그 내에 코드를 작성할지를 선택해야 합니다.

위의 예시는 스크립트 두 개로 분리하면 정상적으로 실행됩니다.

```html
<script src="file.js"></script>
<script>
  alert(1);
</script>
```

### 요약

- 웹 페이지에 자바스크립트 코드를 추가하기 위해 `<script>` 태그를 사용합니다.
- `type` 과 `language` 속성은 필수가 아닙니다.
- 외부 스크립트 파일은 `<script src="path/to/script.js"></script>`와 같이 삽입합니다.

### 과제

---

****alert 창 띄우기****

"자바스크립트!"라는 메시지를 담고 있는 alert 창을 띄워주는 페이지를 만들어 보세요.

```html
// helloworld.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
   <script>
    alert( "I'm JavaScript!" );
   </script>
</body>
</html>
```

****외부 스크립트를 이용해 alert 창 띄우기****

이전 과제 [alert 창 띄우기](https://ko.javascript.info/task/hello-alert)의 해답에 있는 스크립트를 `alert.js`라는 외부 파일로 옮겨보세요.

해당 파일을 문서와 동일한 경로로 옮긴 후, 스크립트가 기존처럼 alert 창을 잘 띄워주는지 확인해보세요.

```html
// helloworld.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script src="./alert.js"></script>
</body>
</html>
```

```jsx
//alert.js

alert("I'm javascript!");
```
