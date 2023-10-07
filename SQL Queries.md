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
       where mgr>7369;
```

**11. Display all the details of the emps whose Comm. Is more than their Sal.**

**Answer:**

```
Select * from emp
	where comm > sal;
```

**12. List the emps in the asc order of Designations of those joined after the
	second half of 1981.**

**Answer:**

```
Select e.ename,e.hiredate,d.dname
	from emp e
	join dept d on e.deptno = d.deptno
	where date(hiredate) > '1981-06-30'
	order by d.dname;
```

**13. List the emps along with their Exp and Daily Sal is more than Rs.100.**

**Answer:**

```
Select ename,sal, concat(Extract(year from age(now(),hiredate)),' year') as exp_year from emp
	where (sal/30)>100;
```

**14. List the emps who are either ‘CLERK’ or ‘ANALYST’ in the Desc
	order.**

**Answer:**

```
Select ename from emp
	where job='clerk' or job='analyst'
	order by ename desc;
```

**Answer 2:**

```
Select ename from emp
	where job in ('clerk','analyst')
	order by ename desc;
```

**15. List the emps who joined on 1-MAY-81,3-DEC-81,17-DEC-81,19-JAN80 in asc order of seniority.**
**Answer:**

```
Select ename from emp
	where hiredate in ('1-may-81','3-dec-81','17-dec-81','19-jan-80')
	order by hiredate asc;
```

**Answer 2:**

```
Select ename,extract(year from age(current_date,hiredate)) as exp_year from emp
	where hiredate in ('1-may-81','3-dec-81','17-dec-81','19-jan-80')
	order by exp_year desc;
```

**16. List the emp who are working for the Deptno 10 or 20.**
**Answer:**

```
Select ename from emp
	Where deptno in (10,20);
```

**17. List the emps who are joined in the year 81.**

**Answer:**

```Select ename from emp
	where Extract(year from hiredate) ='1981';
```

**Answer 2:**

```
Select ename from emp
	where hiredate between '1-jan-1981' and '31-dec-1981';
```

**18. List the emps who are joined in the month of Aug 1980.**

**Answer:**

```
Select ename from emp
	where hiredate between '1-aug-1980' and '31-aug-1980';
```

**Answer 2:**

```select ename from emp
	where to_char(hiredate,'mon-yyyy')='aug-1980';
```

**19. List the emps Who Annual sal ranging from 22000 and 45000.**

**Answer:**

```
Select ename from emp
	where 12*sal between 22000 and 45000;
```

**20. List the Enames those are having five characters in their Names.**

**Answer:**

```
Select ename,length(ename) from emp
	where length(ename) = 5;
```
