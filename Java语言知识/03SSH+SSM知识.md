# SSH+SSM知识

## 目录

## 1.Hibernate之POJO类对象状态

  * **自由状态（Transient）：**实体在内存中自由存在，与数据库中的记录无关

  * ****

## 2.Hibernate中get()和load()的区别：

  * 1.get()采用立即加载方式，而load()采用延迟加载。get()方法执行的时候，会立即向数据库发出查询语句，而load()方法返回的是一个代理（此代理中只有一个id属性），只有等真正使用该对象属性的时候，才会发出sql语句。

  * 2.如果数据库中没有对应的记录，get()方法返回的是null，而load()方法出现异常ObjectNotFoundException.

## 3.Spring事务传播特性

* PROPAGATION_REQUIRED——支持当前事务，如果当前没有事务，就**新建一个事务**。这是最常见的选择。

* PROPAGATION_SUPPORTS——支持当前事务，如果当前没有事务，就**以非事务方式执行**。

* PROPAGATION_MANDATORY——支持当前事务，如果当前没有事务，就**抛出异常**。

* PROPAGATION_REQUIRES_NEW——新建事务，如果当前存在事务，就**把当前事务挂起**。

* PROPAGATION_NOT_SUPPORTED——以**非事务方式执行操作**，如果当前存在事务，就**把当前事务挂起**。

* PROPAGATION_NEVER——以**非事务方式执行**，如果当前存在事务，则**抛出异常**。
