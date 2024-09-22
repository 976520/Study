## PCB

> Process Control Block은 process에 대한 정보를 표현하는 OS kernel의 자료구조이다.

<img src="https://github.com/user-attachments/assets/c874d2a1-9f91-49a7-b4b8-bcb37e805e77" width="200">

PCB는 특정 process와 관련된 여러 정보와 함께 process를 시작하거나 다시 시작시키는 데 필요한 모든 data를 저장하며, 이의 구성은 다음과 같다.

1. [process state](https://github.com/976520/Study/blob/main/Operating%20System/process/Process%20State.md)

2. program counter

   Process가 다음에 실행할 명령어의 주소를 가리키는 pointer이다. 이후에 process가 다시 schedule될 때 계속 실행되어야 하므로, interrupt가 발생하면 이를 저장해야 한다.

3. CPU register

   Accumulator(누산기), index register, stack pointer, general-purpose(범용) register와 condition code(상태 코드) 등을 포함한다. PC와 같은 이유로 interrupt가 발생하면 이를 저장해야 한다.

4. CPU scheduling information

   Process의 우선순위, scheduling queue에 대한 pointer, 그리고 scheduling parameters 등 기타 scheduling 관련 정보를 포함한다.

5. memory management information

   사용되는 memory system에 따라 base register, limit register, page table, segment table 등을 포함한다.

6. accounting information

   Process의 CPU 사용 시간, 경괴된 실행 시간, 할당된 시간, 계정 번호, job 또는 process 번호 등을 포함한다.

7. I/O status information

   Process에 할당된 I/O devices와 열린 file 목록, 그리고 I/O buffer의 상태 등을 포함한다.

---
