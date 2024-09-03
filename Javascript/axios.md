# 액시오스

> Axios는 Promise API를 활용하는 비동기 통신 라이브러리이다.

외부 라이브러리이기 때문에 별도의 설치가 필요하다.

```shell
npm install axios

yarn add axios
```

---

## 이해

1. 개념

   Axios는 JS6 기반의 HTTP 라이브러리로, 서버와 클라이언트 간의 통신을 아주 간편하게 해준다. javascript에서는 fetch를 이용하여 api 통신을 해도 무방하지만, 간결한 코드를 통한 간편성과 더불어 편리한 에러 handling, 취소 기능, timeout 기능 등 유용성 또한 가지기 때문에 axios를 이용하는 경우도 다분하다.

   하지만 비교적 큰 라이브러리 크기와 추가적인 종속성이 필요한 경우가 있다. fetch API와 비교해 브라우저 호환성 문제는 덜하지만, 최신 브라우저에서 fetch 를 선호하는 경우도 있다.

2. 특징

   Axios는 Promise 기반이기 때문에 기본적으로 비동기적인 request와 response 처리를 지원한다. 이러한 HTTP request와 response를 JSON 형태로 자동으로 변환하며, HTTP 요청을 캔슬하거나, 요청과 응답에 대해 인터셉터를 사용할 수 있는 등 유연한 기능을 제공한다.

   또한, 클라이언트 측에서 쿠키와 인증 토큰 등을 쉽게 관리할 수 있도록 도와준다. Error Handling이 간편하고, Node.js와 브라우저 환경 모두에서 사용할 수 있는 범용성을 갖추고 있다. 다양한 HTTP 메서드와 URL 매개변수 등을 쉽게 설정할 수 있어 REST API 통신을 보다 효율적으로 할 수 있다.

---

## 문법

1. 구조

   대략적인 구조는 다음과 같다.

   ```javascript
   axios({
     url: "대충 통신할 URL",
     data: {
       data: "대충 인자로 보낼 데이터",
     },
   });
   ```

   axios를 이용한 요청 중에서 `url`, `data`와 같은 파라미터 config을 추가할 수 있으며, 그 종류는 다음과 같다.

2. config

   1. `url`

      통신할 서버의 주소이다.

   1. `method`

      사용할 [HTTP](https://github.com/976520/TIL/blob/main/network/HTTP%EC%99%80%20%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C.md) request 방식을 정한다. 기본값은 `get`이다.

      1. `get`

         `get`은 서버에서 데이터를 받아서 보여줄 때 사용한다.

         ```javascript
         const getData = async () => {
           const response = await axios.get("URL");
           console.log(response.data);
         };
         ```

      2. `post`

         `post`는 리소스를 새롭게 생성할 때 사용한다. 이때 두 번째 인자로 첫 번째의 URL 주소로 보낼 데이터 객체가 들어가게 된다.

         ```javascript
         const postData = async () => {
           const response = await axios.post("URL", { data: "data" });
           console.log(response.data);
         };
         ```

      3. `delete`

         이름에서 알 수 있듯, `delete`는 URL 주소에서의 데이터를 삭제한다. 따라서 두 번째 인자를 전달할 필요가 없다.

         ```javascript
         const deleteData = async () => {
           const response = await axios.delete("URL");
           console.log(response.data);
         };
         ```

      4. `put`

         `put`은 보낸 내용으로 리소스를 덮어쓸 때 사용한다.

         ```javascript
         const putData = async () => {
           const response = await axios.put("URL", { data: "data" });
           console.log(response.data);
         };
         ```

      5. `patch`

         `put`과 비슷하게 리소스를 갱신하기 위해 사용되지만, `patch`는 보낸 내용으로 리소스의 일부만을 변경할 때 사용한다.

         ```javascript
         const patchData = async () => {
           const response = await axios.put("URL", { data: "data" });
           console.log(response.data);
         };
         ```

   1. `data`

      요청 방식이 `put`, `post`, `patch` 일 경우 보낼 데이터이다.

   1. `timeout`

      request가 timeout되는 시간을 지정한다. 이때 단위는 ms이며, 기본값은 0으로 이 옵션을 사용하지 않으면 적용되지 않는다.

      request에 걸리는 시간이 설정된 시간보다 길다면 request가 중단되고, 예외가 catch로 전달된다.

      ```javascript
      axios({ timeout: 5000 });
      ```

   1. `responseType`

      `responseType`는 서버로부터 받아오는 response 데이터의 형식을 정할 때 사용한다.

      1. json

         `responseType`의 기본값으로, 옵션을 사용하지 않으면 서버로부터 json 형식의 데이터를 받아온다.

      2. text

         서버로부터 text 형식의 데이터를 받아온다.

         ```javascript
         const getTextData = async () => {
           const response = await axios.get("URL", {
             responseType: "text",
           });
           console.log(response.data);
         };
         ```

      3. blob

         서버로부터 blob 형식의 데이터를 받아온다. blob은 binary large object의 약자로, 하나의 리소스로 저장되는 이진 데이터의 모임이다. 일반적으로 이미지, 오디오 등 멀티미디어 형태이다.

         다음은 이미지를 blob 형식으로 받아와서 blob URL을 생성하고 이미지 요소를 생성하는 코드이다.

         ```javascript
         const getImageData = async () => {
           const response = await axios.get("URL", {
             responseType: "blob",
           });
           const img = document.createElement("img");
           img.src = URL.createObjectURL(response.data);
           document.body.appendChild(img);
         };
         ```

      4. arraybuffer

         서버로부터 이진 데이터를 arraybuffer 형식으로 받아온다.

         다음 코드에서는 arraybuffer 형식으로 가져온 데이터를 Uint8Array(8비트 부호 없는 정수)로 변환하여 출력한다.

         ```javascript
         const fetchBinaryData = async () => {
           const response = await axios.get("URL", {
             responseType: "arraybuffer",
           });
           console.log(new Uint8Array(response.data));
         };
         ```

---

## 사용

1. api 통신

   [promise](https://github.com/976520/TIL/blob/main/javascript/promise.md)만 쓸 때와, [async, await](https://github.com/976520/TIL/blob/main/javascript/async%2C%20await.md)를 쓸 때와 비교하는 것이 중요하다.

   ```javascript
   function fetchData(url) {
     return axios
       .get(url)
       .then((response) => {
         response.data;
       })
       .catch((error) => {
         throw error;
       });
   }
   ```

2. async, await 병행 사용

   위와 같이 chaining을 계속 이어나가다 보면 복잡한 요청의 경우 handler가 끝없이 이어져 코드의 가독성이 떨어질 수 있다. 따라서 async, await를 다음과 같이 적절히 이용하여 이를 해결할 수 있다.

   ```javascript
   async function fetchData(url) {
     try {
       const response = await axios.get(url);
       return response.data;
     } catch (error) {
       throw error;
     }
   }
   ```

3. 요청 취소

   Axios에서는 요청을 취소하기 위해 `CancelToken`을 사용한다. 이 기능을 사용하면 다음과 같이 요청을 보낸 후 언제든지 해당 요청을 무효화 할 수 있다. 아래 코드에서는 1초 간격으로 요청을 두 번 보내게 되는데, 두 번째 요청이 들어갔을 때 첫 번째 요청이 취소되게 된다.

   ```javascript
   const CancelToken = axios.CancelToken;
   let cancel;
   function fetchData(url) {
     if (cancel) cancel();

     return axios
       .get(url, {
         cancelToken: new CancelToken((c) => (cancel = c)),
       })
       .then((response) => {
         response.data;
       })
       .catch((error) => {
         throw error;
       });
   }

   fetchData("First_URL");

   setTimeout(() => {
     fetchData("Second_URL");
   }, 1000);
   ```

---
