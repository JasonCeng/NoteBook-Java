# SSH+SSM知识

## 目录

## 1.Hibernate之POJO类对象状态

  * **自由状态（Transient）：**实体在内存中自由存在，与数据库中的记录无关

  * ****

## 2.Hibernate中get()和load()的区别：

  * 1.get()采用立即加载方式，而load()采用延迟加载。get()方法执行的时候，会立即向数据库发出查询语句，而load()方法返回的是一个代理（此代理中只有一个id属性），只有等真正使用该对象属性的时候，才会发出sql语句。

  * 2.如果数据库中没有对应的记录，get()方法返回的是null，而load()方法出现异常ObjectNotFoundException.
