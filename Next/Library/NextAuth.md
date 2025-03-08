## Auth.js

> NextAuth는 Next.js 앱의 유저 인증과 세션 관리를 위한 라이브러리이다.

외부 라이브러리이기 때문에 별도의 설치가 필요하다.

```shell
npm install next-auth@beta path-to-regexp
```

다음 명령어를 통해

```shell
npx auth secret
```

---

1. 설정

   NextAuth는 다른 라이브러리처럼 설치하고 끝이 아니라 별도의 설정이 약간 필요하다.

   우선 다음과 같은 `NEXTAUTH_SECRET` 환경변수를 생성할 수 있다.

   ```env
   NEXTAUTH_SECRET=514cim00000RBthAEmZ0000000000y364MAIgtNfn000
   ```

   그리고 app/api/auth/[...nextauth].js

2. OAuth
