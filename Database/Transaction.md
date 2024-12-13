# 거래

> DB의 상태를 변화시키기 위해 수행하는 작업의 논리적 최소 단위이다.

---

1. 이해

   DB의 상태를 변화시키는 것은 다음 query를 수행하는 것이다.

   1. `SELECT`

   2. `INSERT`

   3. `UPDATE`

   4. `DELETE`

   그렇다고 하여 transaction이 query문 하나를 의미하지는 않는다. 예를 들어 게시판에 글을 쓰는 것은 다음 query를 수행하는 것이다.

   ```sql
   INSERT INTO board (title, context, writer) VALUES ('제목', '내용', '작성자');
   SELECT * FROM board;
   ```

   이와 같이 `INSERT`를 통해 게시물을 추가하고, `SELECT`를 통해 최신 게시물을 조회하는 것을 하나의 transaction으로 친다. 이처럼 한 번에 수행되어야만 하는 처리를 모은 것이 transaction이다.

   만약 두 query 중 게시물을 추가하는 것만 수행되고, 최신 게시물을 조회하는 것은 수행되지 않는다면 추가한 게시물이 조회되지 않는다면 문제가 생긴다. 반대로 최신 게시물을 조회하는 것만 수행되고, 게시물을 추가하는 것은 수행되지 않는 것 역시 문제이다.

   두 query를 한 transaction으로 묶어서 **모두 제대로 수행되었을 때만 결과를 반영**하고, **하나라도 실패하면 모든 작업을 취소하고 원상복구**하도록 한다. 이를 통해 data의 안정성을 보장한다.

2. 상태

   Transaction은 다음과 같은 상태를 가진다.

   <img src="https://github.com/user-attachments/assets/8ea0dfa5-5176-442e-bc8a-4742452ee1e0" alt="Transaction State" width="500">

   1. **Active(활동)**

      Transaction이 시작되고 연산들이 처리 중인 상태이다. 이때 transaction은 DB에 대한 읽기/쓰기 작업을 실행하며, 이 상태에서는 transaction의 결과가 아직 DB에 반영되지 않는다.

   이때 처리의 성공 여부에 따라 그 transaction의 운명이 결정된다. 처리를 성공적으로 수행했다면 Partially Committed 상태로 넘어간다.

   2. **Partially Committed(부분 완료)**

      Active에서 성공적으로 처리되었다고 바로 DB에 반영하는 것이 아니라 최종 승인이 되어야만 반영된다.

      Transaction이 마지막까지 성공적으로 처리되었지만, 아직 commit이 되지 않아 이를 기다리는 상태이다. Commit은 처리 결과를 `UPDATE`하여 DB에 영구 반영하겠다는 의미이다.

      이 상태에서는 언제든 abort(중단)되어 Failed 상태로 넘어갈 수 있다.

   3. **Committed(완료)**

      Transaction이 commit이 된 상태이다. Commit이 된 transaction은 성공적으로 종료되며, 이 상태가 되면 DB에 모든 변경사항이 영구적으로 반영된다.

      한번 committed 상태가 되면 어떤 장애가 발생하더라도 변경사항은 보존되어야 한다. 이는 transaction의 durability(영구성) 특성을 보장하기 위함이다.

   만약 처리가 실패했다면 Failed 상태로 넘어간다.

   4. **Failed(실패)**

      Transaction 실행 중 어떠한 오류가 발생하여 비정상적으로 중단된 상태이다.

      Transaction 작업을 이전 상태로 완전히 복구하기 위해 rollback을 수행한다. Rollback은 마지막 commit을 한 시점으로 되돌아가는 것이다.

   5. **Aborted(철회)**

      Transaction이 rollback된 상태이다. 이 상태에서는 transaction이 수행한 모든 변경사항이 취소되어 마지막 commit 시점으로 되돌아간다.

      Aborted 상태가 된 transaction은 재시작하거나 완전히 종료할 수 있다. 재시작하는 경우 새로운 transaction으로 간주되어 처음부터 다시 시작된다.

3. 특징

   Transaction은 다음과 같은 특징을 가진다.

   1. Atomicity(원자성)

      상술했듯, 하나의 transaction이 모두 제대로 수행되었을 때만 DB에 모두 반영하고, 아니라면 전혀 반영되지 않게 해야 한다는 것이 atomicity이다. 따라서 완전 성공 또는 완전 실패 둘 중 하나만 있고(all or nothing), 그 중간 상태는 존재하지 않는다.

   2. Consistency(일관성)

      Transaction의 처리 결과가 항상 일관적이여야 한다는 것이다.

   3. Isolation(격리성)

      여러 transaction이 동시에 실행되는 경우, 한 transaction이 수행되는 동안 다른 transaction이 결과를 참조하지 못하도록 격리하는 것이다.

   4. Durability(지속성)

      Transaction이 완료된 후, 그 결과는 영구적으로 저장되어야 한다는 것이다. 이는 장애가 발생하더라도 쉽게 복구하여 변경사항이 손실되지 않도록 보장하는 것이다.

---
