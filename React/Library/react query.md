# 쿼리..? SQL..?

> React query는 react 환경에서 데이터 관리를 편리하게게 해주는 라이브러리이다.

React query이지만, vue.js나 svelte에서도 이용할 수 있게 확장되며 TanStack query라고도 불린다.

외부 라이브러리이기 때문에 별도의 설치가 필요하다.

```shell
npm install react-toastify
```

---

## 개념

React query 데이터 관리는, **서버 상태**에 대해 fatching, caching 등의 작업을 수행하는 것이다.

1. 서버 상태

   > 서버 상태란 클라이언트에서 제어할 수 없는 위치에서 관리되는 상태이다.

   소유권이 공유되어 다른 사용자가 데이터를 변경할 수 있다는 특징이 있다. 이를 fatching하고 update하기 위해서는 비동기 api가 필요하다.
