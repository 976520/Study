## React에서도.. Markov Process에서도.. 여기서도..?

Process는 여러 상태를 가질 수 있다. 이러한 상태들은 process의 현재 활동에 따라 변화한다.

<img src="https://github.com/user-attachments/assets/7a496ef3-c4f1-47c7-bc89-d90d70186d79" width="400">

Process는 다음 상태 중 하나를 취하게 된다.

1. new

   Process가 생성 중인 상태이다. 여기서 생성 중이란, process가 생성되었지만 아직 OS에 의해 admit(승인)되지 않은 상태이다.

2. running

   명령어들이 실행되고 있는 상태이다.

3. waiting

   Process가 어떠한 event가 일어나기를 기다리는 상태이다. 이 event에는 입출력 완료, 신호의 수신 등이 있다.

4. ready

   Process가 처리기, 즉 CPU를 할당받기를 기다리는 상태이다.

5. terminated

   Process의 실행이 종료된 상태이다.
