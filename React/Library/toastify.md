## 토스틔파이

> react-toastify는 react에서 toast를 만들 수 있게 해주는 라이브러리이다.

외부 라이브러리이기 때문에 별도의 설치가 필요하다.`shell
npm install react-toastify`

1. toast

   Toast는 사용자에게 직접 보이는 알림 메시지를 의미하며, 보통 error나 event 발생 시 이를 알리기 위해 사용한다. 간단한 알림으로 대부분 추가적인 event를 요구하지 않는다.

   Vanilla JS에 `alert()`가 있지만 너무 못생겼고, 확인 버튼을 누르는 event를 요구하기 때문에 일반적으로 toast를 사용한다.

2. 사용

   App.js나 index.js에 ToastContainer를 import하고 컴포넌트를 추가한다.

   ```jsx
   import { ToastContainer, toast } from "react-toastify";
   import "react-toastify/dist/ReactToastify.css";

   function App() {
     return (
       <div>
         <ToastContainer />
       </div>
     );
   }
   ```

   그리고 toast를 쓰고 싶은 component에서 다음과 같이 사용할 수 있다.

   ```jsx
   import { toast } from "react-toastify";

   function Component() {
     const notify = () => {
       toast("i am toast lol");
     };

     return (
       <>
         <button onClick={notify}>who is toast?</button>
       </>
     );
   }
   ```

3. 종류

   우리가 사용자에게 제공하려는 알림에는 여러 목적이 있다. 이에 따라 toast의 종류도 다음과 같이 나뉜다.

   ```jsx
   toast("i am default toast");
   toast.success("i am success toast");
   toast.error("i am error toast");
   toast.warning("i am warning toast");
   toast.info("i am info toast");
   ```

   위에서부터 순서대로 기본, 성공, 오류, 경고, 정보 알림을 위한 toast이다. 기호에 맞게 사용하면 된다.

---
