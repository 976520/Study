## 모델

1. 이해

   Django model은 data의 구조를 정의하고, 동작의 방식을 결정한다. 이는 `django.db.models.Model`을 상속받은 python class로 구현된다. 각 model의 DB field가 class의 각 attribute를 표현하는 단일 DB table에 mapping된다. Django는 DB의 객체를 쉽게 query할 수 있는 API를 제공한다.

2. 사용

   다음은 간단한 게시물 생성을 위한 model을 정의한 예시이다.

   ```python
   from django.db import models

   class Post(models.Model):
       title = models.CharField(max_length=100)
       slug = models.SlugField(max_length=100)
       content = models.TextField()
   ```

---
