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
```
CREATE TABLE IF NOT EXISTS `runoob_tbl`(
   `runoob_id` INT UNSIGNED AUTO_INCREMENT,
   `runoob_title` VARCHAR(100) NOT NULL,
   `runoob_author` VARCHAR(40) NOT NULL,
   `submission_date` DATE,
    id int not null default 0 primary key,       //非null，默认值0， 主键，
    name char(20) default '1',                   // 默认值 '1'
   PRIMARY KEY ( `runoob_id` ),
   primary key (id,name)                         // 复合主键
)ENGINE=InnoDB DEFAULT CHARSET=utf8;

userid int(4) primary key not null auto_increment       //创建主键非空并自增

primary key    标识该属性为该表的主键，可以唯一的标识对应的元组
foreign key    标识该属性为该表的外键，是与之联系的某表的主键
not null       标识该属性不能为空
unique         标识该属性的值是唯一的
auto_increment 标识该属性的值自动增加
default        为该属性设置默认值
```

* 向xxx表中插入一条数据
> mysql> insert into tablename (field1, field2, field3, ...) values ("value1", "value2", "value3", ...);

> **tablename**表示表名， **field1**表示字段名，**value1**表示值。insert，into，values是关键字

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
### 增加，修改，删除表字段
* ALTER TABLE tableName ADD field INT ...
> **tableName**表示表名，**field**表示字段名， `...`表示其他约束
```
ALTER TABLE tab ADD i INT not null default 0;
给表tab添加一个(名为i，类型为int，非空，默认值为0的)字段


```
|类型 	|字节 	|格式 	|用途 	|是否支持设置系统默认值
|:----:|:----:|:----:|:----:|:----:|
|date 	|3 	|YYYY-MM-DD 	|日期值 	|不支持
|time 	|3 	|HH:MM:SS 	|时间值或持续时间 	|不支持
|year 	|1 	|YYYY 	|年份 	|不支持
|datetime 	|8 	|YYYY-MM-DD HH:MM:SS 	|日期和时间混合值 	|不支持
|timestamp 	|4 	|YYYYMMDD HHMMSS 	|混合日期和时间，可作时间戳 	|支持
### Using User-Defined Variables
### 其他


