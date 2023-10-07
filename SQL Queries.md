**1. Display all the information of the EMP table?**

**Answer:**

```sql
SELECT * FROM emp; 
```

**2. Display unique Jobs from EMP table?**

**Answer:**

```sql
Select distinct job from emp;
```

**3. List the emps in the asc order of their Salaries?**

**Answer:**

```
Select * from emp order by sal asc;
```
**4. List the details of the emps in asc order of the Dptnos and desc of Jobs?**

**Answer:**

```
Select * from emp order by deptno asc ,job desc;
```
**5. Display all the unique job groups in the descending order?**

**Answer:**

```
Select distinct job from  emp order by job desc;
```

**6. Display all the details of all ‘Mgrs’**

**Answer:**

```
Select * from emp e inner join dept d
	     on e.deptno = d.deptno
	     where mgr in (Select mgr from emp
				where e.deptno = d.deptno);
```

**Answer 2:**

```
Select * from emp where mgr in (select mgr from emp);
```

**7. List the emps who joined before 1981.**

**Answer:**

```
select * from emp where hiredate < ('01-01-1981');
```

**8. List the Empno, Ename, Sal, Daily sal of all emps in the asc order of
    Annsal.**
    
**Answer:**

```
Select empno,ename,sal,sal/30 as daily_sal,12*sal as annsal from emp
      order by annsal asc;
```

**9. Display the Empno, Ename, job, Hiredate, Exp of all Mgrs**

**Answer:**

```
SELECT empno, ename, job, hiredate,
         EXTRACT(YEAR FROM AGE(CURRENT_DATE, hiredate)) * 12 +
           EXTRACT(MONTH FROM AGE(CURRENT_DATE, hiredate)) AS exp_months
        FROM emp
        WHERE empno IN (SELECT mgr FROM emp);
```
    
**Answer 2:**

```
SELECT empno, ename, job, hiredate,
          concat( (EXTRACT(YEAR FROM CURRENT_DATE) - EXTRACT(YEAR FROM hiredate)) * 12 +
           EXTRACT(MONTH FROM CURRENT_DATE) - EXTRACT(MONTH FROM hiredate),' months') AS exp_months
        FROM emp
        WHERE empno IN (SELECT mgr FROM emp);
```

**10. List the Empno, Ename, Sal, Exp of all emps working for Mgr 7369.**
 
 **Answer:**
 
 ```
Select empno,ename,sal,mgr,
            extract(year from age(current_date,hiredate))*12 +
        	extract(month from age(current_date,hiredate)) as exp_month
       FROM emp
       where mgr>7369
```
