# SELECT

> table의 data를 조회하는 명령어이다.

---

## 문법

```sql
SELECT column1, column2, ... FROM table_name
[WHERE condition]
[GROUP BY column1, column2, ...]
[HAVING condition]
[ORDER BY column1, column2, ... [ASC|DESC]]
[LIMIT number];
```

다음 명령어를 실행하면

```sql
SELECT column1, column2 FROM EMP;
```

`EMP` table의 `column1`과 `column2` 열을 출력한다. 이 자리에 \*(애스터리스크)를 넣어서 모든 열을 출력하게 할 수 있다.

1. **WHERE 절**

   특정 조건에 맞는 data만 필터링하여 조회하게 한다. 프로그래밍 언어에서 if문과 비슷하다.

   ```sql
   SELECT * FROM EMP
   WHERE DEPTNO = 30;
   ```

   이와 같이 입력하면 `DEPTNO`가 30인 열만 출력하는 식이다.

   1. 비교 연산자

      등호 뿐만 아니라 여러 비교 연산자를 사용하여 이를 만족하는 결과만 출력하게 할 수 있다.

      ```SQL
      SELECT * FROM EMP
      WHERE SAL >= 3000;
      ```

      이와 같이 입력하면 `SAL`이 3000 이상인 열을 출력한다.

      숫자 뿐만 아니라 문자도 비교할 수 있다. 예를 들어 다음과 같이 입력하면,

      ```SQL
      SELECT * FROM EMP
      WHERE ENAME >= `J`;
      ```

      사전 순서로 알파벳 `'J'`보다 뒤에 있는 데이터만 출력한다.

   1. 산술 연산자

      조건에서 여러 산술 연산자를 이용할 수 있다.

      ```sql
      SELECT * FROM EMP
      WHERE SAL * 12 + 1000 >= 36000;
      ```

   1. `NOT`

      특정 조건 앞에 붙여서 만족하지 않는 데이터만 출력하게 할 수 있다.

   1. `AND` `OR`

      여러 조건을 만족하는 결과만 출력하게 할 수 있다.

      ```sql
      SELECT * FROM EMP
      WHERE DEPTNO = 30 AND JOB = 'SALESMAN';
      ```

      이와 같이 압력하면 `DEPTNO`가 30임과 동시에 `JOB`이 `'SALESMAN'`인 열만 출력한다.

   1. `IN`

      더 여러 조건을 만족하는 결과만 출력하게 할 수 있다.

      ```sql
      SELECT * FROM EMP
      WHERE JOB IN ('MANAGER', 'SALESMAN', 'CLERK');
      ```

      이 경우 `'MANAGER'`, `'SALESMAN'`, `'CLERK'` 중 하나라도 해당되는 데이터를 출력한다.

   1. `BETWEEN`

      다음과 같이 입력하여 `SAL`값이 2000과 3000 사이인 데이터를 출력할 수 있다.

      ```sql
      SELECT * FROM EMP
      WHERE SAL BETWEEN 2000 AND 3000;
      ```

      이는 비교 연산자를 활용하여 다음과 같이 나타낼 수 있다.

      ```sql
      SELECT * FROM EMP
      WHERE SAL >= 2000 AND SAL <= 3000
      ```

   1. `IS NULL`

      값이 `NULL`인 데이터를 출력한다. `IS NOT NULL`로 `NULL`이 아닌 데이터를 출력 할 수도 있다.

2. **GROUP BY 절**

3. **ORDER BY 절**

   특정 속성을 기준으로 정렬할 수 있다.

   다음 명령어를 실행하면

   ```sql
   SELECT * FROM EMP
   ORDER BY SAL DESC;
   ```

   `EMP` table의 모든 열을 `SAL`값 기준으로 내림차순 정렬한다. `DESC` 대신 `ASC`를 넣으면 오름차순 정렬이 된다.

   다음과 같이 사용하여 오름차순과 내림차순을 동시에 사용할 수 있다.

   ```sql
   SELECT * FROM EMP
   ORDER BY DEPTNO ASC, SAL DESC;
   ```

   `DEPTNO`에 대해 오름차순, `SAL`에 대해 내림차순으로 정렬된다.

4. **LIMIT 절**

   결과 집합의 행 수를 제한할 수 있다. 많은 양의 데이터 중 일부만 보고 싶을 때 사용된다. 페이지네이션같은걸 구현할 때 유용하다.

   다음 명령어를 실행하면

   ```sql
   SELECT * FROM EMP
   LIMIT 5;
   ```

   `EMP` table의 상위 5개 행만 출력한다.

   OFFSET과 함께 사용하여 시작 위치를 지정할 수도 있다.

   ```sql
   SELECT * FROM EMP
   LIMIT 5 OFFSET 10;
   ```

   이와 같이 입력하면 10개를 건너뛰고 11번째 행부터 5개의 행을 출력한다.

5. **집계 함수**

   - `COUNT()`, `SUM()`, `AVG()`, `MAX()`, `MIN()`

6. **JOIN 절**

## 사용
