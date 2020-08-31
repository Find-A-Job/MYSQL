常用的命令
===
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
