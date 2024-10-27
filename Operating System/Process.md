# Kim Ximya X D.Sanders - Process <-- 명곡추

> Process는 실행 중인 program을 의미한다.

## 이해

1. 등장 배경

   초기의 컴퓨터는 한 번에 하나의 작업만을 처리할 수 있었다. 실행되고 있는 하나의 program이 system을 완전히 제어하고, 모든 자원에 access할 수 있었다. 하지만 현재는 memory에 다수의 program이 적재되어 병행 실행 되는 것이 가능하다. 이러한 변화는 다양한 program을 보다 효율적으로 제어하고 구획화할 것을 필요로 했다.

2. 개념

   Process는 현대의 computer system에서 작업의 단위를 의미한다.

   OS는 각각의 program을 독립적인 공간에 적재하고, 이를 위해 각각의 program에 대한 독립적인 memory 영역을 제공하는 방법을 사용한다. 이러한 각각의 독립적인 memory 영역을 가지는 program을 process라고 한다.

   OS가 복잡해질수록, 사용자를 위해 더 많은 기능을 제공한다. 예를 들어 하나의 system은 일부는 사용자에게 직접적으로 제공되는 서비스를 제공하고, 일부는 kernel에서 작업을 처리하는 process들로 구성된다. 이 process들은 병행 실행이 가능하며, CPU는 이 process 간에서 multiplex(다중화)된다.

---
