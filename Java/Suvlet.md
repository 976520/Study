## servlet

> Servlet이란 동적인 web page를 만들기 위해 사용되는 java class이다.

1. 이해

   JSP와 달리 java code 안에 HTML을 넣어 사용한다.

   Servlet은 WAS에서 실행된다. WAS가 client로부터 요청을 받으면 `HttpServletRequest`와 `HttpServletResponse` 객체를 만들고 알맞은 servlet을 찾아 그의 `service()` method를 실행한다. 해당 servlet은 `HttpServletRequest`에 있는 기능을 수행한 후 `HttpServletResponse`에 담아 전송한다. WAS는 이를 받아 HTTP response를 생성하여 client에 반환한다. 따라서 **client의 request에 대해 동적으로 작동하는 component**라고 할 수 있다.

2. 생명주기

   Servlet도 class이기 때문에 생명주기가 있다.

   1. client의 request가 오면 container는 해당하는 servlet이 있는지 찾는다.

      만약 없을 경우, `init()`을 호출하여 memory상에 올린다. `init()`은 요청 시 최초 한 번만 실행되며, 이름처럼 servlet 초기화 작업을 수행한다. Servlet의 thread에서 공통적으로 써야 하는 logic이 있다면 이를 override하여 구현하면 된다.

      실행 중 servlet이 update되면 `destroy()`를 통해 memory상에서 삭제한 후, 다시 `init()`을 통해 새로운 servlet을 올린다.

   2. `service()` method가 실행된다.

      받은 요청에 따라 `doGet()` 또는 `doPost()` method를 실행한다. `doGet()`과 `doPost()`는 각각 GET과 POST 요청에 대한 기능을 수행하며, `HttpServletResponse`에 응답을 전송하는 역할을 한다.

      이 `service()`는 request가 올 때마다 실행된다.

   3. `destroy()` method가 실행된다.

      `destroy()`는 servlet이 종료되어 memory에서 소멸될 때 실행된다. 이는 주로 servlet이 종료될 때 필요한 작업을 수행할 때 이를 override하여 구현하면 된다.

3. servlet container

   1. 생명주기 관리

      Servlet의 생명주기를 관리하는 역할을 한다. Servlet을 loading하여 instance화하고 `init()`을 통해 초기화하는 역할을 한다. 또한 수명이 끝난 servlet을 garbage collection을 통해 삭제 한다.

   2. multi thread 지원

      Servlet container는 thread pool을 이용하여 요청을 처리하는데, 새로운 요청이 올 때마다 thread pool에서 가용한 thread를 할당하고,
      HTTP method를 처리하고 나면 thread를 pool로 반환한다. 이를 통해 thread 생성/소멸의 오버헤드를 줄이고 효율적인 자원 관리를 할 수 있다.

   3. 보안 관리

      `web.xml` 파일을 통해 보안 관련 설정을 하면, 보안 관련 update가 발생해도 java code를 수정하여 compile을 다시 할 필요가 없다.

      물론 annotation을 이용하여 할 수도 있다...

4. 특징

   Multi thread를 지원하기 위해 java의 thread를 이용한다.

   MVC pattern에서 controller의 역할을 한다.

   HTML을 이용하여 response를 작성한다. 이 HTML의 변경이 일어나면 다시 compile 과정을 거쳐 변경된 내용을 반영한다.

---
