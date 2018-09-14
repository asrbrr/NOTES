# SQL cheatsheet and recipies

I'm using the Microsoft SQL-Server flavour


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

### Delete

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


### References
 * SQL Cookbook, by Anthony Molinaro. 2006 O’Reilly
