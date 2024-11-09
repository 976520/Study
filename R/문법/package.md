## 패키지 관련 명령어

1. 설치

   다음과 같이 매개변수로 package명을 넣어 해당 package를 설치할 수 있다.

   ```R
   install.packages("tensorflow")
   ```

1. 삭제

   비스무리하게 삭제도 가능하다.

   ```R
   remove.packages("tensorflow")
   ```

1. 불러오기

   다음과 같이 `library()` 함수를 이용하여 불러올 수 있다.

   ```R
   library(tensorflow)
   ```

   또한 `require()` 함수를 이용하여도 불러올 수 있다.

   ```R
   require(tensorflow)
   ```

   `library()`와 달리 package를 불러올 때 확인 메시지를 출력한다.

   ![image](https://github.com/user-attachments/assets/f52e7504-c89f-4640-abde-aa1090feb2c7)

---
