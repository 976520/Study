## 관계형 DB model

1. 이해

   관계형 database은 data가 table(표) 형태로 표현되어서 단순하고, user가 data를 쉽게 조회하고 관리할 수 있도록 자연어에 가까운 SQL(Structured Query Language)을 제공한다.

   1. Relation

      Relation은 관계형 DB에서 정보를 구분하는 기본 단위이며, 행(row)과 열(column)로 구성된다. Relation은 서로를 구분하기 위해 이름을 가지며, 이는 동일한 DB에서 중복될 수 없다. 가령 학생에 대한 정보를 저장하기 위해 STUDENT라는 relation을 생성하는 식이다.

   2. Attribute

      한 relation은 어떠한 entity에 대한 정보를 저장하기 위해 사용된다. 이렇게 표현할 entity의 구체적인 특성을 나타내는 것이 attribute이다. 예를 들어 학생 entity에 대한 정보를 저장하기 위해 STUDENT relation을 생성한다면, 학생의 이름, 나이, 학번 등의 특성을 나타내는 attribute를 생성하는 식이다.

      Attribute는 또한 서로를 구분하기 위해 이름을 가지며, 이는 동일한 relation에서 중복될 수 없다.

   3. Tuple

   4. Domain

---
