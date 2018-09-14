# SQL cheatsheet and recipies

(I'm using the Microsoft SQL-Server flavour)

------

## Language elements
[https://docs.microsoft.com/en-us/sql/t-sql/language-elements/language-elements-transact-sql?view=sql-server-2017](https://docs.microsoft.com/en-us/sql/t-sql/language-elements/language-elements-transact-sql?view=sql-server-2017)
`coalesce(a,b)` take first not NULL  
`nullif(a,b)`  if equal, returns NULL  
`UNION, UNION ALL, EXCEPT, INTERSECT`
`substring, len`
Variables:

```sql
DECLARE @MyVariable int;
SET @MyVariable = 1;
```

## SELECTING

### Random rows

```sql
select top 5 ename,job from emp order by newid( )
```



## CREATING

### Create table

```sql
create table D (id integer default 0)
```
Copying definition from antother table
```sql
select *  into dept_2 from dept where 1 = 0
```

### Insert rows

Explicit values
```sql
insert into dept (deptno,dname,loc) values (50,'PROGRAMMING','BALTIMORE')
```

From another table
```sql
insert into dept_east (deptno,dname,loc)
select deptno,dname,loc  from dept where loc in ( 'NEW YORK','BOSTON' )
```
Note: it is possible to insert values on views, that expose say a subset of cols.


### Update rows

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
````sql
select column_name, data_type, ordinal_position from information_schema.columns where table_schema = 'SMEAGOL' and table_name = 'EMP'
```

## CONCEPTS

NULL: NULL is never equal to or not equal to any value, not even itself. If you want to evaluate values returned by a nullable column like you would evaluate real values, use coalesce(var, 0)

CTE - common table expressions

Correlated subquery



### References
 * SQL Cookbook, by Anthony Molinaro. 2006 O’Reilly
 * The Art of SQL. By Stephane Faroult, Peter Robson. O’Reilly
