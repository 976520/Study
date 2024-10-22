## 웹소켓

1. 이해

   HTTP 통신은 client가 request을 보내야 server가 response을 보낼 수 있는 방식이다. 이 방식은 비연결성(connectionless)을 가지기 때문에, server가 요청을 받지 않으면 client는 응답을 받을 수 없다. 이러한 문제를 해결하기 위해 web socket이 등장했다.

   Web socket은 client와 server 간의 양방향 통신을 가능하게 한다. 즉, server가 response을 보내지 않아도 client는 server에 data를 보낼 수 있으며, server도 client에 data를 보낼 수 있다.
