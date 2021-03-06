# Java平台与内存管理

## 1.为什么说Java是平台性语言？
Java可以在一个平台上编写和编译程序，而在其他平台上运行。保证Java具有平台独立性的机制为“中间码”和“Java虚拟机（Java Virtual Machine，JVM）”，Java呗编译后生成的是“中间码”，由JVM来负责把“中间码”翻译成硬件平台能执行的代码。

解释执行过程分为三步进行：代码的装入、代码的校验和代码的执行。装入代码的工作由“类加载器”完成。被装入的代码由字节码校验器进行检查。

Java字节码的执行分为两种方式：即时编译方式与解释执行方式。即时编译方式指的是解释器先将字节码编译成机器码，然后再执行该机器码。解释执行方式指的是解释器通过每次解释并执行一小段代码来完成Java字节码程序的所有操作。**通常采用的是解释执行方式。**

## 2.Java平台与其他语言平台有哪些区别？
Java平台是一个纯软件平台，这个平台可以运行在一些基于硬件的平台（例如Linux、Windows等）之上。Java平台主要包含两个模块：JVM与Java API（Java Application Program Interface，应用程序接口）。

JVM是一个虚构出来的计算机，用来把Java编译生成的中间代码转换为机器可以识别的编码并运行。它有自己完善的硬件架构，例如处理器、堆栈、寄存器等，还具有相应的指令系统，它屏蔽了与具体操作系统平台相关的信息，使得Java程序只需生成在JVM上运行的目标代码（即字节码），就可以在多种平台上不加修改地顺利运行。

每当一个Java程序运行时，都会有一个对应的JVM实例，只有当程序运行结束后，这个JVM才会退出。JVM实例通过调用类的main()方法来启动一个Java程序，而这个main()方法必须是公有的、静态的且返回void的方法，该方法接受一个字符串数组的参数，只有同时满足这些条件才可以作为程序的入口方法。

Java API是Java为了方便开发人员进行开发而设计的，它提供了许多非常有用的接口，这些接口也是用Java语言编写的，并且运行在JVM上。

## 3.JVM加载class文件的原理机制是什么？

## 4.什么是GC？

## 5.Java是否存在内存泄漏问题？

## 6.Java重的堆和栈有什么区别
