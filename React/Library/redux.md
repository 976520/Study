# Redux

> redux는 react의 상태 관리 라이브러리이다.

외부 라이브러리이기 때문에 별도의 설치가 필요하다.

```shell
npm install redux @reduxjs/toolkit react-redux
```

---

## 개념

1. 상태 관리

   react의 경우 상태 관리를 위해 state를 사용한다. 하지만 이 state는 component 내에서 관리되기 때문에 여러 component에서 동일한 상태를 관리해야 하는 경우 이는 상태를 전달하기 위해 중간 component들을 계속 거쳐야 하는 props drilling 이슈가 생길 수 있다. 또한 component가 많아질수록 상태 관리가 복잡해지고 유지보수가 어려워진다.

   redux를 사용하면 store를 통해 어떤 component에서든 상태에 직접 접근할 수 있어 이러한 문제를 해결할 수 있다. 즉, 상태 관리를 component 외부에서 하는 것이다.

2. store

   store는 component와 별개로 state를 저장하는 전역 상태 저장소이다. 이 store에 app에서 필요한 state를 저장하고, 필요한 component에서 이 state를 쉽게 불러올 수 있다.

   1. Action

      Action의 type을 만드는 곳이다. Action을 불러올 주소를 정의한다고 생각하면 편하다.

      ```js
      const CREATE = "bucket/CREATE";
      ```

   1. Action creator

      Action creator는 말 그대로 action을 생성하는 함수이다.

      ```js
      const createBucket = (bucket) => {
        return {
          type: CREATE,
          bucket: bucket,
        };
      };
      ```

---
