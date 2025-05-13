## 서버 컴포넌트

> Server component는 번들링 전에 client app이나 SSR server와는 다른 별도의 환경에서 미리 랜더링되는 component이다.

요구사항에 따라 어디에서 렌더링할 지 정할 수 있다.

---

1. 이해

   Client component만 이용하여 app을 구축할 때보다 번들 사이즈가 작아지는 장점이 있다. 크고 우람한 의존성은 모두 server 측에서 처리하고, 아담하고 cacheable한 런타임 결과만 클라이언트로 전송한다.

2. 특징

   1. 서버에서만 실행되며 클라이언트로 전송되지 않는다

      JWT token이나 API key 등 보안상 민감한 데이터를 안전하게 보호할 수 있다.

   2. **client측 interactivity를 사용할 수 없다**

      useState, useEffect와 같은 React client hook이나 lifecycle 관련 기능을 사용할 수 없으며, 브라우저 API나 Event에 접근할 수 없다.

      따라서 일단 모두 server component로 개발하고, interactive한 UI만 client component로 하는 식이 좋다.

   3. 백엔드 리소스에 직접 접근 가능하다

      Database나 File system에 접근이 가능하긴 하지만, 특별한 이유가 없다면 더 나은 성능과 사용자 경험을 위해 Server에서 하는걸 권장한다고 한다.

3. 사용

   파일 최상단에 다음과 같은 지시문을 추가하면 client component로 인식한다.

   ```jsx
   "use client";
   ```

   해당 파일 뿐만 아니라, 의존하고 있는 모든 module과 하위 component들이 모두 client component가 된다.

---
