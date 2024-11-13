# Redux

> redux는 react의 상태 관리 라이브러리이다.

외부 라이브러리이기 때문에 별도의 설치가 필요하다.

```shell
npm install redux @reduxjs/toolkit react-redux
```

---

## 개념

1.  상태 관리

    react의 경우 상태 관리를 위해 state를 사용한다. 하지만 이 state는 component 내에서 관리되기 때문에 여러 component에서 동일한 상태를 관리해야 하는 경우 이는 상태를 전달하기 위해 중간 component들을 계속 거쳐야 하는 props drilling 이슈가 생길 수 있다. 또한 component가 많아질수록 상태 관리가 복잡해지고 유지보수가 어려워진다.

    redux를 사용하면 store를 통해 어떤 component에서든 상태에 직접 접근할 수 있어 이러한 문제를 해결할 수 있다. 즉, 상태 관리를 component 외부에서 하는 것이다.

2.  원칙

    Redux에는 다음과 같은 세 가지 원칙이 있다.

    1.  Single source of truth

        App의 모든 state를 하나의 store에 저장한다.

    2.  State is read-only

        Store에 저장된 state는 read-only이므로, 직접 변경할 수 없다. Action으로만 state를 변경할 수 있다.

    3.  Changes are made with pure functions

        변경은 순수함수로만 이루어져야 한다.

3.  요소

    1.  store

        Store는 component와 별개로 state를 저장하는 전역 상태 저장소이다. 이 store에 app에서 필요한 state를 저장하고, 필요한 component에서 이 state를 쉽게 불러올 수 있다.

        `createStore()` method를 불러와서 store를 생성할 수 있다.

        ```js
        import { createStore } from "redux";

        const store = createStore(reducer);
        ```

        `Provider` component를 이용하여 store를 사용할 component를 감싸고, `Provider` component의 props로 store를 전달한다.

        ```js
        import { createRoot } from "react-dom/client";
        import { Provider } from "react-redux";

        createRoot(document.getElementById("root")!).render(
          <Provider store={store}>
            <App />
          </Provider>
        );
        ```

    2.  action

        Action은 app에서 store로 운반되는 data이다. JS 객체 형식으로 되어있으며, 어떤 action을 취할 지 결정하는 type을 가진다.

        ```js
        const CREATE_BUCKET = "bucket/CREATE";
        ```

        Action creator는 action을 생성하는 함수이다.

        ```js
        const createBucket = (bucket) => {
          return {
            type: CREATE_BUCKET,
            bucket: bucket,
          };
        };
        ```

        store의 `dispatch()` 메소드를 호출하면서 action 객체를 인자로 전달하면, reducer 함수가 호출되면서 해당 action에 따라 state가 변경된다.

        ```js
        store.dispatch(createBucket({ title: "bucket" }));
        ```

    3.  reducer

        Reducer는 action의 type에 따라 store에 저장된 state를 변경하는 함수이다.

        ```js
        const reducer = (state = initialState, action) => {
          switch (action.type) {
            case CREATE_BUCKET:
              return [...state, action.bucket];
            case DELETE_BUCKET:
              return state.filter((bucket) => bucket.id !== action.id);
            case UPDATE_BUCKET:
              return state.map((bucket) => (bucket.id === action.id ? { ...bucket, ...action.bucket } : bucket));
            default:
              return state;
          }
        };
        ```

        Reducer 함수의 첫번째 매개변수로 state의 초기값(initialState)을 기본값으로 설정한다.

4.  hooks

    Redux는 다음과 같은 hooks를 제공한다.

    1.  `useSelector`

        component에서 store에 저장된 state에 접근할 수 있게 한다.

        ```js
        import { useSelector } from "react-redux";

        const state = useSelector((state) => state);
        ```

        `useSelector`의 callback function 인자에 store에 저장된 모든 state가 담긴 객체가 전달된다.

    2.  `useDispatch`

        Dispatch를 사용할 수 있게 한다.

        ```js
        import { useDispatch } from "react-redux";

        const dispatch = useDispatch();
        dispatch(createBucket({ title: "bucket" }));
        ```

---
