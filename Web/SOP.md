## SOP

1. 이해

   SOP는 Same Origin Policy의 약자로, 다른 출처에서 가져온 resource와 상호작용하는 것을 제한하는 정책이다.

   SOP를 위반하였는지는 server가 아닌 browser가 확인하게 된다. 이 때 다음 중 하나라도 다르면 출처가 다르다고 간주한다.

   1. Protocol

   2. Host (domain)

   3. Port

   이를 통하여 잠재적 악성 문서를 격리하여, XSS(Cross-Site Scripting) 및 CSRF(Cross-Site Request Forgery, 요청 위조)등의 보안 공격을 막을 수 있다는 장점이 있다.

2. 적용

   SOP가 적용되는 리소스는 다음과 같다.

   1. cookie

      동일 출처에서만 cookie에 access할 수 있다.

   2. DOM

      동일 출처에서만 DOM 조작이 가능하다.

   3. AJAX 요청

      동일 출처에서만 AJAX를 통한 data request 이 가능하다.

3. 예외

   1. CORS

      서버에서 적절한 header로 허용된 경우는 access가 허용된다.

   2. `<script>` 태그

      이를 이용한 JSONP 취약점이 있다.

   3. 이미지, stylesheet 등

---
