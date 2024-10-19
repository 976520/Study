# 교차 ㅊ.. 뭐?

> CORS는 Cross Origin Resource Sharing의 약자로, 직역하면 교차 출처 자원 공유 라는 뜻이다.

CORS를 설정한다는 뜻은 browser가 자신의 origin이 아닌 다른 origin으로부터 resource를 load하는 것을 server가 허가해주도록 하는 것이다.

~~필자와 같은 뉴비 웹 개발자들을 한 번씩은 괴롭혀 주는~~ CORS error 역시 이 CORS 설정을 하라는 소리이다.

---

## 원리

1. Request

   대개 application에서 다른 origin의 resource를 request할 때는 HTTP protocol을 이용하게 되는데, 이 때 browser는 Request header의 origin이라는 filed에 요청을 보내는 출처를 함께 보내게 된다.

2. Response

   Server에서 그에 대한 응답을 할 때, Response header에 Access-Control-Allow-Origin 정보를 담아 보낸다.

   이때 header에 access를 허락하는 내용이 없다면 CORS error가 발생하기도 한다.

3. 대조

   Server가 response에 Access-Control-Allow-Origin header를 포함하지 않거나, request한 origin이 server에서 허용된 origin과 일치하지 않으면, browser는 그 request를 차단한다. 이때 browser는 CORS error를 개발자 console에 표시한다.
