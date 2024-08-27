# 돔? 참돔? 줄돔?

> DOM은 XML, HTML 문서의 각 항목을 계층으로 표현하여 생성, 변형, 삭제 할 수 있도록 돕는 인터페이스이다.

DOM은 Document Object Model(문서 객체 모델)의 약자로 JS에서 HTML의 문서에 접근할 수 있는 API이다. 여기서 접근이란, 정의에서 알 수 있듯 HTML의 요소를 JS의 Object처럼 조작할 수 있다는 뜻이다!

---

## DOM 이해

다음과 같은 HTML 문서가 있다고 가정해보자.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>sexy title</title>
  </head>
  <body>
    <p>sexy text</p>
    <a>sexy href</a>
  </body>
</html>
```

이렇게 텍스트 파일로 만들어진 문서를 브라우저에 렌더링하려면 이를 브라우저가 이해할 수 있는 구조로 메모리에 올려야 한다. 브라우저에 내장된 화면을 그리는 엔진(rendering engine)이 이 문서를 로드한 후, 다음과 같이 **파싱하여 브라우저가 이해할 수 있는 구조로 표현**하고 메모리에 로드하는데, 이를 DOM이라고 부르는 것이다.

<img src="https://github.com/976520/TIL/assets/123460320/a5a08e31-c5c2-4521-a1bd-7793ab3ddbd2" width="400"/>

즉, 모든 요소와 속성을 객체로 만들고, 이 객체를 **부모-자식 관계를 표현하는 트리 구조로 구성**한 것이 DOM이다. DOM의 의의는 DOM이 제공하는 API를 이용해 개발자가 JS로 이것을 조작할 수 있는 데에 있다. JS는 이것을 이용해 HTML 요소나 style을 생성/변경/삭제하거나 event를 추가하고 그에 반응할 수 있다.

이때 `<html>`, `<head>`와 같은 tag들은 모두 이 트리의 node이자 element이다. 하지만 “sexy text”, “sexy link”와 같이 text로 표현된 것들은 element는 아니지만 node는 맞다.

---

## DOM 조회

DOM구조를 조회할 때는 `console.dir` 을 사용한다. 이는 `console.log` 와 다르게 DOM을 Object 형태로 출력한다.

1. `<body>`의 자식요소

   `console.dir(document.body)` 를 입력하여 body 아래의 모든 속성을 객체의 형태로 확인할 수 있다. 이중 chileren이 body의 자식요소를 뜻한다.

   <img src="https://github.com/976520/TIL/assets/123460320/6b0a5d3a-d22e-4ac3-8884-6ac3872c222b" width="800"/>

   정신없으니까 `console.dir(document.body.children)` 을 통해 자식 요소만 골라내보자.

   <img src="https://github.com/976520/TIL/assets/123460320/e2b3b60b-4cc8-403d-84ac-9e458ec65bb4" width="400"/>

   여기서 `console.dir(document.body.children[n])` 으로 n번째 자식만을 조회할 수 있다.

2. 특정 id를 가진 엘리먼트의 자식요소

   매번 자식요소를 조회할 때 마다 `console.dir(document.body.children[3])` 이런걸 쓰고 있으면 귀찮기 마련이다. 이럴 때 따로 변수 선언을 하고 id를 할당하면 번거롭지 않을 수 있다.

   ```jsx
   const exampleId = document.body.children[3];
   console.dir(exampleId);
   ```

3. 특정 id를 가진 엘리먼트의 부모요소 ~~느그 아부지 뭐하시노~~

   `console.dir(document.body.children[n].parentElement)` 는 n번째 자식 요소의 부모요소를 조회하는 코드이다. 정말 읽기 불편하기 때문에 아까와 같이 변수 선언을 해서 가독성을 높여보겠다.

   ```jsx
   const exampleId = document.body.children[3];
   console.dir(exampleId.parentElement);
   ```

---

## DOM 조작

JS에서는 DOM을 조작하여 HTML 요소에 대해 변경, 추가, 삭제 등의 작업을 할 수 있다.

1. 선택

   `getElementById()`, `getElementsByClassName()`를 통해 각각 특정 id 혹은 class를 가진 요소를 선택할 수 있다.

   ```javascript
   const firstElement = document.getElementById("id");
   const secondElement = document.getElementsByClassName("class");
   ```

   또한 `querySelector()`, `querySelectorAll()`을 통해 CSS 선택자를 이용해 요소를 선택할 수 있다.

   ```javascript
   const firstElement = document.querySelector("#id");
   const secondElement = document.querySelector(".class");
   ```

2. 생성

   `createElement()`를 통해 새로운 요소를 생성할 수 있고, `appendChild()`를 통해 생성한 요소를 특정 부모 요소의 하위에 추가할 수 있다.

   ```javascript
   const element = document.createElement("div");
   document.body.appendChild(element);
   ```

   `prepend()`를 통해 부모 요소의 첫 번째 자식으로 요소를 추가할 수 있고, `before()`,`after()`를 통해 각각 선택한 요소의 앞과 뒤에 새 요소를 추가할 수 있다.

3. 삭제

   `removeChild`를 통해 부모 요소로부터 특정 자식 요소를 제거할 수 있다.

   ```javascript
   const parentElement = document.getElementById("parent");
   const childElement = document.getElementById("child");
   parentElement.removeChild(childElement);
   ```

4. 속성 조작

   `setAttribute`, `getAttribute`를 통해 요소의 속성을 설정하거나 조회할 수 있다. 이때 첫 번째 매개변수로 변경할 속성의 이름, 두 번째 매개변수로 변경할 내용을 입력한다. 또한 `classList`를 통해 다음과 같이 요소의 class를 추가, 제거, 혹은 토글할 수 있다.

   ```javascript
   const link = document.querySelector("a");
   link.setAttribute("href", "https://velog.io/@haensol/dom");
   link.classList.add("active");
   ```

5. style 조작

   `style`을 이용해 요소의 CSS style을 조작할 수 있다.

   ```javascript
   const root = document.getElementById("root");
   root.style.color = "tomato";
   ```

6. event 추가

   `addEventListener`를 통해 요소에 event listener를 추가하여 특정 event에 반응하게 할 수 있다.

   ```javascript
   const button = document.querySelector("button");
   button.addEventListener("click", () => {
     alert("clicked");
   });
   ```

---
