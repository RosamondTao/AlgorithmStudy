# 数据库相关

### 登录

```sql
mysql -u root -p
```

### 管理

添加用户，用户验证信息是存在名为mysql的库中。

```sql
use mysql;
INSERT INTO user 
          (host, user, password, 
           select_priv, insert_priv, update_priv) 
           VALUES ('localhost', 'guest', 
           PASSWORD('guest123'), 'Y', 'Y', 'Y');
FLUSH PRIVILEGES;
```

列出 MySQL 数据库管理系统的数据库列表。

```sql
SHOW DATABASES;
```

输出mydatabase数据库中所有表的信息。

```sql
SHOW TABLE STATUS FROM mydatabase;
```

显示指定数据库的所有表，使用该命令前需要使用 use 命令来选择要操作的数据库。

```sql
SHOW TABLES;
```

显示mytable表的属性，属性类型，主键信息 ，是否为 NULL，默认值等其他信息。

```SQL
SHOW COLUMNS FROM mytable;
```

显示mytable表的详细索引信息，包括PRIMARY KEY（主键）。

```SQL
SHOW INDEX FROM mytable;
```



### DDL(Data Definition Language)数据定义语言

用来定义数据库对象：数据库，表，列等。关键字：create, drop,alter 等



### DML(Data Manipulation Language)数据操作语言

用来对数据库中表的数据进行增删改。关键字：insert, delete, update 等



### DQL(Data Query Language)数据查询语言

用来查询数据库中表的记录(数据)。关键字：select, where 等



### DCL(Data Control Language)数据控制语言(了解)

用来定义数据库的访问权限和安全级别，及创建用户。关键字：GRANT， REVOKE 等



### where和having

用于分组查询。
where和having区别：
   			1. where 在分组之前进行限定，如果不满足条件，则不参与分组。having在分组之后进行限定，如果不满足结果，则不会被查询出来
   			2. where 后不可以跟聚合函数，having可以进行聚合函数的判断。

```sql
-- 按照性别分组。分别查询男、女同学的平均分
SELECT sex , AVG(math) FROM student GROUP BY sex;
			
-- 按照性别分组。分别查询男、女同学的平均分,人数
SELECT sex , AVG(math),COUNT(id) FROM student GROUP BY sex;
			
--  按照性别分组。分别查询男、女同学的平均分,人数 要求：分数低于70分的人，不参与分组
SELECT sex , AVG(math),COUNT(id) FROM student WHERE math > 70 GROUP BY sex;
			
--  按照性别分组。分别查询男、女同学的平均分,人数 要求：分数低于70分的人，不参与分组,分组之后。人数要大于2个人
SELECT sex , AVG(math),COUNT(id) FROM student WHERE math > 70 GROUP BY sex HAVING COUNT(id) > 2;
SELECT sex , AVG(math),COUNT(id) 人数 FROM student WHERE math > 70 GROUP BY sex HAVING 人数 > 2;

```

