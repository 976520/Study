## Java Server Pages

> JSP는 HTML에 java code를 넣어 dynamic(동적) web page를 생성하는 도구이다.

1. Dynamic(동적) web page

   Static web page는 web server에 저장된 파일을 그대로 전송하는 방식이다. Client가 어떤 request를 보내든 항상 동일한 모습을 보여준다.

   이와 달리 Dynamic web page는 서버에서 동적으로 생성되는 page이다. 같은 page라도 전처리 과정을 통해 각 request를 해석하여 이에 따라 다른 내용을 보여줄 수 있다.

2. 이해

   JSP는 WAS의 servlet container에서 **servlet으로 변환**되고, 이 servlet code가 compile되어 실행된다. Servlet이기 때문에 HTML 형태의 response를 생성하는데, 이를 통해 dynamic web page를 생성할 수 있다. 한변 servlet으로 변환된 JSP file은 cache에 저장되어 다음 요청이 있을 때 이를 통해 빠르게 응답할 수 있다.

3. 특징

   MVC pattern에서 view의 역할을 한다.

4. 문법

   Java code를 HTML 안에 넣기 위해 이렇게 생긴 scriptlet tag를 사용한다.

   ```jsp
   <% %>
   ```

   이 안에 java code나 JSP 지시어, JSP action tag를 넣을 수 있다.

   1. directive(지시어)

      JSP directive는 그 속성에 따라 java code를 생성한다. Directive는 `<%@ ... %>`와 같은 형태로 작성되며, JSP 페이지의 전체적인 속성을 지정할 때 사용된다. 주요 directive에는 다음과 같은 것들이 있다:

      1. page directive

         JSP page의 전반적인 속성을 지정한다.

         ```jsp
         <%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
         ```

         이 속성의 종류는 다음과 같다.

         1. `language`

            사용할 script language를 지정한다.

         2. `contentType`

            생성할 문서의 type과 encoding을 지정한다.

         3. `import`

            사용할 java class를 지정한다.

         4. `errorPage`

            Error 발생 시 보여줄 page를 지정한다.

      2. include directive

         다른 HTML이나 JSP 문서를 현재 JSP page에 포함시킨다.

         ```jsp
         <%@ include file="header.jsp" %>
         ```

         지정한 파일의 code를 그대로 현재 위치에 포함시킨다. 이름처럼 C언어의 `#include`랑 비슷하다.

      3. taglib directive

         ```jsp
         <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
         ```

         JSTL이나 사용자 정의 tag를 사용할 수 있도록 한다.

   2. declaration(선언부)

      Servlet class의 member variable이나 method를 선언하는 부분이다.

      ```jsp
      <%! %>
      ```

   3. expression(표현부)

      결과를 출력하는 역할을 한다.

      ```jsp
      <%= %>
      ```

   4. JSP action

      JSP에서 제공하는 tag들을 JSP action tag라고 한다.

      1. `<jsp:include>`

         다른 JSP 페이지를 포함시킨다.

         ```jsp
         <jsp:include page="example.jsp" />
         ```

      2. `<jsp:forward>`

         현재 page를 멈추고 `page`에 지정한 곳으로 이동시킨다.

         ```jsp
         <jsp:forward page="example.jsp" />
         ```

      3. `<jsp:param>`

         `<jsp:include>`, `<jsp:forard>`의 자식 tag로서 사용된다. 다른 page로 이동할 때 필요한 parameter를 전달한다.

         ```jsp
         <jsp:include page="example.jsp">
            <jsp:param name="id" value="123" />
         </jsp:include>
         ```

      4. `<jsp:element>`

         `<jsp:element>`은 특정 요소를 생성하는데 사용된다.

         ```jsp
         <jsp:element name="div">
            <jsp:attribute name="class">example</jsp:attribute>
            <jsp:body>Hello</jsp:body>
         </jsp:element>
         ```

   5. JSP implicit object

      JSP에서 별도의 선언 없이 사용할 수 있는 객체들을 말한다.

---
