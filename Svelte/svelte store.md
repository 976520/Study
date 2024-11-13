## 스벨트도 상태 관리 할 수 있어요..!

> store는 svelte의 전역 상태 관리 도구이다.

1. 이해

   Svelte에서 전역으로 사용 가능한 state 저장소라고 생각하면 된다.

2. 생성

   먼저 store로 사용할 파일을 생성해야 한다. 보통 `stores.js` 로 이름을 지정한다.

   Svelte store에서 writable module을 불러와서 다음과 같이 사용한다. 이때 writable의 인자에 초기값으로 지정할 값을 넣는다.

   ```svelte
   <script>
     import { writable } from "svelte/store";
     export const count = writable(0);
   </script>
   ```

3. 참조

   생성한 store를 참조하는 방법은 다음과 같다. store 값의 경우 일반적인 상태와 달리 $(달러) 기호를 사용하여 참조한다.

   ```svelte
   <script>
     import { count } from "./stores.js";
     const increment = () => {
       $count += 1;
     };
   </script>

   <h1>{$count}</h1>
   <button on:click={increment}>click</button>
   ```

---
