### view

> 뷰의 사용목적 - 보안에 유리
> 

emp 테이블의 급여와 커미션(수당)을 제외한 내용으로 테이블을 구성

```sql
create view emp_view
as
select empno, ename, job, mgr, hiredate, deptno
from emp;
```

---

> 뷰 제거
> 

1) 생성된 뷰 이름 검색

```sql
select view_name
from user_views;
```

```sql
VIEW_NAME
--------------------
EMP_COPY_VIEW
EMP_VIEW
EMP_VIEW_DEPT
EMP_VIEW_DEPT30
```

2) emp_view 삭제

```sql
drop view emp_view;
```

---

> 뷰 옵션
> 

**1) or replace : 뷰를 생성하는데, 이미 존재하면 overwrite 하는 옵션**

- 이미 존재하는 emp_view_dept30에 sal 추가(변경)하기

```sql
create or replace view emp_view_dept30
as
select empno, ename, sal, deptno
from emp_copy
where deptno=30;
```

*** 이미 'emp_view_dept30' 이라는 뷰가 있는데 똑같은 이름의 뷰를 생성했음에도 불구하고 오류가 나지 않음
     ⇒ or replace 라는 속성 때문에 있는 뷰를 대체해주기 때문!*

```sql
select view_name, text
from user_views
where view_name = 'EMP_VIEW_DEPT30';
```

```sql
VIEW_NAME            TEXT
-------------------- --------------------------------------------------------------------------------
EMP_VIEW_DEPT30      select empno, ename, sal, deptno
                     from emp_copy
                     where deptno=30
```

**2) with check option : 조건의 컬럼 값을 뷰를 통해서 변경하지 못하게 하는 옵션** 

- 실습에 필요한 테이블 생성

```sql
create table emp_copy2
as
select * from emp_copy;
```

- 뷰 생성

```sql
create or replace view view_chk30
as
select empno, ename, sal, deptno
from emp_copy2
where deptno = 30
with check option;
```

```sql
SQL> select * from view_chk30;

EMPNO ENAME         SAL DEPTNO
----- ---------- ------ ------
 7499 ALLEN        1600     30
 7521 WARD         1259     30
 7654 MARTIN       1250     30
 7698 BLAKE        2850     30
 7844 TURNER       1500     30
 7900 JAMES         950     30
```

- 급여가 1200 이상인 사원의 부서 번호를 20으로 변경하기

```sql
update 테이블명
set 변경할값
where 조건;
```

```sql
update view_chk30
set deptno = 20
where sal >= 1200;
```

*** ERROR at line 1:
    ORA-01402: view WITH CHECK OPTION where-clause violation
     => 뷰에 WITH CHECK OPTION이 있기 때문에 변경하지 못함!*

- 급여(sal)가 1300보다 작은 경우 급여를 1000 인상

```sql
SQL> select * from view_chk30;

EMPNO ENAME         SAL DEPTNO
----- ---------- ------ ------
 7499 ALLEN        1600     30
 7521 WARD         1259     30
 7654 MARTIN       1250     30
 7698 BLAKE        2850     30
 7844 TURNER       1500     30
 7900 JAMES         950     30
```

```sql
update view_chk30
set sal = sal + 1000
where sal <= 1300;
```

```sql
SQL> select * from view_chk30;

EMPNO ENAME         SAL DEPTNO
----- ---------- ------ ------
 7499 ALLEN        1600     30
 7521 WARD         2259     30
 7654 MARTIN       2250     30
 7698 BLAKE        2850     30
 7844 TURNER       1500     30
 7900 JAMES        1950     30
```

*** 조건절(where)에 있는 컬럼 값만 변경하지 못할 뿐 다른 건 변경 가능함!*

**3)  with read only : 기본 테이블의 내용을 변경하지 못하게 함**

- comm을 추가한 'view_chk30' 뷰 생성

```sql
create or replace view view_chk30
as
select empno, ename, sal, comm, deptno
from emp_copy2
where deptno = 30
with check option;
```

- comm을 1000으로 변경

```sql
update view_chk30
set comm = 1000;
```

```sql
SQL> select * from view_chk30;

EMPNO ENAME         SAL   COMM DEPTNO
----- ---------- ------ ------ ------
 7499 ALLEN        1600   1000     30
 7521 WARD         2259   1000     30
 7654 MARTIN       2250   1000     30
 7698 BLAKE        2850   1000     30
 7844 TURNER       1500   1000     30
 7900 JAMES        1950   1000     30
```

- view_chk30 뷰의 기본 테이블인 emp_copy2 테이블 확인

```sql
SQL> select * from emp_copy2;

EMPNO ENAME      JOB               MGR HIREDATE      SAL   COMM DEPTNO
----- ---------- ---------- ---------- ---------- ------ ------ ------
 7369 SMITH      CLERK            7902 80/12/17      800            20
 7499 ALLEN      SALESMAN         7698 81/02/20     1600   1000     30
 7521 WARD       SALESMAN         7698 81/02/22     2259   1000     30
 7566 JONES      MANAGER          7839 81/04/02     2975            20
 7654 MARTIN     SALESMAN         7698 81/09/28     2250   1000     30
 7698 BLAKE      MANAGER          7839 81/05/01     2850   1000     30
 7782 CLARK      MANAGER          7839 81/06/09     2450            10
 7788 SCOTT      ANALYST          7566 87/04/19     3000            20
 7839 KING       PRESIDENT             81/11/17     5000            10
 7844 TURNER     SALESMAN         7698 81/09/08     1500   1000     30
 7876 ADAMS      CLERK            7788 87/05/23     1100            20
 7900 JAMES      CLERK            7698 81/12/03     1950   1000     30
 7902 FORD       ANALYST          7566 81/12/03     3000            20
 7934 MILLER     CLERK            7782 82/01/23     1300            10
```

*⇒  'view_chk30' 뷰에 있던 6명의 데이터만 변경됨!*

- read only 옵션 뷰를 생성

```sql
create or replace view view_read30
as
select empno, ename, sal, comm, deptno
from emp_copy2
where deptno = 30
with read only;
```

- 값을 변경

```sql
update view_read30
set comm = 2000;
```

** ERROR at line 2:
    ORA-42399: cannot perform a DML operation on a read-only view

    ⇒ read-only 옵션 때문에 DML 을 수행하지 못함
    
    
    
### subQuery    
> **JONES와 같은 부서에 근무하는 사원들의 사원번호, 사원 이름, 급여, 부서번호를 검색**
> 
- jones이 어떤 부서인지 검색(서브쿼리)

```sql
SQL> select deptno
  2  from emp
  3  where ename = 'JONES';

DEPTNO
------
    20
```

- 부서번호가 20번인 사원들의 사원번호, 사원 이름, 급여, 부서번호 출력

```sql
select empno, ename, sal, deptno
from emp
where deptno = (select deptno
                from emp
                where ename = 'JONES');
```

*****  jones의 부서 번호가 20번인걸 처음부터 알지 못하기 때문에 사용하기 때문에 서브쿼리를 사용***

---

> **JONES와 같은 직무를 가진 사원들의 이름과 직무를 검색**
> 
- jones의 직무를 검색(서브쿼리)

```sql
SQL> select job
  2  from emp
  3  where ename = 'JONES';

JOB
----------
MANAGER
```

- 직무가 manager인 사원들의 이름과 직무 출력

```sql
select ename, job
from emp
where job = (select job
             from emp
             where ename = 'JONES');
```

---

> **clark보다 급여를 많이 받는 사원의 이름, 급여를 출력하시오**
> 
- clark의 급여 알아보기(서브쿼리)

```sql
SQL> select sal
  2  from emp
  3  where ename = 'CLARK';

   SAL
------
  2450
```

- 급여가 2450보다 높은 사원의 이름, 급여 출력

```sql
select ename, sal
from emp
where sal > (select sal
             from emp
             where ename = 'CLARK');
```

---

> **사원 전체의 평균 급여보다 적은 사원의 이름, 급여를 출력하시오**
> 
- 사원 전체의 평균 급여 알아보기(서브쿼리) ⇒ avg함수 사용

```sql
SQL> select avg(sal)
  2  from emp;

  AVG(SAL)
----------
2073.85714
```

- 급여가 2073보다 낮은 사원의 이름, 급여 출력

```sql
select ename, sal
from emp
where sal < (select avg(sal)
             from emp);
```

---

> **emp 테이블에서 부서 별로 평균 급여를 구했을 때, 부서 번호가 30번인 사원들의 급여보다 큰 부서의 부서 번호와, 평균 급여를 구하시오**
> 
- 부서 번호가 30번인 사원들의 평균 급여 구하기

```sql
SQL> select avg(sal)
  2  from emp
  3  where deptno = 30;

  AVG(SAL)
----------
1568.16667
```

- 메인쿼리

```sql
select deptno, avg(sal)
from emp
group by deptno
having avg(sal) > (select avg(sal)
                  from emp
                  where deptno = 30);
```

***** 부서 별로 → group by 사용***

1) group by 절을 쓸 때는 select 다음에 집계 함수와 group by절에 나온 것만 쓸 수 있음

2) 조건에 그룹 함수를 사용했으므로 where대신 having절을 사용해야 함
    
    
### 과제

- emp 테이블로부터 DEPTNO = 30인 사원들로만 된 emp_copy_view30을 만들어라.
단 DEPTNO의 값은 변경될 수 없도록 하여라.

```sql
create view emp_copy_view30
as
select *
from emp
where deptno = 30 with check option;
```

- 뷰 emp_copy_view30의 구조를 확인하여라.

```sql
desc emp_copy_view30;
```

- 뷰 emp_copy_view30의 데이터를 확인하여라.

```sql
select * from emp_copy_view30;
```

- 뷰 emp_copy_view30에서 DEPTNO가 30인 것을 10으로 바꾸어라.
바꿀 수 없다면 그 이유에 대해 설명하여라.

```sql
update emp_copy_view30
set deptno = 10
where deptno = 30;
```

⇒ 조건 제시에 사용된 컬럼값을 뷰에서 변경하지 못하게 하는 with check option이 있기 때문에 바꿀 수 없음

- 데이터 사전을 이용해서 생성된 뷰 emp_copy_view30의 이름과 생성 구문을 확인하여라.

```sql
select view_name, text
from user_views
where view_name in ('EMP_COPY_VIEW30');
```

- 이름이 ‘ALLEN’인 사원의 부서 이름을 출력하여라.

```sql
select dname
from dept
where deptno = (select deptno
                from emp
                where ename = 'ALLEN');
```
