---
layout: post
title: 学习sql Part 1
categories: [数据库]
description: 学习sql Part 1，总结sql的基础知识，来源《sql必知必会》
keywords: 数据库, sql
---


<h2 align = "center"> 学习sql Part 1 </h2>

<br/>

## 1、了解sql

### 1.1 数据库基础知识

#### 1.1.1 数据库

**数据库(database)**: 以一种有组织的方式存储的数据集合。我们常说的数据库，实际上保存有组织的数据的容器（通常是一个文件或者一组文件）。

**数据库软件**：实际上是数据库管理系统（DBMS），数据库通过DBMS创建和操作。

#### 1.1.2 表

**表**：某种特定类型数据的结构化清单。存储在同一张表内的数据实际上是同一类型的。

**表名**：数据库名 + 表名唯一确定一个表。

**模式(schema)**：描述数据库和表的布局及特征的信息。

#### 1.1.3 列和数据类型

表由列组成，列存储表中的某部分的信息。

**列**：表中的一个字段，所有表都有一个或者多个列组成。

数据库中每个列都有相应的数据类型，数据类型定义了列可以存储哪些数据类型。例如如果列中存储的是数字，则相应的数据类型应该是数值类型。日期、文本、注释、金额等，都有相应的数据类型。

**数据类型**：所允许的数据的类型，每个表列都有相应的数据类型，它限制（或者允许）该列中存储的数据。

数据类型可以帮助正确地分类数据，并在优化磁盘使用方面起到重要的作用。因此，在创建表的时候，要特别关注所用的数据类型。

数据类型及其名称是SQL不兼容的一个主要原因，虽然大多数基本数据类型得到了一致的支持，但许多高级的数据类型却没有。更糟的是，偶尔会有相同的数据类型在不同的DBMS中具有不同的名称。因此我们需要在创建表结构的时候就记住这些差异。

#### 1.1.4 行

表中的数据是按照行来存储的，所保存的每个记录都存储在自己的行内。如果把表想象成网格，网格中垂直的列是表名，水平的行是表行。

**行**：表中的一个记录。有时也称之为record，即记录。

#### 1.1.5 主键

表中每一行都应该有一列或者几列来唯一标示自己。

**主键** ：一列（或者一组列），其值能够唯一标识表中的每一行。

如果没有主键，更新或者删除表中特定的行就会变得非常困难，因为你不能保证你的操作只会涉及到相应的行。

作为主键的条件：

* 任意两行都不具有相同的主键值；

* 每一行都必须有一个主键值（主键列是不允许NULL值的）；

* 主键列的值**不允许修改或者更新**；

* 主键值不能重用（一般不建议重用，如果某行从表中删除，它的主键是不能赋给以后的新行的）。

当然也可以用多个列的组合来作为主键，但是这些列的组合的值必须是唯一的。

### 1.2 什么是sql

SQL： Structured Query Language（—结构化查询语言），SQL是一种专门与数据库沟通的语言。

SQL只提供了很少的词，它可以实现从数据库中简单有效地读写数据。

SQL的优点：

* SQL不是某个特定数据库供应商的专有语言，几乎所有重要的DBMS都支持SQL。

* 简单易学，关键词少；

* 看起来很简单，但是实际上是一种强有力的语言，可以实现非常复杂和高级的数据库操作。

SQL的拓展：许多DBMS厂商通过增加语句或者指令，对SQL进行了拓展。这种拓展的目的是提供执行特定操作的额外功能或者简化方法。

标准的SQL由ANSI标准委员会管理，从而成为ANSI SQL，所有主要的DBMS，即使有自己的拓展，也都支持ANSI SQL。各个实现都有自己的名称，如：PL/SQL， Transact-SQL。

学习SQL最好的方法就是自己动手实践，为此需要一个数据库和用来测试SQL语句的应用系统。


## 2、检索数据

### 2.1 SELECT语句

**关键字**：作为SQL组成部分的保留字， 关键字不能作为表或者列的名字。

为了使用SELECT语句，至少需要给出两条信息：想选择什么，以及从什么地方开始选择。

### 2.2 检索单个列

```sql
  SELECT 列名 FROM 表名;
```
SQL语句以分号结尾，SQL语句不区分大小写，sql语句中的换行会被忽略。

### 2.3 检索多个列

```sql
SELECT 列1, 列2, ... , 列n FROM 表名;
```
不同列之间用半角逗号分隔。

### 2.4 检索所有列

```sql
SELECT * FROM 表名
```

其中星号 * 称为通配符，可以返回所有列，而列的顺序一般是列在表中出现的物理顺序。

一般不用*，因为我们不一定需要把所有的列都取出来，只需要按需取就行。

### 2.5 检索不同的值

```sql
SELECT DISTINCT 列名 FROM 表名;
```

只返回列的不同取值，注意DISTINCT关键词必须在列名前面。

DISTINCT 对后面所有的列起作用。

### 2.6 限制结果

如何让数据库返回某几行的结果。不用数据库使用限制的方法不一样。mysql数据库使用LIMIT关键词。

```sql
SELECT 列名 FROM 表名 LIMIT offs, num;

等价：
SELECT 列名 FROM 表名 LIMIT num OFFSET offs;
```

这样会返回第offs行开始不超过num行的结果。

### 2.7 使用注释

对sql语句进行标注，或者注释部分语句来进行调试

**行内注释**

```SQL
SELECT 列名  --这是sql的行内注释
FROM 表名;

等价：

SELECT 列名  #这是sql的行内注释
FROM 表名;
```

**多行注释**

```SQL
/* SELECT *
FROM TEST*/
SELECT 列名 FROM 表名;
```

## 3、排序检索数据

### 3.1 排序数据

前面的SQL语句返回某个数据库表的某个列，输出结果并没有特定的顺序。

为了明确排序SELECT语句检索出的数据，可以使用ORDER BY子句，它可以取一个或者多个列的名字，据此对输出进行排序。

```SQL
SELECT 列名 FROM 表名 ORDER BY 列名;
```

ORDER BY 子句一般是SQL语句的最后一部分。否则会出现报错。

排序原则：数字和字符串都按照升序。

### 3.2 按照多个列排序

```SQL
SELECT 列名 FROM 表名 ORDER BY 列名1,列名2;
```

要注意多个列排序的结果，实际上是先按前面的列排序，然后对于前面列结果相同的，按照后面的列进行排序。

列名之间用逗号分割。

### 3.3 按照列的位置排序

ORDER BY 子句支持按照相对位置来进行排序。

```SQL
SELECT 列名1, 列名2 FROM 表名 ORDER BY 位置1,位置2;

如：
SELECT * FROM ORDERS ORDER BY 1,2;
```
这里的位置就是前面select的列号，从1开始。

后面的位置不能超过前面的列数。

### 3.4 指定排序方向

SQL排序结果默认是升序的，如果要降序，需要用到DESC关键字。

```SQL
SELECT 列名 FROM 表名 ORDER BY 列名 DESC;
```

DESC只应用到直接位于其前面的列名。


## 4、过滤数据

### 4.1 使用WHERE语句

只检索需要的数据需要指定**搜索条件**，搜索条件也称为**过滤条件**。

过滤条件可以使用WHERE语句来实现。

```SQL
SELECT 列名 FROM 表名 WHERE 列名 = value;
```

只返回列等于value的数据。

WHERE 语句和 ORDER BY语句一起使用的时候，WHERE语句放在ORDER BY语句前面。

### 4.2 WHERE子句的操作符

|符号|说明|
|--|--|
|=|等于|
|<>|不等于|
|!=|不等于|
|<|小于|
|>|大于|
|<=|小于等于|
|>=|大于等于|
|BETWEEN|在指定两个值之间|
|IS NULL|为NULL的值|

#### 4.2.1 检查单个值

可以使用WHERE 列名 = value
等操作，根据需要选择操作符。

#### 4.2.2 不匹配检查

使用!=或者<>

注意value是字符串时，需要使用单引号。

#### 4.2.3 范围值检查

要检查某个范围的值，可以用BETWEEN操作符。其后需要需要连两个值。

```SQL
SELECT 列名 FROM 表名 WHERE 列名 BETWEEN v1 AND v2;
```

between指包含v1和v2的二者之间的所有值。

#### 4.2.4 空值检查

NULL 表示不包含值

```SQL
SELECT 列名 FROM 表名 WHERE 列名 IS NULL;
```

不能直接返回非NULL的匹配。（需要使用NOT）

## 5、高级过滤

如何组合WHERE子句以创建功能更强的搜索条件。

### 5.1 组合WHERE子句

可以使用WHERE子句中的子句关键词来连接，他们称为逻辑操作符。

#### 5.1.1 AND操作符

```SQL
SELECT 列名 FROM 表名 WHERE 条件1 AND 条件2;
```

#### 5.1.2 OR操作符

```SQL
SELECT 列名 FROM 表名 WHERE 条件1 OR 条件2;
```

#### 5.1.3 括号、AND、OR的组合

通过三者的组合实现复杂的过滤。

### 5.2 IN操作符

IN操作符用来限定条件范围，范围内的所有条件都可以进行匹配。IN 取一组由逗号分隔、括在圆括号里面的合法值。

```SQL
SELECT 列名 FROM 表名 WHERE 列名 IN (V1, V2);
```

IN的功能，可以通过OR实现，但是IN具有更多优点：

* IN在选项很多的时候，更简洁直观；
* IN 操作符一般比一组OR操作执行的更快；
* IN 最大的优点就是可以包含其他的SELECT语句，能够更加动态地简历WHERE子句。

### 5.3 NOT操作符

WHERE语句中的NOT操作符只有一个功能，即否定其后所跟的任何条件。

```SQL
SELECT 列名 FROM 表名 WHERE NOT 条件1;
```

## 6、用通配符进行过滤

### 6.1 LIKE通配符

**通配符**：用来匹配值的一部分的特殊字符

**搜索模式**：由字面值、通配符或者两者组合构成的搜索条件

为了在搜索子句中使用通配符，必须使用LIKE操作符。LIKE指示DBMS，后面的搜索模式利用通配符匹配而不是简单的相等匹配。

通配符只能用于搜索文本字段（字符串），非文本数据类型字段不能使用通配符搜索。

#### 6.1.1 百分号(%)通配符

%表示任意字符出现任意次数。

例如匹配HAHA：

```sql
--HAHA出现在开头
SELECT * FROM T WHERE a like 'HAHA%'
--HAHA出现在任意位置
SELECT * FROM T WHERE a like '%HAHA%'
--HAHA出现在尾部
SELECT * FROM T WHERE a like '%HAHA'
```

注意%不能匹配NULL

#### 6.1.2 下划线(_)

用法与%类似，只是它每次只匹配一个字符，一个不多一个不少。%可以匹配0到任意个字符。

#### 6.1.3 更复杂的情况

可以使用正则表达式
