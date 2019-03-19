# JVM堆内存设置原理

## 1.原理
JVM堆内存分为2块：**Permanent Space** 和 **Heap Space**

* Permanent 即 持久代（Permanent Generation），主要存放的是**Java类定义信息**，与垃圾收集器要收集的Java对象关系不大。

* Heap = { Old + NEW = {Eden, from, to} }，Old 即 年老代（Old Generation），New 即 年轻代（Young Generation）。年老代和年轻代的划分对**垃圾收集GC**影响比较大。

## 2.持久代（Permanent Space）
用于存放静态类型数据，如 Java Class, Method 等。持久代对垃圾回收没有显著影响。但是有些应用可能动态生成或调用一些Class，例如 Hibernate CGLib 等，在这种时候往往需要设置一个比较大的持久代空间来存放这些运行过程中动态增加的类型。

## 3.年轻代与老年代（Heap Space）
### （1）年轻代
所有新生成的对象首先都是放在年轻代。年轻代的目标就是尽可能快速的收集掉那些生命周期短的对象。年轻代一般分3个区，1个Eden区，2个Survivor区（from 和 to）。

大部分对象在Eden区中生成。当Eden区满时，还存活的对象将被复制到Survivor区（两个中的一个），当一个Survivor区满时，此区的存活对象将被复制到另外一个Survivor区，当另一个Survivor区也满了的时候，从前一个Survivor区复制过来的并且此时还存活的对象，将可能被复制到年老代。

2个Survivor区是对称的，没有先后关系，所以同一个Survivor区中可能同时存在从Eden区复制过来对象，和从另一个Survivor区复制过来的对象；而复制到年老区的只有从另一个Survivor区过来的对象。而且，因为需要交换的原因，Survivor区至少有一个是空的。特殊的情况下，根据程序需要，Survivor区是可以配置为多个的（多于2个），这样可以增加对象在年轻代中的存在时间，减少被放到年老代的可能。

针对年轻代的垃圾回收即 **Young GC**

### （2）年老代
在年轻代中经历了N次（可配置）垃圾回收后仍然存活的对象，就会被复制到年老代中。因此，可以认为年老代中存放的都是一些生命周期较长的对象。

针对年老代的垃圾回收即 **Full GC**

## 4.生成一组对象的内存申请过程
（1）JVM会试图为相关Java对象在年轻代的Eden区中初始化一块内存区域。
（2）当Eden区空间足够时，内存申请结束。否则执行下一步。
（3）JVM试图释放在Eden区中所有不活跃的对象（Young GC）。释放后若Eden空
（4）间仍然不足以放入新对象，JVM则试图将部分Eden区中活跃对象放入Survivor区。
（5）Survivor区被用来作为Eden区及年老代的中间交换区域。当年老代空间足够时，Survivor区中存活了一定次数的对象会被移到年老代。
（6）当年老代空间不够时，JVM会在年老代进行完全的垃圾回收（Full GC）。
（7）Full GC后，若Survivor区及年老代仍然无法存放从Eden区复制过来的对象，则会导致JVM无法在Eden区为新生成的对象申请内存，即出现“Out of Memory”。
