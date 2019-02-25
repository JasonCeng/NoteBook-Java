# JDBC事务

## 目录

## 1.事务概述

### 1.1什么是事务
一件事情有n个组成单元，要么这n个组成单元同时成功，要么这n个组成单元同时失败。

### 1.2mysql的事务

* 默认事务：一条sql语句就是一个事务，默认就开启事务并提交事务。

* 手动事务：

1）显示的开启一个事务：start transaction

2）事务提交：commit 代表从开始事务到事务提交，中间所有sql都认为有效，真正地更新数据库。

3）事务回滚：rollback 代表事务的回滚从开始事务到事务回滚，中间所有sql都认为无效，数据库没有被更新。

## 2.JDBC事务操作

* 默认是自动事务：

执行sql语句：executeUpdate() 每执行一次execcuteUpdate方法代表事务自动提交

* 通过jdbc的API手动事务

  * 开启事务：conn.setAutoCommit(false);

  * 提交事务：conn.commit();

  * 回滚事务：conn.rollback();

  * 注意：控制事务的connection必须是同一个。执行sql的connection与开启事务的connection必须是同一个才能对事务进行控制。

## 3.DBUtils事务操作

### 3.1 QueryRunner

* 有参构造：QueryRunner runner = new QueryRunner(DataSource dataSource);

有参构造将数据源（连接池）作为参数传入QueryRunner，QueryRunner会从连接池中获得一个数据库连接资源操作数据库，所以直接使用无Connection参数的update方法即可操作数据库。

* 无参构造：QueryRunner runner = new QueryRunner();

无参的构造将没有将数据源（连接池）作为参数传入QueryRunner，那么我们在使用QueryRunner对象操作数据库时要使用Connection参数的方法。

## 4.使用ThreadLocal绑定连接资源

## 5.事务的特性和隔离级别

### 5.1事务的特性ACID

1）原子性（Atomicity）

2）一致性（Consistency）一个事务中

3）隔离性（Isolation）

4）持久性（Durability）

### 5.2并发访问问题——由隔离性引起

1）脏读

2）不可重复读

3）幻读/虚读

### 5.3事务的隔离级别

1）read uncommitted

2）read committed

3）repeatable read

4）serializable

* 隔离级别的性能

read uncommitted>read committed>repeatable read>serializable

* 隔离级别的安全性

read uncommitted<read committed<repeatable read<serializable
