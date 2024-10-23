## 웹소켓

1. 이해

   HTTP 통신은 client가 request을 보내야 server가 response을 보낼 수 있는 방식이다. 이 방식은 비연결성(connectionless)을 가지기 때문에, server가 요청을 받지 않으면 client는 응답을 받을 수 없다. 이러한 문제를 해결하기 위해 WebSocket이 등장했다.

   WebSocket은 client와 server 간의 양방향 통신을 가능하게 한다. 즉, server가 response을 보내지 않아도 client는 server에 data를 보낼 수 있으며, server도 client에 data를 보낼 수 있다.

2. Hand Shake

   WebSocket의 Handshake는 HTTP protocol을 사용하여 이루어진다. Client가 server에 WebSocket connection을 요청하면, server는 이를 수락하거나 거부할 수 있다. 이 Handshake 과정은 다음과 같다

   1. Client가 server에 HTTP request을 보낸다. 이 요청은 upgrade header를 포함하여 WebSocket protocol로의 upgrade를 요청한다.

      ```HTTP
      GET /chat HTTP/1.1
      Host: server.example.com
      Upgrade: websocket
      Connection: Upgrade
      Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
      Sec-WebSocket-Version: 13
      ```

   2. Server가 client의 request를 수락하면, HTTP 101 Switching Protocols 응답을 보낸다. 이 응답은 client와 server 간의 WebSocket 연결이 성공적으로 수립되었음을 나타낸다.

      ```HTTP
      HTTP/1.1 101 Switching Protocols
      Upgrade: websocket
      Connection: Upgrade
      Sec-WebSocket-Accept: s3pPLMBiTxaQ9kYGzzhZRbK+xOo=
      ```

   3. Handshake가 완료되면, 클라이언트와 서버는 WebSocket 연결을 통해 데이터를 주고받을 수 있다. 이때부터는 HTTP 프로토콜이 아닌 WebSocket 프로토콜을 사용하여 통신이 이루어진다.

   WebSocket Handshake는 클라이언트와 서버 간의 초기 연결 설정을 위한 중요한 과정이며, 이를 통해 양방향 통신이 가능해진다.
