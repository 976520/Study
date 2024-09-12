## permission denied please try again

1. 개념

   대부분의 파일 시스템에서는 group 각 파일과 directory에 **사용자 혹은 group의 read(읽기), write(쓰기), execute(사용)에 대한 접근 권한**을 부여할 수 있으며 이를 permission이라고 한다. read는 파일을 열어서 열람할 수 있는 권한, write는 파일을 쓰거나 잘라낼 수 있는 권한, execute는 파일을 프로그램으로 처리하여 실행할 수 있도록 허용하는 권한이다.

   Linux를 포함한 Unix 계열 OS들도 이러한 permission 시스템을 가지고 있으며, 이를 traditional Unix permissions 라고 하기도 한다.

2. 조회

   파일과 directory에게 부여된 권한은 다음 명령어를 통해 확인항 수 있다.

   ```shell
   ls al
   ```

   이 명령어를 입력하면 다음과 같은 형식으로 모든 파일과 directory의 상세 정보가 출력될 것이다.

   ![image](https://github.com/user-attachments/assets/0ac17d3e-d883-4705-adf7-c7833b7c2b20)

   이때 한 행의 첫 열에서 파일 유형을 나타내는 첫 글자를 제외한, `rwxr-x---`와 같이 생긴 것이 permission에 대한 정보를 나타낸 것이다.

3. bit pattern

   앞서 예시로 나온 `rwxr-x---`를 다시 세 글자씩 분리해 보자면 `rwx` `r-x` `---` 와 같이 나뉠 것이다. 이는 순서대로 파일 소유자(user)의 권한, 파일 소유 group의 권한, 그 외 기타 사용자의(ohter)의 권한을 뜻한다.

   또한 권한의 세 종류인 read, write, execute를 각각 한 글자로 줄여 r, w, x로 표현한다. 권한이 있다면 종류에 따라 r, w, x 중 하나를 작성하고, 권한이 없다면 글자가 들어갈 자리를 -(하이픈)으로 대체한다.

   예를 들어 `rwx` `r-x` `---` 의 경우, 부여된 권한은 다음과 같다.

   - 파일 소유자는 read, write, execute가 모두 가능하다.
   - 파일 소유 group는 read, execute는 가능하지만 write는 불가능하다.
   - 이외의 경우 read, write, execute 모두 불가능하다.

4. octat

---
