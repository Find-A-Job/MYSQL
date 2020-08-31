常用的命令
===
* golang版的mysql驱动https://github.com/go-sql-driver/mysql
### 命令行操作mysql
* 显示所有数据库
> mysql> show databases;

* 显示当前选择的数据库
> mysql> select database();

> You can see at any time which database is currently selected using SELECT DATABASE().

* 显示当前数据库下所有表
> mysql> show tables;

* 显示xxx表的结构
> mysql> describe tableName;

> tableName代指表名，非关键字

* 创建xxx数据库
> mysql> create database dbName;

> dbName代指数据库名，非关键字

* 使用xxx数据库
> mysql> use dbName;

> dbName代指数据库名，非关键字

* 新建xxx表
> mysql> create table tableName (field1 type, field2 type, field3 type, ...);

> tableName表示表名，field1表示字段名， type表示字段类型（常见有varchar(x),char(x),date,x取值1~65535），...表示还可以继续添加

* 向xxx表中插入一条数据
> mysql> insert into tablename values ("value1", "value2", "value3", ...);

> **tablename**表示表名，**value1**表示值。insert，into，values是关键字

* 向xxx表中导入数据
> mysql> load data local infile "filePath" into table tableName;

> **filePath**是文件路径，**tableName**是表名
```
LINES TERMINATED BY '\r\n';
在不同的系统中使用不同的换行符，
\*unix'\n', 
On an Apple machine running macOS '\r', 
windows '\r\n'
```

* 删除xxx表
> mysql> delete from tableName;

> **tableName**表示表名

* 更新xxx表中某条数据
> mysql> update tableName set field = "value" where ...

> **tableName**表示表名，**field**表示字段名，**value**表示新的值，`...`表示筛选条件


---
### 查询
* 基本用法
```
select column from tableName where row
```
> **column** 表示筛选列，`select name, sex, other from xxx`多个字段用逗号隔开，也可用\*代指全部字段

> **tableName** 表示所查询的表

> **row** 表示筛选行，用各种条件。`'where name = "abc"', 'where birrh >= "1998-01-01"'`

* 排序 
```
select * from tableName order by field
select * from tableName order by field1, field2
select * from tableName order by field desc
select * from tableName order by field1, field2 desc
```

* 内置函数
```
TIMESTAMPDIFF(unit,datetime_expr1,datetime_expr2)
```

* 统计行
```
SELECT COUNT(*) FROM tableName;
SELECT owner, COUNT(*) FROM pet GROUP BY owner;
SELECT species, sex, COUNT(*) FROM pet GROUP BY species, sex;
SELECT species, sex, COUNT(*) FROM pet
       WHERE sex IS NOT NULL
       GROUP BY species, sex;
SET sql_mode = 'ONLY_FULL_GROUP_BY';
SET sql_mode = '';
```

* 多表联合查找
```
SELECT pet.name,
       TIMESTAMPDIFF(YEAR,birth,date) AS age,
       remark
       FROM pet INNER JOIN event
         ON pet.name = event.name
       WHERE event.type = 'litter';
       
SELECT p1.name, p1.sex, p2.name, p2.sex, p1.species
       FROM pet AS p1 INNER JOIN pet AS p2
         ON p1.species = p2.species
         AND p1.sex = 'f' AND p1.death IS NULL
         AND p2.sex = 'm' AND p2.death IS NULL;
```

---
### Using User-Defined Variables
### 其他


