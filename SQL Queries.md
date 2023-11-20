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
