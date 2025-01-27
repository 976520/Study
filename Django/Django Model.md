## 모델

1. 이해

   Django model은 data의 구조를 정의하고, 동작의 방식을 결정한다. 이는 `django.db.models.Model`을 상속받은 python class로 구현된다. 각 model의 DB field가 class의 각 attribute를 표현하는 단일 DB table에 mapping된다. Django는 DB의 객체를 쉽게 query할 수 있는 API를 제공한다.

2. 사용

   다음은 간단한 게시물 model을 정의한 예시이다.

   ```python
   from django.db import models

   class Post(models.Model):
       title = models.CharField(max_length=100)
       slug = models.SlugField(max_length=100)
       content = models.TextField()
   ```

   `title`은 게시물의 제목을 나타내는 field이며, SQL에서 `VARCHAR` type으로 변환되는 `CharField`이다.

   `slug`는 게시물의 고유 식별자를 나타내는 field이며, `VARCHAR` type으로 변환되는 `SlugField`이다.

   `content`는 게시물의 본문을 나타내는 field이며, `TEXT` type으로 변환되는 `TextField`이다.

   ```sql
   CREATE TABLE posts (
       id INT AUTO_INCREMENT PRIMARY KEY,
       title VARCHAR(100),
       slug VARCHAR(100),
       content TEXT
   );
   ```

   Django는 이 field들에 대응하는 DB column을 생성한다. 이때 각 model에 자동으로 primary key field를 추가하며, 이는 `settings.py`의 `DEFAULT_AUTO_FIELD`를 통해 설정되고, 기본값은 `BigAutoField`이다. Model field에 `primary_key=True`를 설정하여 model field 중 하나를 primary key로 정의할 수 있다.

---
