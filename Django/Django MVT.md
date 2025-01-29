## controller는 어디갔어요?

Django framework 자체가 controller 역할을 수행한다. URL 구성에 따라 적절한 view로 요청을 보내는 방식이다.

1. 이해

   1. model

      Django에서 model은 **DB와 view 사이**에서 사용될 data에 대한 정의를 담당하며, **DB의 구조를 Python class로 표현**한다. Model class는 django.db.models.Model을 상속받아 구현되며, 각 attribute는 DB의 필드를 나타낸다.

      1. object relational mapping

         > Object relational mapping(ORM)은 OOP의 class와 관계형 DB의 table을 자동으로 mapping해주는 기술이다.

         Raw SQL 쿼리 대신 직관적인 python method를 통해 DB를 조작할 수 있고 schema를 정의하고 변경할 수 있다는 ㄹㅈㄷ 장점이 있다. Model class의 변경사항을 자동으로 DB에 commit하는 migration 기능을 제공한다.

   2. view

      UI를 담당하는 계층으로, 사용자로부터의 입력을 받고 결과를 적절한 template를 통해 사용자에게 표시하는 역할을 한다.

   3. template

      Dynamic data를 HTML로 rendering하는 presentation 계층으로, 사용자에게 보여질 HTML을 제어한다.

2. 구조

   아래 그림은 MVT pattern을 이용하여 django가 HTTP request를 처리하는 방법을 나타낸다.

   <img src="https://github.com/user-attachments/assets/31d65400-d041-46e1-bc97-a36067d173f5" alt="Image" width="500">

   Browser에서 URL을 통해 요청을 보내면, Web server가 요청을 받아서 Django에 전달한다. Django는 요청을 뜯어서 설정된 URL을 확인하고, 일치하는 URL에 해당하는 view를 실행한다.

   그럼 view는 model을 이용하여 DB로부터 data를 검색하여 가져오고 template을 이용하여 표시할 HTML을 생성한다. 이는 Web server에 의해 browser로 전달되어 사용자에게 표시된다.

---
