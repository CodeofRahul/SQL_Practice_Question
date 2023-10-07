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

``
Select distinct job from  emp order by job desc;
``
