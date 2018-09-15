# SQL cheatsheet and recipies

(I'm using the Microsoft SQL-Server flavour)

------

## NOTES

##### Language elements
[https://docs.microsoft.com/en-us/sql/t-sql/language-elements/language-elements-transact-sql?view=sql-server-2017](https://docs.microsoft.com/en-us/sql/t-sql/language-elements/language-elements-transact-sql?view=sql-server-2017)



`UNION, UNION ALL, EXCEPT, INTERSECT`

Strings: `substring(x,2,5)`, `len(x)`

Dates: `DATEADD(day, 1, getdate( ))`, `DATEDIFF(day, i, e)`, `DATEPART( hour, getdate())`, `datename(dw,x) -- 'Friday'`

`NULL`: NULL is never equal to or not equal to any value, not even itself. If you want to evaluate values returned by a nullable column like you would evaluate real values, use coalesce(var, 0). Aggregate functions ignore NULLs
 * `coalesce(a,b)` take first not NULL  
 * `nullif(a,b)`: if equal, returns NULL  
 * `isnull(a,0)`: replace NULLs in a by 0

**Variables**

```sql
DECLARE @MyVariable int;
SET @MyVariable = 1;
```

**Correlated subquery**: a subquery making use of elements from the envelope query

**Scalar subquery**

**CTE - common table expressions**: specifies a temporary named result set: `WITH x as (...)`


**Recursive WITH**: allows looping (recursive query). Exmaple, generate sequence of 10 integers:
```sql
with x (id) as (
	select 1  --anchor

	union all

	select id+1
	from x
	where id+1 <= 10
	)
select * from x
--OPTION (MAXRECURSION 6)
```


**Options**

`SET ANSI_NULLS ON` : always use ON. specifies that how SQL Server handles the comparison operations with NULL values.  

`SET QUOTED_IDENTIFIER ON` : always ON. When it is set to ON any character set that is defined in the double quotes “”is treated as a T-SQL Identifier (Table Name, Proc Name, Column Name….etc) When any character set that is defined in the single quotes ‘’ is treated as a literal. When it is set to OFF any character set that is defined either in Single Quotes or in Double Quotes is treated as a literal.  



## SELECTING

Random rows
```sql
select top 5 ename,job from emp order by newid( )
```
Sample table
```sql
SELECT *
FROM (VALUES (1), (5), (10), (50), (100), (200), (300), (359)) AS x(angle)
```



## CREATING

Create table
```sql
create table D (id integer default 0)
```
Copying definition from antother table
```sql
select *  into dept_2 from dept where 1 = 0
```

Insert rows (explicit values)
```sql
insert into dept (deptno,dname,loc) values (50,'PROGRAMMING','BALTIMORE')
```

Insert rows (from another table)
```sql
insert into dept_east (deptno,dname,loc)
select deptno,dname,loc  from dept where loc in ( 'NEW YORK','BOSTON' )
```
Note: it is possible to insert values on views, that expose say a subset of cols.


## UPDATING

```sql
update emp
set sal = sal*1.10
where deptno = 20
```
Updating with Values from Another Table
```sql
update e
set e.sal = ns.sal,
e.comm = ns.sal/2
from emp e, new_sal ns where ns.deptno = e.deptno
```

Conditionally insert, update, or delete records in a table depending on whether or not corresponding records exist

```sql
merge into emp_commission ec using (select * from emp) emp on (ec.empno=emp.empno)
when matched then
  update set ec.comm = 1000
  delete where (sal < 2000)
when not matched then
  insert (ec.empno,ec.ename,ec.deptno,ec.comm)
  values (emp.empno,emp.ename,emp.deptno,emp.comm)
```

## DELETING

All rows

```sql
delete from emp
```
Some rows
```sql
delete from emp where deptno = 10
```

Table
```sql
drop table if exists TableName
```

## METADATA

Query table names:
```sql
select table_name from information_schema.tables where table_schema = 'SMEAGOL'
```

Query column names
```sql
select column_name, data_type, ordinal_position from information_schema.columns where table_schema = 'SMEAGOL' and table_name = 'EMP'
```




## References
 * SQL Cookbook, by Anthony Molinaro. 2006 O’Reilly
 * The Art of SQL. By Stephane Faroult, Peter Robson. O’Reilly
