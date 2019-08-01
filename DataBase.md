# MySQL

code.tarena.com.cn  
tarenacode  
code_123  

## 数据库

>数据库是按照一定的形式来组织、存储数据，目的是为了对数据操作——增删改查

### 数据库发展历史

   网状数据库->层次型数据库->**关系型数据库**->非关系型数据库(NoSql)

### 关系型数据库逻辑结构

 Server->Database->Table->Row->Column

### 常见的关系型数据库

- SQLite  微型数据库
- SQL Server 适用于Windows系统，收费，中型数据库
- Oracle  大型数据库，收费
- MySQL  中小型数据库，免费的，适用于各种操作系统

## MySQL数据库

  MySQL AB  -> SUN -> Oracle  

- oracle分支：mysql  
- martin分支：MariaDB  

 [XAMPP软件](https://www.apachefriends.org/download.html)  
服务器套装，包含多款服务器软件mysql、Apache...  

### mysql部署结构

- 服务器端：服务存储/维护数据 ——银行服务器机房  
     c:/xampp/mysql/bin/mysqld.exe  启动服务  
     确保3306端口不被占用  
- 客户端：负责向服务器端发起增删改查 ——ATM机  
     c:/xampp/mysql/bin/mysql.exe   客户端工具  

### 使用客户端连接服务器端

```sql
   mysql.exe  -h127.0.0.1  -P3306  -uroot  -p
     -h   host    主机(IP地址/域名)
     -P   port    端口
     -u   user    用户
     -p   password   密码
   mysql  -uroot   简写形式
```

   注意事项：**连接的时候，不能在结尾加分号。**

## mysql常用管理命令

- `quit;`  退出服务器连接
- `show databases;`  显示服务器上当前所有的数据库
- `use  数据库名;`  进入指定的数据库
- `show  tables;`  显示当前数据库中所有的数据表
- `desc  表名;`  描述表中都有哪些列(表头)

## SQL命令

>SQL: Structured Query Language，结构化查询语言，用于操作**关系型数据库**服务器，对数据执行增删改查等操作。

### SQL命令的两种执行方式

- 交互模式:  
  客户端输入一行，点击回车，服务器执行一行。适用于临时性的查看数据
- 脚本模式:  
  客户端把要执行的多行命令写在一个文本文件中，一次性的提交给服务器,适用于批量的操作数据;  
   **不能进入mysql数据库**  
   `mysql -uroot <  c:/xampp/.../02.sql`    回车  

### SQL语法规范

- 每条SQL命令可以跨越多行，遇到英文分号作为结束
- 假如某一条命令出现语法错误，则此条语句以及后边所有的语句不会再执行
- SQL命令不区分大小写，习惯上关键字用大写，非关键字用小写
- SQL命令中可以使用单行注释(#...)和多行注释(/*...*/)，注释的内容不会被服务器所执行

### 常用的SQL命令

- 丢弃指定的数据库，如果存在的话  
   `DROP  DATABASE  IF  EXISTS  xuezi;`  
- 创建新的数据库  
   `CREATE  DATABASE  xuezi;`  
- 进入创建的数据库  
   `USE  xuezi;`  
- 创建保存数据的表  

```sql
   CREATE  TABLE  student(  
     sid  INT,  
     name  VARCHAR(8),  
     sex  VARCHAR(1),  
     score  INT  
   );  
```

- 向数据表中插入数据  
   `INSERT INTO  student  VALUES('1','tom','m','85');`  
- 查询表中所有的数据  
   `SELECT * FROM  student;`  
- 修改数据  
   `UPDATE student SET name='lucy',score='100' WHERE  sid='2';`  
- 删除数据  
   `DELETE  FROM  student  WHERE  sid='3';`  

```sql
#丢弃指定的数据库xuezi，如果存在
DROP DATABASE IF EXISTS xuezi;
#创建新的数据库xuezi
CREATE DATABASE xuezi;
#进入数据库xuezi
USE xuezi;
#创建保存学生数据的表(编号、姓名、性别、分数)
CREATE TABLE student(
  sid INT,  #integer  整型
  name VARCHAR(8),  #variable character 字符串型
  sex VARCHAR(1),#m->男 f->女
  score INT
);
#往学生表中插入数据
INSERT INTO student VALUES('1','tom','m','85');
INSERT INTO student VALUES('2','kate','f','92');
INSERT INTO student VALUES('3','king','m','74');
#修改数据
#修改编号为2的学员，成绩为100，姓名为Lucy
UPDATE student SET name='Lucy',score='100' WHERE sid='2';
#删除编号为3的学员数据
DELETE FROM student WHERE sid='3';
#查询所有的数据
SELECT * FROM student;
```

## 标准SQL命令分类

- DDL: Data Define Language 定义数据结构  
 CREATE/DROP/ALTER
- DML: Data Manipulate Languge 操作数据  
 INSERT/UPDATE/DELETE
- DQL: Data Query Language 查询数据  
 SELECT
- DCL: Data Control Language 控制用户权限  
 GRANT(授权)/REVOKE(收权)

## 计算机存储字符

### 如何存储英文字符

- ASCII: 总共有128个,对所有的英文字母和符号进行编码  
     abc =====>    979898
- Latin-1: 总共有256，兼容ASCII码，同时对欧洲符号进行了编码，**mysql默认使用这种编码**。

### 如何存储中文字符

- GB2312: 对常用的6千多汉字进行编码，兼容ASCII码
- GBK: 对2万多汉字进行了编码，兼容GB2312
- BIG5: 台湾繁体字编码，兼容ASCII码
- Unicode: 对世界上主流的国家常用的语言进行了编码，兼容ASCII，不兼容GB2312,GBK,BIG5，具体分为三种存储方案：  
  - UTF-8，
  - UTF-16，
  - UTF-32存储方案

### 解决mysql存储中文乱码

  使用UTF-8编码形式  

1. sql脚本文件另存为的编码  
1. 客户端连接服务器的编码(SET NAMES UTF8)  
1. 服务器端创建数据库使用的编码(CHARSET=UTF8)  

```sql
#设置客户端连接服务器端的编码为utf8
SET NAMES UTF8;
#先丢弃数据库xz，如果存在
DROP DATABASE IF EXISTS xz;
#创建数据库xz，设置存储的编码为UTF8
CREATE DATABASE xz CHARSET=UTF8;
#进入该数据库
USE xz;
#创建保存用户数据的表user
CREATE TABLE user(
  uid INT,
  uname VARCHAR(9),
  upwd VARCHAR(16),
  email VARCHAR(32),
  phone VARCHAR(11),
  sex VARCHAR(1),
  userName VARCHAR(4),
  regTime VARCHAR(10),   #2018-12-31
  isOnline INT    # 1是/0否
);
#插入数据
INSERT INTO user VALUES
('1','tom','123456','tom@163.com','18112345678','m','张三','2018-12-31','1'),
('2','king','123789','king@qq.com','19198766789','m','李四','2019-1-2','0'),
('3','kate','123789','kate@qq.com','19198766333','f','李四1','2019-3-2','1');
#修改数据
UPDATE user SET upwd='666666',email='666@163.com' WHERE uid='2';
#删除数据
DELETE FROM user WHERE uid='3';
#查询数据
SELECT * FROM user;
```

## mysql中的列类型

>创建数据表的时候，指定的列可以存储的数据类型  
CREAT  TABLE  book( bid 列类型 );

- 数值类型——引号可加可不加
  - TINYINT  微整型，占1个字节  范围-128~127
  - SMALLINT 小整型，占2个字节 范围-32768~32767
  - INT  整型，占4个字节 范围 -2147483648~2147483647
  - BIGINT  大整型，占8个字节
  - FLOAT(M,D)  单精度浮点型，占4个字节，范围3.4E38，范围比INT大的多，**可能产生计算误差**。
  - DOUBLE(M,D)  双精度浮点型，占8个字节，范围比BIGINT大的多
  - DECIMAL(M,D)  **定点小数，不会产生计算误差**，M代表总的有效位数，D代表小数点后的有效位数
  - BOOL  布尔型，只有两个结果TRUE、FALSE(不能加引号)，真正存储数据的时候，会自动变成1和0；也可直接使用1和0；**数组库的列类型会自动变成TINYINT;**
- 日期时间类型——必须加引号
  - DATE  日期型   '2018-12-31'
  - TIME  时间型   '14:37:30'
  - DATETIME  日期时间型   '2018-12-31 14:37:30'
- 字符串类型——必须加引号
  - VARCHAR(M)  
  变长字符串，不会产生空间浪费，操作速度相对慢，M的最大值是65535
  - CHAR(M)  
  定长字符串，可能产生空间浪费，操作速度快，用于存储手机号码、身份证号等固定长度字符，M最大值是255
  - TEXT(M)  
  大型变长字符串，M最多存2G

|        |  CHAR(5)   | VARCHAR(5) |
| :----: | :--------: | :--------: |
|   a    | a\0\0\0\0  |    a\0     |
|   ab   |  ab\0\0\0  |    ab\0    |
|  abc   |  abc\0\0   |   abc\0    |
| abcde  |   abcde    |   abcde    |
| 一二三 | 一二三\0\0 |  一二三\0  |

```SQL
  CREATE  TABLE  t1( 
    id  INT,
    age  TINYINT,
    commentCount  INT,
    price  DECIMAL(6,2),     # 9999.99
    phone  CHAR(11),
    article  VARCHAR(3000),
    sex  BOOL,   #1 男  0女
    pubTime  DATE
  );
```

## 列约束

>mysql可以对插入的数据进行特定的验证，只有满足条件才允许插入到数据表中，否则认为是非法的插入。

- 主键约束——PRIMARY KEY  
  声明了主键约束的列上不能出现重复的值，表中查询的记录会按照主键从小到大排序——加快查找速度；  
  通常主键添加到编号列中。  
  注意：一个表中只能出现一个主键，主键列上不允许插入NULL。  
NULL表示空，在插入数据时，无法确定要保存的值；  
例如：无法确定员工的工资、姓名、声明...  

```SQL
CREATE TABLE emp(
  eid INT PRIMARY KEY,
  dname VARCHAR(6),
  sex BOOL,
  birthday DATE,
  salary DECIMAL(8,2), #999999.99
  deptId SMALLINT
);
```

- 非空约束——NOT NULL  
声明了非空约束的列上不允许插入NULL值
- 唯一约束——UNIQUE  
声明了唯一约束的列上不能插入重复的值，允许插入NULL，甚至多个NULL；  
一个表中可以出现多个唯一约束  
说明：**NULL这个值比较特殊，它和任何值都不等，甚至和自身都不等。**
- 检查约束——CHECK  
   检查约束可以对插入的数据进行自定义验证  

```SQL
   CREATE  TABLE  student(
    score TINYINT CHECK(score>=0 AND score<=100)
   );
```

**mysql不支持检查约束，会降低数据的插入速度**。

- 默认值约束——DEFAULT  
   可以使用DEFAULT关键字声明默认值，有两种方式可以使用默认值  
   `INSERT INTO laptop_family VALUES(50,'华硕',DEFAULT);`  
   `INSERT INTO laptop_family(fid,fname) VALUES(60,'神州');`  
- 外键约束——FOREIGN KEY  
    声明了外键约束的列上，取值必须在另一个表中的主键列上出现过，  
    两者的列类型要保持一致，允许使用NULL  
   `FOREIGN KEY(外键列) REFERENCES 另一数据表(主键列)`

```SQL
#创建保存笔记本数据的表
CREATE TABLE laptop(
  lid INT PRIMARY KEY AUTO_INCREMENT,
  title VARCHAR(64) UNIQUE,
  price DECIMAL(7,2) NOT NULL DEFAULT 6999,   #99999.99
  spec VARCHAR(32) UNIQUE,
  detail VARCHAR(3000),
  shelfTime DATE NOT NULL,
  isOnsale BOOL NOT NULL,
  familyId SMALLINT,
  FOREIGN KEY(familyId) REFERENCES laptop_family(fid)
);
```

## mysql中的自增列

 `AUTO_INCREMENT`:  自动增长  
 假如一个列声明了自增列，无需手动赋值，直接赋值为NULL，会获取当前的最大值，然后加1;  

 **TIPS**:  

- 只适用于整型的列上  
- 自增列允许手动赋值  

## 简单查询

### 查询特定的列

查询所有员工的姓名、生日  
  `SELECT ename,birthday FROM emp;`

### 查询所有的列

  `SELECT * FROM emp;`  
  `SELECT eid,ename,sex,birthday,salary,deptId FROM emp;`

### 给列起别名

- 查询所有员工的姓名和工资，使用中文别名  
  `SELECT ename AS 姓名,salary AS 工资 FROM emp;`
- 查询所有员工的编号，姓名，性别，生日；使用中文别名  
  `SELECT eid AS 编号,ename AS 姓名,sex AS 性别,birthday AS 生日 FROM emp;`
- 查询所有员工的编号和姓名，使用一个字母作为别名  
  `SELECT eid a,ename b FROM emp;`  

 **在起别名的时候，AS关键字可以省略**;

### 显示不同的记录/合并相同的记录

- 查询出都有哪些性别的员工  
  `SELECT DISTINCT sex FROM emp;`
- 查询出员工都在哪些部门  
  `SELECT DISTINCT deptId FROM emp;`

### 查询时执行计算

- 计算2+3-4+5*6/3  
  `SELECT 2+3-4+5*6/3;`
- 查询所有员工的姓名及其年薪  
  `SELECT ename,salary*12 FROM emp;`

### 查询结果集排序

- 查询所有部门表数据,结果集按照编号从小到大排序  
  `SELECT* FROM dept ORDER BY did ASC;` #ascendant
- 查询所有部门表数据,结果集按照编号从大到小排序  
`SELECT*FROM dept ORDER BY did DESC;#descendant;`
- 查询员工所有的列，结果集按照工资降序排列  
  `SELECT * FROM emp ORDER BY salary DESC;`  
- 查询员工所有的列，结果集按照年龄从小到大排列  
  `SELECT * FROM emp ORDER BY birthday DESC;`  
- 查询员工所有的列，结果集按照姓名的升序排序  
  `SELECT * FROM emp ORDER BY ename;`  
- 查询员工所有的列，结果按照工资降序排序，如果工资相同，按照姓名升序排列  
  `SELECT * FROM emp ORDER BY salary DESC,ename;`  
- 查询员工所有的列，要求女员工显示在前，如果性别相同按照生日降序排列。  
  `SELECT * FROM emp ORDER BY sex,birthday DESC;`  

**ORDER BY 可以按照数值、字符串、日期时间排序**;  
**默认是按照升序排列(ASC)**;

### 条件查询

- 查询出编号为5的员工所有列  
  `SELECT * FROM emp WHERE eid=5;`
- 查询出姓名为king的员工的编号，工资，姓名，生日  
  `SELECT eid,salary,ename,birthday FROM emp WHERE ename='king';`
- 查询出20号部门下员工所有列。  
  `SELECT * FROM emp WHERE deptId=20;`
- 查询出工资在6000以上员工所有列  
  `SELECT * FROM emp WHERE salary>=6000;`
- 查询出1993-1-1后出生的员工所有列  
  `SELECT * FROM emp WHERE birthday>'1993-1-1';`
- 查询出不在10号部门的员工所有列  
  `SELECT * FROM emp WHERE deptId!=10;`
- 查询出没有明确部门的员工所有列 ==> **IS NULL**  
  `SELECT * FROM emp WHERE deptId IS NULL;`
- 查询出有明确部门的员工所有列 ==> **IS NOT NULL**  
  `SELECT * FROM emp WHERE deptId IS NOT NULL;`
- 查询出工资在6000以上的男员工所有列  
  `SELECT * FROM emp WHERE salary>=6000 AND sex=1;`
- 查询出工资在7000~10000之间员工所有列 ==> **BETWEEN**  
  `SELECT * FROM emp WHERE salary>=7000 AND salary<=10000;`  
  `SELECT * FROM emp WHERE salary BETWEEN 7000 AND 10000;`
- 查询出工资不在7000~10000之间员工所有列  
  `SELECT * FROM emp WHERE salary NOT BETWEEN 7000 AND 10000;`  
  `SELECT * FROM emp WHERE salary<7000 OR salary>10000;`
- 查询出1990年之前和1995年之后出生的员工所有列  
  `SELECT *FROM emp WHERE birthday<'1990-1-1' OR birthday>'1995-12-31';`
- 查询出20号和30号部门员工所有的列 ==> **IN**  
  `SELECT * FROM emp WHERE deptId=20 OR deptId=30;`  
  `SELECT * FROM emp WHERE deptId IN(20,30);`
- 查询出不在20号和30号部门员工所有的列  
  `SELECT * FROM emp WHERE deptId NOT IN(20,30);`

**TIPS**:  
IS NULL / IS NOT NULL  
AND / OR  
BETWEEN..AND.. / NOT BETWEEN..AND..  
IN( ) / NOT IN( )  

### 分页查询

  假如查询的结果集有太多的数据，一次显示不完，可以使用分页显示。  
  需要两个条件：**当前的页码**，**每页的数据量**  
  **每页的开始** = (当前的页码 - 1 ) * 每页数据量  

分页查询语法：  
`SELECT * FROM emp LIMIT start,count;`  
  start:每页的开始  
  count:每页数据量  

 假设每页显示5条数据  
 第1页：SELECT * FROM emp LIMIT 0,5;  
 第2页：SELECT * FROM emp LIMIT 5,5;  
 第3页：SELECT * FROM emp LIMIT 10,5;  

 假设每页显示6条记录，查询前3页。  
 第1页：SELECT * FROM emp LIMIT 0,6;  
 第2页：SELECT * FROM emp LIMIT 6,6;  
 第3页：SELECT * FROM emp LIMIT 12,6;  

### 模糊条件查询

- 查询出姓名中含有字母e的员工所有列  
 `SELECT * FROM emp WHERE ename LIKE '%e%';`
- 查询出姓名中倒数第2个字符为e的员工所有列  
 `SELECT * FROM emp WHERE ename LIKE '%e_';`
- 查询出姓名中以e结尾的员工所有列  
 `SELECT * FROM emp WHERE ename LIKE '%e';`  

SQL中提供了两个模糊查询的字符:  

- %  可以匹配任意个字符   >=0
- _   可以匹配任意1个字符  =1

注意：**在模糊条件查询中必须使用关键字LIKE，不能使用 " = "**

## 复杂查询

### 聚合查询/分组查询

- 查询出所有员工的数量  
  `SELECT COUNT(eid) FROM emp;`  
  `SELECT COUNT(*) FROM emp;` ==> 推荐写法
- 使用员工的姓名计算员工数量  
  `SELECT COUNT(ename) FROM emp;`  
- 使用员工部门编号计算员工数量  
  `SELECT COUNT(deptId) FROM emp;`  
- 查询所有男员工的数量  
  `SELECT COUNT(*) FROM emp WHERE sex=1;`  

#### 聚合函数

>函数就是一个功能体，需要提供若干个数据，产出某个结果。

- COUNT( )   总数量
- SUM( )   总和
- AVG( )   平均
- MAX( )  最大
- MIN( )   最小  

#### 聚合查询

- 查询出所有员工的工资总和  
 `SELECT SUM(salary) FROM emp;`
- 查询出所有员工的平均工资  
 `SELECT AVG(salary) FROM emp;`  
 `SELECT SUM(salary)/COUNT(*) FROM emp;`
- 查询出男员工工资最高的  
 `SELECT MAX(salary) FROM emp WHERE sex=1;`
- 查询出年龄最大的员工  
 `SELECT MIN(birthday) FROM emp;`

#### 分组查询：只能查询分组条件和聚合函数

- 查询出男女员工的平均工资，最高工资  
 `SELECT sex,AVG(salary),MAX(salary) FROM emp GROUP BY sex;`
- 查询出每个部门的员工数量，最高工资，最低工资  
 `SELECT deptId,COUNT(*),MAX(salary),MIN(salary) FROM emp GROUP BY deptId;`  

#### 函数补充

- YEAR( )  获取日期中的年份
- MONTH( )  获取日期中的月份
  - 查询出1993年出生的员工所有列  
 `SELECT * FROM emp WHERE YEAR(birthday)=1993;`
  - 查询出5月份出生的员工所有列  
 `SELECT * FROM emp WHERE MONTH(birthday)=5;`

### 子查询

>把一个SQL语句的查询结果作为另一个SQL语句的查询条件

- 查询出研发部员工所有的列  
  步骤1：查询出研发部的部门编号——10  
  `SELECT did FROM dept WHERE dname='研发部';`  
  步骤2：根据研发部部门编号查询员工  
  `SELECT * FROM emp WHERE deptId=10;`  
  综合：  
  `SELECT *FROM emp WHERE deptId=(SELECT did FROM dept WHERE dname='研发部');`  

- 查询出比tom工资高的员工有哪些  
  步骤1：查询出tom的工资——6000  
  `SELECT salary FROM emp WHERE ename='tom';`  
  步骤2：查询出比6000工资高的  
  `SELECT * FROM emp WHERE salary>6000;`  
  综合：  
  `SELECT * FROM emp WHERE salary>( SELECT salary FROM emp WHERE ename='tom');`  
- 查询出和tom同一年出生的员工  
   步骤1：查询出tom出生的年份  
   `SELECT YEAR(birthday) FROM emp WHERE ename='tom';`  
   步骤2：查询出1990年出生的员工  
   `SELECT * FROM emp WHERE YEAR(birthday)=1990;`  
   综合：  
   `SELECT * FROM emp WHERE YEAR(birthday)=(SELECT YEAR(birthday) FROM emp WHERE ename='tom');`  

### 多表查询

**查询所有的员工姓名及其部门名称**。  
  ~~`SELECT ename,dname FROM emp,dept;`~~ ==>   错误：笛卡尔积  

多表查询如何**避免笛卡尔积**：添加查询条件:  
  `SELECT ename,dname FROM emp,dept WHERE deptId=did;`  
上述多表查询语法是SQL-92中的，  
**无法查询出没有部门的员工，也无法查询出没有员工的部门**。  

SQL-99中提出了新的多表查询语法。  

- 内连接 INNER JOIN..ON 和SQL92结果一致  
 `SELECT ename,dname FROM emp INNER JOIN dept ON deptId=did;`
- 左外连接 LEFT OUTER JOIN.. ON  
 `SELECT ename,dname FROM emp LEFT OUTER JOIN dept ON deptId=did;`  
 查询结果是左侧所有的记录都显示；OUTER可以省略
- 右外连接 RIGHT OUTER JOIN..ON  
 `SELECT ename,dname FROM emp RIGHT OUTER JOIN dept ON deptId=did;`  
 查询结果是右侧表中所有记录都显示，OUTER可以省略
- 全连接 FULL JOIN ON  
 显示左侧和右侧所有的记录——**mysql不支持**  
 **UNION** 合并相同的项  
 **UNION** ALL 不合并相同的项  

```sql
 (SELECT ename,dname FROM emp LEFT OUTER JOIN dept ON deptId=did)
 UNION
 (SELECT ename,dname FROM emp RIGHT OUTER JOIN dept ON deptId=did);
```
