# Java Server Pages

> JSP는 HTML에 java code를 넣어 동적인 web page를 생성하는 도구이다.

---

## suvlet

1. 이해

   > Suvlet이란 동적인 web page를 만들기 위해 사용되는 java class이다.

   Suvlet은 WAS에서 실행된다. WAS가 client로부터 요청을 받으면 알맞은 suvlet을 찾아 그의 `service()` method를 실행하고, 해당 suvlet은 그에 대한 기능을 수행한 후 response를 전송한다. 따라서 client의 request에 대해 동적으로 작동하는 component라고 할 수 있다.

2. 생명주기

   Suvlet도 class이기 때문에 생명주기가 있다.

   1. client의 request가 오면 container는 해당하는 suvlet이 있는지 찾는다.

      만약 없을 경우, `init()`을 호출하여 memory상에 올린다. `init()`은 요청 시 최초 한 번만 실행되며, 이름처럼 suvlet 초기화 작업을 수행한다. Suvlet의 thread에서 공통적으로 써야 하는 logic이 있다면 이를 override하여 구현하면 된다.

      실행 중 suvlet이 update되면 `destroy()`를 통해 memory상에서 삭제한 후, 다시 `init()`을 통해 새로운 suvlet을 올린다.

   2.

3. 특징

   Java의 thread를 이용한다.

   MVC pattern에서 controller의 역할을 한다.

---
