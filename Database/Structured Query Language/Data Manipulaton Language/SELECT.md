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

`EMP` table의 `column1`과 `column2` 열을 출력한다. 이 자리에 `*`를 넣어서 모든 열을 출력하게 할 수 있다.

1. **WHERE 절**

   특정 조건에 맞는 data만 필터링하여 조회하게 한다. 프로그래밍 언어에서 if문과 비슷하다.

   ```sql
   SELECT ENAME FROM EMP
   WHERE DEPTNO = 30;

   /*
    ENAME
    --------------------
    ALLEN
    WARD
    MARTIN
    BLAKE
    TURNER
    JAMES
   */
   ```

   이와 같이 입력하면 `DEPTNO`가 30인 열의 `ENAME`만 출력하는 식이다.

   1. 비교 연산자

      등호 뿐만 아니라 여러 비교 연산자를 사용하여 이를 만족하는 결과만 출력하게 할 수 있다.

      ```SQL
      SELECT ENAME, SAL FROM EMP
      WHERE SAL >= 3000;

      /*
      ENAME                       SAL
      -------------------- ----------
      SCOTT                      3000
      KING                       5000
      FORD                       3000
      */
      ```

      이와 같이 입력하면 `SAL`이 3000 이상인 열의 `ENAME`과 `SAL`을 출력한다.

      숫자 뿐만 아니라 문자도 비교할 수 있다. 예를 들어 다음과 같이 입력하면,

      ```SQL
      SELECT ENAME FROM EMP
      WHERE ENAME >= 'J';

      /*
      ENAME
      --------------------
      SMITH
      WARD
      JONES
      MARTIN
      SCOTT
      KING
      TURNER
      JAMES
      MILLER
      */
      ```

      사전 순서로 알파벳 `'J'`보다 뒤에 있는 `ENAME`만 출력한다. 이때 대소문자를 구분한다.

   2. 산술 연산자

      조건에서 여러 산술 연산자를 이용할 수 있다.

      ```sql
      SELECT * FROM EMP
      WHERE SAL * 12 + 1000 >= 36000;
      ```

   3. `NOT`

      특정 조건 앞에 붙여서 만족하지 않는 데이터만 출력하게 할 수 있다.

   4. `AND` `OR`

      여러 조건을 만족하는 결과만 출력하게 할 수 있다.

      ```sql
      SELECT * FROM EMP
      WHERE DEPTNO = 30 AND JOB = 'SALESMAN';
      ```

      이와 같이 압력하면 `DEPTNO`가 30임과 동시에 `JOB`이 `'SALESMAN'`인 열만 출력한다.

   5. `IN`

      더 여러 조건을 만족하는 결과만 출력하게 할 수 있다.

      ```sql
      SELECT ENAME, JOB FROM EMP
      WHERE JOB IN ('MANAGER', 'SALESMAN', 'CLERK');


      /*
      ENAME                JOB
      -------------------- ------------------
      SMITH                CLERK
      ALLEN                SALESMAN
      WARD                 SALESMAN
      JONES                MANAGER
      MARTIN               SALESMAN
      BLAKE                MANAGER
      CLARK                MANAGER
      TURNER               SALESMAN
      ADAMS                CLERK
      JAMES                CLERK
      MILLER               CLERK
      */
      ```

      이 경우 `'MANAGER'`, `'SALESMAN'`, `'CLERK'` 중 하나라도 해당되는 데이터를 출력한다.

   6. `BETWEEN`

      다음과 같이 입력하여 `SAL`값이 2000과 3000 사이인 데이터를 출력할 수 있다.

      ```sql
      SELECT ENAME, SAL FROM EMP
      WHERE SAL BETWEEN 2000 AND 3000;

      /*
      ENAME                       SAL
      -------------------- ----------
      JONES                      2975
      BLAKE                      2850
      CLARK                      2450
      SCOTT                      3000
      FORD                       3000
      */
      ```

      이는 비교 연산자를 활용하여 다음과 같이 나타낼 수 있다.

      ```sql
      SELECT * FROM EMP
      WHERE SAL >= 2000 AND SAL <= 3000
      ```

   7. `IS NULL`

      값이 `NULL`인 데이터를 출력한다. `IS NOT NULL`로 `NULL`이 아닌 데이터를 출력 할 수도 있다.

   8. `LIKE`

      문자열 패턴 매칭을 위해 사용된다. `%`와 `_` 와일드카드를 사용하여 다양한 패턴을 검색할 수 있다. `%`는 0개 이상의 임의의 문자를 나타내고, `_`은 정확히 1개의 임의의 문자를 나타낸다.

      ```sql
      SELECT * FROM EMP
      WHERE ENAME LIKE '__S%'
      ```

      이와 같이 입력하면 이름의 3번째 글자가 'S'인 모든 사원을 검색한다. 처음 두 글자는 어떤 문자든 가능하고, 'S' 뒤에는 어떤 문자열이 어떤 개수로든 올 수 있다.

2. **GROUP BY 절**

   `GROUP BY` 바로 다음에 오는 column 기준으로 같은 값을 가진 행들을 하나의 그룹으로 묶어 처리한다. 주로 집계 함수와 함께 사용하여 그룹별 통계를 계산할 때 활용된다.

   ```sql
   SELECT DEPTNO, COUNT(*), AVG(SAL) FROM EMP
   GROUP BY DEPTNO;

   /*
         DEPTNO   COUNT(*)   AVG(SAL)
     ---------- ---------- ----------
             30          6 1566.66667
             20          5       2175
             10          3 2916.66667
   */
   ```

   이 쿼리는 부서별로 직원 수, 평균 급여, 최대 급여, 최소 급여를 계산한다. `GROUP BY`를 사용할 때는 SELECT 절에 그룹화 기준 열과 집계 함수만 사용할 수 있다.

   여러 열을 기준으로 그룹화도 가능하다.

   ```sql
   SELECT DEPTNO, JOB, COUNT(*), AVG(SAL)
   FROM EMP
   GROUP BY DEPTNO, JOB;

   /*
      DEPTNO JOB                  COUNT(*)   AVG(SAL)
   ---------- ------------------ ---------- ----------
          20 CLERK                       2        950
          30 SALESMAN                    4       1400
          20 MANAGER                     1       2975
          30 CLERK                       1        950
          10 PRESIDENT                   1       5000
          30 MANAGER                     1       2850
          10 CLERK                       1       1300
          10 MANAGER                     1       2450
          20 ANALYST                     2       3000
   */
   ```

   이 쿼리는 `DEPTNO`와 `JOB`별로 열의 수와 `SAL`의 평균을 계산한다.

3. **HAVING 절**

4. **ORDER BY 절**

   특정 속성을 기준으로 정렬할 수 있다.

   다음 명령어를 실행하면

   ```sql
   SELECT ENAME, SAL FROM EMP
   ORDER BY SAL DESC;
   ```

   `EMP` table의 모든 열을 `SAL`값 기준으로 내림차순 정렬한다. `DESC` 대신 `ASC`를 넣으면 오름차순 정렬이 된다.

   다음과 같이 사용하여 오름차순과 내림차순을 동시에 사용할 수 있다.

   ```sql
   SELECT ENAME, SAL FROM EMP
   WHERE SAL >= 2500
   ORDER BY DEPTNO ASC, SAL DESC;

   /*
    ENAME                       SAL
    -------------------- ----------
    KING                       5000
    SCOTT                      3000
    FORD                       3000
    JONES                      2975
    BLAKE                      2850
   */
   ```

   `SAL`이 2500 이상인 열을 `DEPTNO`에 대해 오름차순, `SAL`에 대해 내림차순으로 정렬하여 출력한다.

5. **집계 함수**

   - `COUNT()`, `SUM()`, `AVG()`, `MAX()`, `MIN()`

6. **JOIN 절**

## 사용
