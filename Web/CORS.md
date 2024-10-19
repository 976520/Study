# 교차 ㅊ.. 뭐?

> CORS는 Cross Origin Resource Sharing의 약자로, 직역하면 교차 출처 리소스 공유 라는 뜻이다.

CORS를 설정한다는 뜻은 브라우저가 자신의 origin이 아닌 다른 출처로부터 자원을 load하는 것을 서버가 허가해주도록 하는 것이다.

~~필자와 같은 뉴비 웹 개발자들을 한 번씩은 괴롭혀 주는~~ CORS error 역시 이 CORS 설정을 하라는 소리이다.

---

## SOP

1. 이해

   SOP는 Same Origin Policy의 약자로, 다른 출처에서 가져온 리소스와 상호작용하는 것을 제한하는 정책이다.

   이를 통하여 잠재적 악성 문서를 격리하여, XSS(Cross-Site Scripting) 및 CSRF(Cross-Site Request Forgery, 요청 위조)등의 보안 공격을 막을 수 있다는 장점이 있다.

   SOP를 위반하였는지는 서버가 아닌 브라우저가 확인하게 된다.

1. 적용

   SOP가 적용되는 리소스는 다음과 같다.

   1. 쿠키

      동일 출처에서만 쿠키에 접근할 수 있다.

   2. DOM

      동일 출처에서만 DOM 조작이 가능하다.

   3. AJAX 요청

      동일 출처에서만 AJAX를 통한 데이터 요청 가능.

---

## Origin
