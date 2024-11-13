## 복합체

1. 이해

   > 객체들의 관계를 tree로 구성하여 부분-전체 계층을 표현하는 방법이다.

   Composite pattern은 composite(복합 객체)와 leaf(단일 객체)를 동일한 component로 취급하는 pattern이다.

   다음 그림과 같은 OS의 파일 시스템 구조가 있다고 가정할 때, directory는 그 안에 여러 파일을 포함할 수 있으며, 다른 directory를 포함할 수도 있다. 이러한 구조는 directory가 여러 객체를 포함할 수 있는 composite임을 의미한다. 반면, 파일은 그 자체로 존재하는 단일 객체이다. 즉, 파일은 더 이상 다른 객체를 포함하지 않으며, 최종적인 구성 요소이다. 따라서, directory는 composite로, 파일은 leaf로 취급됩니다.

   ![image](https://github.com/user-attachments/assets/c72f21e8-768a-4052-8312-b8a595d1b36f)

   Composite pattern은 이 directory와 file을 구분하지 않고 동일한 interface를 사용하도록 하는 pattern이다.

2. 사용

---
