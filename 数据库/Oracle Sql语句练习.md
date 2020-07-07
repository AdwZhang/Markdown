1. 连接数据库：
```sql
    sqlplus/nolog
```

2. 连接管理员:
```sql 
    conn system/ok;
```
    目的：有dba权限可以创建用户

3. 通过管理员创建用户:
```sql
       create user haha identified by ok;
           identified by :指定用户密码
```

4. 连接用户
```Sql 
        haha:conn haha/ok;  (失败)
       1.缺失登陆权限：create session
```

5. 登陆管理员给haha授予登陆权限
```Sql      
      1.conn system/ok;
      2.grant create session to haha;
```
6. 连接haha用户:
```Sql 
       conn haha/ok;
```
7. 创建表：
```Sql
       create table student(id number(4),name varchar2(10)) 
```
8. 登录管理员

```Sql
    conn system/123;
```

9. 授予haha用户建表权限
```Sql
    grant create table to haha
```

10. 给用户haha分配内存大小
```Sql
    alter user haha quota unlimited on users;
```

11. haha用户进行建表
```Sql
    conn haha/123;
    create table student(id number(4),name varchar2(10));
```

12. 插入数据
```Sql
    insert into student(id,name) values(1,'张三');
```

13. 授予dba权限
```Sql
    conn system/123;
    grant dba to haha;
```

14. 修改haha的密码
```Sql
    conn system/123;
    alter user haha identified by 1234;
```

15. 设置haha的密码过期   
```Sql
    conn system;
    alter user haha password expire;
```

16. 锁定与解锁账号
```Sql
    alter user haha account lock;
    alter user haha account unlock;
```

17. 分页查询
```Sql
    select d.* from (select p.*,Rownum r from person p)
    where r>(index-1)*size and r<=index*size;
```

18. 插入指定列
```Sql
    insert into student(id,name) 
    values(2,'李四');
```

19. 插入不指定列
```Sql
    insert into student
    values(3,'李四',to_date('2019-01-10','yyyy,mm,dd'),'02');


    insert into student
    values(3,'李四',to_date('2019-01-10 10:10:10','yyyy,mm,dd hh:mi:ss'),'02');
```

20. 修改数据
```Sql
    update student set name='王五',birthday=sysdate
    where name='张三';
```

21. 删除数据
```Sql
    delete from student
    where id=1;
```