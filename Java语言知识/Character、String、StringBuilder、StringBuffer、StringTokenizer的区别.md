# String、StringBuilder、StringBuffer、StringTokenizer的区别

## 1.String
* 不可变类。即String对象一旦被创建，其值就不能被改变。

* 适合在需要被共享的场景中使用。

* 适合保存一个不需要经常被修改的字符串。

  如果用String本保存一个经常被修改的字符串时，在字符串被修改时会比StringBuffer多很多附加操作，同时生产很多无用的对象，由于这些无用的对象会被垃圾回收器来回收，因此会影响程序的性能。在规模小的项目里面这个影响很小，但是在规模大的项目里面，这会对程序的运行效率带来很大的影响。

* 当实例化String时，可以利用构造函数```String s1 = new String("hello world");```的方式对其进行初始化，也可以用赋值```String s = "Hello world";```的方式来初始化。

* String字符串修改实现原理：首先创建一个StringBuffer，其次调用StringBuffer的append()方法，最后调用StringBuffer的toString()方法把结果返回。示例如下：

```java
//修改String字符串：
String s = "Hello";
s += " World";

//等价代码：
Srting s = "Hello";
StringBuffer sb = new StringBuffer(s);
sb.append(" World");
s = sb.toString();

//直接创建StringBuffer对象进行字符串修改：
StringBuffer sb = new StringBuffer("Hello");
sb.append(" World");
String s = sb.toString();
```

我进行了一个实验，看看在多次修改String对象和StringBuilder的过程中，哪一个类更耗时间。

```Java
public class Text {

	public static void main(String[] args) {
		testString();
		System.out.println();
		testStringBuffer();
	}

	public static void testString() {
		String s = "Hello";
		String s1 = "World";
		Runtime rt = Runtime.getRuntime();
		rt.gc();
		long startMem = rt.freeMemory();
		long start = System.currentTimeMillis();
		for (int i = 0; i < 10000; i++) {
			s += s1;
		}
		long end = System.currentTimeMillis();
		long runTime = end - start;
		long remain = rt.freeMemory();
		long occ = startMem - rt.freeMemory();
		System.out.println("testString 耗时:" + runTime + "ms");
		System.out.println("testString 剩余内存:" + remain + "Bytes");
	}

	public static void testStringBuffer() {
		StringBuffer sb = new StringBuffer("Hello");
		String s1 = "World";
		Runtime rt = Runtime.getRuntime();
		rt.gc();
		long startMem = rt.freeMemory();
		long start = System.currentTimeMillis();
		for (int i = 0; i < 10000; i++) {
			sb.append("World");
		}
		long end = System.currentTimeMillis();
		long runTime = end - start;
		long remain = rt.freeMemory();
		long occ = startMem - rt.freeMemory();
		System.out.println("testStringBuffer 耗时:" + runTime + "ms");
		System.out.println("testString 剩余内存:" + remain + "Bytes");
	}

}
```

运行结果如下：

![String与StringBuffer的比较](https://github.com/JasonCeng/NoteBook-Java/blob/master/Java%E8%AF%AD%E8%A8%80%E7%9F%A5%E8%AF%86/img/String%E4%B8%8EStringBuffer%E7%9A%84%E6%AF%94%E8%BE%83.png)

可见在频繁修改字符串对象的情况下，String比StringBuffer更耗时，且会消耗更多的内存空间。这深刻地警醒我们，在频繁地、大量地修改字符串对象的场景下，应尽可能选择StringBuffer或StringBuilder这两个带有字符串缓冲区的类进行使用，避免使用不可修改的String对象。

## 2.StringBuffer

* 可变类。当对象被创建后仍然可以对其值进行修改。

* 适合于一个字符串经常需要被修改的**多线程**场景中。

* 只能使用构造函数```StringBuffer s = new StringBuffer("Hello");```的方式来初始化。

* 调用```append(String str | Char c)```等方法进行字符串修改。

* 因为StringBuffer是线程安全的，所以适用于多线程场景。

* StringBuffer必要时可以对这些方法进行同步，所以任意特定实例上的所有操作就好像是以串行顺序发生的，该顺序与所涉及的每个进程进行的方法调用顺序一致。

## 3.StringBuilder

* 可变类。

* 适合于一个字符串经常需要被修改的**单线程**场景中。

* 调用```append(String str | Char c)、insert(int offset, String str | Char c)```等方法进行字符串修改。

* 因为StringBuilder是非线程安全的，所以只适用于单线程场景，但这也使其执行效率上更优一些。

* 执行效率上，```StringBuilder > StringBuffer > String```

* **小结：**如果要操作的数据量比较小，可以考虑优先使用String类；如果在单线程下操作大量数据应优先使用StringBuilder类；如果在多线程下操作大量数据，应优先考虑StringBuffer类。

## 4.StringTokenizer
分隔字符串的工具类。示例如下：
```Java
import java.util.StringTokenizer;

public class StringTokenizerTest {

	public static void main(String[] args) {
		StringTokenizer st = new StringTokenizer("Welcome to our country");
		while (st.hasMoreTokens()) {
			System.out.println(st.nextToken());
		}
	}
}
```
