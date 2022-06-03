---
title: "MysqlLearning"
date: 2021-09-25T23:44:44+08:00
draft: false
---

### mysql学习文档

##### 一 为什么要学习数据库

##### 二 数据库的相关概念 

DBMS DB SQL 

##### 三 数据库存储数据的特点

##### 四 初始mysql

mysql产品的介绍

mysql产品的安装

mysql服务的启动和停止

mysql服务的登陆和退出

mysql的常见命令和语法规范

##### 五DQL语言的学习

基础查询

条件查询

排序查询

常见函数

分组查询

连接查询

子查询

分页查询

union联合查询

##### 六 DML语言的学习

插入语句

修改语句

删除语句

##### 七 DDL语言的学习

库和表的管理

常见数据类型介绍

常见约束



保存数据的容器:

数组 集合 内存数据 断电就没了

文件 但是文件不好查找 

因此把文件做成方便增删改查的软件 对文件进行操作 这样的软件就叫做数据库

##### 数据库的好处

- 实现数据持久化
- 使用完整的管理系统统一管理,易于查询

##### 数据库的概念

DB 数据库 database:存储数据的仓库,保存了一系列有组织的数据.

DBMS 数据库管理系统 database management system 数据库是通过dbms创建和操作的容器

常见的数据库管理系统 mysql oracle db2 sqlserver

SQL 结构化查询语言 structure query language :专门用来与数据库通信的语言

sql的优点:

1. 不是某个特定数据库供应商专有的语言,几乎所有DBMS都支持sql
2. 简单易学
3. 虽然简单,但实际上是一种强有力的语言,灵活使用其语言元素,可以进行非常复杂和高级的数据库操作

类似于管家 管理 文件柜  DBMS 管理 DB

##### 数据库的特点

1. 将数据放到表中,表再放到库中
2. 一个数据库中够可以有多个表,每个表都有一个自己的名字,用来标识自己,表名具有唯一性
3. 表具有一些特性,这些特性定义了数据在表中如何存储,类似java中类的设计
4. 表由列组成,我们也称为字段.所有表都是由一个或多个列组成的,每个列类似java中的属性
5. 表中的数据是按行存储的,每一行类似于java中的对象

##### Mysql产品的特点

- mysql数据库隶属于mysqlab公司,总部位于瑞典,后被oracle收购
- 优点
  - 成本低:开放源代码,一般可以免费使用
  - 性能高:执行很快
  - 简单:很容易安装和使用

##### DBMS分为两类

- 基于共享文件系统的DBMS 例如 access
- 基于客户机---服务器的DBMS 例如 mysql oracle sqlserver

##### mysql版本

- 社区版 免费
- 企业版 收费

##### mysql卸载

先控制面板卸载

然后在安装目录下删除文件夹

然后在programdata中删除残余文件

清理注册表 

![image-20210919154523464](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210919154523464.png)

##### my.ini 配置文件

![image-20210919160841225](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210919160841225.png)

端口号 安装位置 数据存放位置 字符集 默认存储引擎 语法模式 最大连接数

改完服务需要重启

##### mysql服务的启动和停止

![image-20210919161439996](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210919161439996.png)

##### mysql服务端的登陆和退出

1. 使用mysql command line client 不建议 只适用于root用户

![image-20210919161620401](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210919161620401.png)



![image-20210919161637466](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210919161637466.png)



2.命令行 p输入密码不能有空格 -h 主机名 -P 端口号 -u 用户名 -p密码

![image-20210919161848290](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210919161848290.png)

简化命令 退出exit 或者 ctrl+C

![image-20210919161938321](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210919161938321.png)



基本命令

```sql
show databases ; 
use tset ; //进入数据库
```

![image-20210919163057930](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210919163057930.png)

```sql
show tables ; //查看数据库里的表 在当前用户进入的数据库中查看
show tables from sys ; //查看数据库里的表 可以在当前数据库中查看别的数据库中的表
select database() ; //查看当前处于什么位置  类似于linux中的 pwd
create table ... //创建表
```

![image-20210919163334648](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210919163334648.png)

```sql
desc stuInfo ; //查看表stuInfo中的字段
insert into stuInfo(id,name) value (1,'ljs') ;
delete from stuInfo where id = 1;
update stuInfo set name ='jwt' where id =1;
select * from stuInfo ;
#增删改查
```

![image-20210919163430191](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210919163430191.png)

练习

![image-20210919164509494](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210919164509494.png)



```sql
sql
select version() ; //查看版本号 sql中
cmd
mysql --version 
mysql -V 
```

##### mysql的语法规范

1. 不区分大小写,但建议关键字大写,表名 列名小写
2. 每条命令用分号结尾
3. 每条命令根据需要,可以进行缩进或者换行 
4. 注释 
   1. 单行注释 #注释文字 -- 注释文字 (必须要有空格)
   2. 多行注释 /*     lkdfjasldfj     */

##### 基础查询

select 查询列表 from 表名

- 查询列表可以是:表中的字段 / 常量值 / 表达式 / 函数 
- 查询的结果可以是一个虚拟的表格

查询单个字段

查询多个字段

查询所有字段

select * 不能控制字段的显示顺序

之所以用`` 着重号 第一为了直白,第二为了区分关键字 防止与关键字重名

查询常量

查询表达式

查询函数 

![image-20210919202609756](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210919202609756.png)

```sql
select 100 ;
select 'join' ; 
select 100*98 ;
select database () ;
select version () ;
show tables ;
```

起别名 方便理解 如果要查询的字段有重名的情况,使用别名可以区分开来

方式一: 使用as

方式二: 直接不用as 

```sql
select last_name as 姓 ,first_name as 名 from employees  ;
select last_name  姓 ,first_name  名 from employees  ;
# 防止歧义 双引号也行 单引号也可以
select salary as `out put` from employees ;
```

去重

```sql
select database() ;
show tables ;
desc employees ;
select distinct department_id from employees ;
```

![image-20210919203515527](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210919203515527.png)

+号的作用

姓名连接成一个字段 , 显示为姓名

以下错误

![image-20210919203805417](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210919203805417.png)

java中的+号:

- 运算符 , 操作数为数值型
- 连接符, 只要有一个操作数为字符串

mysql中的+号:

- 仅仅只有一个功能:运算符

select 100+90 ; 

select '123' +90 ; 其中一方为字符型,视图将字符型数值转换为数值型, 如果转换成功,则继续做加法运算

select 'james' + 90 ; 如果转换失败,则将字符型数值转换成0 

select null +10 ; 只要其中一方为null , 则结果肯定为null ![image-20210919204251938](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210919204251938.png)

所以需要使用函数 concat() ; 

```sql
#这是错误的用法 , 加上了单引号 , 无法解析
select concat ('last_name' , 'first_name') 姓名 from employees ;
#这是正确的
select concat (last_name , first_name) 姓名 from employees ;
```

##### 显示出表employees中的全部列,各个列之间用逗号连接,列头显示成out_put

```sql
#查看某表列名
select column_name fuck_name from information_schema.columns where table_schema = 'myemployees' and table_name = 'employees' ;
#没问题 因为不存在null
select concat (employee_id ,',',first_name ) from employees ;
#有问题 因为存在null  , 导致那行都变成null 了
select concat (employee_id ,',',first_name,',',commission_pct ) from employees ;
+----------------------------------------------------------+
| concat (employee_id ,',',first_name,',',commission_pct ) |
+----------------------------------------------------------+
| NULL                                                     |
| NULL                                                     |
| NULL                                                     |
| NULL                                                     |
| NULL                                                     |
```

##### 引入函数 IFNULL 

```sql
select IFNULL(a,b)
select ifnull(commission_pct,0) as 奖金率, commission_pct from employees ;
mysql> select ifnull(commission_pct,0) as 奖金率, commission_pct from employees ;
+--------+----------------+
| 奖金率 | commission_pct |
+--------+----------------+
|   0.00 |           NULL |
|   0.00 |           NULL |
|   0.00 |           NULL |
|   0.00 |           NULL |
|   0.00 |           NULL |
|   0.00 |           NULL |
|   0.40 |           0.40 |
|   0.30 |           0.30 |
|   0.30 |           0.30 |
```

```sql
#这是正确的
select concat (employee_id ,',',first_name,',',ifnull(commission_pct,0) ) from employees ;
+--------------------------------------------------------------------+
| concat (employee_id ,',',first_name,',',ifnull(commission_pct,0) ) |
+--------------------------------------------------------------------+
| 142,Curtis,0.00                                                    |
| 143,Randall,0.00                                                   |
| 144,Peter,0.00                                                     |
| 161,Sarath,0.25                                                    |
| 169,Harrison,0.20                                                  |
| 170,Tayler,0.20                                                    |
| 171,William,0.15                                                   |
```

##### 条件查询 select 查询列表 from 表名 where 筛选条件 ; 

先查表名有没有在,再筛选,再查询

分类 

- 按条件表达式筛选
  - 条件运算符 > < = <>(不等于)
- 按逻辑表达式筛选 作用用于连接条件表达式
  - && || ! and or not  
- 模糊查询 
  - like 
  - between and 
  - in 
  - is null 

```sql
#条件运算符
select * from employees where salary >12000 ;
#逻辑运算符
select first_name , department_id from employees where department_id <> 90 ;
#逻辑表达式筛选
select first_name , salary , commission_pct from employees where salary >10000 and salary <20000 ;
#好像三个不太一样
select * from employees where not(department_id between 90 and 120) or salary >15000 ;
 
select * from employees where department_id not in(90, 120) or salary >15000 ;
 
select * from employees where department_id not in(department_id between 90 and 120) or salary >15000 ;
```

模糊查询

-  like 
  - 一般和通配符使用
    - % 0到任意个字符
    - _ 任意一个字符
- between and
- in
- is null | is not null

 ```sql
 #模糊查询
 select * from employees where first_name like '%a%' ;
 
 select first_name , salary from employees where first_name like '__e_a%' ;
 
 #如果不想使用转义字符 , 第二个字符就是_ 而不是任意单个字符的话
 mysql> select last_name from employees where last_name like '_\_%' ;
 +-----------+
 | last_name |
 +-----------+
 | K_ing     |
 | K_ing     |
 +-----------+
 2 rows in set (0.00 sec)
 
 #或者使用以下这种 使用ESCAPE 来取消转义
 mysql> select last_name from employees where last_name like '_$_%' escape '$' ;
 +-----------+
 | last_name |
 +-----------+
 | K_ing     |
 | K_ing     |
 +-----------+
 2 rows in set (0.00 sec)
 
 mysql> select last_name from employees where last_name like '_h_%' escape 'h' ;
 +-----------+
 | last_name |
 +-----------+
 | K_ing     |
 | K_ing     |
 +-----------+
 2 rows in set (0.00 sec)
 ```

##### between and

- 提高语句简洁度
- 左右都包含临界值
- 不能颠倒顺序

```sql
#左闭右闭
select * from employees where employee_id between 100 and 120 ;
```

##### in 判断某字段的值是否属于in列表中的某一项

- 使用 in 提高语句的简洁度

- in 列表的值类型必须一致或兼容
- in 不支持通配符  毕竟不是like关键字

```sql
select employee_id , job_id from employees where job_id in('IT_PROG','AD_VP','AD_PRES') ;
```

##### is null 

- = 或 <> 不能用于判断null值

```sql
select first_name , commission_pct from employees where commission_pct is null ;
```

##### is not null

##### 安全等于   <=>

```sql
#安全等于可以用来判断是不是为空
select first_name , commission_pct from employees where commission_pct <=> null ;
#安全等于也可以用来判断是不是某个数值
mysql> select last_name , salary from employees where salary <=> 12000 ;
+-----------+----------+
| last_name | salary   |
+-----------+----------+
| Greenberg | 12000.00 |
| Errazuriz | 12000.00 |
| Higgins   | 12000.00 |
+-----------+----------+
3 rows in set (0.00 sec)
```

##### 安全等于和is null 的区别

is null 仅仅可以判断null值 , 可读性较高 , 建议使用

<=> 既可以判断null值,又可以判断普通的数值



##### 复习一下

##### mysql

##### 与mysql的第一次亲密接触

##### 数据库的好处

1. 持久化数据到本地
2. 结构化查询

##### 数据库的常见概念

1. DB 数据库,存储数据的容器
2. DBMS 数据库管理系统, 又称为数据库软件或数据库产品,用于创建或管理DB
3. SQL 结构化查询语言 ,用于和数据库通信的语言,不是某个数据库软件特有的,而是几乎所有的主流数据库软件通用的语言

##### 数据库存储的特点

1. 数据存放到表中,然后表再存放到库中
2. 一个库中可以有多张表,每张表具有唯一的表名用以标识自己
3. 表有一个或多个列,列又称为字段,相当于java中的属性
4. 表中的每一行数据,相当于java中的对象

##### 常见的数据库管理系统

mysq oracle db2 sqlserver

##### mysql的介绍

##### mysql的背景

前身属于瑞典的一家公司 mysql ab , 08被sun收购 , 09年被oracle收购

##### mysql的优点

1. 开源免费成本低
2. 性能高 , 移植性好
3. 体积小,便于安装

##### mysql的安装

属于c/s架构的软件,一般来讲是安装服务端

企业版/社区版

环境变量配置

##### mysql服务的启动和停止

net start mysql

图形化界面里开服务

##### mysql服务的登陆和退出

mysql -h localhost -P 3306 -u root -p123456

exit或者ctrl+C

##### DQL语言

##### 基础查询

select 查询列表 from 表名 

特点

1. 查询列表可以是字段/常量 / 表达式/ 函数/ 也可以是多个
2. 查询结果是一个虚拟表

示例

##### 查询单个字段

select 字段名 from 表名  ; 

##### 查询多个字段

select 字段名 , 字段名 from 表名 ; 

##### 查询所有字段 

select * from 表名 ; 

##### 查询常量 

select 常量 as ... ; 

**注意:字符型和日期型的常量值必须用单引号引起来,数值型不需要**

##### 查询函数

select 函数名(实参列表) ; 

##### 查询表达式

select 100%98 ; 

##### 起别名

1. as
2. 空格

##### 去重

distinct 只能给一个参数用 

##### +号的作用

只能做加法运算

select 数值+数值 ; 直接运算

select 字符 +数值 ; 尝试隐式转换然后运算 , 成功就成功,不成功就是0+数值

select null + 数值; 返回null

##### concat函数

拼接字符

select concat (字符1 , 字符2 , 字符3 ...) ; 

##### ifnull函数

判断某自字段或表达式是否为null , 如果为null 返回指定的值, 否则返回原本的值

select ifnull(commission_pct,0) from employees ; 如果是null则返回0 , 如果不是null , 则返回原值

##### isnull函数

判断是不是null , 是的话返回1 , 否的话就返回0

##### 条件查询

select 查询列表 from 表名 where 筛选条件

筛选条件的分类

1. 简单条件运算符 > < = <> <=> >= <=
2. 逻辑运算符  || && ! and or not
3. 模糊查询 

like in is null is not null between and 

like :一般搭配通配符使用, 用于判断字符型数值, **在5.5版本之后 , 也可以判断int类型的** , % 和 _ 区别

```sql
mysql>  select * from employees where department_id like '1__' ;
+-------------+-------------+-----------+----------+--------------+------------+----------+----------------+------------+---------------+---------------------+
| employee_id | first_name  | last_name | email    | phone_number | job_id     | salary   | commission_pct | manager_id | department_id | hiredate            |
+-------------+-------------+-----------+----------+--------------+------------+----------+----------------+------------+---------------+---------------------+
|         108 | Nancy       | Greenberg | NGREENBE | 515.124.4569 | FI_MGR     | 12000.00 |           NULL |        101 |           100 | 1998-03-03 00:00:00 |
|         109 | Daniel      | Faviet    | DFAVIET  | 515.124.4169 | FI_ACCOUNT |  9000.00 |           NULL |        108 |           100 | 1998-03-03 00:00:00 |
|         110 | John        | Chen      | JCHEN    | 515.124.4269 | FI_ACCOUNT |  8200.00 |           NULL |        108 |           100 | 2000-09-09 00:00:00 |
|         111 | Ismael      | Sciarra   | ISCIARRA | 515.124.4369 | FI_ACCOUNT |  7700.00 |           NULL |        108 |           100 | 2000-09-09 00:00:00 |
|         112 | Jose Manuel | Urman     | JMURMAN  | 515.124.4469 | FI_ACCOUNT |  7800.00 |           NULL |        108 |           100 | 2000-09-09 00:00:00 |
|         113 | Luis        | Popp      | LPOPP    | 515.124.4567 | FI_ACCOUNT |  6900.00 |           NULL |        108 |           100 | 2000-09-09 00:00:00 |
|         205 | Shelley     | Higgins   | SHIGGINS | 515.123.8080 | AC_MGR     | 12000.00 |           NULL |        101 |           110 | 2016-03-03 00:00:00 |
|         206 | William     | Gietz     | WGIETZ   | 515.123.8181 | AC_ACCOUNT |  8300.00 |           NULL |        205 |           110 | 2016-03-03 00:00:00 |
+-------------+-------------+-----------+----------+--------------+------------+----------+----------------+------------+---------------+---------------------+
8 rows in set (0.00 sec)
```

##### is null 和<=> 的区别

is null 只会判断null

<=> 不仅判断null 还可以普通类型的数值

##### 排序查询

select 查询列表 from 表 where 筛选条件 order by 排序列表 asc|desc

**默认是asc 升序**

支持单个字段/多个字段/表达式/函数/别名

order by 一般是放在查询语句的最后面 limit子句除外

- 按表达式排序
- 按字段排序
- 按别名排序
- 按函数排序
- 按多字段排序

```sql
select * from employees order by salary desc ;
select * from employees order by salary asc ; 
#默认升序 asc
select * from employees where department_id >=90 order by hiredate desc ;

# *必须放在前面 可以按照表达式排序 也可以按照别名排序
select * , salary*12*(1+ifnull(commission_pct,0))as 年薪 from employees order by 年薪 desc;
# 按照函数排序
select last_name , salary from employees order by length(last_name) desc ;
#双重排序 先按照工资升序排 , 再按照员工编号降序排
select * from employees order by salary asc , employee_id desc ;
```

练习

```sql
select last_name , department_id , salary * 12 * (1+ifnull(commission_pct,0)) as 年薪 from employees order by 年薪 desc , length(last_name) asc ;

#以下用法 错误 between and 不能 按照 别名来 
select last_name , salary as 工资 from employees where not(工资 between 8000 and 17000) order by 工资 ;
#以下用法 正确
select last_name , salary as 工资 from employees where not(salary between 8000 and 17000) order by 工资 ;

#可以这样 直接 not between and 
select last_name , salary as 工资 from employees where salary not between 8000 and 17000 order by 工资

select * from employees where email like '%e%' order by length(email) desc , department_id ;
```

##### 常见函数

功能:类似于java中的方法,将一组逻辑语句封装在方法体中,对外暴露方法名

好处:1.隐藏了实现细节 2.提高代码的重用性

调用: select 函数名(实参列表)  [from 表] ;

特点:

- 叫什么 函数名
- 干什么 函数功能

分类：

- 单行函数
  - 字符函数 length concat substr substring replace lpad rpad upper lower instr trim
  - 数学函数 mod floor round ceil  truncate
  - 日期函数 now curdate curtime year month monthname day hour minute second date_format str_to_date
  - 其他函数
  - 流程控制函数
  - concat / length / ifnull 等
- 分组函数
  - 做统计使用 又称为统计函数、聚合函数、组函数

```sql
#查看字节长度
mysql> select length('lalala') ;
+------------------+
| length('lalala') |
+------------------+
|                6 |
+------------------+
1 row in set (0.00 sec)

#查看字节长度
mysql> select length ('林健树') ;
+-------------------+
| length ('林健树') |
+-------------------+
|                 6 |
+-------------------+
1 row in set (0.00 sec)

#展示字符集
mysql> show variables like '%char%' ;
+--------------------------+---------------------------------------------------------+
| Variable_name            | Value                                                   |
+--------------------------+---------------------------------------------------------+
| character_set_client     | gbk                                                     |
| character_set_connection | gbk                                                     |
| character_set_database   | utf8mb4                                                 |
| character_set_filesystem | binary                                                  |
| character_set_results    | gbk                                                     |
| character_set_server     | utf8mb4                                                 |
| character_set_system     | utf8mb3                                                 |
| character_sets_dir       | C:\Program Files\MySQL\MySQL Server 8.0\share\charsets\ |
+--------------------------+---------------------------------------------------------+

#拼接字符
select concat(last_name , '_' , first_name ) from employees ;
 
# upper / lower 
select upper('aaabbbccc') ;
select lower('aBc') ;

#函数嵌套
select concat(lower(last_name),'_',upper(first_name)) from employees ;

#substr / substring
#sql中索引从1开始
 mysql> select substring('李莫愁爱上了陆展元',7) out_put ;
+---------+
| out_put |
+---------+
| 陆展元  |
+---------+
1 row in set (0.00 sec)
#函数的重载 从指定索引出指定字符长度的字符
mysql> select SUBSTRING('李莫愁爱上了陆展元',1,3) ;
+-------------------------------------+
| SUBSTRING('李莫愁爱上了陆展元',1,3) |
+-------------------------------------+
| 李莫愁                              |
+-------------------------------------+
1 row in set (0.00 sec)

select concat(concat(upper(substring(first_name,1,1)),substr(first_name,2)),'_',last_name) from employees ;

#instr 判断是否在字符串中 
#返回的是第一次出现的索引 索引仍然从1开始 , 如果找不到返回0
mysql> select instr('杨不悔爱上了尹柳霞','尹柳霞') ;
+--------------------------------------+
| instr('杨不悔爱上了尹柳霞','尹柳霞') |
+--------------------------------------+
|                                    7 |
+--------------------------------------+
1 row in set (0.00 sec)

mysql> select instr('杨不悔尹柳霞爱上了尹柳霞','尹柳霞') out_put ;
+---------+
| out_put |
+---------+
|       4 |
+---------+
1 row in set (0.00 sec)

#trim 去空格 
mysql>  select length('   张翠山   ') , length (trim('    张翠山   '))  ;
+------------------------+--------------------------------+
| length('   张翠山   ') | length (trim('    张翠山   ')) |
+------------------------+--------------------------------+
|                     12 |                              6 |
+------------------------+--------------------------------+
1 row in set (0.00 sec)

#trim 可以去掉指定的字符或者字符串 中间不会去掉的
mysql> select trim('a' from 'aabbaaccaa') as out_put ;
+---------+
| out_put |
+---------+
| bbaacc  |
+---------+
1 row in set (0.00 sec)

#trim 只是按照单位去去的
mysql> select trim('aa' from 'aaabbaaccaaa') as out_put ;
+----------+
| out_put  |
+----------+
| abbaacca |
+----------+
1 row in set (0.00 sec)

#lpad 用指定的字符来实现左填充指定长度
mysql> select lpad('殷素素',10,'*') ;
+-----------------------+
| lpad('殷素素',10,'*') |
+-----------------------+
| *******殷素素         |
+-----------------------+
1 row in set (0.00 sec)

mysql> select lpad('97',3,'0') ;
+------------------+
| lpad('97',3,'0') |
+------------------+
| 097              |
+------------------+
1 row in set (0.00 sec)

#lpad 如果长度超过了 反而会发生截断 从左边开始向右边截断
mysql> select lpad('101',2,'0') ;
+-------------------+
| lpad('101',2,'0') |
+-------------------+
| 10                |
+-------------------+
1 row in set (0.00 sec)

#Rpad同理
#replace替换
mysql> select replace('张无忌爱上了周芷若','周芷若','赵敏') as out_put ;
+------------------+
| out_put          |
+------------------+
| 张无忌爱上了赵敏 |
+------------------+
1 row in set (0.00 sec)

#replace 凡是有的全部替换喔
mysql> select replace('周芷若张无忌爱上了周芷若','周芷若','赵敏') as out_put ;
+----------------------+
| out_put              |
+----------------------+
| 赵敏张无忌爱上了赵敏 |
+----------------------+
1 row in set (0.00 sec)
```

##### 数学函数

round 四舍五入

```sql
#round 四舍五入
mysql> select round(4.65) ;
+-------------+
| round(4.65) |
+-------------+
|           5 |
+-------------+
1 row in set (0.00 sec)

#round 两个参数时,后面的参数是值按小数点后几位来四舍五入
mysql> select round(4.65,1) ;
+---------------+
| round(4.65,1) |
+---------------+
|           4.7 |
+---------------+

mysql> select round(4.65,0) ;
+---------------+
| round(4.65,0) |
+---------------+
|             5 |
+---------------+
1 row in set (0.00 sec)

#ceil 向上取整
mysql> select ceil(1.001) ;
+-------------+
| ceil(1.001) |
+-------------+
|           2 |
+-------------+
1 row in set (0.00 sec)

#floor 向下取整
mysql> select floor(-1.01) ;
+--------------+
| floor(-1.01) |
+--------------+
|           -2 |
+--------------+
1 row in set (0.00 sec)
 
#truncate 截断 保留小数点后几位
mysql> select truncate(1.6999,2)  ;
+--------------------+
| truncate(1.6999,2) |
+--------------------+
|               1.69 |
+--------------------+
1 row in set (0.00 sec)

#mod 取余运算 a-a/b*b a/b会发生截断的可能 所以这个等式没毛病
# -10 mod -3 = -1  -10 mod 3 = -1 10 mod -3 = 1 只要被除数是- 就是-
mysql> select mod(10,-3) ;
+------------+
| mod(10,-3) |
+------------+
|          1 |
+------------+
1 row in set (0.00 sec)
```

##### 日期函数

```sql
# now 返回当前系统日期 包含时间
mysql> select now() ;
+---------------------+
| now()               |
+---------------------+
| 2021-09-20 16:00:28 |
+---------------------+
1 row in set (0.00 sec)

# curdate 返回当前日期 不包含时间
mysql> select curdate() ;
+------------+
| curdate()  |
+------------+
| 2021-09-20 |
+------------+
1 row in set (0.00 sec)
# curtime 返回当前时间 不包含日期
mysql> select curtime() ;
+-----------+
| curtime() |
+-----------+
| 16:01:21  |
+-----------+
1 row in set (0.00 sec)

#获取指定的部分 , 年 月 日 时 分 秒
mysql> select year(now()) 年 , month ('1998-1-1') 月, day(curdate())日 ;
+------+------+------+
| 年   | 月   | 日   |
+------+------+------+
| 2021 |    1 |   20 |
+------+------+------+
1 row in set (0.00 sec)

# 获取月份的英文 
 mysql> select monthname(hiredate) 月份英文, year(hiredate) from employees ;
+-----------+----------------+
| 月份英文  | year(hiredate) |
+-----------+----------------+
| April     |           1992 |
| April     |           1992 |

# 日期转换函数 str_to_date() date_format()
mysql> select str_to_date ('9--10--2021','%m--%d--%Y') as out_put ;
+------------+
| out_put    |
+------------+
| 2021-09-10 |
+------------+
1 row in set (0.00 sec)

mysql> select date_format('2021-09-20','%y年%m月%d日') as out_put ;
+--------------+
| out_put      |
+--------------+
| 21年09月20日 |
+--------------+
1 row in set (0.00 sec)
 
# 前端传进来的是字符串 而且格式不一 我们要使用函数来将字符串做处理 解析成想要的格式 然后再到数据库中查找 
mysql> select hiredate from employees where hiredate = str_to_date('4-3 1992','%c-%d %Y') ;
+---------------------+
| hiredate            |
+---------------------+
| 1992-04-03 00:00:00 |
| 1992-04-03 00:00:00 |
| 1992-04-03 00:00:00 |
| 1992-04-03 00:00:00 |
| 1992-04-03 00:00:00 |
+---------------------+
5 rows in set (0.00 sec)

#数据库这边也需要做好相应的处理 将日期处理成对应格式字符串然后返回回去
mysql> select last_name ,date_format(hiredate,'%m月/%d日 %y年') as 入职日期 from employees where commission_pct <=> null ;
+-------------+----------------+
| last_name   | 入职日期       |
+-------------+----------------+
| K_ing       | 04月/03日 92年 |
| Kochhar     | 04月/03日 92年 |
```

![image-20210920161042293](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210920161042293.png)



![image-20210920161613677](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210920161613677.png)

#####  其他函数

```sql
mysql> select version() ;
+-----------+
| version() |
+-----------+
| 8.0.24    |
+-----------+
1 row in set (0.00 sec)

mysql> select database() ;
+-------------+
| database()  |
+-------------+
| myemployees |
+-------------+
1 row in set (0.00 sec)

mysql> select user() ;
+----------------+
| user()         |
+----------------+
| root@localhost |
+----------------+
1 row in set (0.00 sec)
```

##### 流程控制函数

```sql
# IF函数 true就是第二个参数 false就是第三个参数
mysql> select commission_pct , if(isnull(commission_pct)=0,'没奖金 呵呵','有奖金 嘻嘻') 备注 from employees ;
+----------------+-------------+
| commission_pct | 备注        |
+----------------+-------------+
|           NULL | 有奖金 嘻嘻 |
|           NULL | 有奖金 嘻嘻 |

# mysql中默认 0就是第三个参数 1就是第二个参数
mysql> select commission_pct , if(isnull(commission_pct),'没奖金 呵呵','有奖金 嘻嘻') 备注 from employees ;
+----------------+-------------+
| commission_pct | 备注        |
+----------------+-------------+
|           NULL | 没奖金 呵呵 |
|           NULL | 没奖金 呵呵 |

mysql> select commission_pct , if(isnull(commission_pct),concat('没奖金 呵呵 ',0),concat('有奖金 嘻嘻 ',commission_pct)) 备注 from employees ;
+----------------+------------------+
| commission_pct | 备注             |
+----------------+------------------+
|           NULL | 没奖金 呵呵 0    |
|           NULL | 没奖金 呵呵 0    |

#case 函数 相当于 switch case的效果
/*
	case 要判断的字段或者表达式
	when 常量1 then 要显示的值1或语句1
	when 常量2 then 要显示的值2或语句2
	...
	else 要显示的值n或语句n
	end
*/
mysql> select salary 原始工资 , department_id 部门, case department_id when 30 then salary*1.1 when 40 then salary*1.2 when 50 then salary*1.3 else salary end  as 新工资 from employees ;
+----------+------+----------+
| 原始工资 | 部门 | 新工资   |
+----------+------+----------+
| 24000.00 |   90 | 24000.00 |
| 17000.00 |   90 | 17000.00 |

#case 多重if类似于
/*
	case 
	when 条件1 then 要显示的值1或语句1
	when 条件2 then 要显示的值2或语句2
	...
	else 要显示的值n或语句n
	end
*/
mysql> select salary ,  case when salary >20000 then 'A' when salary >15000 then 'B' when salary >10000 then 'C' else 'D' end as 工资级别 from employees ;
+----------+----------+
| salary   | 工资级别 |
+----------+----------+
| 24000.00 | A        |
| 17000.00 | B        |
| 17000.00 | B        |
```

练习

```sql
select employee_id , last_name , salary , salary * 1.2 as `new salary` from employees ;

mysql> select last_name , substr(last_name , 1,1) as szm ,length(last_name) `length` from employees order by szm ;
+-------------+------+--------+
| last_name   | szm  | length |
+-------------+------+--------+
| Austin      | A    |      6 |
| Atkinson    | A    |      8 |

mysql> select concat(last_name,' earns ' ,salary ,' monthly but wants ', salary*3 ) `Dream Salary`  from employees  ;
+-----------------------------------------------------+
| Dream Salary                                        |
+-----------------------------------------------------+
| K_ing earns 24000.00 monthly but wants 72000.00     |
| Kochhar earns 17000.00 monthly but wants 51000.00   |

mysql> select job_id as job , case job_id when 'AD_PRES' then 'A' when 'ST_MAN' then 'B' when 'IT_PROG' then 'C'end  grade from employees ;
+------------+-------+
| job        | grade |
+------------+-------+
| AC_ACCOUNT | NULL  |
| AC_MGR     | NULL  |

```

##### 分组函数

功能:用作统计使用,又称为聚合函数或统计函数或组函数

分类:

sum 求和 avg平均值 max最大值 min最小值 count计算个数

```sql
mysql>  select sum(salary) from employees ;
+-------------+
| sum(salary) |
+-------------+
|   691400.00 |
+-------------+
1 row in set (0.00 sec)

mysql> select avg(salary) from employees ;
+-------------+
| avg(salary) |
+-------------+
| 6461.682243 |
+-------------+
1 row in set (0.00 sec)

mysql> select min(salary) from employees ;
+-------------+
| min(salary) |
+-------------+
|     2100.00 |
+-------------+
1 row in set (0.00 sec)

mysql> select max(salary) from employees ;
+-------------+
| max(salary) |
+-------------+
|    24000.00 |
+-------------+
1 row in set (0.00 sec)

mysql> select count(salary) from employees ;
+---------------+
| count(salary) |
+---------------+
|           107 |
+---------------+
1 row in set (0.00 sec) 

mysql> select sum(salary) 和 , round(avg(salary),2) 平均 , min(salary) 最低 , max(salary) 最高,count(salary) 个数 from employees ;
+-----------+---------+---------+----------+------+
| 和        | 平均    | 最低    | 最高     | 个数 |
+-----------+---------+---------+----------+------+
| 691400.00 | 6461.68 | 2100.00 | 24000.00 |  107 |
+-----------+---------+---------+----------+------+

#参数支持哪些类型
#sum avg 不支持字符型
mysql> select sum(last_name) , avg(last_name) from employees ;
+----------------+----------------+
| sum(last_name) | avg(last_name) |
+----------------+----------------+
|              0 |              0 |
+----------------+----------------+

# max min 支持字符型/日期型 只要能够排序 max 和 min就能支持
mysql> select max(last_name) , min(last_name) from employees ;
+----------------+----------------+
| max(last_name) | min(last_name) |
+----------------+----------------+
| Zlotkey        | Abel           |
+----------------+----------------+

mysql> select max(hiredate) , min(hiredate) from  employees ;
+---------------------+---------------------+
| max(hiredate)       | min(hiredate)       |
+---------------------+---------------------+
| 2016-03-03 00:00:00 | 1992-04-03 00:00:00 |
+---------------------+---------------------+
1 row in set (0.00 sec)

#count支持计数 计的是非null的数
mysql> select count(last_name) from employees ;
+------------------+
| count(last_name) |
+------------------+
|              107 |
+------------------+
1 row in set (0.00 sec)

mysql> select count(commission_pct)from employees ;
+-----------------------+
| count(commission_pct) |
+-----------------------+
|                    35 |
+-----------------------+

#判断是否忽略null来计算 这里说明sum肯定是没参与 因为如果有null null+任何都是null 不可能有值
#avg也没有参与 所以avg不将null的项加入运算
mysql> select sum(commission_pct)总计 , avg(commission_pct) 平均值, sum(commission_pct)/35 没参与 , sum(commission_pct)/107 参与了 from employees ;
+------+----------+----------+----------+
| 总计 | 平均值   | 没参与   | 参与了   |
+------+----------+----------+----------+
| 7.80 | 0.222857 | 0.222857 | 0.072897 |
+------+----------+----------+----------+
1 row in set (0.00 sec)

#min 和 max 也忽略了null 否则肯定会在一头出现的
mysql> select max(commission_pct) max , min(commission_pct) min from employees ;
+------+------+
| max  | min  |
+------+------+
| 0.40 | 0.10 |
+------+------+
1 row in set (0.00 sec)

#可以和distinct 匹配使用
mysql> select sum(distinct salary) 去重, sum(salary) 不去重 from employees ;
+-----------+-----------+
| 去重      | 不去重    |
+-----------+-----------+
| 397900.00 | 691400.00 |
+-----------+-----------+
1 row in set (0.00 sec)

mysql> select count(distinct(salary)) 几种工资 from employees ;
+----------+
| 几种工资 |
+----------+
|       57 |
+----------+
1 row in set (0.00 sec)

# count 1 和 2 意思是加了一列 那么当然就等同于统计行数辣
mysql> select count(*) from employees ;
+----------+
| count(*) |
+----------+
|      107 |
+----------+
1 row in set (0.00 sec)

mysql> select count(1) from employees ;
+----------+
| count(1) |
+----------+
|      107 |
+----------+
1 row in set (0.00 sec)

mysql> select count(2) from employees ;
+----------+
| count(2) |
+----------+
|      107 |
+----------+
1 row in set (0.00 sec)
```

**所有的分组函数 都忽略null值**

**可以和distinct搭配**

**count函数的详细介绍**

 效率:

MYISAM 存储引擎下, count(*) 的效率高

INNODB存储引擎下, count(*) 和 count(1) 的效率差不多,比count(字段) 要高一点儿



和分组函数一同查询的字段有限制

```sql
#已经不存在逻辑意义了
mysql> select avg(salary) , employee_id from employees ;
+-------------+-------------+
| avg(salary) | employee_id |
+-------------+-------------+
| 6461.682243 |         100 |
+-------------+-------------+
1 row in set (0.00 sec)
```

和分组函数一同查询的字段要求是group by 后的字段



练习一下

```sql
mysql> select datediff(max(hiredate),min(hiredate)) from employees ;
+---------------------------------------+
| datediff(max(hiredate),min(hiredate)) |
+---------------------------------------+
|                                  8735 |
+---------------------------------------+
1 row in set (0.00 sec)

mysql> select datediff(now(),'1997-11-21') 活了多久了 ;
+------------+
| 活了多久了 |
+------------+
|       8705 |
+------------+
1 row in set (0.00 sec)

mysql> select count(*) from employees where department_id = 90 ;
+----------+
| count(*) |
+----------+
|        3 |
+----------+
1 row in set (0.00 sec)
```

##### 分组查询

select 分组函数, 列(要求出现在group by的后面) from 表 where 筛选条件 group by 分组的列表 order by 子句

**注意:	**查询列表必须特殊,要求是分组函数和group by 后出现的字段

**group by可以使用别名**  **oracle是不支持的 mysql支持**

**having 可以使用别名** **oracle是不支持的 mysql支持**

**order by 可以使用别名 oracle是不支持的 mysql支持**

**where 不可以使用别名**

```sql
mysql> select max(salary) 最高工资 , job_id 工种 from employees group by 工种 ;
+----------+------------+
| 最高工资 | 工种       |
+----------+------------+
|  8300.00 | AC_ACCOUNT |
| 12000.00 | AC_MGR     |
|  4400.00 | AD_ASST    |

mysql> select count(*) 部门个数 , location_id 位置 from departments group by 位置;
+----------+------+
| 部门个数 | 位置 |
+----------+------+
|        1 | 1400 |
|        1 | 1500 |

mysql> select avg(salary) 平均工资,department_id 部门编号 from employees where email like '%a%' group by 部门编号 ;
+--------------+----------+
| 平均工资     | 部门编号 |
+--------------+----------+
|  7000.000000 |     NULL |
|  4400.000000 |       10 |
+--------------+----------+
11 rows in set (0.00 sec)

#查询有奖金的每个领导手下员工的最高工资 很奇怪
mysql> select max(salary)最高工资,manager_id 领导 from employees where commission_pct <=> null group by manager_id ;
+----------+------+
| 最高工资 | 领导 |
+----------+------+
| 24000.00 | NULL |
| 17000.00 |  100 |
|  9000.00 |  102 |
|  6000.00 |  103 |
| 12000.00 |  101 |
|  9000.00 |  108 |
|  3100.00 |  114 |
|  3200.00 |  120 |
|  4200.00 |  121 |
|  3800.00 |  122 |
|  4000.00 |  123 |
|  3500.00 |  124 |
|  6000.00 |  201 |
|  8300.00 |  205 |
+----------+------+
14 rows in set (0.00 sec)

mysql> select max(salary)最高工资,manager_id 领导 from employees where commission_pct is not null group by manager_id ; 
+----------+------+
| 最高工资 | 领导 |
+----------+------+
| 14000.00 |  100 |
| 10000.00 |  145 |
| 10000.00 |  146 |
| 10500.00 |  147 |
| 11500.00 |  148 |
| 11000.00 |  149 |
+----------+------+
6 rows in set (0.00 sec)

#查询每个部门的员工个数 其实就是having 在每个group之下的筛选
mysql> select department_id 部门 , count(*)员工个数 from employees group by 部门 having 员工个数>2 ;
+------+----------+
| 部门 | 员工个数 |
+------+----------+
|   30 |        6 |
|   50 |       45 |
|   60 |        5 |
|   80 |       34 |
|   90 |        3 |
|  100 |        6 |
+------+----------+
6 rows in set (0.00 sec)

#查询每个工种有奖金的员工的最高工资>12000的工种编号和最高工资
mysql> select max(salary) 最高工资 , job_id 工种编号 from employees where commission_pct is not null group by 工种编号 having 最高工资>12000 ;
+----------+----------+
| 最高工资 | 工种编号 |
+----------+----------+
| 14000.00 | SA_MAN   |
+----------+----------+
1 row in set (0.00 sec)

#查询领导编号>102的每个领导手下的最低工资>5000的领导编号是那个,以及其最低工资
mysql> select min(salary) 最低工资 , manager_id 领导编号 from employees where manager_id>102 group by 领导编号 having 最低工资>5000 ;
+----------+----------+
| 最低工资 | 领导编号 |
+----------+----------+
|  6900.00 |      108 |
|  7000.00 |      145 |
```

##### 特点

1. 分组查询中的筛选条件分为两类
   1. 分组前筛选  来源于原始表  放在group by 子句的前面 使用where关键字
   2. 分组后筛选  来源于分组后的结果集 放在group by子句的后面 使用having关键字
   3. 分组函数 min max count avg 作为条件肯定是放在having子句中
   4. 能用分组前筛选的,就优先考虑放在分组前面,考虑到性能
2. group by 子句支持单个字段分组,多个字段分组(多个字段之间用逗号隔开,没有顺序之分),也支持表达式或函数(较少)
3. 也可以添加排序(排序放在整个分组查询的最后)

##### 按表达式或函数分组

```sql
#按员工姓名的长度分组,查询每一组的员工个数,筛选同学个数>5的有哪些
mysql> select length(last_name) 姓名长度 , count(*) 员工个数 from employees group by length(last_name) having 员工个数>5 ;
+----------+----------+
| 姓名长度 | 员工个数 |
+----------+----------+
|        5 |       29 |
|        7 |       15 |
```

##### 按多个字段分组

```sql
#查询每个部门每个工种的员工的平均工资 交换group by 的顺序不影响
mysql> select avg(salary) 平均工资, department_id 部门编号 , job_id 工种编号 from employees group by 部门编号 , 工种编号 ;
+--------------+----------+------------+
| 平均工资     | 部门编号 | 工种编号   |
+--------------+----------+------------+
| 24000.000000 |       90 | AD_PRES    |
| 17000.000000 |       90 | AD_VP      |
|  5760.000000 |       60 | IT_PROG    |
```

##### 分组后添加排序

```sql
mysql> select avg(salary) 平均工资, department_id 部门编号 , job_id 工种编号 from employees group by 部门编号 , 工种编号 order by 平均工资 asc ;
+--------------+----------+------------+
| 平均工资     | 部门编号 | 工种编号   |
+--------------+----------+------------+
|  2780.000000 |       30 | PU_CLERK   |
|  2785.000000 |       50 | ST_CLERK   |
```

练习一下

```sql
mysql> select job_id 工种, max(salary) 最大 ,min(salary) 最小 ,avg(salary) 平均 ,sum(salary) 总和 from employees group by 工种 order by 工种 asc ;
+------------+----------+----------+--------------+-----------+
| 工种       | 最大     | 最小     | 平均         | 总和      |
+------------+----------+----------+--------------+-----------+
| AC_ACCOUNT |  8300.00 |  8300.00 |  8300.000000 |   8300.00 |
| AC_MGR     | 12000.00 | 12000.00 | 12000.000000 |  12000.00 |

mysql> select max(salary)-min(salary) DIFFERENCE from employees ;
+------------+
| DIFFERENCE |
+------------+
|   21900.00 |
+------------+

mysql> select manager_id 领导编号, employee_id 员工编号, min(salary) 最低工资 from employees where salary >=6000 and manager_id is not null group by 领导编号  ;
+----------+----------+----------+
| 领导编号 | 员工编号 | 最低工资 |
+----------+----------+----------+
|      100 |      101 |  6500.00 |
|      102 |      103 |  9000.00 |

mysql> select department_id 部门编号 , count(*) 员工数量 , avg(salary) 平均工资 from employees group by 部门编号 order by 平均工资 desc ;
+----------+----------+--------------+
| 部门编号 | 员工数量 | 平均工资     |
+----------+----------+--------------+
|       90 |        3 | 19333.333333 |
|      110 |        2 | 10150.000000 |

mysql> select job_id 工种 , count(*)人数 from employees group by 工种 ;
+------------+------+
| 工种       | 人数 |
+------------+------+
| AC_ACCOUNT |    1 |
| AC_MGR     |    1 |
```

#####  连接查询

含义:又称为多表查询,当查询的字段来自于多个表时,就会用到连接查询

笛卡尔积现象: 表1 有m行 表2 有n行 结果有m*n行

发生原因:没有有效的连接条件

如何避免:添加有效的连接条件

![image-20210921141653473](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210921141653473.png)

每个都匹配了一遍 , 这不好 ,都是我的

```sql
mysql> select name , boyName from beauty , boys where beauty.boyfriend_id =boys.id ;
+------------+---------+
| name       | boyName |
+------------+---------+
| Angelababy | 黄晓明  |
| 热巴       | 鹿晗    |
| 周芷若     | 张无忌  |
| 小昭       | 张无忌  |
| 王语嫣     | 段誉    |
| 赵敏       | 张无忌  |
+------------+---------+
```

分类:

- 按照年代分类
  - sql92标准 仅仅支持内连接
  - sql99标准 [推荐] 支持内连接+外连接(左外+右外)+交叉连接
- 按功能分类
  - 内连接	
    - 等值连接
    - 非等值连接
    - 自连接
  - 外连接
    - 左外连接
    - 右外连接
    - 全外连接
  - 交叉连接

```sql
#以下是sql92标准的等值连接用法

mysql> select last_name , department_name from employees , departments where employees.department_id =departments.department_id ;
+-------------+-----------------+
| last_name   | department_name |
+-------------+-----------------+
| K_ing       | Exe             |
| Kochhar     | Exe             |

#为表起别名 提高语句的简洁度 区分多个重名的字段
mysql> select last_name , e.job_id , job_title from employees e , jobs where e.job_id = jobs.job_id ;
+-------------+------------+---------------------------------+
| last_name   | job_id     | job_title                       |
+-------------+------------+---------------------------------+
| Gietz       | AC_ACCOUNT | Public Accountant               |
| Higgins     | AC_MGR     | Accounting Manager              |

#交换表的出现顺序是可以的

#加上筛选条件
mysql> select last_name , commission_pct , department_name from employees e ,departments d where commission_pct is not null and e.department_id  = d.department_id ;
+------------+----------------+-----------------+
| last_name  | commission_pct | department_name |
+------------+----------------+-----------------+
| Russell    |           0.40 | Sal             |
| Partners   |           0.30 | Sal             |

mysql> select department_name , city from departments d ,locations l where d.location_id = l.location_id and city like '_o%' ;
+-----------------+---------------------+
| department_name | city                |
+-----------------+---------------------+
| IT              | Southlake           |
| Shi             | South San Francisco |

#查询每个城市的部门个数
mysql> select city , count(*) 部门个数 from departments d , locations l where d.location_id = l.location_id group by city ;
+---------------------+----------+
| city                | 部门个数 |
+---------------------+----------+
| Southlake           |        1 |
| South San Francisco |        1 |
| Seattle             |       21 |

mysql> select d.department_id , department_name , d.manager_id , min(salary) 最低工资 from employees e , departments d where e.department_id = d.department_id and commission_pct is not null group by department_id ;
+---------------+-----------------+------------+----------+
| department_id | department_name | manager_id | 最低工资 |
+---------------+-----------------+------------+----------+
|            80 | Sal             |        145 |  6100.00 |
+---------------+-----------------+------------+----------+

mysql>  select job_title , count(*) 员工个数 from employees e , jobs j where e.job_id = j.job_id group by j.job_id order by 员工个数 desc ;
+---------------------------------+----------+
| job_title                       | 员工个数 |
+---------------------------------+----------+
| Sales Representative            |       30 |
| Shipping Clerk                  |       20 |

#三表连接
mysql> select last_name , department_name , city from employees e , departments d , locations l where e.department_id = d.department_id and d.location_id = l.location_id ;
+-------------+-----------------+---------------------+
| last_name   | department_name | city                |
+-------------+-----------------+---------------------+
| Whalen      | Adm             | Seattle             |
| Hartstein   | Mar             | Toronto             |
```

**注意:如果为表起了别名,则查询的字段就不能使用原来的表名去限定了**

##### sql92标准

1. 等值连接
   1. 多表等值连接的结果为多表的交集部分
   2. n表连接,至少需要n-1个连接条件
   3. 多表的顺序没有要求
   4. 一般需要为表其别名
   5. 可以搭配前面介绍的所有子句使用,比如排序/筛选/分组
2. 非等值连接

```sql
#非等值连接 也可以加上排序/筛选/分组  
mysql> select salary , grade_level from employees e , job_grades g where salary between lower_sal and highest_sal ;
+----------+-------------+
| salary   | grade_level |
+----------+-------------+
| 24000.00 | E           |
| 17000.00 | E           |
```

​	3.自连接

```sql
#
mysql>  select a.last_name 员工名 ,b.last_name 领导名称 from employees a , employees b where a.manager_id =b.employee_id ;
+-------------+-----------+
| 员工名      | 领导名称  |
+-------------+-----------+
| Kochhar     | K_ing     |
| De Haan     | K_ing     |
```

##### 练习一下

```sql
mysql> select max(salary) , min(salary) from employees ;
+-------------+-------------+
| max(salary) | min(salary) |
+-------------+-------------+
|    24000.00 |     2100.00 |
+-------------+-------------+

mysql> select employee_id , job_id , last_name from employees order by department_id desc , salary asc ;
+-------------+------------+-------------+
| employee_id | job_id     | last_name   |
+-------------+------------+-------------+
|         206 | AC_ACCOUNT | Gietz       |
|         205 | AC_MGR     | Higgins     |

mysql> select job_id from employees where job_id like '%a%e%' order by job_id ;
+---------+
| job_id  |
+---------+
| AD_PRES |
| SA_REP  |

mysql> select substr('aabbcc',3) ;
+--------------------+
| substr('aabbcc',3) |
+--------------------+
| bbcc               |
+--------------------+
1 row in set (0.00 sec)

mysql> select trim( 'aa' from 'aaabbbcccaaa') ;
+---------------------------------+
| trim( 'aa' from 'aaabbbcccaaa') |
+---------------------------------+
| abbbccca                        |
+---------------------------------+
1 row in set (0.00 sec)
```

##### 复习一下

语法

select 查询列表 from 表 where 筛选条件 order by 排序列表 asc|desc

特点

asc 升序 默认 desc 降序

排序列表 支持 单个字段 多个字段 函数 表达式 别名

order by 位置一般放在查询语句的最后(除了limit语句之外)

常见函数

功能:类似于java中的方法

好处:提高重用性和隐藏实现细节

调用:select 函数名(实参列表) ; 

单行函数

- 字符函数 length concat substr substring upper lower instr  replace trim lpad rpad
- 数学函数 truncate round ceil mod floor rand(获取随机数 0-1) 
- 日期函数 curdate curtime now year month monthname day hour minute second date_format str_to_date **timediff datediff** 
- 其他函数 version user database ifnull isnull **md5**(自动将字符加密成md格式密文)
- 流程控制函数 if case when then else end 

```sql
mysql> select MD5('lalala123') ;
+----------------------------------+
| MD5('lalala123')                 |
+----------------------------------+
| 24500fa6ecaeb8300905727802af3081 |
+----------------------------------+
1 row in set (0.00 sec)
```

流程控制函数

```sql
if(条件表达式, 表达式1 , 表达式2) 如果条件表达式成立, 返回表达式1 , 否则返回表达式2

#case 情况1 

case 变量或表达式或字段

	when 常量1 then 值1

	when 常量2 then 值2

	else 值n

 end

#case 情况2

case 

	when 条件1 then 值1

	when 条件2 then 值2

	else 值n

 end
```

##### 分组函数

分类

max min avg sum count

特点

select max(字段) from 表名

支持的类型

**sum 和 avg 一般用于处理数值型**

**max min count 可以处理任何数据类型**

**以上分组函数都忽略null**

**都可以搭配distinct使用,实现去重的统计**

select sum(distinct 字段) from 表 ; 

count函数 

count(字段) 统计该字段非空值的个数

count(*) 统计结果集的行数

count(1) 统计结果集的行数

效率上:

myisam 存储引擎 count(*) 最高

innodb 存储引擎 count(*)和count(1) 效率>count(字段)

和分组函数一同查询的字段,要求是group by后面出现的字段

##### 分组查询

select 分组函数, 分组后的字段 from 表 where 筛选条件 group by 分组的字段 having 分组后的筛选 order by 排序列表

分组前筛选 where 原始表 group by的前面

分组后筛选 having 分组后的结果 group by的后面

##### 连接查询

##### 含义

当查询中涉及到了多个表的字段,需要使用多表连接

select 字段1 , 字段2 from 表1 , 表2

笛卡儿乘积:当查询多个表时,没有添加有效的连接条件,导致多个表所有行实现完全连接

如何解决:添加有效的连接条件

##### 分类

- 按年代分类
  - sql92
    - 等值
    - 非等值
    - 自连接
    - 也支持一部分外连接 用于oracle sqlserver , mysql不支持
  - sql99 [推荐使用]
    - 内连接
      - 等值
      - 非等值
      - 自连接
    - 外连接
      - 左外
      - 右外
      - 全外(mysql 不支持)
    - 交叉连接

##### 等值连接:

select 查询列表 from 表1 别名, 表2 别名 where 表1.key = 表2.key and 筛选条件 group by 分组字段 having 分组后的筛选 order by 排序字段

特点:

- 一般为表起别名
- 多表顺序可以调换
- n表连接至少需要n-1个连接条件
- 等值连接的结果是多表的交集部分

##### 非等值连接

select 查询列表 from 表1 别名, 表2 别名 where 非等值连接条件 and 筛选条件 group by 分组字段 having 分组后的筛选 order by 排序字段

##### 自连接

select 查询列表 from 表 别名1, 表 别名2 where 等值连接条件 and 筛选条件 group by 分组字段 having 分组后的筛选 order by 排序字段

练习一下

```sql
mysql> select last_name , e.department_id , department_name from employees e , departments d where e.department_id = d.department_id ;
+-------------+---------------+-----------------+
| last_name   | department_id | department_name |
+-------------+---------------+-----------------+
| Whalen      |            10 | Adm             |
| Hartstein   |            20 | Mar             |

mysql> select job_id , d.location_id from employees e , departments d where d.department_id = 90 and e.department_id = d.department_id ;
+---------+-------------+
| job_id  | location_id |
+---------+-------------+
| AD_PRES |        1700 |
| AD_VP   |        1700 |

mysql> select last_name , department_name , d.location_id , city from employees e , departments d ,locations l where e.department_id = d.department_id and d.location_id = l.location_id and commission_pct is not null ;
+------------+-----------------+-------------+--------+
| last_name  | department_name | location_id | city   |
+------------+-----------------+-------------+--------+
| Russell    | Sal             |        2500 | Oxford |
| Partners   | Sal             |        2500 | Oxford |

mysql> select last_name , job_id , d.department_id , department_name from employees e ,departments d , locations l where e.department_id = d.department_id and d.location_id = l.location_id and city ='Toronto' ;
+-----------+--------+---------------+-----------------+
| last_name | job_id | department_id | department_name |
+-----------+--------+---------------+-----------------+
| Hartstein | MK_MAN |            20 | Mar             |
| Fay       | MK_REP |            20 | Mar             |
+-----------+--------+---------------+-----------------+\

#查询每个工种 每个部门的部门名 工种名 和最低工资
mysql> select department_name , job_title ,min(salary) from employees e , departments d,jobs j where e.department_id = d.department_id and j.job_id = e.job_id group by j.job_title , d.department_name ;
+-----------------+---------------------------------+-------------+
| department_name | job_title                       | min(salary) |
+-----------------+---------------------------------+-------------+
| Acc             | Public Accountant               |     8300.00 |
| Acc             | Accounting Manager              |    12000.00 |

#查询每个国家下的部门个数大于2的国家编号
mysql>  select country_id,count(*) 部门个数 from locations l , departments d where l.location_id = d.location_id group by country_id having 部门个数>2  ;
+------------+----------+
| country_id | 部门个数 |
+------------+----------+
| US         |       23 |
+------------+----------+

#选择指定员工的姓名 员工号 以及他的管理者的姓名和员工号 结果类似于下面的格式
mysql> select a.last_name employees , a.employee_id Emp , b.last_name manager , b.employee_id Mgr from employees a , employees b where a.manager_id = b.employee_id ;
+-------------+-----+-----------+-----+
| employees   | Emp | manager   | Mgr |
+-------------+-----+-----------+-----+
| Kochhar     | 101 | K_ing     | 100 |
| De Haan     | 102 | K_ing     | 100 |
```

##### sql99语法

语法:

select 查询列表 from 表1 别名 连接类型 join 表2 别名 on 连接条件 where 筛选条件 group by 分组条件 having 筛选条件 order by 排序列表

分类:

内连接: inner

外连接:

​	左外:left outer

​	右外:right outer

​	全外:full outer

交叉连接 :cross

##### 内连接

select 查询列表 from 表1 别名 inner join 表2 别名 on 连接条件 where 筛选条件 ... 

分类:

- 等值连接
- 非等值连接
- 自连接

```sql
#调换顺序是可以的
mysql>  select last_name , department_name from employees e inner join departments d on e.department_id = d.department_id ;
+-------------+-----------------+
| last_name   | department_name |
+-------------+-----------------+
| Whalen      | Adm             |


mysql> select last_name , job_title from employees e inner join jobs j on e.job_id = j.job_id where last_name like '%e%' ;
+-------------+---------------------------------+
| last_name   | job_title                       |
+-------------+---------------------------------+
| De Haan     | Administration Vice President   |
| Ernst       | Programmer                      |

mysql> select last_name , job_title from employees e inner join jobs j on e.job_id = j.job_id where e.last_name like '%e%' ;
+-------------+---------------------------------+
| last_name   | job_title                       |
+-------------+---------------------------------+
| De Haan     | Administration Vice President   |
| Ernst       | Programmer                      |

#查询部门个数>3的城市名和部门个数
mysql> select city , count(*) 部门个数 from departments d join locations l on d.location_id = l.location_id group by l.location_id having 部门个数>3 ;
+---------+----------+
| city    | 部门个数 |
+---------+----------+
| Seattle |       21 |
+---------+----------+

#查询哪个部门的员工个数>3的部门名和员工个数,并按个数降序
mysql>  select department_name , count(*) 员工个数 from departments d inner join employees e on e.department_id = d.department_id group by e.department_id having count(*)>3 order by count(*) desc;
+-----------------+----------+
| department_name | 员工个数 |
+-----------------+----------+
| Shi             |       45 |
| Sal             |       34 |
| Pur             |        6 |

#多表连接 是有顺序的 第一个表和第二个表在连接的时候形成了新的表 然后新的表里的字段和第三个表里的字段再连接 所以是有顺序之分的 这个和两表连接有差别 
mysql> select last_name , department_name , job_title from employees e join departments d on e.department_id = d.department_id join jobs j on j.job_id = e.job_id order by department_name desc ;
+-------------+-----------------+---------------------------------+
| last_name   | department_name | job_title                       |
+-------------+-----------------+---------------------------------+
| Taylor      | Shi             | Shipping Clerk                  |
| Fleaur      | Shi             | Shipping Clerk                  |
```

特点:

- 添加排序/分组/筛选
- inner可以省略
- 筛选条件放在where后面 , 连接条件放在on后面, 提高分离性, 便于阅读
- inner join等值连接和sql92中的等值连接效果是一样的,都是查询多表的交集

##### 非等值连接

```sql
#非等值连接 
mysql> select salary , grade_level from employees e join job_grades g on e.salary between g.lower_sal and g.highest_sal ;
+----------+-------------+
| salary   | grade_level |
+----------+-------------+
| 24000.00 | E           |
| 17000.00 | E           |

#查询工资级别的个数>2并且按工资级别降序
mysql> select count(*) 级别个数 , grade_level from employees e join job_grades g on e.salary between g.lower_sal and g.highest_sal group by g.grade_level having 级别个数>2 order by  g.grade_level ;
+----------+-------------+
| 级别个数 | grade_level |
+----------+-------------+
|       24 | A           |
|       26 | B           |
|       38 | C           |
```

##### 自连接

```sql
#自连接
#查询员工姓名和他的领导的姓名
mysql> select a.last_name , b.last_name from employees a join employees b on a.manager_id = b.employee_id ;
+-------------+-----------+
| last_name   | last_name |
+-------------+-----------+
| Kochhar     | K_ing     |
| De Haan     | K_ing     |
```

##### 外连接

##### 应用场景

用于查询一个表中有,另一个表中没有的记录

特点

1. 外连接的查询结果为主表中的所有记录
   1. 如果从表中有和他匹配的,则显示匹配的值
   2. 如果从表中没有和他匹配的,则显示null
   3. 外连接查询结果=内连接结果+主表中有而从表中没有的记录
2. 左外连接,left join左边的是主表
3. 右外连接,right join右边的是主表
4. 交换两表的顺序和关键字,可以实现同样的结果

```sql
#查询没有男朋友的女神名
#这样的话就是内连接 内连接是取的交集 没有用查不到
mysql> select name,b.id from beauty g join boys b on g.boyfriend_id = b.id ;
+------------+----+
| name       | id |
+------------+----+
| Angelababy |  3 |
| 热巴       |  2 |

#这样的话就是外连接 外连接全取了 要加筛选条件
mysql> select name,b.id from beauty g left join boys b on g.boyfriend_id = b.id ;
+------------+------+
| name       | id   |
+------------+------+
| 柳岩       | NULL |
| 苍老师     | NULL |
| Angelababy |    3 |

#这样没错
mysql> select name,b.id from beauty g left join boys b on g.boyfriend_id = b.id where b.id is null ;
+--------+------+
| name   | id   |
+--------+------+
| 柳岩   | NULL |
| 苍老师 | NULL |

#查询那个部门没有员工
mysql> select d.department_id ,department_name from departments d left join employees e on d.department_id = e.department_id  where e.department_id is null ;
+---------------+-----------------+
| department_id | department_name |
+---------------+-----------------+
|           120 | Tre             |
|           130 | Cor             |
```

##### 全外连接 好像不支持 全外连接=内连接的结果+表1中有但表2没有的+表2中有但表1没有的

##### 交叉连接

```sql
#交叉做 笛卡尔乘积
mysql>  select beauty.* , boys.* from beauty cross join boys ;
+----+------------+------+---------------------+-------------+--------------+--------------+----+---------+--------+
| id | name       | sex  | borndate            | phone       | photo        | boyfriend_id | id | boyName | userCP |
+----+------------+------+---------------------+-------------+--------------+--------------+----+---------+--------+
|  1 | 柳岩       | 女   | 1988-02-03 00:00:00 | 18209876577 | NULL         |            8 |  4 | 段誉    |    300 |
|  1 | 柳岩       | 女   | 1988-02-03 00:00:00 |
```

##### sql92和sql99的区别

功能:sql99 支持的较多

可读性:sql99实现连接条件和筛选条件的分离,可读性较高

![image-20210923202009215](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210923202009215.png)



![image-20210923202111351](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210923202111351.png)



```sql
#查询编号>3的女生的男朋友信息,如果有则列出,如果没有就null填充
mysql> select g.id 女生id,g.name ,b.* from beauty g left join boys b on g.boyfriend_id = b.id where g.id>3 ;
+--------+--------+------+---------+--------+
| 女生id | name   | id   | boyName | userCP |
+--------+--------+------+---------+--------+
|      4 | 热巴   |    2 | 鹿晗    |    800 |
|      5 | 周冬雨 | NULL | NULL    |   NULL |
|      6 | 周芷若 |    1 | 张无忌  |    100 |

#查询哪个城市没有部门
mysql> select city 这个城市没有部门 from locations l left join departments d on l.location_id = d.location_id where department_id is null ;
+------------------+
| 这个城市没有部门 |
+------------------+
| Roma             |
| Venice           |
```

##### 子查询

含义:出现在其他语句中的eslect语句,称为子查询或内查询

外部的查询语句,称为主查询或外查询

分类:

- 按子查询出现的位置
  - select后面
    - 一般只支持标量子查询
  - from后面
    - 支持表子查询
  - where 或者 having 后面**(重要)**
    - 支持标量子查询/列子查询/行子查询
  - exists 后面 (相关子查询)
    - 表子查询
- 按功能(结果集的行列书不同)
  - 标量子查询(结果集只有一行一列)
  - 列子查询(结果集中只有一列多行)
  - 行子查询(结果集有一行多列)
  - 表子查询(结果结一般为多行多列)

##### where或having后面的子查询

支持标量子查询 / 列子查询 / 行子查询(多列多行)

特点:

1. 子查询放在小括号内
2. 一般放在条件的右侧
3. 标量子查询,一般搭配着单行操作符使用 > < >= <= <> 
4. 列子查询,一般搭配着多行操作符使用 in any/some all
5. 子查询的执行顺序优先于主查询执行,主查询的条件用到了子查询的结果

##### 标量子查询

```sql
#谁的工资比Abel高
mysql> select last_name , salary from employees where salary>(select salary from employees where last_name = 'Abel') ;
+-----------+----------+
| last_name | salary   |
+-----------+----------+
| K_ing     | 24000.00 |
| Kochhar   | 17000.00 |

mysql> select last_name , job_id ,salary from employees where employee_id=141 and salary >(select salary from employees where employee_id =143) ;
+-----------+----------+---------+
| last_name | job_id   | salary  |
+-----------+----------+---------+
| Rajs      | ST_CLERK | 3500.00 |
+-----------+----------+---------+

#查询 job_id 和 141号员工的job_id相同的,salary比143号员工多的员工
mysql> select last_name , job_id ,salary from employees where job_id=(select job_id from employees where employee_id =141) and salary >(select salary from employees where employee_id =143) ;
+-------------+----------+---------+
| last_name   | job_id   | salary  |
+-------------+----------+---------+
| Nayer       | ST_CLERK | 3200.00 |
| Mikkilineni | ST_CLERK | 2700.00 |
| Bissot      | ST_CLERK | 3300.00 |

#查询公司工资最少的员工的last_name , job_id, 和salary
mysql> select last_name , job_id , salary from employees where salary = (select min(salary) from employees ) ;
+-----------+----------+---------+
| last_name | job_id   | salary  |
+-----------+----------+---------+
| Olson     | ST_CLERK | 2100.00 |
+-----------+----------+---------+
1 row in set (0.00 sec)

#查询最低工资大于50号部门的最低工资的部门id和其最低工资
mysql> select department_id , min(salary) 最低工资 from employees group by department_id having min(salary) >(select min(salary) from employees where department_id = 50) ;
+---------------+----------+
| department_id | 最低工资 |
+---------------+----------+
|          NULL |  7000.00 |
|            10 |  4400.00 |
```

##### 标量子查询可能出现的问题

- 子查询里查到的元素个数不止一个
- 子查询里压根没查到任何元素

##### 列子查询

![image-20210923211703043](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210923211703043.png)

**any就是大于最小值小于最大值 all就是大于最大值小于最小值**

```sql
#查询location_id是1400或1700的部门中的所有员工姓名
mysql> select last_name from employees e where department_id in (select distinct department_id from departments where location_id in (1400,1700));
+------------+
| last_name  |
+------------+
| Hunold     |
| Ernst      |
| Austin     |

#返回比job_id为IT_PROG部门任意工资低的员工的员工号/姓名/job_id以及salary
mysql> select employee_id , last_name , job_id , salary from employees where salary < any(select salary from employees where job_id='IT_PROG') ;
+-------------+-------------+------------+---------+
| employee_id | last_name   | job_id     | salary  |
+-------------+-------------+------------+---------+
|         104 | Ernst       | IT_PROG    | 6000.00 |
|         105 | Austin      | IT_PROG    | 4800.00 |

#也可以使用max或者min来代替any
mysql> select employee_id , last_name , job_id , salary from employees where salary < any(select salary from employees where job_id='IT_PROG') order by employee_id;
+-------------+-------------+------------+---------+
| employee_id | last_name   | job_id     | salary  |
+-------------+-------------+------------+---------+
|         104 | Ernst       | IT_PROG    | 6000.00 |
|         105 | Austin      | IT_PROG    | 4800.00 |

#all也是同样的
#in 和 =Any也是一样的
#not in 和 <>All也是一样的
```

##### 行子查询

```sql
#查询员工编号最小并且工资最高的员工信息 (不一定存在)
#简单粗暴的做法
mysql>  select * from employees where employee_id = (select min(employee_id) from employees ) and salary = (select max(salary) from employees ) ;
+-------------+------------+-----------+-------+--------------+---------+----------+----------------+------------+---------------+---------------------+
| employee_id | first_name | last_name | email | phone_number | job_id  | salary   | commission_pct | manager_id | department_id | hiredate            |
+-------------+------------+-----------+-------+--------------+---------+----------+----------------+------------+---------------+---------------------+
|         100 | Steven     | K_ing     | SKING | 515.123.4567 | AD_PRES | 24000.00 |           NULL |       NULL |            90 | 1992-04-03 00:00:00 |
+-------------+------------+-----------+-------+--------------+---------+----------+----------------+------------+---------------+---------------------+
1 row in set (0.00 sec)

#行子查询 有局限性
mysql> select * from employees where (employee_id,salary)=(select min(employee_id),max(salary) from employees) ;
+-------------+------------+-----------+-------+--------------+---------+----------+----------------+------------+---------------+---------------------+
| employee_id | first_name | last_name | email | phone_number | job_id  | salary   | commission_pct | manager_id | department_id | hiredate            |
+-------------+------------+-----------+-------+--------------+---------+----------+----------------+------------+---------------+---------------------+
|         100 | Steven     | K_ing     | SKING | 515.123.4567 | AD_PRES | 24000.00 |           NULL |       NULL |            90 | 1992-04-03 00:00:00 |
+-------------+------------+-----------+-------+--------------+---------+----------+----------------+------------+---------------+---------------------+
1 row in set (0.00 sec)
```

##### 放在select后面的子查询

**仅仅支持标量子查询**

```sql
#查询每个部门的员工个数 
#通过子查询来做
mysql> select d.* ,(select count(*) from employees where department_id=d.department_id) from departments d ;
+---------------+-----------------+------------+-------------+----------------------------------------------------------------------+
| department_id | department_name | manager_id | location_id | (select count(*) from employees where department_id=d.department_id) |
+---------------+-----------------+------------+-------------+----------------------------------------------------------------------+
|            10 | Adm             |        200 |        1700 |                                                                    1 |
|            20 | Mar             |        201 |        1800 |                                                                    2 |
#也可以通过左右连接来做
mysql> select d.* , count(*) from employees e right join departments d on e.department_id = d.department_id group by d.department_id ;
+---------------+-----------------+------------+-------------+----------+
| department_id | department_name | manager_id | location_id | count(*) |
+---------------+-----------------+------------+-------------+----------+
|            10 | Adm             |        200 |        1700 |        1 |
|            20 | Mar             |        201 |        1800 |        2 |
|            30 | Pur             |        114 |        1700 |        6 |

#查询员工号=102的部门名
mysql> select employee_id ,(select department_name from departments where department_id =e.department_id) from employees e where e.employee_id =102;
+-------------+--------------------------------------------------------------------------------+
| employee_id | (select department_name from departments where department_id =e.department_id) |
+-------------+--------------------------------------------------------------------------------+
|         102 | Exe                                                                            |
+-------------+--------------------------------------------------------------------------------+
1 row in set (0.00 sec)
```

##### from后面

特点：将子查询充当一张表 **要求必须起别名**

```sql
#查询每个部门的平均工资的工资等级
#sql92语法
mysql> select department_id ,grade_level,av from (select department_id , avg(salary) av from employees group by department_id) a,job_grades where av between lower_sal and highest_sal ;
+---------------+-------------+--------------+
| department_id | grade_level | av           |
+---------------+-------------+--------------+
|          NULL | C           |  7000.000000 |
|            10 | B           |  4400.000000 |

#sql99语法
mysql> select av.department_id , grade_level from (select e.department_id , avg(salary) avs from employees e group by e.department_id) av join job_grades j on av.avs between j.lower_sal and j.highest_sal ;
+---------------+-------------+
| department_id | grade_level |
+---------------+-------------+
|          NULL | C           |
|            10 | B           |
|            20 | C           |
```

##### exists后面（子查询）

select exists(select employee_id from employees)

语法:

exists(完整的查询语句) 结果是1/0

```sql
#回顾
mysql> select last_name , (select department_name from departments where department_id = e.department_id )部门 from employees e;
+-------------+------+
| last_name   | 部门 |
+-------------+------+
| K_ing       | Exe  |
| Kochhar     | Exe  |

#查询有员工的部门名
mysql> select d.department_id , d.department_name from departments d where exists(select d.department_id from employees e where d.department_id = e.department_id);
+---------------+-----------------+
| department_id | department_name |
+---------------+-----------------+
|            10 | Adm             |
|            20 | Mar             |

#可以用in来代替
mysql> select d.department_id , d.department_name from departments d where d.department_id in (select distinct e.department_id from employees e ) ;
+---------------+-----------------+
| department_id | department_name |
+---------------+-----------------+
|            10 | Adm             |
|            20 | Mar             |

#查询没有女朋友的男生信息
mysql> select b.* from boys b where not exists(select boyfriend_id from beauty where boyfriend_id =b.id) ;
+----+---------+--------+
| id | boyName | userCP |
+----+---------+--------+
|  4 | 段誉    |    300 |
+----+---------+--------+
1 row in set (0.00 sec)
```

练习一下

```sql
mysql> select last_name , salary from employees where department_id = (select department_id from employees where last_name = 'Zlotkey') ;
+------------+----------+
| last_name  | salary   |
+------------+----------+
| Russell    | 14000.00 |
| Partners   | 13500.00 |


mysql> select last_name , salary from employees where salary > (select avg(salary) from employees ) ;
+------------+----------+
| last_name  | salary   |
+------------+----------+
| K_ing      | 24000.00 |
| Kochhar    | 17000.00 |

#查询各部门中工资比本部门平均工资中搞的员工和员工号,姓名和工资
mysql> select e.department_id , e.employee_id , e.last_name , e.salary from employees e where salary >(select avg(salary) from employees where department_id = e.department_id ) ;
+---------------+-------------+-----------+----------+
| department_id | employee_id | last_name | salary   |
+---------------+-------------+-----------+----------+
|            90 |         100 | K_ing     | 24000.00 |
|            60 |         103 | Hunold    |  9000.00 |


mysql> select department_id , employee_id , last_name from employees where department_id in (select department_id from employees where last_name like '%u%') ;
+---------------+-------------+-------------+
| department_id | employee_id | last_name   |
+---------------+-------------+-------------+
|            60 |         103 | Hunold      |
|            60 |         104 | Ernst       |

#查询部门的location_id是1700的部门工作的员工的员工号
mysql> select e.employee_id , e.department_id from employees e where e.department_id in (select department_id from departments where location_id =1700) ;
+-------------+---------------+
| employee_id | department_id |
+-------------+---------------+
|         200 |            10 |
|         114 |            30 |


mysql> select last_name , salary from employees where manager_id in (select employee_id from employees where last_name = 'K_ing') ;
+-----------+----------+
| last_name | salary   |
+-----------+----------+
| Kochhar   | 17000.00 |
| De Haan   | 17000.00 |

#查询最高工资的员工的姓名,要求first_name和last_name显示为一列,列名为姓名
mysql> select concat(a.姓 , a.名)姓名 from (select first_name 姓,last_name 名 from employees where salary = (select max(salary) from employees)) a ;
+-------------+
| 姓名        |
+-------------+
| StevenK_ing |
+-------------+
1 row in set (0.00 sec)
```

##### 分页查询

应用场景:当要显示的数据,一页显示不全,需要分页提交sql请求的时候

**语法**:select  查询列表 from 表 inner join 表2 on 连接条件 group by 分组字段 having 分组后的筛选 order by 排序后的字段 limit offset,size ; 

offset要显示条目的起始索引(起始索引从0开始)

size要显示的条目个数

**特点**:

- limit语句放在查询语句的最后
- 公式  要显示的页数 page 每页的条目数size , 那么就是limit (page-1)*size,size

```sql
mysql> select * from employees limit 0,5 ;
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
| employee_id | first_name | last_name | email    | phone_number | job_id  | salary   | commission_pct | manager_id | department_id | hiredate            |
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
|         100 | Steven     | K_ing     | SKING    | 515.123.4567 | AD_PRES | 24000.00 |           NULL |       NULL |            90 | 1992-04-03 00:00:00 |
|         101 | Neena      | Kochhar   | NKOCHHAR | 515.123.4568 | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         102 | Lex        | De Haan   | LDEHAAN  | 515.123.4569 | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         103 | Alexander  | Hunold    | AHUNOLD  | 590.423.4567 | IT_PROG |  9000.00 |           NULL |        102 |            60 | 1992-04-03 00:00:00 |
|         104 | Bruce      | Ernst     | BERNST   | 590.423.4568 | IT_PROG |  6000.00 |           NULL |        103 |            60 | 1992-04-03 00:00:00 |
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
5 rows in set (0.00 sec)

#如果从第一条开始的话,那么这样可以省略前一个数字
mysql> select * from employees limit 5 ;
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
| employee_id | first_name | last_name | email    | phone_number | job_id  | salary   | commission_pct | manager_id | department_id | hiredate            |
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
|         100 | Steven     | K_ing     | SKING    | 515.123.4567 | AD_PRES | 24000.00 |           NULL |       NULL |            90 | 1992-04-03 00:00:00 |
|         101 | Neena      | Kochhar   | NKOCHHAR | 515.123.4568 | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         102 | Lex        | De Haan   | LDEHAAN  | 515.123.4569 | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         103 | Alexander  | Hunold    | AHUNOLD  | 590.423.4567 | IT_PROG |  9000.00 |           NULL |        102 |            60 | 1992-04-03 00:00:00 |
|         104 | Bruce      | Ernst     | BERNST   | 590.423.4568 | IT_PROG |  6000.00 |           NULL |        103 |            60 | 1992-04-03 00:00:00 |
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
5 rows in set (0.00 sec)

#第11到第25条
mysql> select * from employees limit 10,15 ;

mysql> select * from employees where commission_pct is not null order by salary*(1+commission_pct) desc limit 0,10 ;
```

##### 练习一下

```sql
mysql>  select substr(email,1,instr(email,'@')-1) from stuinfo ;

mysql> select count(*) 个数 , sex from stuinfo group by sex ;

mysql> select min(age) , (select gradeName , id from grade where id = stuinfo.gradeid) from stuinfo group by gradeId ;

mysql> select min(age) , (select gradeName , id from grade where id = stuinfo.id) from stuinfo group by gradeId having min(age)>20;
```

##### 查询语句中涉及到的所有关键字,以及执行先后顺序.

select 查询列表  ⑦

 from 表   ① 锁定数据源

连接类型 join 表2   ②拼接数据源 笛卡尔儿乘积

 on 连接条件  ③缩小数据源 非笛卡尔乘积

 where 筛选条件   ④缩小数据范围

 group by 分组列表    ⑤

having 分组后的筛选   ⑥分组后筛选

order by 排序列表    ⑧

limit 偏移,条目数;    ⑨

##### sql99语法

##### 内连接

select 查询列表 from 表1 别名 inner join 表2 别名 on 连接条件 where 筛选条件 group by 分组列表 having 分组后的筛选 order by 排序列表 limit子句

**特点:**

表的顺序可以调换

内连接的结果=多表的交集

n表连接至少需要n-1个连接条件

分类: 等值连接 非等值连接 自连接

##### 外连接

select 查询列表 from 表1 别名 left|right|full outer join 表2 别名 on 连接条件

where 筛选条件 group by 分组列表 having 分组后的筛选 order by 排序列表 limit 子句; 

**特点:**

查询的结果=主表中所有的行,其中从表和他匹配的将显示匹配行,如果从表没有匹配的则显示null

left join 左边的就是主表,right join右边的就是主表

full join 两边都是主表

一般用于查询除了交集部分的剩余的不匹配的行  

##### 交叉连接

select 查询列表 from 表1 别名 cross join 表2 别名 ; 

**特点:	**

类似于笛卡尔乘积

##### 子查询

嵌套在其他语句内部的select语句称为子查询或内查询

外面的语句可以是insert update select delete 等等,一般select 作为外面语句较多

外面如果为select语句,则此语句成为外查询或主查询

**分类:	**

1. 按出现的位置

   - select 后面 仅仅支持标量子查询
   - from 后面 表子查询
   - **where或having后面 标量子查询 / 列子查询** / 行子查询
   - exists后面 标量子查询 列子查询 行子查询 表子查询

2. 按结果集的行列

   - **标量子查询(单行子查询):结果集为一行一列**
   - **列子查询(多行子查询):结果集为多行一列**
   - 行子查询(结果集为多行多列)
   - 表子查询(结果集为多行多列)

3. 示例

   标量子查询

   查询最低工资的员工姓名和工资

   ```sql
   mysql> select last_name , salary from employees where salary=(select min(salary) from employees) ;
   +-----------+---------+
   | last_name | salary  |
   +-----------+---------+
   | Olson     | 2100.00 |
   +-----------+---------+
   1 row in set (0.00 sec)
   ```

   列子查询

   查询所有是领导的员工姓名

   ```sql
   mysql>  select last_name from employees where employee_id in (select manager_id from employees) ;
   +-----------+
   | last_name |
   +-----------+
   | K_ing     |
   | De Haan   |
   ```

##### 分页查询

当要查询的条目数太多,一页显示不全

语法

select 查询列表 from 表 limit offset,size

**注意	** offset代表的是起始的条目索引,默认是从0开始  size代表的是要显示的条目数

公式 limit (page-1)*size , size

##### 练习一下

```sql
mysql>  select last_name from employees where employee_id in (select manager_id from employees) ;
+-----------+
| last_name |
+-----------+
| K_ing     |
| De Haan   |

#查询平均工资最低的部门信息 直接使用order by 平均工资 asc 再limit 1
mysql> select d.* from departments d where d.department_id = (select department_id from employees group by department_id order by avg(salary) asc limit 1);
+---------------+-----------------+------------+-------------+
| department_id | department_name | manager_id | location_id |
+---------------+-----------------+------------+-------------+
|            50 | Shi             |        121 |        1500 |
+---------------+-----------------+------------+-------------+

#查询平均工资最低的部门信息和它的平均工资
mysql> select d.*,a.avgsalary from departments d join (select department_id,avg(salary) avgsalary from employees group by department_id order by avg(salary) asc limit 1) a on d.department_id = a.department_id;
+---------------+-----------------+------------+-------------+-------------+
| department_id | department_name | manager_id | location_id | avgsalary   |
+---------------+-----------------+------------+-------------+-------------+
|            50 | Shi             |        121 |        1500 | 3475.555556 |
+---------------+-----------------+------------+-------------+-------------+
1 row in set (0.00 sec)


#查询平均工资最高的job信息
mysql> select j.* from jobs j where j.job_id =(select job_id from employees group by job_id order by avg(salary) desc limit 1);
+---------+-----------+------------+------------+
| job_id  | job_title | min_salary | max_salary |
+---------+-----------+------------+------------+
| AD_PRES | President |      20000 |      40000 |
+---------+-----------+------------+------------+

mysql> select avg(salary),department_id from employees group by department_id having avg(salary) > (select avg(salary) from employees ) ;
+--------------+---------------+
| avg(salary)  | department_id |
+--------------+---------------+
|  7000.000000 |          NULL |
|  9500.000000 |            20 |
|  6500.000000 |            40 |
| 10000.000000 |            70 |
|  8955.882353 |            80 |
| 19333.333333 |            90 |
|  8600.000000 |           100 |
| 10150.000000 |           110 |
+--------------+---------------+

mysql> select * from employees where employee_id in (select manager_id from employees ) ;
+-------------+------------+-----------+----------+--------------------+---------+----------+----------------+------------+---------------+---------------------+
| employee_id | first_name | last_name | email    | phone_number       | job_id  | salary   | commission_pct | manager_id | department_id | hiredate            |
+-------------+------------+-----------+----------+--------------------+---------+----------+----------------+------------+---------------+---------------------+
|         100 | Steven     | K_ing     | SKING    | 515.123.4567       | AD_PRES | 24000.00 |           NULL |       NULL |            90 | 1992-04-03 00:00:00 |
|         102 | Lex        | De Haan   | LDEH

#查询各个部门中最高工资中最低的那个部门的最低工资是多少
mysql>  select min(salary) from employees where department_id =(select department_id from (select max(salary),department_id from employees group by department_id order by max(salary) asc limit 1) a );
+-------------+
| min(salary) |
+-------------+
|     4400.00 |
+-------------+
1 row in set (0.00 sec)

#查询平均工资最高的部门的manager的详细信息:last_name , department_id , email , salary
mysql> select last_name , department_id , email , salary from employees where employee_id =(select manager_id from departments where department_id = (select department_id from employees group by department_id order by avg(salary) desc limit 1)) ;
+-----------+---------------+-------+----------+
| last_name | department_id | email | salary   |
+-----------+---------------+-------+----------+
| K_ing     |            90 | SKING | 24000.00 |
+-----------+---------------+-------+----------+
```

练习一下

```sql
mysql> select count(*)个数 , (select majorid from major where majorid = s.majorid)专业号 from student s group by majorid ;
+------+--------+
| 个数 | 专业号 |
+------+--------+
|    8 |      1 |
|    3 |      2 |


mysql> select avg(score),max(score) from result group by studentno ;
+--------------------+------------+
| avg(score)         | max(score) |
+--------------------+------------+
|                100 |        100 |
|                 90 |         90 |

#查询姓张的每个学生的最低分大于60的学号姓名  其实可以用join 就不用那么麻烦了
mysql> select min(score) 最低分,r.studentno,(select s.studentname from student s where s.studentno=r.studentno and s.studentname like'张%') a from result r group by r.studentno having 最低分>60 and a is not null ;
+--------+-----------+--------+
| 最低分 | studentno | a      |
+--------+-----------+--------+
|    100 | s001      | 张三封 |
|     70 | s004      | 张翠山 |
+--------+-----------+--------+

#可以使用diff函数 和 join
mysql> select s.studentname,(select majorname from major where majorid = s.majorid) 专业名称 from student s where s.borndate > '1998-1-1' ;
+-------------+----------+
| studentname | 专业名称 |
+-------------+----------+
| 张无忌      | html5    |
| 赵敏        | javaee   |
+-------------+----------+
2 rows in set (0.00 sec)

mysql> select s.studentname from student s join major m on s.majorid = m.majorid where datediff(s.borndate,'1998-1-1')>0 ;
+-------------+
| studentname |
+-------------+
| 张无忌      |
| 赵敏        |
+-------------+
2 rows in set (0.00 sec)

#查询每个专业的男生人数和女生人数分别是多少 在这里s.majorid=s1.majorid s1一定不能省略
mysql> select s1.majorid,(select count(*) from student s where s.majorid=s1.majorid and s.sex ='男')男生,(select count(*) from student s where s.majorid=s1.majorid and s.sex='女') 女生  from student s1 group by s1.majorid ;
+---------+------+------+
| majorid | 男生 | 女生 |
+---------+------+------+
|       1 |    5 |    3 |
|       2 |    2 |    1 |
|       3 |    2 |    2 |
+---------+------+------+
3 rows in set (0.00 sec)

#查询专业和张翠山一样的学生的最低分
mysql> select min(score) from result where studentno in (select s.studentno from student s where majorid =(select majorid from student where studentname ='张翠山') and studentname <>'张翠山') group by studentno;
+------------+
| min(score) |
+------------+
|        100 |
|         90 |
+------------+
2 rows in set (0.00 sec)

#查询大于60分的学生的姓名 密码 专业名
mysql> select s.studentname , s.loginpwd , (select majorname from major where majorid = s.majorid) from student s where s.studentno in (select distinct studentno from result where score >60) ;
+-------------+----------+---------------------------------------------------------+
| studentname | loginpwd | (select majorname from major where majorid = s.majorid) |
+-------------+----------+---------------------------------------------------------+
| 张三封      | 8888     | javaee                                                  |
| 殷天正      | 8888     | javaee                                                  |
| 周伯通      | 8888     | html5                                                   |
| 张翠山      | 8888     | javaee                                                  |
| 小小张      | 8888     | android                                                 |
| 张无忌      | 8888     | html5                                                   |
+-------------+----------+---------------------------------------------------------+

#按邮箱的位数分组,并查询个数
mysql> select count(*)个数, length(s.email) from student s group by length(s.email) ;
+------+-----------------+
| 个数 | length(s.email) |
+------+-----------------+
|    1 |              20 |
|    2 |              19 |
|    2 |              18 |
|    6 |            NULL |
|    2 |              17 |
|    2 |              15 |
+------+-----------------+

#查询学生名 专业名 分数 这是错误的 如果使用join是取完全交集
mysql> select s.studentname ,m.majorname , r.score from student s join major m on s.majorid = m.majorid join result r on s.studentno = r.studentno ;
+-------------+-----------+-------+
| studentname | majorname | score |
+-------------+-----------+-------+
| 张翠山      | javaee    |    70 |
| 殷天正      | javaee    |    90 |

#查询学生名 专业名 分数 这是错误的 应该使用left join防止出现score为null的情况
mysql> select s.studentname ,m.majorname , r.score from student s join major m on s.majorid = m.majorid left join result r on s.studentno = r.studentno ;
+-------------+-----------+-------+
| studentname | majorname | score |
+-------------+-----------+-------+
| 张三封      | javaee    |   100 |
| 殷天正      | javaee    |    90 |
| 周伯通      | html5     |    80 |

mysql> select s.studentname ,m.majorname , r.score from student s join major m on s.majorid = m.majorid left join result r on s.studentno = r.studentno ;

#查询没有成绩的学生人数
mysql> select * from (select distinct s.studentno 学号,(select score from result where studentno =s.studentno limit 1 )a from student s) b where b.a is null ;
+------+------+
| 学号 | a    |
+------+------+
| S007 | NULL |
| S008 | NULL |
| S009 | NULL |

mysql> select count(*) from (select distinct s.studentno 学号,(select score from result where studentno =s.studentno limit 1 )a from student s) b where b.a is null ;
+----------+
| count(*) |
+----------+
|        9 |
+----------+
```

##### 联合查询

union 联合 合并:将多条查询语句的结果合并成一个结果

查询语句1 union 查询语句2 union 查询语句3 ...

查询部门编号>90 或 邮箱包含a的员工信息

**应用场景**

保证两个表的列数一致 , 并不要求两个表的列名一致 ,就可以使用联合查询

要查询的结果来源于多个表,且多个表没有直接的连接关系,但查询的信息一致时

例如全站搜索 ,肯定不可能所有的数据都放在一个表里 , 所以这时候就需要union

**注意**

**union 会默认去重**

**union all 可以包含重复项**

```sql
mysql> select * from employees where department_id >90 or email like'%a%' ;

mysql> select * from employees where department_id >90 union select * from employees where  email like'%a%' ;
```

##### DML语言 数据操作语言

插入 insert

更新 update

删除 delete

##### 插入语句

**方式一**

语法:

insert into 表名(列名, ...) values(值, ...) ;

**注意**

-  插入的值的类型要与列的类型一直或兼容
- 不可以为null的列必须插入值,可以为null的列如何插入值
  - 插入null
  - 或者在 into beauty(少一点字段)
- 列的顺序可以调换
- 列和值的个数必须一致
- 可以省略列名,默认所有列名,而且列的顺序和表中列的顺序一直

```sql
#经典型 insert
mysql> insert into beauty(id,name,sex,borndate,phone,photo,boyfriend_id) values(13,'唐艺昕','女','1990-4-23','18988888',null,2);
Query OK, 1 row affected (0.00 sec)

mysql> insert into beauty(id,name,sex,phone) values(14,'金星','女','13888888');
Query OK, 1 row affected (0.00 sec)

mysql> insert into beauty values(18,'张飞','女','1990-4-23','119',null,null);
Query OK, 1 row affected (0.00 sec)
```

**方式二	**

语法

insert into 表名 set 列名 = 值 , 列名 = 值 ...

```sql
mysql> insert into beauty set id = 19 , name  = '文涛' , phone = '999' ;
Query OK, 1 row affected (0.00 sec)
```

**两种方式的区别	**

- 方式一支持多行插入,方式二不支持
- 方式一支持子查询,方式二不支持

```sql
#方式一 支持子查询
mysql> insert into beauty(id,name,phone) select 26,'宋西','11809866';
Query OK, 1 row affected (0.01 sec)
Records: 1  Duplicates: 0  Warnings: 0

#方式一 支持多行插入
mysql> insert into beauty(id,name,phone) select id , boyname,'120' from boys where id<3;
ERROR 1062 (23000): Duplicate entry '1' for key 'beauty.PRIMARY'
```

##### 修改语句

修改单表的记录(重要)

update 表名 set 列=新值 , 列=新值 where 筛选条件 ; 

```sql
update beauty set phone = '11010011' where name like '唐%' ; 

update boys set boyname = '张飞' ,userCp = 10 where id = 2 ;  
```

修改多表的记录(补充)

**sql92语法**

update 表1 别名 , 表2 别名

set 列=值 , ... where 连接条件 and 筛选条件 ; 

**sql99语法**

update 表1 别名 inner join 表2 别名 on 连接条件 set 列=值, ... where 筛选条件

```sql
#修改张无忌的女朋友的手机号为114
mysql> update beauty b join boys on b.boyfriend_id = boys.id  set phone = '114' where boys.boyname ='张无忌' ;
Query OK, 3 rows affected (0.00 sec)
Rows matched: 3  Changed: 3  Warnings: 0

#也可以使用修改单表 使用子查询
mysql> update beauty b set phone = '115' where b.boyfriend_id = (select id from boys where boyname ='张无忌') ;
Query OK, 3 rows affected (0.00 sec)
Rows matched: 3  Changed: 3  Warnings: 0

#修改没有男朋友的女神的男朋友编号都为2号
#先select
mysql> select b.name ,b.boyfriend_id,boyname from beauty b left join boys on b.boyfriend_id = boys.id where boyfriend_id is not null and boyname is null;
+--------+--------------+---------+
| name   | boyfriend_id | boyname |
+--------+--------------+---------+
| 柳岩   |            8 | NULL    |
| 苍老师 |            9 | NULL    |
| 周冬雨 |            9 | NULL    |
| 岳灵珊 |            9 | NULL    |
| 双儿   |            9 | NULL    |
| 夏雪   |            9 | NULL    |
+--------+--------------+---------+
6 rows in set (0.00 sec)

#再update
mysql> update beauty b left join boys on b.boyfriend_id = boys.id set b.boyfriend_id =2 where boyfriend_id is not null and boyname is null;
Query OK, 6 rows affected (0.00 sec)
Rows matched: 6  Changed: 6  Warnings: 0

#再查一下
mysql> select b.name ,b.boyfriend_id,boyname from beauty b left join boys on b.boyfriend_id = boys.id where boyfriend_id is not null and boyname is null;
Empty set (0.00 sec)
```

#####  删除语句

方式一  delete

方式二 truncate

语法:truncate table 表名 (删除的是所有的 不能加筛选条件)

**单表的删除**

语法:delete from 表名 where 筛选条件

**多表的删除**

语法: 

**sql92语法**

delete 表1的别名 from 表1 别名 , 表2 别名 where 连接条件 and 筛选条件 ;  //删除的是表1的数据内容

delete 表2的别名 from 表1 别名 , 表2 别名 where 连接条件 and 筛选条件 ;  //删除的是表2的数据内容

delete 表1的别名, 表2的别名 from 表1 别名 , 表2 别名 where 连接条件 and 筛选条件 ; //删除的是表1和表2的数据内容

**sql99语法**

delete 表1的别名,表2的别名 from 表1 别名 join 表2 别名 on 连接条件 where 筛选条件 

```sql
#单表的删除
delete from beauty where phone like '%9' ; 

#删除张无忌的女朋友的信息
#多表删除
mysql> delete b from beauty b join boys boy on b.boyfriend_id = boy.id where boy.boyname = '张无忌' ;
Query OK, 3 rows affected (0.01 sec)

#删除黄晓明和他女朋友的信息
mysql> delete g , b from beauty g join boys b on g.boyfriend_id = b.id where b.boyname = '黄晓明' ;
Query OK, 2 rows affected (0.00 sec)
```

**方式二 truncate语句**

直接清空 truncate table boys ; 

##### delete和truncate的区别

- delete可以加where条件 , truncate不能加
- truncate 删除, 效率高一丢丢
- 假如要删除的表中有自增长列,如果用delete删除后,再插入数据,自增长列的值依旧是从断点开始,而如果truncate删除后,再插入数据,自增长列的值从1开始
- truncate删除没有返回值,delete删除有返回值
- truncate删除回滚,delete删除可以回滚

##### 练习一下

```sql
mysql> desc users ;
+---------------+-------------+------+-----+---------+-------+
| Field         | Type        | Null | Key | Default | Extra |
+---------------+-------------+------+-----+---------+-------+
| id            | int         | YES  |     | NULL    |       |
| userid        | varchar(10) | YES  |     | NULL    |       |
| department_id | int         | YES  |     | NULL    |       |
+---------------+-------------+------+-----+---------+-------+

mysql> insert into my_employees(First_name,Last_name,Userid,salary) values ('patel','Ralph','Rpatel', 895),('Dance' , 'Betty' , 'Bdancs' , 860),('Biri','Ben','Bbiri', 1100),('Newman','Chad','Cnewman',750),('Ropeburn','Audrey' ,'Aropebur',1150);
Query OK, 5 rows affected (0.01 sec)
Records: 5  Duplicates: 0  Warnings: 0

#也可以这样
mysql>  insert into my_employees(First_name,Last_name,Userid,salary)  select 'patel','Ralph','Rpatel', 895 union select 'Dance' , 'Betty' , 'Bdancs' , 860 union select 'Biri','Ben','Bbiri', 1100 union select 'Newman','Chad','Cnewman',750 union select 'Ropeburn','Audrey' ,'Aropebur',1150;

mysql> insert into users(userid,id) values('Rpatel',10),('Bdancs',10),('Bbiri',20),('Chewman',30),('Aropebur',40);
Query OK, 5 rows affected (0.01 sec)
Records: 5  Duplicates: 0  Warnings: 0

mysql> update my_employees set last_name = 'drelxer' where id =3 ;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> update my_employees set salary = 1000 where salary <900 ;
Query OK, 3 rows affected (0.00 sec)
Rows matched: 3  Changed: 3  Warnings: 0

mysql> delete me , u from my_employees me join users u on me.userid = u.userid where u.userid = 'Bbiri';
Query OK, 2 rows affected (0.00 sec)

mysql> truncate table users ;
```

##### DDL

数据定义语言

库和表的管理

##### 库的管理

创建/修改/删除

##### 表的管理

创建/修改/删除

创建:create

修改:alter

删除:drop

##### 库的管理

##### 库的创建

语法 create database [if not exists] 库名 ; 

```sql
#如果已存在 这样执行会报错
mysql>  create database books ;
Query OK, 1 row affected (0.01 sec)

#会先判断一下
mysql>  create database if not exists books ;
Query OK, 1 row affected, 1 warning (0.00 sec)
```

##### 库的修改

更改库的字符集 

```sql
alter database books character set gbk ; 
```

##### 库的删除

```sql 
drop database books ; 

drop database if exists books ; 
```

##### 表的管理

##### 表的创建

```sql
create table 表名 (
	列名 列的类型[(长度) 约束], 
	列名 列的类型[(长度) 约束], 
	列名 列的类型[(长度) 约束], 
	列名 列的类型[(长度) 约束], 
	列名 列的类型[(长度) 约束], 
	...
)

mysql> select database() ;
+-------------+
| database()  |
+-------------+
| myemployees |
+-------------+
1 row in set (0.00 sec)

mysql> use books ;
Database changed

mysql> create table book( id int , bName varchar(20) , price double , authorId int ,publishDate datetime) ;
Query OK, 0 rows affected (0.03 sec)

mysql> desc book ;
+-------------+-------------+------+-----+---------+-------+
| Field       | Type        | Null | Key | Default | Extra |
+-------------+-------------+------+-----+---------+-------+
| id          | int         | YES  |     | NULL    |       |
| bName       | varchar(20) | YES  |     | NULL    |       |
| price       | double      | YES  |     | NULL    |       |
| authorId    | int         | YES  |     | NULL    |       |
| publishDate | datetime    | YES  |     | NULL    |       |
+-------------+-------------+------+-----+---------+-------+
5 rows in set (0.00 sec)

mysql> create table author (id int, au_name varchar(20) , nation varchar(10)) ;
Query OK, 0 rows affected (0.02 sec)
```

##### 表的修改

alter table 表名 add column / drop column / change column /modify column /raname to 列名/列类型/表名

- 修改列名
- 修改列的类型或约束
- 添加新列
- 删除列
- 修改表名

```sql
#修改列名
mysql> alter table book change column publishDate pbDate datetime;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

#修改列的类型或约束
mysql> alter table book modify column pbdate timestamp;
Query OK, 0 rows affected (0.05 sec)
Records: 0  Duplicates: 0  Warnings: 0

#添加新列
mysql> alter table author add column annual double ;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

#删除列
mysql> alter table book drop column annual ;
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0

#修改表名
mysql> alter table author rename to book_author ;
Query OK, 0 rows affected (0.01 sec)
```

##### 表的删除

drop table 表

drop table if exist 表

通用的写法:

drop database if exists 旧库名 ; 

create database 库名 ; 



drop table if exists 旧表名; 

create table 表名 (...) ; 

##### 表的复制

- 仅仅复制表的结构

```sql
mysql> create table copy like author ;
Query OK, 0 rows affected (0.02 sec)

mysql> select * from copy ;
Empty set (0.00 sec)
```

- 复制表的结构和数据

```sql
#子查询
mysql> create table copy2 select * from author ;
Query OK, 4 rows affected (0.02 sec)
Records: 4  Duplicates: 0  Warnings: 0

mysql> select * from copy2 ;
+------+----------+--------+
| id   | au_name  | nation |
+------+----------+--------+
|    1 | 村上春树 | 日本   |
|    2 | 莫言     | 中国   |
|    3 | 冯唐     | 中国   |
|    4 | 金庸     | 中国   |
+------+----------+--------+
4 rows in set (0.00 sec)
```

- 只复制部分数据

```sql
#根据一张表的部分数据 建立另一张表
mysql> create table copy3 select id,au_name from author where nation ='中国' ;
Query OK, 3 rows affected (0.02 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> select * from copy3 ;
+------+---------+
| id   | au_name |
+------+---------+
|    2 | 莫言    |
|    3 | 冯唐    |
|    4 | 金庸    |
+------+---------+
3 rows in set (0.00 sec)
```

- 仅仅复制某些字段

```sql
#这样就只会复制字段,并且不满足条件不携带任何一条数据过来
mysql> create table copy4 select id from author where 0 ;
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> select * from copy4 ;
Empty set (0.00 sec)
```

##### 练习一下

```sql
mysql> create database test ;
Query OK, 1 row affected (0.01 sec)

mysql> create table dept1(id int(7),name varchar(25));
Query OK, 0 rows affected, 1 warning (0.03 sec)

#将departments中的数据插入新表
mysql> create table dept2 select * from myemployees.departments ;
Query OK, 27 rows affected (0.02 sec)
Records: 27  Duplicates: 0  Warnings: 0

mysql> create table emp5 (id int(7),first_name varchar(25),last_name varchar(25),dept_id int(7)) ;
Query OK, 0 rows affected, 2 warnings (0.02 sec)

#这样是修改列名和类型的
mysql> alter table emp5 change column last_name last_name varchar(50);
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

#这样只是修改类型的
mysql> alter table emp5 modify column last_name varchar(50) ;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

#复制结构
mysql> create table employees2 like myemployees.employees ;
Query OK, 0 rows affected, 2 warnings (0.03 sec)

mysql> drop table emp5 ;
Query OK, 0 rows affected (0.02 sec)

#修改表的名字
mysql> alter table employees2 rename to emp5 ;
Query OK, 0 rows affected (0.02 sec)

#增加列
mysql> alter table dept1 add column test_column int ;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> alter table emp5 add column test_column int ;
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

#删除列
mysql> alter table emp5 drop column department_id ;
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

##### 常见的数据类型

数值型

- 整形
- 小数
  - 定点数
  - 浮点数

字符型

- 较短的文本 char varchar
- 较长的文本 text blob(较长的二进制数据)

日期型:

**整形**

![image-20210926214209015](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210926214209015.png)

分类

tinyint smallint mediumin int/interger bigint

  1              2                3                  4            8

特点

- 如果不设置无符号还是有符号，默认是有符号，如果想设置无符号，需要添加unsigned关键字
- 如果插入的数值超出了类型的范围,会报out of range异常 ,但是与mysql5.0不同的是,现在不会插入数据了,mysql5.0会插入临界值
- 如果不设置长度,会有默认的长度

如何设置无符号和有符号

```sql
mysql> desc tab_int ;
+-------+------+------+-----+---------+-------+
| Field | Type | Null | Key | Default | Extra |
+-------+------+------+-----+---------+-------+
| t1    | int  | YES  |     | NULL    |       |
+-------+------+------+-----+---------+-------+
1 row in set (0.01 sec)

#说明能够插入负数 说明默认的int是有符号的int
mysql> insert into tab_int values(-123456) ;
Query OK, 1 row affected (0.01 sec)

#
mysql> drop table if exists tab_int ;
Query OK, 0 rows affected (0.02 sec)

#插入无符号int类型
mysql> create table tab_int ( t1 int , t2 int unsigned) ;
Query OK, 0 rows affected (0.02 sec)

#想给无符号整数插入负数的话会报错 0行一共 但是在mysql5.5会插入 然后默认填充0
mysql> insert into tab_int values(-123456,-123456) ;
ERROR 1264 (22003): Out of range value for column 't2' at row 1
mysql> select * from tab_int ;
Empty set (0.00 sec)

#zerofill 默认长度不够以0填充 默认是无符号数 int(7)不是2的7位,代表的是显示的最大宽度
mysql> create table int_zeroFill (t1 int(7) zerofill , t2 int(7) zerofill);
Query OK, 0 rows affected, 4 warnings (0.02 sec)

mysql> desc int_zeroFill ;
+-------+--------------------------+------+-----+---------+-------+
| Field | Type                     | Null | Key | Default | Extra |
+-------+--------------------------+------+-----+---------+-------+
| t1    | int(7) unsigned zerofill | YES  |     | NULL    |       |
| t2    | int(7) unsigned zerofill | YES  |     | NULL    |       |
+-------+--------------------------+------+-----+---------+-------+
2 rows in set (0.01 sec)

mysql> insert into int_zerofill values (123,123);
Query OK, 1 row affected (0.00 sec)

mysql> select * from int_zerofill ;
+---------+---------+
| t1      | t2      |
+---------+---------+
| 0000123 | 0000123 |
+---------+---------+
1 row in set (0.00 sec)
```

##### 小数

![image-20210929224058024](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210929224058024.png)

浮点型

float(M,D)

double(M,D)

定点型

dec(M,D)

decimal(M,D)

特点:

- M和D什么意思
  - m是小数部位+整数部位 d是小数部位 如果超过范围, 则插入临界值
- m和d都可以省略
  - 如果是decimal , 则m默认为10,d默认为0
  - 如果是float和double,则会根据插入的数值的精度来决定精度
- 定点型和浮点型的区别
  - 定点型的精确度较高,如果要求插入数值的精度较高如货币运算等则考虑使用

```sql
#小数
mysql>  create table tab_float (f1 float(5,2) ,f2 double(5,2) ,f3 decimal(5,2)) ;
Query OK, 0 rows affected, 2 warnings (0.02 sec)

mysql> insert into tab_float values (123.45,123.45,123.45) ;
Query OK, 1 row affected (0.01 sec)

#会被截取 位数太长的话
mysql> insert into tab_float values (123.456,123.456,123.456) ;
Query OK, 1 row affected, 1 warning (0.00 sec)

#短了就自动填充 
mysql> insert into tab_float values (123.4 , 123.4 , 123.4) ;
Query OK, 1 row affected (0.00 sec)

#(5,2) 2代表小数后几位
mysql> select * from tab_float ;
+--------+--------+--------+
| f1     | f2     | f3     |
+--------+--------+--------+
| 123.45 | 123.45 | 123.45 |
| 123.46 | 123.46 | 123.46 |
| 123.40 | 123.40 | 123.40 |
+--------+--------+--------+
3 rows in set (0.00 sec)

#超出位数了 超出的话mysql8.0将不会插入 (5,2) 5代表一共多少位数 , 如果小数位2位,那整数位最多3位,所以整数最多999 mysql5.0会插入最大值
mysql> insert into tab_float values(1523.4,1523.4,1523.4);
ERROR 1264 (22003): Out of range value for column 'f1' at row 1

mysql> select * from tab_float ;
+--------+--------+--------+
| f1     | f2     | f3     |
+--------+--------+--------+
| 123.45 | 123.45 | 123.45 |
| 123.46 | 123.46 | 123.46 |
| 123.40 | 123.40 | 123.40 |
+--------+--------+--------+
3 rows in set (0.00 sec)

#如果不填写 m和d decimal默认是(10,0) 小数后面是0位
mysql> create table tab_float_default (f1 float , f2 double , f3 decimal) ;
Query OK, 0 rows affected (0.03 sec)

mysql> desc tab_float_default ;
+-------+---------------+------+-----+---------+-------+
| Field | Type          | Null | Key | Default | Extra |
+-------+---------------+------+-----+---------+-------+
| f1    | float         | YES  |     | NULL    |       |
| f2    | double        | YES  |     | NULL    |       |
| f3    | decimal(10,0) | YES  |     | NULL    |       |
+-------+---------------+------+-----+---------+-------+
3 rows in set (0.01 sec)

#如果插入了多了,会自动截断
mysql> insert into tab_float_default values (123.456,123.456,123.456) ;
Query OK, 1 row affected, 1 warning (0.01 sec)

mysql> select * from tab_float_default ;
+---------+---------+------+
| f1      | f2      | f3   |
+---------+---------+------+
| 123.456 | 123.456 |  123 |
+---------+---------+------+
1 row in set (0.00 sec)
```

#####  选择类型的原则

所选择的类型越简单越好,能保存数值的类型越小越好

##### 字符型

较短的文本:

char

varchar

较长的文本:

text

blob(较大的二进制)

其他:

binary和varbinary用于保存较短的二进制数据

enum用于保存枚举

set用于保存集合



![image-20210929230011199](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210929230011199.png)

特点:

- char char(m) m代表最大的字符数,可以省略,默认为1  代表固定长度的字符  效率高一点
- varchar varchar(m) m代表最大的字符数,不可以省略 可变长度的字符 比较节省 效率低一点

![image-20210929230312590](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210929230312590-16329277930351.png)

```sql
#类型为enum的字段
mysql> create table tab_char(c1 enum('a','b','c'));
Query OK, 0 rows affected (0.02 sec)

mysql> desc tab_char ;
+-------+-------------------+------+-----+---------+-------+
| Field | Type              | Null | Key | Default | Extra |
+-------+-------------------+------+-----+---------+-------+
| c1    | enum('a','b','c') | YES  |     | NULL    |       |
+-------+-------------------+------+-----+---------+-------+
1 row in set (0.01 sec)

mysql> insert into tab_char values('a') ;
Query OK, 1 row affected (0.01 sec)

#不区分大小写
mysql> insert into tab_char values('A');
Query OK, 1 row affected (0.00 sec)

#没有定义的插入不进去
mysql> insert into tab_char values ('m');
ERROR 1265 (01000): Data truncated for column 'c1' at row 1
mysql> select * from tab_char ;
+------+
| c1   |
+------+
| a    |
| a    |
+------+
2 rows in set (0.00 sec)
```

![image-20210929230732259](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210929230732259.png)

可以从在一个字段里插入多个元素辣

```sql
#创建类型为set的字段
mysql> create table tab_set(s1 set('a','b','c','d'));
Query OK, 0 rows affected (0.02 sec)

mysql> insert into tab_set values('a');
Query OK, 1 row affected (0.01 sec)

mysql> insert into tab_set values('a,B');
Query OK, 1 row affected (0.00 sec)

#不符合的不会插入
mysql> insert into tab_set values ('a,m');
ERROR 1265 (01000): Data truncated for column 's1' at row 1

mysql> select * from tab_set ;
+------+
| s1   |
+------+
| a    |
| a,b  |
+------+
2 rows in set (0.00 sec)
```

##### 日期型

分类:

date只保存日期

time只保存时间

year只保存年

datetime 保存日期+时间

timestamp 保存日期+时间

特点:

datetime 字节 8 范围 1000-9999 不受时区影响

timastamp 字节 4 范围 1970-2038 受时区影响

![image-20210929233916597](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210929233916597.png)



![image-20210929234007359](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20210929234007359.png)

```sql
mysql> select * from tab_date ;
+---------------------+---------------------+
| t1                  | t2                  |
+---------------------+---------------------+
| 2021-09-29 23:40:53 | 2021-09-29 23:40:53 |
+---------------------+---------------------+
1 row in set (0.00 sec)

#时区 如果将时区改成其他时区 , timestamp可以更加真实地反映当前时区的真实时间 而不是不变
mysql> show variables like 'time_zone' ;
+---------------+--------+
| Variable_name | Value  |
+---------------+--------+
| time_zone     | SYSTEM |
+---------------+--------+
1 row in set, 1 warning (0.00 sec)
```

##### 复习一下

**联合查询**

union 联合 , 将多次查询结果合并为一个结果

查询语句1 union [all] 查询语句2 ...

**意义	**

1. 将一条比较复杂的查询语句拆分为多条语句
2. 适用于查询多个表的时候,查询的列基本是一致的

**特点**

1. 要求多条查询语句的查询列数必须一致
2. 要求多条查询语句的查询的各列类型/顺序最好一致 不一致会视图隐式转换
3. union会默认去重 和 union all 可以包含重复项

查询的语法:

select *   ⑦

from 表1 别名   ①

join 表2 别名     ②

on 连接条件    	③

where 筛选条件   ④

group by 分组条件  ⑤

 having 分组后筛选条件   ⑥

order by 排序条件  ⑧

 limit(起始索引,条目数)选多少个  ⑨

 union ...  

##### DML语言

**插入**

insert into 表名 (字段名 , ...) values (...)  //一一对应

**特点**

1. 要求值的类型和字段的类型要一致或兼容
2. 字段的个数和顺序不一定与原始表中的字段的个数和顺序一致,但必须保证值和字段一一对应
3. 假如可以为null的字段,注意可以通过以下两种方式插入null值
   - 字段和值都省略
   - 字段写上,然后值也使用null插入
4. 字段和值的个数必须一致
5. 字段名可以省略,但是默认为所有列

**插入2**

insert into 表名 set 字段名 = 值 , 字段名 = 值 ...

**两种方式的区别**

- 方式一支持**子查询**
  - insert into 表名 (select * from 表名 where ...)

- 方式一支持一次插入多行,方式二不支持 

  - insert into 表名 values (...),(...) ...

   

##### 修改单表的记录

update 表名 set 字段=值 , 字段= 值 where 筛选条件

##### 修改多表的记录

update 表名 别名 join  表名 别名 on 连接条件 set 字段=值 , 字段 = 值 where 筛选语句

##### 删除

##### 方式一使用delete

删除单表的记录

delete from 表名 where 筛选条件 [limit 条目数]

```sql
mysql> select * from copy_girls ;
+----+--------+------+---------------------+-------------+--------------+--------------+
| id | name   | sex  | borndate            | phone       | photo        | boyfriend_id |
+----+--------+------+---------------------+-------------+--------------+--------------+
|  1 | 柳岩   | 女   | 1988-02-03 00:00:00 | 18209876577 | NULL         |            2 |
|  2 | 苍老师 | 女   | 1987-12-30 00:00:00 | 18219876577 | NULL         |            2 |
|  4 | 热巴   | 女   | 1993-02-03 00:00:00 | 18209876579 | NULL         |            2 |
|  5 | 周冬雨 | 女   | 1992-02-03 00:00:00 | 18209179577 | NULL         |            2 |

mysql> delete from copy_girls limit 1 ;
Query OK, 1 row affected (0.01 sec)

mysql> select * from copy_girls ;
+----+--------+------+---------------------+-------------+--------------+--------------+
| id | name   | sex  | borndate            | phone       | photo        | boyfriend_id |
+----+--------+------+---------------------+-------------+--------------+--------------+
|  2 | 苍老师 | 女   | 1987-12-30 00:00:00 | 18219876577 | NULL         |            2 |
|  4 | 热巴   | 女   | 1993-02-03 00:00:00 | 18209876579 | NULL         |            2 |
```

删除多表的记录

delete 表1 别名1, 表2 别名2 from 表名 别名  join 表名 别名 on 连接条件 where 筛选条件 

**方式二使用truncate**

**两种方式的区别**

- delete不会让自增列归零,从断点开始,truncate会让自增列归零

- delete可以加筛选条件,truncate 不能加筛选条件 

- truncate 效率较高
- truncate 没有返回值,delete可以返回受影响的行数
- truncate不可以回滚,delete可以回滚

##### DDL语言

##### **库的管理**

创建库

create database  [if not exists] 库名 [character set 字符集名] ; 

修改库

alter database 库名 character set 字符集名 ; 

修改库名很少用,不行就换个库呗何必呢,如果实在要改,就先net stop mysql80 然后到mysql8.0下的data文件夹中重命名某个数据库名,然后net start mysql80 ,刷新数据库管理工具

删除库

drop database [if exists] 库名 ; 

**表的管理**

**创建表**

create table [if not exists] 表名(字段名 类型 [约束], 字段名 类型 [约束] ...) ; 

**修改表**

**添加列**

alter table 表名 add column 列名 列的类型 [first|after 字段名];

```sql
mysql> create table test_add_column (
    -> t1 int ,
    -> t2 int ,
    -> t3 int );
Query OK, 0 rows affected (0.02 sec)

mysql> desc test_add_column ;
+-------+------+------+-----+---------+-------+
| Field | Type | Null | Key | Default | Extra |
+-------+------+------+-----+---------+-------+
| t1    | int  | YES  |     | NULL    |       |
| t2    | int  | YES  |     | NULL    |       |
| t3    | int  | YES  |     | NULL    |       |
+-------+------+------+-----+---------+-------+
3 rows in set (0.01 sec)

mysql> alter table test_add_column add column t11 bigint first ;
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc test_add_column ;
+-------+--------+------+-----+---------+-------+
| Field | Type   | Null | Key | Default | Extra |
+-------+--------+------+-----+---------+-------+
| t11   | bigint | YES  |     | NULL    |       |
| t1    | int    | YES  |     | NULL    |       |
| t2    | int    | YES  |     | NULL    |       |
| t3    | int    | YES  |     | NULL    |       |
+-------+--------+------+-----+---------+-------+
```

**修改列的类型或者约束**

alter table 表名 modify column 列名 新类型[新约束] ;

**修改列名**

alter table 表名 change column 旧列名 新列名 类型; 

**删除列名** 

alter table 表名 drop column 列名 ; 

**修改表名**

alter table 表名 rename to 新表名

**删除表**

drop table [if exists] 表名; 

**复制表** 可以跨库

**仅仅复制表的结构** create table 表名 like 原表 ; 

**复制表的结构+数据** 

create table 表名 select * from 原表 ;  

create table 表名 select 特定字段 from 原表 where 筛选条件

##### 数据类型

**数值型**

1. 整型
   1. tinyint smallint mediumint int integer bigint 1 2 3 4 8
   2. 特点
      1. 都可以设置无符号和有符号 默认是有符号 ,通过 unsigned设置无符号
      2. 如果超出范围,out of range 异常,mysql5.0 和 8.0 不同
      3. 长度可以不指定,默认会有一个长度
      4. 长度代表的是显示的最大宽度,而不是只有2的长度位那个范围,但需要搭配zerofill,搭配之后将默认变为无符号整型
2. 浮点型
   1. 定点数 decimal(m,d) 默认为(10,0)
   2. 浮点数 float(m,d) 4位字节  double(m,d) 8位字节  默认为可变的
   3. 特点
      1. m代表整数+小数部位的个数,d代表小数部位
      2. 如果超出范围,则报out of range异常,并且插入临界值
      3. m和d都可以省略,但对于定点数,m默认为10,d默认为0
      4. 如果精度要求较高,则有限考虑使用定点数

**字符型**

char varchar binary varbinary enum set text blob

char:固定长度的字符,写法为char(M) ,最大长度不能超过M ,其中M可以省略,默认为1

varchar:可变长度的字符 写法varchar(M),最大长度不能超过M,其中M不可以省略

**日期型**

year 年

date 日期

datetime 日期+时间   8 

time 时间

timestamp 时间戳   4  1970-2038 比较容易受到时区,语法模式,版本的影响,更能反映当前时区的真实时间



#### 新的一杰克

##### 常见约束

含义 : 一种限制 , 用于限制表中的数据,为了保证表中的数据的准确和可靠性

**分类** **六大约束**

- NOT NULL 非空 用于保证该字段的值不能为空  比如姓名/学号等等

- default 默认 , 用于保证该字段有默认值
- PRIMARY KEY 主键 用于保证该字段的值具有唯一性,并且非空,如学号,工号
- UNIQUE 唯一,用于保证该字段的值具有唯一性,可以为空 如座位号/老婆
- CHECK 检查约束 [mysql 不支持] 比如性别 只能男和女 或者青年人年龄
- FOREIGN KEY 外键,用于限制两个表的关系,用于保证该字段的值必须来自于主表的关联列的值 在从表添加外键约束,用于引用主表中的某列的值 例如学生表的专业编号,员工表的部门编号,员工表的工种编号

添加约束的时机:

1. 创建表时
2. 修改表时

约束的添加分类:

-  列级约束
  - NOT NULL DEFAULT PRIMARY KEY UNIQUE CHECK FOREIGN KEY 六大约束语法上都支持,但是外键约束没有效果
-  表级约束
  - 除了非空/默认,其他的都支持

```sql
create table 表(
	字段名 字段类型 列级约束,
    字段名	字段类型,
    表级约束
)
```

**创建表时添加约束**

**添加列级约束**

语法:直接在字段名和类型后面追加约束类型即可

只支持:默认/非空/主键

```sql
mysql> create database students ;
Query OK, 1 row affected (0.01 sec)

mysql> use students ;
Database changed

#创建列级约束
mysql> create table stuinfo ( id int primary key , stuName varchar(20) not null , gender char(1) check(gender='男' or gender='女') ,seat int unique,age int default 18,majorId int references major(id));
Query OK, 0 rows affected (0.03 sec)

mysql> desc stuinfo ;
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| id      | int         | NO   | PRI | NULL    |       |
| stuName | varchar(20) | NO   |     | NULL    |       |
| gender  | char(1)     | YES  |     | NULL    |       |
| seat    | int         | YES  | UNI | NULL    |       |
| age     | int         | YES  |     | 18      |       |
| majorId | int         | YES  |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+
6 rows in set (0.00 sec)

#查看索引 唯一/主键/外键都可以查看
mysql> show index from stuinfo ;
```



**添加表级约束**

语法:在各个字段的最下面

[constraint 约束名] 约束类型(字段名) ...

```sql
mysql> create table stuinfo(id int , stuname varchar(20),gender char(1),seat int , age int ,majorid int ,constraint pk primary key(id),constraint uq unique(seat) , constraint ck check(gender in ('男','女')),constraint fk_stuinfo_major foreign key(majorid) references major(id)) ;
Query OK, 0 rows affected (0.04 sec)

mysql> show index from stuinfo ;
```

![image-20211001160138048](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20211001160138048.png)

**constraint 约束名 可以去掉**

```sql
mysql> create table stuinfo(id int , stuname varchar(20),gender char(1),seat int , age int ,majorid int ,primary key(id),unique(seat),check(gender in ('男','女')),foreign key(majorid) references major(id)) ;
Query OK, 0 rows affected (0.06 sec)
```

![image-20211001160643505](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20211001160643505.png)

**通用写法**

```sql
crete table if not exists stuinfo(
	id int primary key ,
    stuname varchar(20) not null , 
    sex char(1)
    age int default 18,
    seat int unique ,
    majorid int ,
    constraint fk_stuinfo_major foreign key(majroid) references major(id)
)
```

主键和唯一的大对比

|      | 保证唯一性 | 是否允许为空 | 一个表中可以有几个 | 是否允许组合键 |
| ---- | ---------- | ------------ | ------------------ | -------------- |
| 主键 | 对         | 不对         | 一个表中至多有一个 | 是,但不推荐    |
| 唯一 | 对         | 对           | 可以有多个         | 是,但不推荐    |

```sql
primar key (id,stuname)
unique (seat,majorid)
```

外键:

1. 要求在从表设置外键关系
2. 从表的外键列的类型和主表的关联列一致或兼容,名称无所谓
3. 主表的关联咧必须是一个key或者唯一键
4. 插入数据时,先插入主表,再插入从表
5. 删除数据时,先删除从表,再删除主表

**修改表时添加约束**

- 添加列级约束 alter table 表名 mofidy column 字段名  字段类型 新约束 ; 
- 添加表级约束 alter table 表名 add [constraint 约束名] 约束类型(字段名)  [外键的引用] ;  

添加非空约束

**添加列级约束**

```sql
mysql> drop table if exists stuinfo ;
Query OK, 0 rows affected (0.02 sec)

mysql> create table stuinfo(id int,stuname varchar(20),gender char(1),seat int,age int,majorid int);
Query OK, 0 rows affected (0.02 sec)

mysql> alter table stuinfo modify column stuname varchar(20) not null ;
Query OK, 0 rows affected (0.03 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc stuinfo;
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| id      | int         | YES  |     | NULL    |       |
| stuname | varchar(20) | NO   |     | NULL    |       |
| gender  | char(1)     | YES  |     | NULL    |       |
| seat    | int         | YES  |     | NULL    |       |
| age     | int         | YES  |     | NULL    |       |
| majorid | int         | YES  |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+
6 rows in set (0.00 sec)

mysql> alter table stuinfo modify column age int defeault 18 ;

mysql> alter table stuinfo modify column age int default 18 ;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> alter table stuinfo modify column id int primary key ;
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

**添加表级约束**

```sql
mysql> alter table stuinfo add unique(seat);
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

**添加外键**

```sql
mysql> alter table stuinfo add constraint fk_studentinfo_major foreign key(majorid) references major (id) ;
Query OK, 0 rows affected (0.05 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

**修改表时删除约束**

```sql
#取消非空约束
mysql> alter table stuinfo modify column stuname varchar(20) null ;
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0

#取消默认约束
mysql> alter table stuinfo modify column age int ;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

#删除主键
mysql> alter table stuinfo  drop primary key ;
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0

#删除唯一键
mysql> alter table stuinfo drop index seat ;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> show index from stuinfo ;
+---------+------------+----------------------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| Table   | Non_unique | Key_name             | Seq_in_index | Column_name | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment | Visible | Expression |
+---------+------------+----------------------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| stuinfo |          1 | fk_studentinfo_major |            1 | majorid     | A         |           0 |     NULL |   NULL | YES  | BTREE      |         |               | YES     | NULL       |
+---------+------------+----------------------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
1 row in set (0.01 sec)

#删除外键
mysql> alter table stuinfo drop foreign key fk_studentinfo_major ;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

##### 练习一下

```sql
#添加主键约束
mysql> create table emp2 (id int,constraint my_emp_id_pk primary key(id));
Query OK, 0 rows affected (0.02 sec)

mysql> use test ;
Database changed

#添加主键约束
mysql> alter table dept2 add constraint my_dept_id_pk primary key(department_id);
Query OK, 0 rows affected (0.03 sec)
Records: 0  Duplicates: 0  Warnings: 0

#拷贝数据和结构
mysql> create table emp2 select * from students.emp2 ;
Query OK, 0 rows affected (0.03 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> show tables ;
+-------------------+
| Tables_in_test    |
+-------------------+
| dept1             |
| dept2             |
| emp2              |
| emp5              |
| int_zerofill      |
| tab_char          |
| tab_date          |
| tab_float         |
| tab_float_default |
| tab_int           |
| tab_set           |
| test_add_column   |
+-------------------+
12 rows in set (0.00 sec)

mysql> alter table emp2 add column dept_id int ;
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

#添加外键约束
mysql> alter table emp2 add foreign key(dept_id) references dept2(department_id);
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

**表级约束和列级约束的区别**

​					位置							支持的约束类型									是否可以起约束名

列级约束     列的后面 					支持所有语法,但是外键没有效果	  不可以起约束名

表级约束 	所有列的下面 			默认和非空不支持,其他支持			  可以起约束名

##### 标识列  

又称为自增长列

可以不用手动的插入值，系统提供默认的序列值

**创建表时设置标识列**

**特点**

- 标识列必须和主键搭配吗？不一定，但要求是一个key
- 一个表可以有多少个标识列？至多一个
- 标识列的类型只能是数值型 一般是int
- 标识列可以通过 set auto_increment =3 ;设置步长
- 标识列可以通过手动的方式设置起始值 

```sql
mysql> create table tab_identity(id int primary key , name varchar(20) ) ;
Query OK, 0 rows affected (0.02 sec)

mysql> insert into tab_identity value (1,'john') ;
Query OK, 1 row affected (0.01 sec)

#不是自增的话，搞不定 会主键重复的
mysql> insert into tab_identity value (1,'john') ;
ERROR 1062 (23000): Duplicate entry '1' for key 'tab_identity.PRIMARY'

mysql> drop table if exists tab_identity ;
Query OK, 0 rows affected (0.01 sec)

mysql> create table tab_identity (id int primary key auto_increment , name varchar(20)) ;
Query OK, 0 rows affected (0.02 sec)

#可以给他不设置列值
mysql> insert into tab_identity(name) values ('john') ;
Query OK, 1 row affected (0.01 sec)

#或者可以给他设置为null就好了
mysql> insert into tab_identity values (null , 'jwt') ;
Query OK, 1 row affected (0.00 sec)

mysql> insert into tab_identity values (null , 'jwt') ;
Query OK, 1 row affected (0.00 sec)

mysql> insert into tab_identity values (null , 'jwt') ;
Query OK, 1 row affected (0.00 sec)

mysql> select * from tab_identity ;
+----+------+
| id | name |
+----+------+
|  1 | john |
|  2 | jwt  |
|  3 | jwt  |
|  4 | jwt  |
+----+------+
4 rows in set (0.00 sec)
```

mysql不支持设置起始的数值，但是可以通过取巧的办法手动设置

```sql
#查看自增长变量
mysql> show variables like '%auto_increment%' ;
+--------------------------+-------+
| Variable_name            | Value |
+--------------------------+-------+
| auto_increment_increment | 1     |
| auto_increment_offset    | 1     |
+--------------------------+-------+
2 rows in set, 1 warning (0.00 sec)

#设置自增长的步长
mysql> set auto_increment_increment = 3 ;
Query OK, 0 rows affected (0.00 sec)

mysql> show variables like '%auto_increment%' ;
+--------------------------+-------+
| Variable_name            | Value |
+--------------------------+-------+
| auto_increment_increment | 3     |
| auto_increment_offset    | 1     |
+--------------------------+-------+
2 rows in set, 1 warning (0.00 sec)

mysql> insert into tab_identity values (null , 'jwt') ;
Query OK, 1 row affected (0.00 sec)

mysql> select * from tab_identity ;
+----+------+
| id | name |
+----+------+
|  1 | john |
|  2 | jwt  |
|  3 | jwt  |
|  4 | jwt  |
|  7 | jwt  |
+----+------+
5 rows in set (0.00 sec)

#手动设置起始值 这样就可以达到效果了
mysql> insert into tab_identity values (100, 'jwt') ;
Query OK, 1 row affected (0.00 sec)

mysql> select * from tab_identity ;
+-----+------+
| id  | name |
+-----+------+
|   1 | john |
|   2 | jwt  |
|   3 | jwt  |
|   4 | jwt  |
|   7 | jwt  |
| 100 | jwt  |
+-----+------+
6 rows in set (0.00 sec)

mysql> insert into tab_identity values (null , 'jwt') ;
Query OK, 1 row affected (0.00 sec)

mysql> select * from tab_identity ;
+-----+------+
| id  | name |
+-----+------+
|   1 | john |
|   2 | jwt  |
|   3 | jwt  |
|   4 | jwt  |
|   7 | jwt  |
| 100 | jwt  |
| 103 | jwt  |
+-----+------+
7 rows in set (0.00 sec)
```

**修改表时设置标识列**

```sql
alter table tab_identity modify column id int primary key auto_increment ;  
```

**修改表时删除标识列**

```sql
alter table tab_identity modify column id int  ; 
```

#### TCL

Transaction Control Languaue 事务控制语言

##### 事务

一个或者一组sql语句组成一个执行单元,这个执行单元要么全部执行,要么全部不执行

**事务的特点**

ACID

- 原子性 一个事务不可再分割,要么执行要么都不执行
- 一致性 一个事务执行会使数据从一个一致状态切换到另一个一致状态
- 持久性 一个事务的执行不受其他事务的干扰
- 隔离性 一个事务一旦提交,则会永久的改变数据库的数据

案例 转账

事务:事务由单独单元的一个或多个语句组成,在这个单元中,每个mysql语句是相互以来的.而整个单独单元作为一个不可分割的整体,如果单元中某条sql语句一旦执行失败或产生错误,整个单元将会回滚.所有受到影响的数据将返回到事务开始以前的状态;如果单元中的所有sql语句均执行成功,则事务被顺利执行.

##### **存储引擎**

- 概念:在mysql中的数据用各种不同的技术存储在文件(或内存)中
- 通过show engines 来查看mysql支持的存储引擎
- 在mysql中用的最多的存储引擎有 innodb myisam memory 等 其中innodb支持事务,而myisam/memory等不支持事务

```sql
mysql> show engines ;
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
| Engine             | Support | Comment                                                        | Transactions | XA   | Savepoints |
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
| MEMORY             | YES     | Hash based, stored in memory, useful for temporary tables      | NO           | NO   | NO         |
| MRG_MYISAM         | YES     | Collection of identical MyISAM tables                          | NO           | NO   | NO         |
| CSV                | YES     | CSV storage engine                                             | NO           | NO   | NO         |
| FEDERATED          | NO      | Federated MySQL storage engine                                 | NULL         | NULL | NULL       |
| PERFORMANCE_SCHEMA | YES     | Performance Schema                                             | NO           | NO   | NO         |
| MyISAM             | YES     | MyISAM storage engine                                          | NO           | NO   | NO         |
| InnoDB             | DEFAULT | Supports transactions, row-level locking, and foreign keys     | YES          | YES  | YES        |
| BLACKHOLE          | YES     | /dev/null storage engine (anything you write to it disappears) | NO           | NO   | NO         |
| ARCHIVE            | YES     | Archive storage engine                                         | NO           | NO   | NO         |
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
9 rows in set (0.00 sec)
```

事务的ACID属性

- 原子性A  事务是一个不可分割的工作单位,事务中的操作要么都发生,要么都不发生
- 持久性D 持久性是指一个事务一旦被提交,它对数据库中数据的改变就是永久性的,接下来的其他操作和数据库故障不应该对其有任何影响  
- 隔离性I  事务的隔离性是指一个事务的执行不能被其他事务干扰,即一个事务内部的操作及使用的数据对并发的其他事务是隔离的,并发执行的各个事务之间不能互相干扰
- 一致性C  事务必须使数据库从一个一致性状态变换到另一个一致性状态

**事务的创建**

- 隐式事务:事务没有明显的开启和结束的标记

比如insert / update / delete 语句

```sql
mysql> show variables like 'autocommit' ;
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| autocommit    | ON    |
+---------------+-------+
1 row in set, 1 warning (0.00 sec)
```

- 显式事务:事务具有明显的开启和结束标记 前提是必须先设置自动提交功能为禁用

```sql
#只是针对当前事务有效 所以每次开启显式事务的时候都要手动的关闭自动提交功能
set autocommit = 0 ; 

```

步骤1 : 开启事务

set autocommit = 0 

start transaction ; 可选的

步骤2 : 编写事务中的sql语句 select insert update delete ... 

语句1 

语句2 

...

步骤3 : 结束事务

commit ; 提交事务

rollback ; 回滚事务

savepoint 节点名 ; 设置保存点

```sql
mysql> create table account(id int primary key auto_increment , username varchar(20), balance double) ;
Query OK, 0 rows affected (0.03 sec)

mysql> insert into account (username,balance) values ('张无忌',1000) , ('赵敏',1000) ;
Query OK, 2 rows affected (0.00 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> select * from account ;
+----+----------+---------+
| id | username | balance |
+----+----------+---------+
|  1 | 张无忌   |    1000 |
|  4 | 赵敏     |    1000 |
+----+----------+---------+
2 rows in set (0.00 sec)

#禁用自动提交 开启事务
mysql> set autocommit = 0 ;
Query OK, 0 rows affected (0.00 sec)

#开启事务
mysql> start transaction ;
Query OK, 0 rows affected (0.01 sec)

mysql> update account set balance =500 where username = '张无忌' ;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

#在navicat里查看好像是1000 1000
mysql> select * from account ;
+----+----------+---------+
| id | username | balance |
+----+----------+---------+
|  1 | 张无忌   |     500 |
|  4 | 赵敏     |    1000 |
+----+----------+---------+
2 rows in set (0.00 sec)

#回滚试了试
mysql> rollback ;
Query OK, 0 rows affected (0.00 sec)

#是可以的
mysql> select * from account ;
+----+----------+---------+
| id | username | balance |
+----+----------+---------+
|  1 | 张无忌   |    1000 |
|  4 | 赵敏     |    1000 |
+----+----------+---------+
2 rows in set (0.00 sec)

#体验一下事务
mysql> set autocommit = 0 ;
Query OK, 0 rows affected (0.00 sec)

mysql> start transaction ;
Query OK, 0 rows affected (0.00 sec)

mysql> update account set balance = 500 where username = '张无忌' ;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> update account set balance = 1500 where username = '赵敏' ;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

#提交
mysql> commit ;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from account ;
+----+----------+---------+
| id | username | balance |
+----+----------+---------+
|  1 | 张无忌   |     500 |
|  4 | 赵敏     |    1500 |
+----+----------+---------+
2 rows in set (0.00 sec)
```

##### **数据库的隔离级别**

- 对于同时运行的多个事务,当这些事务访问数据库中相同的数据时,如果没有采取必要的隔离机制,就会导致各种并发问题
  - 脏读:对于两个事务T1 , T2 ,T1读取了已经被T2更新,但是还没有被提交的字段,之后,若T2回滚,T1读取的内容就是临时且无效的
  - 不可重复读:对于两个事务T1 , T2 , T1 读取了一个字段,然后T2 更新了该字段.之后,T1再次读取同一个字段,值就不同了
  - 幻读:对于两个事务T1 , T2 , T1从一个表中读取了一个字段,然后T2在该表中插入了一些新的行.之后,如果T1再次读取同一个条,就会多出几行.

- 数据库事务的隔离性:数据库系统必须具有隔离并发运行各个事务的能力,使他们不会互相影响,避免各种并发问题.
- 一个事务与其他事务隔离的程度称为隔离级别.数据库规定了多种事务隔离级别,不同隔离级别对应不同的干扰程度,隔离级别越高,数据一致性就越好,但并发性就越弱
- 数据库提供的4中隔离级别
  - read uncommitted(读未提交数据) 允许事务读取未被其他事务提交的变更.脏读/不可重复读/幻读的问题都会出现
  - read commit(读已经提交的数据) 只允许事务读取已经被其他事务提交的变更,可以避免脏读,但不可重复度和幻读的问题仍然可能出现
  - repeatable read(可重复读) 确保事务可以多次从一个字段中读取相同的值,在这个事务持续期间,禁止其他事务对这个字段进行更新.可以避免脏读和不可重复读,但幻读的问题仍然存在.
  - serializable(串行化) 确保事务可以从一个表中读取相同的行.在这个事务持续期间,禁止其他事务对该表执行插入,更新和删除操作.所有并发问题都可以避免,但性能十分低下
- oracle支持的2种事务隔离级别:read commited , serializable . oracle默认的事务隔离级别为:read commited
- mysql支持4种事务隔离级别 mysql默认的事务隔离级别为 repeatable read

**测试一下read uncommitted**

```sql
#重启服务可以保证恢复默认的隔离级别吧好像
PS C:\Users\Administrator.YOURTREEDAD> net stop mysql 80
此命令的语法是:
NET STOP
service
PS C:\Users\Administrator.YOURTREEDAD> net start  mysql80
请求的服务已经启动。

请键入 NET HELPMSG 2182 以获得更多的帮助。
PS C:\Users\Administrator.YOURTREEDAD> mysql -u root -p
Enter password: ******

#查看隔离级别
mysql> select @@transaction_isolation ;
+-------------------------+
| @@transaction_isolation |
+-------------------------+
| REPEATABLE-READ         |
+-------------------------+
1 row in set (0.00 sec)

#设置隔离级别为  read uncommitted 读未提交数据 这样会导致脏读/不可重复读/幻读
mysql> set session transaction isolation level read uncommitted ;
Query OK, 0 rows affected (0.00 sec)

mysql> select @@transaction_isolation ;
+-------------------------+
| @@transaction_isolation |
+-------------------------+
| READ-UNCOMMITTED        |
+-------------------------+
1 row in set (0.00 sec)

mysql> set autocommit= 0 ;
Query OK, 0 rows affected (0.00 sec)

mysql> start transaction ;
Query OK, 0 rows affected (0.00 sec)

#看! 还没提交
mysql> update account set username = 'john' where id = 1 ;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql>
```

在另一个界面打开设置隔离级别为 read uncommitted 

就可以看到脏读的数据

![image-20211002112133588](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20211002112133588.png)

假若原来的回滚了,那就离谱了

```sql
mysql> rollback ;
Query OK, 0 rows affected (0.00 sec)
```

![image-20211002112511055](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20211002112511055.png)

所以会出现脏读幻读不可重复读都可能出现在这种隔离级别下

**测试一下 read committed**

```sql
mysql> set session transaction isolation level read committed ;
Query OK, 0 rows affected (0.00 sec)

mysql> set autocommit =0 ;
Query OK, 0 rows affected (0.00 sec)

#还没提交
mysql> update account set username ='john' where id = 1 ;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

```

![image-20211002113519057](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20211002113519057.png)

这边也确实在第二个事务中没有看到还没提交的数据

但是!!! 但是 说明这可以避免脏读,但是不可重复读和幻读 嘿嘿!不行!

![image-20211002113728187](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20211002113728187.png)

**测试一下 repeatable read **

```sql
mysql>  select @@transaction_isolation ;
+-------------------------+
| @@transaction_isolation |
+-------------------------+
| REPEATABLE-READ         |
+-------------------------+
1 row in set (0.00 sec)

mysql> select * from account ;
+----+----------+---------+
| id | username | balance |
+----+----------+---------+
|  1 | john     |     500 |
|  4 | 赵敏     |    1500 |
+----+----------+---------+
2 rows in set (0.01 sec)

mysql> show variables like 'autocommit' ;
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| autocommit    | ON    |
+---------------+-------+
1 row in set, 1 warning (0.01 sec)

mysql> set autocommit = 0 ;
Query OK, 0 rows affected (0.00 sec)

mysql> start transaction  ;
Query OK, 0 rows affected (0.00 sec)

#更新还未提交
mysql> update account set username = '刘备' where id = 1 ;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

![image-20211002151741957](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20211002151741957.png)完全没问题,避免了脏读

```sql
#提交之后在看看
mysql> commit ;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from account ;
+----+----------+---------+
| id | username | balance |
+----+----------+---------+
|  1 | 刘备     |     500 |
|  4 | 赵敏     |    1500 |
+----+----------+---------+
2 rows in set (0.00 sec)
```

![image-20211002151946236](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20211002151946236.png)

下面演示一下为什么这种隔离级别会出现幻读

cmd中开启事务,插入一条数据

![image-20211002152534283](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20211002152534283.png)

powershell中开启事务,查询数据

```sql
mysql> set autocommit =0 ;
Query OK, 0 rows affected (0.00 sec)

mysql> start transaction ;
Query OK, 0 rows affected (0.00 sec)

#暂时没查到
mysql> select * from account ;
+----+----------+---------+
| id | username | balance |
+----+----------+---------+
|  1 | 刘备     |     500 |
|  4 | 赵敏     |    1500 |
+----+----------+---------+
2 rows in set (0.00 sec)
```

cmd中commit了

![image-20211002152659690](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20211002152659690.png)

```sql
#sql中也没有问题 保证数据一致性 所以么有出现不可重复读 不会多出来刚刚插入的那条数据
mysql> select * from account ;
+----+----------+---------+
| id | username | balance |
+----+----------+---------+
|  1 | 刘备     |     500 |
|  4 | 赵敏     |    1500 |
+----+----------+---------+
2 rows in set (0.00 sec)

#但是 ! 但是! 下面出问题了  本来希望在事务的开始的时候,表里有两条数据,我希望把两条数据的username改一下,但是这时候另一个事务中插入了一条 在更新的时候把插入的也更新了username 这样的话就裂开了 出现幻读
mysql> update account set username = 'mmm';
Query OK, 3 rows affected (0.00 sec)
Rows matched: 3  Changed: 3  Warnings: 0

mysql> select * from account ;
+----+----------+---------+
| id | username | balance |
+----+----------+---------+
|  1 | mmm      |     500 |
|  4 | mmm      |    1500 |
|  5 | mmm      |    1000 |
+----+----------+---------+
3 rows in set (0.00 sec)
```

![image-20211002153254274](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20211002153254274.png)

##### 测试一下 serializable

powershell中尝试开启事务 并且更新数据

```sql
mysql> set autocommit = 0 ;
Query OK, 0 rows affected (0.00 sec)

mysql> set session transaction isolation level serializable ;
Query OK, 0 rows affected (0.00 sec)

mysql> select @@transaction_isolation ;
+-------------------------+
| @@transaction_isolation |
+-------------------------+
| SERIALIZABLE            |
+-------------------------+
1 row in set (0.00 sec)

mysql> set autocommit = 0 ;
Query OK, 0 rows affected (0.00 sec)

mysql> start transaction ;
Query OK, 0 rows affected (0.00 sec)

mysql> select *  from account ;
+----+----------+---------+
| id | username | balance |
+----+----------+---------+
|  1 | mmm      |     500 |
|  4 | mmm      |    1500 |
|  5 | mmm      |    1000 |
+----+----------+---------+
3 rows in set (0.00 sec)

mysql> update account set username ='www' ;
```

这时还没有更新,cmd中开启了一个事务尝试往这张表中插入数据

![image-20211002154329103](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20211002154329103.png)

这就会将表锁住,因为上一个事务在使用这张表,为了防止数据库出现幻读的操作,该隔离级别将表锁住了,这样子完全插入不了,做更新的时候就可以保证更新的数据条目和查出来的数据条目是一致的了.

![image-20211002154520024](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20211002154520024.png)

##### 在mysql中设置隔离级别

- 每启动一个mysql程序,就会获得一个单独的数据库连接.每个数据库连接都有一个全局变量@@tx_isolation,表示当前的事务隔离级别
- 查看当前的隔离级别: select @@tx_isolation ; 
- 设置当前mysql连接的隔离级别: set transaction isolation level read committed ; 
- 设置数据库系统的全局的隔离级别: set global transaction isolation level read committed ; 

##### 事务的隔离级别

|                  | 脏读 | 不可重复读 | 幻读 |
| ---------------- | ---- | ---------- | ---- |
| read uncommitted | 会   | 会         | 会   |
| read committed   | 不会 | 会         | 会   |
| repeated read    | 不会 | 不会       | 会   |
| serializable     | 不会 | 不会       | 不会 |

**mysql中默认的是repeated read ;**

**oracle中默认的是read committed** 

查看 select @@transaction_isolation ; 

设置 set session/global transaction isolation level serilizable...

##### delete和truncate的区别

```sql
mysql> show variables like 'autocommit';
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| autocommit    | OFF   |
+---------------+-------+
1 row in set, 1 warning (0.00 sec)

mysql> set autocommit = 0 ;
Query OK, 0 rows affected (0.00 sec)

mysql> start transaction  ;
Query OK, 0 rows affected (0.00 sec)

#删除数据
mysql> delete from account ;
Query OK, 3 rows affected (0.00 sec)

#回滚
mysql> rollback ;
Query OK, 0 rows affected (0.01 sec)

#数据还在
mysql> select * from account ;
+----+----------+---------+
| id | username | balance |
+----+----------+---------+
|  1 | mmm      |     500 |
|  4 | mmm      |    1500 |
|  5 | mmm      |    1000 |
+----+----------+---------+
3 rows in set (0.00 sec)

mysql> set autocommit = 0 ;
Query OK, 0 rows affected (0.00 sec)

mysql> start transaction ;
Query OK, 0 rows affected (0.00 sec)

#删除数据
mysql> truncate account ;
Query OK, 0 rows affected (0.03 sec)

#回滚
mysql> rollback ;
Query OK, 0 rows affected (0.00 sec)

#无法恢复
mysql> select * from account ;
Empty set (0.01 sec)
```

**savepoint的使用**

```sql
mysql> set autocommit = 0 ;
Query OK, 0 rows affected (0.00 sec)

mysql> start transaction ;
Query OK, 0 rows affected (0.00 sec)

mysql> delete from account where id =1 ;
Query OK, 1 row affected (0.00 sec)

mysql> delete from account where id = 2;
Query OK, 1 row affected (0.00 sec)

#设置保存点
mysql> savepoint a ;
Query OK, 0 rows affected (0.00 sec)

mysql> delete from account where id =3 ;
Query OK, 1 row affected (0.00 sec)

#回到保存点
mysql> rollback to a ;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from account ;
+----+----------+---------+
| id | username | balance |
+----+----------+---------+
|  3 | 关羽     |    3000 |
+----+----------+---------+
1 row in set (0.00 sec)

#还可以再回滚
mysql> rollback ;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from account ;
+----+----------+---------+
| id | username | balance |
+----+----------+---------+
|  1 | 刘备     |    1000 |
|  2 | 张飞     |    2000 |
|  3 | 关羽     |    3000 |
+----+----------+---------+
3 rows in set (0.00 sec)
```

##### 视图

虚拟表,和普通表一样使用,通过普通表动态生成的数据

mysql5.1开始提供视图功能.一种虚拟存在的表,行和列的数据来自定义视图的查询中使用的表,并且是在使用视图时动态生成的,只保存了sql逻辑,不保存查询结果

- 应用场景
  - 多个地方用到了同样的查询结果
  - 该查询结果使用的sql语句较为复杂

**创建视图**

语法 create view 视图名 as 查询语句

```sql
mysql> create view info as select e.last_name,d.department_name,j.* from employees e join departments d on e.department_id = d.department_id join jobs j on j.job_id = e.job_id ;
Query OK, 0 rows affected (0.01 sec)

mysql> select * from info where last_name like '%a%';
+------------+-----------------+------------+---------------------------------+------------+------------+
| last_name  | department_name | job_id     | job_title                       | min_salary | max_salary |
+------------+-----------------+------------+---------------------------------+------------+------------+
| Kochhar    | Exe             | AD_VP      | Administration Vice President   |      15000 |      30000 |
| De Haan    | Exe             | AD_VP      | Administration Vice President   |      15000 |      30000 |

#查询各部门的平均工资级别
mysql> select a.department_id , g.grade_level , a.平均工资 from (select e.department_id , avg(salary) 平均工资 from employees e group by  department_id )a join job_grades  g on a.平均工资 between lower_sal and highest_sal ;
+---------------+-------------+--------------+
| department_id | grade_level | 平均工资     |
+---------------+-------------+--------------+
|          NULL | C           |  7000.000000 |
|            10 | B           |  4400.000000 |
|            20 | C           |  9500.000000 |

#如果用视图来做简化一点点
mysql> create view myv2 as select e.department_id , avg(salary) 平均工资 from employees e group by e.department_id ;
Query OK, 0 rows affected (0.01 sec)

mysql> select m.*,j.grade_level from myv2 m join job_grades j on m.平均工资 between j.lower_sal and j.highest_sal ;
+---------------+--------------+-------------+
| department_id | 平均工资     | grade_level |
+---------------+--------------+-------------+
|          NULL |  7000.000000 | C           |
|            10 |  4400.000000 | B           |

#查询平均工资最低的部门信息
mysql> select * from departments d where d.department_id = (select department_id from employees e group by e.department_id order by avg(salary) asc limit 1);
+---------------+-----------------+------------+-------------+
| department_id | department_name | manager_id | location_id |
+---------------+-----------------+------------+-------------+
|            50 | Shi             |        121 |        1500 |
+---------------+-----------------+------------+-------------+

#使用视图
mysql> select * from departments where department_id = (select department_id from myv2 order by 平均工资 limit 1);
+---------------+-----------------+------------+-------------+
| department_id | department_name | manager_id | location_id |
+---------------+-----------------+------------+-------------+
|            50 | Shi             |        121 |        1500 |
+---------------+-----------------+------------+-------------+

#可以使用视图套视图

```

**视图的优点**

- 重用sql语句
- 简化复杂的sql操作,不知道他的查询细节
- 保护数据,提高安全性

**视图的修改**

- 方式一

create or replace view 视图名 as 查询语句 ; 

- 方式二

alter view 视图名 as 查询语句; 

**视图的删除**

drop view 视图名,视图名,...

```sql
mysql> drop view emp_v1,emp_v2,info,myv2 ;
Query OK, 0 rows affected (0.01 sec)
```

**查看视图**

desc 视图名 ; 

查看具体的过程 show create view 视图名  ; 

##### 练习一下

```sql
mysql>  create or replace view emp_v1 as select last_name , salary , email from employees where phone_number like '011%' ;
Query OK, 0 rows affected (0.01 sec)

#创建视图要求查询部门的最高工资高于12000的部门信息
mysql> create or replace view emp_v2 as select d.* from departments d join employees e on e.department_id = d.department_id group by e.department_id having max(salary) >12000 ;
Query OK, 0 rows affected (0.01 sec)

mysql> select * from emp_v2 ;
+---------------+-----------------+------------+-------------+
| department_id | department_name | manager_id | location_id |
+---------------+-----------------+------------+-------------+
|            90 | Exe             |        100 |        1700 |
|            80 | Sal             |        145 |        2500 |
|            20 | Mar             |        201 |        1800 |
+---------------+-----------------+------------+-------------+
```

**视图的更新**

**视图的插入**

```sql
mysql> create or replace view myv1 as select last_name , email from employees;
Query OK, 0 rows affected (0.01 sec)

mysql> select * from myv1 ;
+-------------+----------+
| last_name   | email    |
+-------------+----------+
| K_ing       | SKING    |
| Kochhar     | NKOCHHAR |

#原始表也插入了张飞这条数据了
mysql> insert into myv1 values('张飞', '101@qq.com');
Query OK, 1 row affected (0.01 sec)
```

**视图的更新**

```sql
mysql> update myv1 set last_name = '张无忌' where last_name = '张飞' ;
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0
#都会修改原始表
```

**视图的删除**

```sql
mysql> delete from myv1 where last_name = '张无忌' ;
Query OK, 1 row affected (0.01 sec)
#都会修改原始表
```

**通常情况下不会对视图进行增删改的操作的**

**备注:** 视图的可更新性和视图中查询的定义有关系,以下类型的视图是不能更新的

- 包含以下关键字的sql语句:分组函数/distinct/group by/having/union/union all
- 常量视图
- select中包含子查询
- join
- from一个不能更新的视图
- where子句的子查询引用了from子句中的表

```sql
 #关键字的sql语句的视图不可以被更新
mysql> create or replace view myv2 as select max(salary) m ,department_id from employees group by department_id ;
Query OK, 0 rows affected (0.01 sec)

#想想也是,怎么能简单的更新一下max(salary)呢,聚合函数的值是算出来的
mysql> update myv2 set m =9000 where department_id = 10 ;
ERROR 1288 (HY000): The target table myv2 of the UPDATE is not updatable
```



 ```sql
 #常量视图不能修改
 mysql> create or replace view myv3 as select 'john' name ;
 Query OK, 0 rows affected (0.01 sec)
 
 mysql> select * from myv3 ;
 +------+
 | name |
 +------+
 | john |
 +------+
 1 row in set (0.00 sec)
 
 mysql> update myv3 set name = 'lucy' ;
 ERROR 1288 (HY000): The target table myv3 of the UPDATE is not updatable
 ```



```sql
#select中包含子查询的不能修改视图
mysql> create or replace view myv4 as select (select max(salary) from employees) 最高工资 ;
Query OK, 0 rows affected (0.01 sec)

mysql> select * from myv4 ;
+----------+
| 最高工资 |
+----------+
| 24000.00 |
+----------+
1 row in set (0.01 sec)

mysql> update myv4 set 最高工资 = 10000 ;
ERROR 1288 (HY000): The target table myv4 of the UPDATE is not updatable
```



```sql
#join中不能更新视图
mysql> create or replace view myv5 as select last_name ,department_name from employees e join departments d on e.department_id = d.department_id ;
Query OK, 0 rows affected (0.01 sec)

#可以更新
mysql> update myv5 set last_name = '张飞' where last_name= 'Whalen' ;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

#不能插入 , 可能是因为两个视图中有一个是department_id是主键叭
mysql> insert into myv5 values ('陈真','xxxx') ;
ERROR 1394 (HY000): Can not insert into join view 'myemployees.myv5' without fields list
```



```sql
#由一个不可更新的视图构成的视图不可更新
mysql> create or replace view myv6 as select * from myv4 ;
Query OK, 0 rows affected (0.01 sec)

mysql> select * from myv6 ;
+----------+
| 最高工资 |
+----------+
| 24000.00 |
+----------+
1 row in set (0.01 sec)

mysql> update myv6 set 最高工资 = 20000 ;
ERROR 1288 (HY000): The target table myv6 of the UPDATE is not updatable
```



```sql
#where子句的子查询引用了from子句中的表 相当于自连接
mysql> create or replace view myv7 as select last_name , email , salary from employees where employee_id in(select manager_id from employees where manager_id is not null) ;
Query OK, 0 rows affected (0.01 sec)

mysql> select * from myv7 ;
+-----------+----------+----------+
| last_name | email    | salary   |
+-----------+----------+----------+
| K_ing     | SKING    | 24000.00 |
| De Haan   | LDEHAAN  | 17000.00 |
| Hunold    | AHUNOLD  |  9000.00 |
| Kochhar   | NKOCHHAR | 17000.00 |
| Greenberg | NGREENBE | 12000.00 |
| Raphaely  | DRAPHEAL | 11000.00 |
| Weiss     | MWEISS   |  8000.00 |
| Fripp     | AFRIPP   |  8200.00 |
| Kaufling  | PKAUFLIN |  7900.00 |
| Vollman   | SVOLLMAN |  6500.00 |
| Mourgos   | KMOURGOS |  5800.00 |
| Russell   | JRUSSEL  | 14000.00 |
| Partners  | KPARTNER | 13500.00 |
| Errazuriz | AERRAZUR | 12000.00 |
| Cambrault | GCAMBRAU | 11000.00 |
| Zlotkey   | EZLOTKEY | 10500.00 |
| Hartstein | MHARTSTE | 13000.00 |
| Higgins   | SHIGGINS | 12000.00 |
+-----------+----------+----------+
18 rows in set (0.00 sec)

mysql> update myv7 set salary =10000 where last_name = 'K_ing' ; 
ERROR 1288 (HY000): The target table myv7 of the UPDATE is not updatable
```

##### 视图和表的对比

|      | 创建语法的关键字 | 是否实际占用物理空间 | 使用                        |
| ---- | ---------------- | -------------------- | --------------------------- |
| 视图 | create view      | 只是保存了sql逻辑    | 增删改查,只是一般不能增删改 |
| 表   | create table     | 保存了数据           | 增删改查                    |

##### delete和truncate在事务使用时的区别

- delete可以回滚 truncate不能回滚

##### 练习一下

```sql
#添加约束 创建表 但是这样 列级约束中外键是不起作用的
mysql> create table Book ( bid int primary key , bname varchar(200) not null unique , price float default(10),btypeId int references booktype(id));
Query OK, 0 rows affected (0.03 sec)

#这里发现索引只有 主键和唯一键
mysql> show index from book ;
+-------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| Table | Non_unique | Key_name | Seq_in_index | Column_name | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment | Visible | Expression |
+-------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| book  |          0 | PRIMARY  |            1 | bid         | A         |           0 |     NULL |   NULL |      | BTREE      |         |               | YES     | NULL       |
| book  |          0 | bname    |            1 | bname       | A         |           0 |     NULL |   NULL |      | BTREE      |         |               | YES     | NULL       |
+-------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
2 rows in set (0.01 sec)

#所以要改成这样
mysql> create table Book ( bid int primary key , bname varchar(200) not null unique , price float default(10),btypeId int , foreign key(btypeId) references bookType(id));
Query OK, 0 rows affected (0.03 sec)

mysql> show index from book ;
+-------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| Table | Non_unique | Key_name | Seq_in_index | Column_name | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment | Visible | Expression |
+-------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| book  |          0 | PRIMARY  |            1 | bid         | A         |           0 |     NULL |   NULL |      | BTREE      |         |               | YES     | NULL       |
| book  |          0 | bname    |            1 | bname       | A         |           0 |     NULL |   NULL |      | BTREE      |         |               | YES     | NULL       |
| book  |          1 | btypeId  |            1 | btypeId     | A         |           0 |     NULL |   NULL | YES  | BTREE      |         |               | YES     | NULL       |
+-------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
3 rows in set (0.01 sec)

mysql> create or replace view myvbook as select bname , name from book b join booktype t on b.btypeid = t.id where price >100 ;
Query OK, 0 rows affected (0.01 sec)

mysql> create or replace view myvbook1 as select bname , price from book where price between 90 and 120 ;
Query OK, 0 rows affected (0.01 sec)

mysql> drop view myvbook , myvbook1 ;
Query OK, 0 rows affected (0.01 sec)
```

##### 复习前一天内容

DDL语言

**常见的约束**

NOT NULL 非空,该字段的值必填 

DEFAULT  默认,该字段的值不用手动插入有默认值

CHECK  检查 mysql不支持

PRIMARY KEY  主键 该字段的值不可重复并且非空 unique+not null

FOREIGN KEY 外键 该字段的值引用了另外的表的字段

UNIQUE   唯一 该字段的值不可重复

**主键和唯一的区别**

1. 一个表至多有一个主键 , 但可以有多个唯一键
2. 主键不允许为空 , 唯一可以为空
3. 都具有唯一性,都支持组合键 , 但不推荐

**外键**

1. 用于限制两个表的关系,从表的字段引用了主表的某字段值
2. 要求外键列和主表的被引用列要求类型一致,意义一样,名称无要求
3. 主表的被引用列要求是一个key(一般就是主键)
4. 插入数据,先插入主表 
5. 删除数据,先删除从表

**级联删除**

实际上就是在删除主表里的数据的时候,把从表里相关的带有该数据的行也一并删除

```sql
#级联删除
alter table stuinfo add constraint fk_stu_major foreign key(majorid) references major(id) on delete cascade ; 
```

**级联置空**

实际上就是在删除主表里的数据的时候,把从表里相关的带有该数据的行的对应字段置为空

```sql
#级联置空
alter table stuinfo add constraint fk_stu_major foreign key(majorid) references major(id) on delete set null ;
```

**创建表时添加约束**

```sql
create table 表名(
	字段名 字段类型 not null , 
    字段名 字段类型 primary key , 
    字段名 字段类型 unique , 
    字段名 字段类型 default , 
    constraint 约束名 foreign key(字段名) references 主表(被引用列)
)
```

**注意:	**

|          | 支持类型      | 可以起约束名字      |
| -------- | ------------- | ------------------- |
| 列级约束 | 除了外键      | 不可以              |
| 表级约束 | 除了默认,非空 | 可以,但是对主键无效 |

列级约束可以在一个字段上追加多个,中间用空格隔开,没有顺序要求

**修改表时添加或删除约束**

**非空**

alter table 表名 modify column 字段名 字段类型 not null ;

**删除非空**

alter table 表名 modify column 字段名 字段类型 ;

**默认**

alter table 表名 modify column 字段名 字段类型 default 值 ; 

**删除默认**

alter table 表名 modify column 字段名 字段类型;

**主键**

alter table 表名 add primary key (字段名) ; 

**删除主键** 

alter table 表名 drop primary key ; 

**唯一**

alter table 表名 add unique (字段名) ; 

**删除**

alter table 表名 drop index 索引名 ; 

**外键**

alter table 表名 add foreign key (字段名) references 主表 (被引用列) ; 

**删除外键**

alter table 表名 drop foreign key 约束名 ; 

**自增长列**

特点

1. 不用手动插入值 , 可以自动提供序列值,默认从1开始,步长为1  auto_increament_increment
2. 如果要更改起始值:手动插入值
3. 如果要更改步长:更改系统变量 set auto_increment_increment = 值 ; 
4. 一个表至多有一个自增长列
5. 自增长列只能支持数值型
6. 自增长列必须为一个key

创建表时设置自增长列

 create table 表 

修改表时设置自增长列

create table 表 modify column 字段名 字段类型  约束 auto_increment  ; 

删除自增长列

alter table 表 modify column 字段名 字段类型 约束

TCL语言

**事务**:一条或多条sql语句组成一个执行单位,一组sql句要么都执行要么都不执行

**特点(ACID)**

- 原子性 一个事务是不可再分割的整体,要么都执行要么都不执行
- 一致性 一个事务可以使数据从一个一致状态切换到另一个一致的状态
- 隔离性 一个事务不受其他事务的干扰,多个事务互相隔离的
- 持久性 一个事务一旦提交了,则永久的持久化到本地

**事务的使用步骤**

了解:

- 隐式事务(自动事务) 没有明显的开始和结束,本事就是一条事务可以自动提交,比如insert update delete
- 显式事务 具有明显的开启和结束

使用显式事务

1. 开启事务 set autocommit = 0 
2. start transacton ; 可以省略
3. 编写逻辑sql语句 一条或者多条 注意 不包含create alter drop 只支持insert update delete select
4. 设置回滚点  savepoint 回滚点名 ;  
5. 结束事务 
   1. 提交 commit
   2. 回滚 rollback
   3. 回滚点 rollback to 回滚点名;

##### 并发事务

- 事务的并发问题是如何发生的

多个事务同时操作同一个数据库的相同数据时

- 并发问题有哪些
  - 脏读 一个事务读取了其他事务还没有提交的数据  读到的是其他事务"更新"的数据
  - 不可重复读 一个事务多次读取结果不一样 重复读取可能造成数据不一致的现象
  - 幻读 一个事务读取了其他事务还没有提交的数据 只是读到的是 其他事务"插入"的数据
- 如何解决并发问题
  - 通过设置隔离级别来解决
- 隔离级别                                                    脏读            不可重复读             幻读
  - read uncommitted  读未提交         会                    会                         会
  - read committed  读已提交           不会              会                        会           (oracle默认)    
  - repeatted read  可重复读            不会              不会                         会       (msyql默认)    
  - serializable  串行化                        不会                       不会                  不会

##### 视图

含义 mysql5.1版本出现的新特性 , 本身是一个虚拟表,是通过表数据动态生成的,查看时动态生成

**好处** 

- 简化sql语句
- 封装重用
- 保护了基表的数据,提高了安全性

**创建**

create or replace view 视图名 as select ......

**修改**

create or replace view 视图名 as select .....

alter view 视图名 as select ....

**删除** 

drop view 视图名,视图名...

**查看**

desc 视图名

show create view 视图名 

**使用**

insert delete update select 

**注意:	**视图一般用于查询的,而不是更新的,所以具备以下的视图都不允许更新

- 带有 group by 分组函数 union having 
- where后的子查询用到了from中的表
- 常量视图
- 从不可更新的视图中生成的视图
- join

**视图和表的区别**

- view 和 table
- 视图占用较少物理空间 表占用实际数据
- 视图一般用于查询 表用于增删改查

##### 变量

- 系统变量
  - 全局变量
  - 会话变量
- 自定义变量
  - 用户变量
  - 局部变量

##### 系统变量

说明:变量由系统提供,不是用户定义,属于服务器层面

使用的语法:

1. 查看所有的系统变量 show golbal/session  variables  ;  session是默认的
2. 查看满足条件的部分系统变量 show global/session variables like '%char%' ;
3. 查看指定的某个系统变量的值 select @@global/session.系统变量名字 ; session是默认的
4. 为某个系统变量赋值 
   1.  方式一 set global/session 系统变量名 = 值 ; 
   2. 方式二 set @@global/session.系统变量名 = 值; 

```sql
show global variables ;

mysql> select @@transaction_isolation ;
+-------------------------+
| @@transaction_isolation |
+-------------------------+
| REPEATABLE-READ         |
+-------------------------+
1 row in set (0.00 sec)
```

**注意**

如果是全局级别,则需要加global , 如果是会话级别,则需要加session , 如果不写, 则默认

**全局变量**  

**作用域:服务器每次启动将为所有的全局变量赋初始值,针对所有的会话连接有效,但不能跨重启**

show gloabl variables ; 

**查看部分的全局变量**

show global variables ; show variables like '%char%' ;

**查看指定的全局变量的值**

select @@global.autocommit ; 

**为某个指定的全局变量赋值**

mysql> set @@global.autocommit = 0 ;
Query OK, 0 rows affected (0.00 sec)

**会话变量**

**作用域:仅仅针对于当前会话(连接)有效**

**查看所有的会话变量**

show session variables ; 

show variables ; 

**查看部分的会话变量**

show variables like '%char%' ; 

show session variables like '%char%' ; 

**查看指定的某个会话变量**

select @@transaction_isolation ;

select @@session.transaction_isolation ;

**为某个会话变量赋值**

方式一

mysql> set @@session.transaction_isolation = 'read-committed' ;
Query OK, 0 rows affected (0.00 sec)

方式二

mysql> set session transaction isolation level read uncommitted ;
Query OK, 0 rows affected (0.00 sec)

方式三

set session transaction_isolation = 'serializable' ; 

```sql
mysql> show variables like '%char%' ;
+--------------------------+---------------------------------------------------------+
| Variable_name            | Value                                                   |
+--------------------------+---------------------------------------------------------+
| character_set_client     | gbk                                                     |
| character_set_connection | gbk                                                     |
| character_set_database   | utf8mb4                                                 |
| character_set_filesystem | binary                                                  |
| character_set_results    | gbk                                                     |
| character_set_server     | utf8mb4                                                 |
| character_set_system     | utf8mb3                                                 |
| character_sets_dir       | C:\Program Files\MySQL\MySQL Server 8.0\share\charsets\ |
+--------------------------+---------------------------------------------------------+
8 rows in set, 1 warning (0.00 sec)

mysql> show session variables like '%char%' ;
+--------------------------+---------------------------------------------------------+
| Variable_name            | Value                                                   |
+--------------------------+---------------------------------------------------------+
| character_set_client     | gbk                                                     |
| character_set_connection | gbk                                                     |
| character_set_database   | utf8mb4                                                 |
| character_set_filesystem | binary                                                  |
| character_set_results    | gbk                                                     |
| character_set_server     | utf8mb4                                                 |
| character_set_system     | utf8mb3                                                 |
| character_sets_dir       | C:\Program Files\MySQL\MySQL Server 8.0\share\charsets\ |
+--------------------------+---------------------------------------------------------+
8 rows in set, 1 warning (0.00 sec)

mysql> select @@transaction_isolation ;
+-------------------------+
| @@transaction_isolation |
+-------------------------+
| REPEATABLE-READ         |
+-------------------------+
1 row in set (0.00 sec)

mysql> select @@session.transaction_isolation ;
+---------------------------------+
| @@session.transaction_isolation |
+---------------------------------+
| REPEATABLE-READ                 |
+---------------------------------+
1 row in set (0.00 sec)

mysql> set session transaction isolation level read uncommitted ;
Query OK, 0 rows affected (0.00 sec)

mysql> set @@session.transaction_isolation = 'read-committed' ;
Query OK, 0 rows affected (0.00 sec)

mysql> select @@transaction_isolation ;
+-------------------------+
| @@transaction_isolation |
+-------------------------+
| READ-COMMITTED          |
+-------------------------+
1 row in set (0.00 sec)

mysql> set session transaction_isolation = 'serializable' ;
Query OK, 0 rows affected (0.00 sec)
```

##### 自定义变量

说明:变量是用户自定义的,不是由系统生成的

使用步骤:声明=>赋值=>使用(查看/比较/运算等) 

**用户变量**

**作用域**:针对当前会话(连接)有效,同于会话变量的作用域 , 应用在任何地方,也就是begin end里面或者begin end 外面

**赋值操作符** =或者 :=

**声明并初始化**  set @用户变量名 = 值 | set@用户变量名 :=值 | select @用户变量名:=值 

**赋值**

- 方式一  set @用户变量名 = 值 | set@用户变量名 :=值 | select @用户变量名:=值 
- 方式二  通过 select into    select 字段 into 变量名 from 表

**使用**

select @用户变量名 

```sql
mysql> set @name := 'ljs' ;
Query OK, 0 rows affected (0.00 sec)
#弱类型
mysql> set @name = 1997 ;
Query OK, 0 rows affected (0.00 sec)

mysql> set @count = 1 ;
Query OK, 0 rows affected (0.00 sec)

mysql> use myemployees ;
Database changed

#方式二
mysql> select count(*) into @count from employees ;
Query OK, 1 row affected (0.00 sec)

mysql> select @name ;
+-------+
| @name |
+-------+
|  1997 |
+-------+
1 row in set (0.00 sec)

mysql> select @count ;
+--------+
| @count |
+--------+
|    107 |
+--------+
1 row in set (0.00 sec)
```

##### 局部变量

**作用域**:仅仅在定义它的begin end中有效

应用在begin end 中的第一句话!!!

**声明**

declare 变量名  类型 ; 

declare 变量名 类型 default 值; 

**赋值**

方式一

set 局部变量名 = 值; 

方式二

set 局部变量名 := 值 ; 

方式三

select @局部变量名 := 值 ; 

方式四

select 值 into @局部变量名 from 表 ; 

**使用**

select 局部变量名 ; 

**对比用户变量和局部变量**

|          | 作用域       | 定义和使用的位置               | 语法                                      |
| -------- | ------------ | ------------------------------ | ----------------------------------------- |
| 用户变量 | 当前会话     | 会话中的任何地方               | 需要加上@符号,不用限定类型                |
| 局部变量 | begin end 中 | 只能在begin end中,且为第一句话 | 一般不用加上@符号,除非select,需要限定类型 |

```sql
#使用用户变量
mysql>  set @a := 1 ;
Query OK, 0 rows affected (0.00 sec)

mysql> select b1 into @b from (select 1 b1)b ;
Query OK, 1 row affected (0.00 sec)

mysql> select @b+@a ;
+-------+
| @b+@a |
+-------+
|     2 |
+-------+

#只能在begin end中才行
mysql> declare m int default 1 ;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'declare m int default 1' at line 1
```

##### 存储过程和函数

存储过程和函数:类似与java中的方法

好处:

- 提高代码的重用性
- 简化操作

存储过程

含义:一组预先编译豪的sql语句的集合,理解成批处理语句

好处:

1. 提高了代码的重用性
2. 简化操作
3. 减少了编译次数并减少了和数据库服务器的连接次数,提高了效率

**创建语法**

create procedure 存储过程名(参数列表)

begin

​	存储过程体(一组合法的sql语句)



end

**注意**:

1. 参数列表包含三部分  参数模式  参数名  参数类型

   - IN stuname varchar(20)
   - 参数模式
     - IN  该参数可以作为输入,也就是该参数需要调用方传入值
     - OUT  该参数可以作为输出,也就是该参数可以作为返回值
     - INOUT 该参数既可以作为输入又可以作为输出,也就是该参数既需要传入值,又可以返回值

2. 如果存储过程体仅仅只有一句话 , begin end 可以省略 

   存储过程体中的每条sql语句的结尾要求必须加分号; 

   存储过程的结尾可以使用 DELIMITER重新设置 

   语法:

   DELIMITER 结束标记 

   DELIMITER $ 



**调用语法**

CALL 存储过程名 (实参列表)  结束标记; 

##### 空参列表

```sql
#实现批量插入数据
mysql> show procedure status like 'myp1';
+-------+------+-----------+----------------+---------------------+---------------------+---------------+---------+----------------------+----------------------+--------------------+
| Db    | Name | Type      | Definer        | Modified            | Created             | Security_type | Comment | character_set_client | collation_connection | Database Collation |
+-------+------+-----------+----------------+---------------------+---------------------+---------------+---------+----------------------+----------------------+--------------------+
| girls | myp1 | PROCEDURE | root@localhost | 2021-10-10 10:19:11 | 2021-10-10 10:19:11 | DEFINER       |         | gbk                  | gbk_chinese_ci       | utf8_general_ci    |
+-------+------+-----------+----------------+---------------------+---------------------+---------------+---------+----------------------+----------------------+--------------------+
1 row in set (0.01 sec)

mysql> use girls ;
Database changed

#写错了 就把存储过程删了重来
mysql> drop procedure myp1 ;
Query OK, 0 rows affected (0.01 sec)

mysql> show procedure status like 'myp1' ;
Empty set (0.01 sec)


mysql> delimiter $
mysql> create procedure myp1()
    -> begin
    -> insert into admin(username ,password)
    -> values ('ljs','11'),('jwt','22'),('lje','33'),('fyz','44'),('wzr','55') ;
    -> end $
Query OK, 0 rows affected (0.01 sec)

mysql> show procedure status like 'myp1' $;
+-------+------+-----------+----------------+---------------------+---------------------+---------------+---------+----------------------+----------------------+--------------------+
| Db    | Name | Type      | Definer        | Modified            | Created             | Security_type | Comment | character_set_client | collation_connection | Database Collation |
+-------+------+-----------+----------------+---------------------+---------------------+---------------+---------+----------------------+----------------------+--------------------+
| girls | myp1 | PROCEDURE | root@localhost | 2021-10-10 11:33:35 | 2021-10-10 11:33:35 | DEFINER       |         | gbk                  | gbk_chinese_ci       | utf8_general_ci    |
+-------+------+-----------+----------------+---------------------+---------------------+---------------+---------+----------------------+----------------------+--------------------+
1 row in set (0.01 sec)

#执行存储过程
mysql> CALL myp1() $ ;
Query OK, 5 rows affected (0.00 sec)

mysql> select * from admin $ ;
+----+----------+----------+
| id | username | password |
+----+----------+----------+
|  1 | john     | 8888     |
|  2 | lyt      | 6666     |
|  3 | ljs      | 11       |
|  4 | jwt      | 22       |
|  5 | lje      | 33       |
|  6 | fyz      | 44       |
|  7 | wzr      | 55       |
+----+----------+----------+
7 rows in set (0.00 sec)
```

##### 创建带IN模式参数的存储过程

```sql
#查看女神的男朋友
mysql> DELIMITER $ ;
mysql> create procedure myp2 (IN girlName varchar(20))
    -> begin
    -> select bo.* from boys bo right join beauty b on bo.id = b.boyfriend_id
    -> where b.name = girlName ;
    -> end $ ;
Query OK, 0 rows affected (0.01 sec)

    -> $
ERROR 1065 (42000): Query was empty
mysql> CALL myp2('柳岩');
    -> $
+------+---------+--------+
| id   | boyName | userCP |
+------+---------+--------+
|    2 | 张飞    |     10 |
+------+---------+--------+
1 row in set (0.01 sec)

Query OK, 0 rows affected, 1 warning (0.01 sec)

#传入多个参数,判断用户是否登陆成功  方式一
mysql> DELIMITER $
mysql> create procedure myp3(IN username varchar(20),IN password varchar(20))
    -> begin
    -> select case when count(*) > 0 then '登陆成功' else '未登陆' end 登陆状态 from admin where admin.username =username and admin.password = password ;
    -> end $
Query OK, 0 rows affected (0.01 sec)

mysql> call myp3('john','8888')$;
+----------+
| 登陆状态 |
+----------+
| 登陆成功 |
+----------+
1 row in set (0.00 sec)

mysql> call myp3('john','8887')$;
+----------+
| 登陆状态 |
+----------+
| 未登陆   |
+----------+
1 row in set (0.00 sec)

#方式二 使用局部变量
mysql> DELIMITER $
mysql> create procedure myp4(in username varchar(20) , in password varchar(20))
    -> begin
    -> declare result varchar(20) default '';
    -> select count(*) into result from admin where admin.username = username and admin.password = password ;
    -> select if(result ='0','未登陆','登陆成功');
    -> end $ ;
Query OK, 0 rows affected (0.01 sec)

mysql> CALL myp4('john','8888')$;
+-------------------------------------+
| if(result ='0','未登陆','登陆成功') |
+-------------------------------------+
| 登陆成功                            |
+-------------------------------------+
1 row in set (0.00 sec)

Query OK, 0 rows affected, 2 warnings (0.00 sec)

mysql> CALL myp4('john','88887')$;
+-------------------------------------+
| if(result ='0','未登陆','登陆成功') |
+-------------------------------------+
| 未登陆                              |
+-------------------------------------+
1 row in set (0.00 sec)

Query OK, 0 rows affected (0.01 sec)
```

##### 创建带out模式的存储过程

```sql
#根据女神名,返回对应男神名
mysql> DELIMITER $
mysql> CREATE procedure myp5(in beautyname varchar(20),out boyname varchar(20))
    -> begin
    -> select bo.boyname into boyname from boys bo where bo.id in (select boyfriend_id from beauty where name = beautyname) ;
    -> end $
Query OK, 0 rows affected (0.01 sec)

#不用初始化也是可以的
mysql> set @boyname := '';
    -> call myp5('柳岩',@boyname)$;
Query OK, 0 rows affected (0.00 sec)

mysql> select @boyname ;
    -> $
+----------+
| @boyname |
+----------+
| 张飞     |
+----------+
1 row in set (0.00 sec)

#多个out返回值 , 返回男朋友的名字和魅力值
mysql> DELIMITER $
mysql> create procedure myp6(in girlname char(20) , out boyname char(20) , out soulIndex int)
    -> begin
    -> select bo.boyname , bo.usercp into boyname , soulIndex from boys bo join beauty b on b.boyfriend_id = bo.id where b.name = girlname ;
    -> end $
Query OK, 0 rows affected (0.01 sec)

mysql> call myp6('柳岩',@boyname,@soulIndex)$;
Query OK, 1 row affected, 2 warnings (0.00 sec)

mysql> select @boyname $
+----------+
| @boyname |
+----------+
| 张飞     |
+----------+
1 row in set (0.00 sec)

mysql> select @soulIndex $
+------------+
| @soulIndex |
+------------+
|         10 |
+------------+
1 row in set (0.00 sec)
```

##### 创建带INOUT模式参数的存储过程

```sql
mysql> DELIMITER $
mysql> CREATE procedure myp7 (inout a int , inout b int )
    -> begin
    -> set a = a*2 ;
    -> set b = b*2 ;
    -> end $
Query OK, 0 rows affected (0.01 sec)

mysql> set @a:=1 ;
    -> set @b:=2 ;
    -> CALL myp7(@a,@b)$;
Query OK, 0 rows affected (0.00 sec)

mysql> select @a,@b;
    -> $
+------+------+
| @a   | @b   |
+------+------+
|    2 |    4 |
+------+------+
1 row in set (0.00 sec)
```

**练习一下**

```sql
#传入用户名密码,插入admin表
mysql> DELIMITER $
mysql> create procedure myp8(in username varchar(20),in password varchar(20))
    -> begin
    -> insert into admin(admin.username , admin.password ) values (username,password);
    -> end $
Query OK, 0 rows affected (0.01 sec)

mysql> CALL myp8('wlz','hellouu')$
Query OK, 1 row affected, 2 warnings (0.00 sec)

#查询传入女神编号 , 返回女神名称和女神电话
mysql> DELIMITER $
mysql> create procedure myp9(in id int , out girlname varchar(20) , out phone varchar(11))
    -> begin
    -> select b.name , b.phone into girlname , phone from beauty b where b.id = id ;
    -> end $
Query OK, 0 rows affected (0.01 sec)

mysql> CALL myp9(1,@girlname , @phone)$
Query OK, 1 row affected, 2 warnings (0.00 sec)

mysql> select @girlname , @phone $
+-----------+-------------+
| @girlname | @phone      |
+-----------+-------------+
| 柳岩      | 18209876577 |
+-----------+-------------+
1 row in set (0.00 sec)

#比较两个日期大小 并返回大小关系
mysql> DELIMITER $
mysql> create procedure myp10(in birth1 datetime , in birth2 datetime , out result int )
    -> begin
    -> select if(datediff(birth1,birth2)>0,1,if(datediff(birth1,birth2)<0,-1,0)) into result ;
    -> end $
Query OK, 0 rows affected (0.01 sec)

mysql> CALL myp10('1997-11-21','1998-11-21',@result)$
Query OK, 1 row affected (0.00 sec)

mysql> select @result $
+---------+
| @result |
+---------+
|      -1 |
+---------+
1 row in set (0.00 sec)
```

**删除存储过程**

drop procedure 存储过程名   **一次只能删除一次**

**查看存储过程的信息**

show create proceduce 存储过程名

**修改存储过程**

比较麻烦,通常不这么做

**练习一下**

```sql
#传入日期,转换成xx年xx月xx日并返回
mysql> create procedure myptest1(in mydate datetime , out strDate varchar(50))
    -> begin
    -> select date_format(mydate,'%y年%m月%d日') into strDate ;
    -> end $
Query OK, 0 rows affected (0.01 sec)

mysql> CALL myptest1('1997-11-21',@strDate);
    -> select @strDate $
Query OK, 1 row affected, 1 warning (0.00 sec)

+--------------+
| @strDate     |
+--------------+
| 97年11月21日 |
+--------------+
1 row in set (0.00 sec)

#传入女神名字 输出 女神名字 and 男生名字  最好使用右连接 另外concat和null拼接永远都是null 所以要用ifnull的函数防止出问题
mysql> delimiter $
mysql> create procedure myptest2(inout girlName varchar(50))
    -> select concat(b.name ,' AND ',bo.boyName) into girlName from beauty b join boys bo on b.boyfriend_id = bo.id where b.name = girlName ;
    -> end $
Query OK, 0 rows affected (0.01 sec)

mysql> set @name :='柳岩' ;
    -> CALL MYPTEST2(@name);
    -> select @name $
Query OK, 0 rows affected (0.00 sec)

Query OK, 1 row affected (0.00 sec)

+---------------+
| @name         |
+---------------+
| 柳岩 AND 张飞 |
+---------------+
1 row in set (0.00 sec)


#传入条目数和起始索引,查询beauty表的记录 limit offset,size 是从offset的下一条开始的
mysql> delimiter $
mysql> create procedure myptest3(in size int , in startIndex int)
    -> begin
    -> select * from beauty limit startIndex,size ;
    -> end $
Query OK, 0 rows affected (0.01 sec)

mysql> CALL myptest3(5,3) $
+----+--------+------+---------------------+-------------+--------------+--------------+
| id | name   | sex  | borndate            | phone       | photo        | boyfriend_id |
+----+--------+------+---------------------+-------------+--------------+--------------+
|  5 | 周冬雨 | 女   | 1992-02-03 00:00:00 | 18209179577 | NULL         |            2 |
|  7 | 岳灵珊 | 女   | 1987-12-30 00:00:00 | 18219876577 | NULL         |            2 |
|  9 | 双儿   | 女   | 1993-02-03 00:00:00 | 18209876579 | NULL         |            2 |
| 11 | 夏雪   | 女   | 1993-02-03 00:00:00 | 18209876579 | NULL         |            2 |
| 13 | 唐艺昕 | 女   | 1990-04-23 00:00:00 | 18988888    | NULL         |            2 |
+----+--------+------+---------------------+-------------+--------------+--------------+
5 rows in set (0.00 sec)

Query OK, 0 rows affected (0.02 sec)
```

##### 函数

含义:一组预先编译豪的sql语句的集合,理解成批处理语句

好处:

1. 提高了代码的重用性
2. 简化操作
3. 减少了编译次数并减少了和数据库服务器的连接次数,提高了效率

区别:

存储过程:可以有0个返回,也可以有多个返回,适合做批量插入/批量更新

函数:有且仅有1个返回,适合做处理数据后返回一个结果

**创建语法**

create function 函数名 (参数列表) return 返回类型

begin

​	函数体

end

**注意:**

- 参数列表 包含两部分

  参数名 参数类型

- 函数体:肯定会有return语句,如果没有会报错

  如果return语句没有放在函数体的最后也不报错,但不建议

  return 值;

- 函数体中仅有一句话,则可以省略begin end

- 使用delimeter语句作为设置结束标记

**调用语法**

select 函数名(参数列表)

**无参有返回**

```sql
#返回公司的员工个数
#和存储过程不一样 这里要声明局部变量 最后一句需要return一下
#mysql中要改一下全局变量 这是我们开启了bin-log, 我们就必须指定我们的函数是否是
mysql> set global log_bin_trust_function_creators=1;
    -> $
Query OK, 0 rows affected (0.00 sec)

mysql> delimiter $
mysql> create function myf1() returns int
    -> begin
    -> declare count int default 0 ;
    -> select count(*) into count from employees ;
    -> return count ;
    -> end $
Query OK, 0 rows affected (0.01 sec)

#使用的时候用select关键字
mysql> select myf1()$
+--------+
| myf1() |
+--------+
|    107 |
+--------+
1 row in set (0.00 sec)
```

**有参有返回**

```sql
#根据员工名,返回他的工资
mysql> delimiter $
mysql> create function myf3(departmentname varchar(20)) returns double(10,2)
    -> begin
    -> set @avgsalary := 0 ;
    -> select avg(salary) into @avgsalary from employees group by department_id having department_id in (select department_id from departments where department_name = departmentname );
    -> return @avgsalary ;
    -> end $
Query OK, 0 rows affected, 1 warning (0.01 sec)

mysql> select myf3('Adm');
    -> $
+-------------+
| myf3('Adm') |
+-------------+
|     4400.00 |
+-------------+
1 row in set (0.00 sec)
```

##### 查看函数

show create function myf3;

**删除函数**

drop function myf3 ; 

**存储过程和函数都在information_schema中的routines表中**

![image-20211010170437148](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20211010170437148.png)

**练习一下**

```sql
#传入两个float的值 返回一个和
mysql> delimiter $
mysql> create function test_func1(a float , b float) returns float
    -> begin
    -> declare sum float default 0 ;
    -> set sum = a+b ;
    -> return sum ;
    -> end $
Query OK, 0 rows affected (0.01 sec)

mysql> select test_func1(1,2) $
+-----------------+
| test_func1(1,2) |
+-----------------+
|               3 |
+-----------------+
1 row in set (0.00 sec)

mysql> select test_func1(1.1,-1.1) $
+----------------------+
| test_func1(1.1,-1.1) |
+----------------------+
|                    0 |
+----------------------+
1 row in set (0.00 sec)
```

##### 流程控制结构

顺序结构:程序从上往下依次执行

分支结构:程序从两条或多条路径中选择一条去执行

循环结构:程序在满足一定条件的基础上,重复执行一段代码

##### 分支结构

- if函数

功能:实现简单的双分支

语法:

if(表达式1,表达式2,表达式3)

如果表达式1成立,则if函数返回表达式2的值,否则返回表达式3的值

应用:任何地方

- case结构

情况1:类似于java中的switch语句,一般用于实现等值判断

case 表达式|字段|变量 

 when 要判断的值 then ... 或语句1 ; 

when 要判断的值 then ...  或语句2 ; 

else ...  或语句n ; 

end  case ; 

情况2:类似于java中的多重if语句,一般用于实现区间判断

case 

when 要判断的条件1 then ... 或语句1 ; 

when 要判断的表达式2 then ...  或语句2 ; 

else  ... 或语句n ; 

end case ; 

**特点:**

- 可以作为表达式,嵌套在其他语句中使用,可以放在任何地方,begin end 中或者begin end 的外面
- 可以作为独立的语句去使用,只能放在begin end 中
- 如果when中的值或条件成立,则执行对应的then后面的语句,并且结束case
- 如果都不满足,则执行else中的语句或值
- else可以省略,如果else省略了,并且所有when条件都不满足,则返回null

![image-20211010203810756](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20211010203810756.png)



![image-20211010203829794](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20211010203829794.png)



**案例**

```sql
#90-100 显示A 80-90 显示B 60-80显示C 其余显示D
mysql> create procedure test_case(in score int)
    -> begin
    -> case when score >=90 and score <=100
    -> then select 'A' ;
    -> when score >=80 and score <90
    -> then select 'B' ;
    -> when score >=60 and score <80
    -> then select 'C' ;
    -> else select 'D' ;
    -> end case ;
    -> end $
Query OK, 0 rows affected (0.01 sec)

mysql> call test_case (95) $
+---+
| A |
+---+
| A |
+---+
1 row in set (0.00 sec)

Query OK, 0 rows affected (0.00 sec)
```

##### if结构

功能:实现多重分支

语法: 

if 条件1 then 语句1 **;** 

else if 条件2 then 语句2 **;** 

...

else 语句n **;** 

end if **;** 

应用在begin end 中

**案例**

```sql
#90-100 返回A 80-90 返回B 60-80返回C 其余返回D

#方式一 可以这样直接return
mysql> create function test_if(score int) returns varchar(20)
    -> begin
    -> if score >=90 and score <=100
    -> then return 'A' ;
    -> elseif score >80
    -> then return 'B' ;
    -> elseif score >60
    -> then return 'C' ;
    -> else
    -> return 'D' ;
    -> end if ;
    -> end $
Query OK, 0 rows affected (0.01 sec)

#或者用原始的这样  这里注意 end if 一定要有封号!!!!
mysql> create function test_id1(score int) returns varchar(20)
    -> begin
    -> set @grade :='' ;
    -> if score >=90 and score <100
    -> then set @grade = 'A' ;
    -> elseif score >80
    -> then set @grade = 'B' ;
    -> elseif score >60
    -> then set @grade = 'C' ;
    -> else
    -> set @grade = 'D' ;
    -> end if ;
    -> return @grade ;
    -> end $
Query OK, 0 rows affected (0.01 sec)
```

##### 循环结构

分类:

-  while
- loop
- repeat

**循环控制:**

iterate类似于continue ,结束本次循环,继续下一次

leave 类似于 break , 跳出,结束当前所在的循环

- while

[标签:] while 循环条件 do 

​			循环体

end while [标签]

- loop

[标签:] loop

​	循环体

end loop [标签]

可以用来模拟简单的死循环

- repeat

[标签:] repeat

​		循环体

until 结束循环的条件

end repeat [标签]

**案例**

```sql
#批量插入 根据次数插入到admin中多条记录
mysql> create procedure pro_while1(in insertcount int )
    -> begin
    -> declare i int default 0;
    -> while i<insertcount do
    -> insert into admin(id,username,password) values (null,concat('rose',i),666);
    -> set i = i+1 ;
    -> end while ;
    -> end $
Query OK, 0 rows affected (0.01 sec)

mysql> call pro_while1(3) $
Query OK, 1 row affected (0.00 sec)

mysql> select * from admin ;
    -> $
+----+----------+----------+
| id | username | password |
+----+----------+----------+
|  1 | john     | 8888     |
|  2 | lyt      | 6666     |
|  9 | rose0    | 666      |
| 10 | rose1    | 666      |
| 11 | rose2    | 666      |
+----+----------+----------+
11 rows in set (0.00 sec)

#添加leave语句
#批量插入 , 根据次数插入到admin表中多条记录 , 如果次数>20 就停止  注意安全 if语句没写好 一直在循环插入了300w条数据
mysql> create procedure test_whileleave(in insertcount int )
    -> begin
    -> declare i int default 0 ;
    -> a:while i < insertcount do
    -> if i=20 then leave a ;
    -> end if  ;
    -> insert into admin(username,password) values (concat('xiaohua',i),'0000') ;
    -> set i = i + 1 ;
    -> end while a ;
    -> end #
Query OK, 0 rows affected (0.01 sec)

mysql> call test_whileleave(30) #
Query OK, 1 row affected (0.03 sec)

#添加iterate
##批量插入 , 根据次数插入到admin表中多条记录 ,  并且插入奇数
mysql> create procedure test_iterate(in insertcount int)
    -> begin
    -> declare i int default 1 ;
    -> a:while i <= insertcount do
    -> if mod(i,2) !=1 then set i = i+ 1 ; iterate a ;
    -> else
    -> insert into admin (username, password) values (concat('jishu',i),'1111');
    -> set i = i + 1;
    -> end if ;
    -> end while a ;
    -> end #
Query OK, 0 rows affected (0.01 sec)

mysql> call test_iterate(20) #
Query OK, 1 row affected (0.02 sec)
```

![image-20211010222825964](mysql%E5%AD%A6%E4%B9%A0%E6%96%87%E6%A1%A3.assets/image-20211010222825964.png)

##### 练习一下

```sql
#新建表 然后像该表插入指定个数的 , 随机字符串
mysql> create table if not exists stringcontent (id int primary key auto_increment , content varchar(20));
Query OK, 0 rows affected, 1 warning (0.01 sec)

mysql> create procedure test_randstr_insert(in insertcount int)
    -> begin
    -> declare i int default 0 ;
    -> declare str varchar(26) default 'abcdefghijklmnopqrstuvwxyz';
    -> declare startIndex int default 1 ;
    -> declare len int default 1 ;
    -> while i<insertcount do
    -> set startIndex = floor(rand()*26+1) ;
    -> set len = floor(rand()*(20-startindex+1)+1) ;
    -> insert into stringcontent(content) values (substr(str,startIndex,len));
    -> set i = i + 1;
    -> end while ;
    -> end #
Query OK, 0 rows affected (0.01 sec)

mysql> call test_randstr_insert(10)#
Query OK, 1 row affected (0.02 sec)

mysql> select * from stringcontent #
+----+--------------+
| id | content      |
+----+--------------+
|  1 | klm          |
|  2 | hijklmn      |
|  3 | pqr          |
|  4 | no           |
|  5 | rs           |
|  6 | abcde        |
|  7 | bcdefghijklm |
|  8 |              |
|  9 | f            |
| 10 | lmn          |
+----+--------------+
10 rows in set (0.00 sec)
```

##### 复习一下

分类:

**系统变量**

说明:变量由系统提供的,不用自定义

语法:

1. 查看系统变量
   1. show global|session variables  ;如果没有显式声明,那默认是session
2. 查看指定的系统变量的值
   1. select @@global|session.变量名 ; 
3. 为系统变量赋值
   1. set gloabl|session 变量名 = 值 ; 
   2. set @@global.变量名 = 值 ; 
   3. set @@变量名 = 值; 

-  全局变量
  - 服务器层面上的,必须拥有super权限才能为系统变量赋值,作用域为整个服务器,也就是针对于所有连接(会话)有效,服务器重启后失效(除非修改配置)
- 会话变量
  - 服务器为每一个连接的客户端都提供了系统变量,作用域为当前的连接(会话)

**自定义变量**

说明:

**用户变量**

-  作用域：针对于当前连接(会话)生效
- 位置:begin end 里面, 也可以放在外面
- 使用  

- **声明并赋值**
  - set @变量名 = 值; 
  - set @变量名:= 值; 
  - select @变量名:=值 ; 
- **更新值**
  - set @变量名 = 值; 
  - set @变量名:= 值; 
  - select @变量名:=值 ; 
  - select xx into @变量名 from 表 ; 
- **使用**
  - select @变量名 ; 

**局部变量**

- 作用域:仅仅在定义它的begin end 中有效
- 位置:只能放在begin end 中， 而且只能放在第一句
- create procedure pro1()
- begin
- declare i int default 1 ; 
- ...
- end
- **声明**
  - declare 变量名 类型 default 值; 
- **赋值或更新**
  - set 变量名=值; 
  - set 变量名:= 值; 
  - select @变量名 := 值; 
  - select xx into 变量名 from 表 ; 
- **使用**
  - select 变量名 ; 

**存储过程和函数**

说明:都类似于java中的方法,将一组完成特定功能的逻辑语句包装起来,对外暴露名字

好处:

- 提高重用性
- sql语句简单
- 减少了和数据库服务器连接的次数,提高了效率

**创建**

create procedure 存储过程名 (参数模式 参数名 参数类型)

begin 

存储过程体

end

- 注意:参数模式 in out inout  其中IN可以省略
- 存储过程体中的每一条sql语句都需要分号结尾 

**调用**

CALL 存储过程名(实参列表) 

调用in模式的参数 call sp1('值') ; 

调用out模式的参数 set @name :="" ; call sp1(@name) ; 

调用inout模式的参数 set @name = 值 ; call sp1(@name)  ; select @name ; 

**查看存储过程**

show create procedure 存储过程名 ; 

**删除存储过程**

drop procedure 存储过程名 ; 

**函数**

**创建**

create function 函数名 (参数名 参数类型) returns 返回值类型 

begin 

declare a int default 0  ; 

...

return a ; 

end 

**注意:	**函数体中肯定需要有return语句

**调用**

select 函数名 (实参列表) ; 

##### 查看

show create function 函数名 ; 

**删除**

drop functioon 函数名 ; 

**流程控制结构**

顺序结构 :程序从上往下依次执行 ; 

分支结构:: 程序按条件进行选择执行, 从两条或多条路径中选择一条执行 ; 

循环结构: 程序满足一定条件下,重复执行一组语句

**分支结构**

- if函数
  - 功能:简单实现双分支
  - if(条件, 值1 , 值2 ) 
  - 位置:任何位置
- case 结构
  - 功能:实现多分支
  - case 表达式字段 when 值1 then ... when 值2 then ... else ... end [case];
  - 位置:可以放在任何位置, 如果放在begin end 外面,作为表达式结合着其他语句使用 , 如果放在begin end 里面, 一般作为独立的语句使用
- if结构
  - 功能:实现多分支
  - if 条件1 then ...; elseif 条件2 then ...; else then ... ;  end if ;
  - 位置: 只能放在begin end中

**循环结构**

**注意:只能放在begin end 中**

**特点:都能实现循环结构**

**对比:**

1.  这三种循环都可以省略名称,但如果循环中添加了循环控制语句(leave或iterate)则必须添加名称
2. loop 一般用于实现简单的死循环 while先判断后执行 repeat 先执行后判断,无条件至少执行一次

- while 

  - [标签:] while 循环条件 do 

    循环体

    end while [标签] ; 

- loop

  - [标签:] loop

    循环体 

    end loop [标签]

- repeat

  - [标签:] repeat

    循环体 

    until 结束条件

    end repeat [名称]

**循环控制语句**

leave:类似于 break , 用于跳出所在的循环

iterate:类似于continue , 用于结束本次循环, 继续下一次

**完结撒花**😋😜💕🤣
