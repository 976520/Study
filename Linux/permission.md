## permission denied please try again

1. 개념

   대부분의 파일 시스템에서는 group 각 파일과 directory에 **사용자 혹은 group의 read(읽기), write(쓰기), execute(사용)에 대한 접근 권한**을 부여할 수 있으며 이를 permission이라고 한다.

   Linux를 포함한 Unix 계열 OS들도 이러한 permission 시스템을 가지고 있으며, 이를 traditional Unix permissions 라고 하기도 한다.

2. 조회

   파일과 directory에게 부여된 권한은 다음 명령어를 통해 확인항 수 있다.

   ```shell
   ls al
   ```

   이 명령어를 입력하면 다음과 같은 형식으로 모든 파일과 directory의 상세 정보가 출력될 것이다.

   ![image](https://github.com/user-attachments/assets/0ac17d3e-d883-4705-adf7-c7833b7c2b20)

   이때 한 행의 첫 열에서 파일 유형을 나타내는 첫 글자를 제외한, `drwxr-x---`와 같이 생긴 것이 permission에 대한 정보이다.

---
