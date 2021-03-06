# ArrayList、Vector和LinkList有什么区别

ArrayList、Vector、LinkList类均在java.util包中，均为科伸缩数组，即可以动态改变长度的数组。

## 1.ArrayList
* 基于存储元素的Object[] array来实现的，会在内存中开辟一块连续的空间来存储。
* 由于数据存储是连续的，因此支持序号（下标）来访问元素，索引速度也比较快。
* 但在插入元素时需要移动大量的元素，所以对数据的插入操作执行得比较慢。
* 有一个初始容量的大小，当里面存储的元素超过这个大小时就需要动态地扩充它们的存储空间。
* 为了提高程序的效率，每次扩充容量，不是简单地扩充一个单元，而是一次增加多个单元。ArrayList一次扩充为原来的**1.5倍**。但ArrayList没有提供方法来设置空间扩充的方法。

## 2.Vector
* 基于存储元素的Object[] array来实现的，会在内存中开辟一块连续的空间来存储。
* 由于数据存储是连续的，因此支持序号（下标）来访问元素，索引速度也比较快。
* 但在插入元素时需要移动大量的元素，所以对数据的插入操作执行得比较慢。
* 有一个初始容量的大小，当里面存储的元素超过这个大小时就需要动态地扩充它们的存储空间。
* 为了提高程序的效率，每次扩充容量，不是简单地扩充一个单元，而是一次增加多个单元。ArrayList一次扩充为原来的**2倍**。Vector每次扩充空间的大小是可以设置的。

#### ArrayList与Vector的区别
* 没有一个ArrayList的方法是同步的，而Vector的绝大多数方法（如add、insert、remove、set、equals、hashcode等）都是直接或间接同步的，所以Vector是线程安全的，ArrayList是非线程安全的。

* 正因为Vector提供了线程安全机制，其性能要略逊于ArrayList。

## 3.LinkedList
* 采用双向同步列表来实现。
* 对数据的索引需要从列表头开始遍历，因此随机访问则效率比较低。
* 但是插入元素时不需要移动元素，因此插入效率比较高。
* LinkedList是非线程安全的容器。

## 4.实际场景中容器方案的选择
* ArrayList是一个数组结构，线程不安全，适合于查询和修改，以及尾部的添加和删除。
* LinkedList是一个双向链表结构，线程不安全，适合于中间部位添加和删除。
* Vector 是一个数组结构。但是关键的添加，删除等方法都已经用synchronized修饰，是线程安全的。适合于**多线程场景下**的查询，以及尾部的添加和删除。
