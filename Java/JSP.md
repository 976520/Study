## Java Server Pages

> JSP는 HTML에 java code를 넣어 dynamic(동적) web page를 생성하는 도구이다.

1. Dynamic(동적) web page

   Static web page는 web server에 저장된 파일을 그대로 전송하는 방식이다. Client가 어떤 request를 보내든 항상 동일한 모습을 보여준다.

   이와 달리 Dynamic web page는 서버에서 동적으로 생성되는 page이다. 같은 page라도 전처리 과정을 통해 각 request를 해석하여 이에 따라 다른 내용을 보여줄 수 있다.

2. 이해

   JSP는 WAS의 servlet container에서 **servlet으로 변환**되고, 이 servlet code가 compile되어 실행된다. Servlet 형태이기 때문에 HTML 형태의 response를 생성하는데, 이를 통해 dynamic web page를 생성할 수 있다.

---
