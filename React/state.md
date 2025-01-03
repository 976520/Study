## 상태

1. 이해

   State는 react에서 데이터를 저장할 수 있는 특수한 변수이다. 이 state는 component 내에서 관리된다.

   값이 바뀌었을 시, 이것이 화면에 반영되도록 연결된 변수가 state이다. 따라서 JS에서 기본적으로 제공하는 기본적인 변수인 `const`, `let` 과는 다르게 state의 값이 변하면 그 값을 참조한 component들이 자동으로 다시 rendering된다.

   UI가 항상 최신의 데이터를 유지하기 때문에 동적인 값을 관리하기 편리하고, 변경된 값을 화면에 즉시 반영해야 할 때 유용하다.

2. 문법

   ```jsx
   const [state, setState] = useState(initialState);
   ```

   이 코드에서 `state`는 실질적으로 데이터가 들어가는 변수이고, `setState`는 `state`값을 update할 때 사용하는 함수이다.

   이때 반드시 `const`로 선언해 주어야 한다. State는 반드시 함수를 통해 값이 변경되어야 하기 때문이다. `let`으로 선언한다면 다음과 같은 요상한 할당이 가능할 수 있으며, 이는 react의 state 관리 알고리즘과 충돌할 수 있다.

   ```jsx
   let state = 1;
   ```

---
