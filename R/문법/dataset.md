## 데이터셋 관련 명령어

1. 불러오기

   다음과 같이 `read.csv()` 함수를 이용하여 불러올 수 있다.

   ```R
   data <- read.csv("data.csv")
   ```

   내장된 dataset의 경우 `library()` 함수를 이용하여 불러올 수 있다.

   ```R
   library(datasets)
   data(iris)
   ```

   여기서 `iris`는 R에 내장된 dataset으로, 3가지 종의 iris 개체 150개에 대해 조사한 자료로써, 각 개체의 꽃받침과 꽃잎의 길이와 넓이에 대한 정보가 담겨있다.

---
