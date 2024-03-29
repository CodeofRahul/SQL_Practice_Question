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

```sql

Select * from emp order by sal asc;
```
**4. List the details of the emps in asc order of the Dptnos and desc of Jobs?**

**Answer:**

```sql

Select * from emp order by deptno asc ,job desc;
```
**5. Display all the unique job groups in the descending order?**

**Answer:**

```sql

Select distinct job from  emp order by job desc;
```

**6. Display all the details of all ‘Mgrs’**

**Answer:**

```sql

Select * from emp e inner join dept d
	     on e.deptno = d.deptno
	     where mgr in (Select mgr from emp
				where e.deptno = d.deptno);
```

**Answer 2:**

```sql

Select * from emp where mgr in (select mgr from emp);
```

**7. List the emps who joined before 1981.**

**Answer:**

```sql

select * from emp where hiredate < ('01-01-1981');
```

**8. List the Empno, Ename, Sal, Daily sal of all emps in the asc order of
    Annsal.**
    
**Answer:**

```sql

Select empno,ename,sal,sal/30 as daily_sal,12*sal as annsal from emp
      order by annsal asc;
```

**9. Display the Empno, Ename, job, Hiredate, Exp of all Mgrs**

**Answer:**

```sql

SELECT empno, ename, job, hiredate,
         EXTRACT(YEAR FROM AGE(CURRENT_DATE, hiredate)) * 12 +
           EXTRACT(MONTH FROM AGE(CURRENT_DATE, hiredate)) AS exp_months
        FROM emp
        WHERE empno IN (SELECT mgr FROM emp);
```
    
**Answer 2:**

```sql

SELECT empno, ename, job, hiredate,
          concat( (EXTRACT(YEAR FROM CURRENT_DATE) - EXTRACT(YEAR FROM hiredate)) * 12 +
           EXTRACT(MONTH FROM CURRENT_DATE) - EXTRACT(MONTH FROM hiredate),' months') AS exp_months
        FROM emp
        WHERE empno IN (SELECT mgr FROM emp);
```

**10. List the Empno, Ename, Sal, Exp of all emps working for Mgr 7369.**
 
 **Answer:**
 
 ```sql

Select empno,ename,sal,mgr,
            extract(year from age(current_date,hiredate))*12 +
        	extract(month from age(current_date,hiredate)) as exp_month
       FROM emp
       where mgr>7369;
```

**11. Display all the details of the emps whose Comm. Is more than their Sal.**

**Answer:**

```sql

Select * from emp
	where comm > sal;
```

**12. List the emps in the asc order of Designations of those joined after the
	second half of 1981.**

**Answer:**

```sql

Select e.ename,e.hiredate,d.dname
	from emp e
	join dept d on e.deptno = d.deptno
	where date(hiredate) > '1981-06-30'
	order by d.dname;
```

**13. List the emps along with their Exp and Daily Sal is more than Rs.100.**

**Answer:**

```sql

Select ename,sal, concat(Extract(year from age(now(),hiredate)),' year') as exp_year from emp
	where (sal/30)>100;
```

**14. List the emps who are either ‘CLERK’ or ‘ANALYST’ in the Desc
	order.**

**Answer:**

```sql

Select ename from emp
	where job='clerk' or job='analyst'
	order by ename desc;
```

**Answer 2:**

```sql

Select ename from emp
	where job in ('clerk','analyst')
	order by ename desc;
```

**15. List the emps who joined on 1-MAY-81,3-DEC-81,17-DEC-81,19-JAN80 in asc order of seniority.**
**Answer:**

```sql

Select ename from emp
	where hiredate in ('1-may-81','3-dec-81','17-dec-81','19-jan-80')
	order by hiredate asc;
```

**Answer 2:**

```sql

Select ename,extract(year from age(current_date,hiredate)) as exp_year from emp
	where hiredate in ('1-may-81','3-dec-81','17-dec-81','19-jan-80')
	order by exp_year desc;
```

**16. List the emp who are working for the Deptno 10 or 20.**

**Answer:**

```sql

Select ename from emp
Where deptno in (10,20);
```

**17. List the emps who are joined in the year 81.**

**Answer:**

```sql

Select ename from emp
where Extract(year from hiredate) ='1981';
```

**Answer 2:**

```sql

Select ename from emp
where hiredate between '1-jan-1981' and '31-dec-1981';
```

**18. List the emps who are joined in the month of Aug 1980.**

**Answer:**

```sql

Select ename from emp
where hiredate between '1-aug-1980' and '31-aug-1980';
```

**Answer 2:**

```sql

select ename from emp
where to_char(hiredate,'mon-yyyy')='aug-1980';
```

**19. List the emps Who Annual sal ranging from 22000 and 45000.**

**Answer:**

```sql

Select ename from emp
where 12*sal between 22000 and 45000;
```

**20. List the Enames those are having five characters in their Names.**

**Answer:**

```sql

Select ename,length(ename) from emp
where length(ename) = 5;
```

**21. List the Enames those are starting with ‘S’ and with five characters.**

**Answer:**

```sql

SELECT ename FROM emp
where ename ilike 'S%' and length(ename) = 5;
```

**22. List the emps those are having four chars and third character must be ‘r’.**

**Answer:**

```sql

SELECT * FROM emp
WHERE ename like '__r_';
```

**23. List the Five character names starting with ‘S’ and ending with ‘H’.**

**Answer:**

```sql

SELECT ename FROM emp
WHERE ename ilike 'S___H';
```
**24. List the emps who joined in January.**

**Answer:**

```sql

SELECT * FROM EMP WHERE TO_CHAR (hiredate,'mon') = 'jan';
```

**25. List the emps who joined in the month of which second character is ‘a’.**
**Answer:**

```sql

SELECT * FROM emp WHERE TO_CHAR(hiredate,'mon') like '_a%';
```

**Answer:**

```sql

SELECT * FROM emp WHERE TO_CHAR(hiredate,'mon') like '_a%';
```

**26. List the emps whose Sal is four digit number ending with Zero.**

**Answer:**

```sql

SELECT * FROM emp WHERE sal between 999 and 9999 AND sal % 10 = 0;
```

**Answer 2:**

```sql

SELECT * FROM emp WHERE sal >= 1000 AND sal <= 9999 AND sal % 10 = 0;
```

**Answer 3:**

```sql

SELECT * FROM emp WHERE sal::text LIKE '___0';
```

**27. List the emps whose names having a character set ‘ll’ together.**

**Answer:**

```sql

SELECT * FROM emp WHERE ename like '%ll%';
```
**28. List the emps those who joined in 80’s.**

**Answer:**

```sql

SELECT * FROM emp where Extract(year from hiredate) = '1980'
```	
**29. List the emps who does not belong to Deptno 20.**

**Answer:**

```sql

SELECT ename,deptno from emp where deptno != 20;
```

**Answer 2:**

```sql

SELECT ename,deptno from emp where deptno <>20;
```

**Answer 3:**

```sql

SELECT ename,deptno from emp where deptno not in (20);
```
**30. List all the emps except ‘PRESIDENT’ & ‘MGR” in asc order of
Salaries.**

**Answer:**

```sql

SELECT * FROM emp
WHERE job not in ('president','manager')
order by sal asc;
```

**Answer 2:**

```sql

SELECT * FROM emp
WHERE job <> 'president' and job <> 'manager'
order by sal asc;
```

**31. List all the emps who joined before or after 1981.**

**Answer:**

```sql

SELECT * FROM emp
WHERE EXTRACT(year from hiredate) <> '1981';
```
  
**Answer 2:**

```sql

SELECT * FROM emp
where to_char(hiredate,'yyyy') != '1981';
```

**Answer 3:**

```sql

SELECT * FROM emp
where to_char(hiredate,'yyyy') not in ('1981')
```

**32. List the emps whose Empno not starting with digit78.**

**Answer:**

```sql

SELECT * FROM emp
where empno::text like '78%';
```

**33. List the emps who are working under ‘MGR’.**

**Answer 1:**

```sql

SELECT e.ename as emp,m.ename as mgr FROM emp as e,emp as m
where e.mgr =m.empno;
```

**Answer 2:**

```sql

SELECT concat(e.ename,' works for ',m.ename) from emp as e,emp as m
where e.mgr = m.empno;
```

**Answer 3:**

```sql

SELECT concat(e.ename,' has an employee ',m.ename) 
FROM emp as e,emp as m
WHERE m.mgr = e.empno;
```

**34. List the emps who joined in any year but not belongs to the month of
April.**

**Answer 1:**

```sql

SELECT * FROM emp
WHERE to_char(hiredate,'mon') <> 'apr';
```

**Answer 2:**

```sql

Select * from emp
Where to_char(hiredate,'mon') !='apr';
```

**Answer 3:**

```sql

select * from emp
where to_char(hiredate,'month') not like 'apr%';
```

**Answer 4:**

```sql

Select * from emp
Where to_char(hiredate,'mon') not in ('apr');
```

**35. List all the Clerks of Deptno 20.**

**Answer:**

```sql

Select * from emp
where deptno = 20 and job = 'clerk';
```

**36. List the emps of Deptno 30 or 10 joined in the year 1981.**

**Answer 1:**

```sql

Select * from emp
Where deptno in (10,30) and extract(year from hiredate) =1981;
```

**Answer 2:**

```sql
Select * from emp
Where deptno in (10,30) and to_char(hiredate,'yyyy') in ('1981');
```

**37. Display the details of SMITH.**

**Answer:**

```sql
Select * from emp as e
join dept as d
on e.deptno = d.deptno
Where ename = 'smith';
```

**38. Display the location of SMITH.**

**Answer 1:**
```sql
Select e.ename as name , d.loc as location from emp as e
join dept as d
on e.deptno = d.deptno
where ename = 'smith'
```

**Answer 2:**
```sql
Select e.ename as name , d.loc as location from emp as e
, dept as d
where ename = 'smith' and e.deptno = d.deptno;
```

**39. List the total information of EMP table along with DNAME and Loc of
all the emps Working Under ‘ACCOUNTING’ & ‘RESEARCH’ in the asc
Deptno.**

**Answer:**
```sql
Select e.*,d.dname,d.loc from emp as e
join dept as d
on e.deptno = d.deptno
Where d.dname in ('accounting','research')
Order by e.deptno asc;
```

**40. List the Empno, Ename, Sal, Dname of all the ‘MGRS’ and ‘ANALYST’
working in New York, Dallas with an exp more than 7 years without receiving
the Comm asc order of Loc.**

**Answer:**

```sql
Select e.empno, e.ename, e.sal, d.dname
From emp as e
join dept as d
on e.deptno = d.deptno
Where job in ('manager','analyst') and d.loc in ('new yourk','dallas')
and (extract(year from now()) - extract(year from hiredate)) >= 7
and e.comm is null
Order by loc asc;
```

**41. Display the Empno, Ename, Sal, Dname, Loc, Deptno, Job of all emps
working at CHICAGO or working for ACCOUNTING dept with Annual
Sal>28000, but the Sal should not be=3000 or 2800 who doesn’t belongs to the
Manager and whose empno is having a digit ‘7’ or ‘8’ in 3rd position in the asc order of
Deptno and desc order of job.**

**Answer:**

```sql
Select e.empno,e.ename,e.sal,d.dname,d.loc,d.deptno,e.job
From emp as e
join dept as d
on e.deptno = d.deptno
where (d.loc = 'chicago' or d.dname = 'accounting')
and e.empno in (
Select e.empno from emp as e
Where (e.sal*12) > 28000 and 
e.sal not in (3000,2800) and e.job != 'manager'
and (e.empno:: text Like '__7%' or e.empno:: text like '__8%'))
order by e.deptno asc, e.job desc;
```

**42. List the details of the Depts along with Empno, Ename or without the
emps.**

**Answer:**
```sql
Select d.*, e.empno, e.ename from dept as d
Left join emp as e on d.deptno = e.deptno
```

**43. List the details of the emps whose Salaries more than the employee
BLAKE.**

**Answer:**
```sql
SELECT ename, sal from emp
where sal > (SELECT sal from emp
where ename = 'blake')
```

**44. List the emps whose Jobs are same as ALLEN.**

**Answer:**
```sql
SELECT ename,job from emp
WHERE job in (SELECT job from emp
where ename = 'allen');
```

**45. List the emps who are senior to King.**

**Answer:**
```sql
Select ename, hiredate from emp
where hiredate < (Select hiredate from emp
where ename = 'king');
```

**46. List the Emps who are senior to their own MGRS.**

**Answer:**
```sql
Select e.ename as employee_name,m.ename as manager_name
from emp as e
join emp as m
on e.mgr = m.empno
where e.hiredate < m.hiredate;
```

**47. List the Emps of Deptno 20 whose Jobs are same as Deptno10.**

**Answer:**
```sql
Select *
From emp
Where job in (Select job
From emp
Where deptno = 10) and deptno =20;
```

