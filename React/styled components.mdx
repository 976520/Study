# Router

> react router는 react의 css-in-js 라이브러리 중 하나이다.

외부 라이브러리이기 때문에 별도의 설치가 필요하다.

```shell
npm install styled-components
```

## 개념

1. inline styleing

   Inline styleing은 코드 내에 style 속성을 사용하여 스타일을 적용하는 방식이다.

2. styled components

   Component를 이용하여 style을 작성할 수 있게 해주는 라이브러리이다. React의 경우 component가 많아질수록 CSS 파일을 관리하기가 힘들어진다. styled components를 사용하면, CSS를 component화하여 JSX로 작성하고, 상황에 따라 `import`하거나 `export`를 하여 사용할 수 있다.

   이에 따라 코드의 재사용성이 높아지고, 유지보수성이 좋아진다는 장점이 있다.

---

## 사용

styled components를 파일에 다음과 같이 `import` 하여 사용한다.

```javascript
import styled from "styled-components";

const ButtonExample = styled.div`
  font-size: 16px;
  background-color: red;
`;

const App = () => {
  return (
    <>
      <ButtonExample />
      <ButtonExample />
    </>
  );
};
```

1. styled component 선언

   `styled.태그명` 형식으로 선언하여 component에 할당한다. 태그명에 알맞은 HTML 태그명을 사용할 수 있다.

2. styled component 사용

   일반 component를 사용하는 방법과 동일하다. 다음과 같이 파일을 분리하여 `export`하고,

   ```javascript
   const ButtonExample = styled.div`
     font-size: 16px;
     background-color: tomato;
   `;

   export default ButtonExample;
   ```

   이후 다른 파일에서 `import`하여 사용할 수 있다.

   ```javascript
   import ButtonExample from "./ButtonExample";

   const App = () => {
     return (
       <>
         <ButtonExample />
         <ButtonExample />
       </>
     );
   };
   ```

3. 상속

   이미 생성된 styled components와 동일한 스타일을 적용하고 싶을 때, 상속을 이용하여 편리하게 작성할 수 있다.

   ```javascript
   import styled from "styled-components";
   import ButtonExample from "./ButtonExample";

   const ButtonExample2 = styled(ButtonExample)`
     font-size: 16px;
     background-color: tomato;
   `;
   ```

4. props

   styled component의 스타일에 props를 적용하여 동적으로 스타일을 변경할 수 있다.

   ```javascript
   const ButtonExample3 = styled.div`
     color: ${(props) => (props.primary ? "tomato" : "black")};
   `;
   ```

   이 코드에서는 `primary` props가 `true`일 때 `tomato` 색상을, `false`일 때 `black` 색상을 적용한다.

5. 가상 선택자

   styled components에서는 가상 선택자를 사용할 수 있다. `&`를 사용하여 현재 component를 참조할 수 있다.

   ```javascript
   const ButtonExample4 = styled.button`
     &:hover {
       background-color: lime;
     }
   `;
   ```

6. global style

   Global로 CSS style을 적용하고 싶은 경우, styled components의 `createGlobalStyle`을 사용하여 작성할 수 있다.

   ```javascript
   import styled, { createGlobalStyle } from "styled-components";
   import ButtonExample from "./ButtonExample";

   const GlobalStyle = createGlobalStyle`
     body {
       margin: 0;
       padding: 0;
       font-family: sans-serif;
     }
     button {
       background-color: tomato;
     }
   `;

   function App() {
     return (
       <>
         <GlobalStyle />
         <ButtonExample />
         <ButtonExample />
       </>
     );
   }
   ```

---
