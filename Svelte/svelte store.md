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

4. methods

   Writable store에서는 다음과 같은 method들을 제공한다.

   1. subscribe

      store의 값이 변경될 때마다 자동으로 반영되도록 한다. 이 method는 callback 함수를 인자로 받아, store의 값이 변경될 때마다 해당 callback 함수가 호출되도록 한다. 이를 통해 store의 상태 변화를 감지하고, 필요한 동작을 수행할 수 있다.

   2. set

      `store의 값을 설정하는 데 사용된다. 이 method는 새로운 값을 인자로 받아, store의 현재 값을 해당 값으로 변경한다. 이를 통해 store의 상태를 직접적으로 업데이트할 수 있다.

   3. update

      store의 값 중 일부를 변경하는 데 사용된다. 이 method는 현재 값을 인자로 받아 새로운 값으로 반환하는 callback 함수를 인자로 받는다. 이를 통해 store의 상태를 부분적으로 업데이트할 수 있다.

   4. get

      store의 현재 값을 가져오는 데 사용된다. 이 method는 store의 현재 값을 반환하여, 외부에서 해당 값을 참조할 수 있도록 한다.

---
