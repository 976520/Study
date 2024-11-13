## 복합체

1. 이해

   > 객체들의 관계를 tree로 구성하여 부분-전체 계층을 재귀적으로 표현하는 방법이다.

   Composite pattern은 composite(복합 객체)와 leaf(단일 객체)를 동일한 component로 취급하는 pattern이다.

   다음 그림과 같은 OS의 파일 시스템 구조가 있다고 가정할 때, directory는 그 안에 여러 파일을 포함할 수 있으며, 다른 directory를 포함할 수도 있다. 이러한 구조는 directory가 여러 객체를 포함할 수 있는 composite임을 의미한다. 반면, 파일은 그 자체로 존재하는 단일 객체이다. 즉, 파일은 더 이상 다른 객체를 포함하지 않으며, 최종적인 구성 요소이다. 따라서, directory는 composite로, 파일은 leaf로 취급됩니다.

   ![image](https://github.com/user-attachments/assets/c72f21e8-768a-4052-8312-b8a595d1b36f)

   Composite pattern은 이 directory와 file을 구분하지 않고 동일한 interface를 사용하도록 하는 pattern이다.

2. 사용

   1. python

      ```python
        from abc import ABC, abstractmethod

        class Element(ABC):
            @abstractmethod
            def show_structure(self, indent=0):
                pass

        class File(Element):
            def __init__(self, name):
                self.name = name

            def show_structure(self, indent=0):
                print(' ' * indent + f"File: {self.name}")

        class Folder(Element):
            def __init__(self, name):
                self.name = name
                self.children = []

            def add(self, element):
                self.children.append(element)

            def show_structure(self, indent=0):
                print(' ' * indent + f"Folder: {self.name}")
                for child in self.children:
                    child.show_structure(indent + 2)

        file1 = File("file1.txt")
        file2 = File("file2.txt")
        file3 = File("file3.txt")

        folder1 = Folder("Folder1")
        folder1.add(file1)
        folder1.add(file2)

        folder2 = Folder("Folder2")
        folder2.add(file3)
        folder2.add(folder1)

        folder2.show_structure()

        '''
        출력:

        Folder: Folder2
          File: file3.txt
          Folder: Folder1
            File: file1.txt
            File: file2.txt
        '''
      ```

   2. java

      ```java
      import java.util.ArrayList;
      import java.util.List;

      abstract class Element {
          abstract void showStructure(int indent);
      }

      class File extends Element {
          private final String name;

          public File(String name) {
              this.name = name;
          }

          @Override
          public void showStructure(int indent) {
              System.out.println(" ".repeat(indent) + "File: " + name);
          }
      }

      class Folder extends Element {
          private final String name;
          private final List<Element> children = new ArrayList<>();

          public Folder(String name) {
              this.name = name;
          }

          public void add(Element element) {
              children.add(element);
          }

          @Override
          public void showStructure(int indent) {
              System.out.println(" ".repeat(indent) + "Folder: " + name);
              for (Element child : children) {
                  child.showStructure(indent + 2);
              }
          }
      }

      public class Main {
          public static void main(String[] args) {
              File file1 = new File("file1.txt");
              File file2 = new File("file2.txt");
              File file3 = new File("file3.txt");

              Folder folder1 = new Folder("Folder1");
              folder1.add(file1);
              folder1.add(file2);

              Folder folder2 = new Folder("Folder2");
              folder2.add(file3);
              folder2.add(folder1);

              folder2.showStructure(0);
          }
      }

      /*
      출력:

      Folder: Folder2
        File: file3.txt
        Folder: Folder1
          File: file1.txt
          File: file2.txt
      */
      ```

   두 코드에서 모두 abstract class로 선언한 `Element`를 이용하여 `composite`과 `leaf`를 정의하고 있다.

---
