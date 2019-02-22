# Java基础知识

## 目录
* <a href="#1Java语言的特点别">1.Java语言的特点</a>
* <a href="#2面向对象与面向过程的区别">2.面向对象与面向过程的区别</a>
* <a href="#3Java与C++的区别">3.Java与C++的区别</a>
* <a href="#4重载与重写的区别">4.重载与重写的区别</a>
* <a href="#5Java面向对象编程三大特性封装-继承-多态">5.Java面向对象编程三大特性：封装 继承 多态</a>
* <a href="#6线程安全与非线程安全">6.线程安全与非线程安全</a>
* <a href="#7接口抽象类">7.接口、抽象类</a>
* <a href="#8finalstaticabstractpublicclass">8.final、static、abstract、public、class</a>
* <a href="#9Java中的赋值与if细节">9.Java中的赋值与if()细节</a>
* <a href="#10webxml">10.web.xml</a>
* <a href="#11常见易混淆api">11.常见易混淆api</a>

## 1.Java语言的特点

在Java中，万物皆对象，你的一切动作必须依赖于某种“类型”实体来实现，面向对象编程实际上就是不断创造性的数据类型，而不可以像过程式编程那样单独调用某个方法（函数），这里的“类型”可以理解为“类”，方法必须包含与某种“类型”，即“类”中。

## 2.面向对象与面向过程的区别



## 3.Java与C++的区别

## 4.重载与重写的区别

* **顺口溜**

  重载：同名不同参，返回值无关。

  重写/覆写：同名同参

* **详解**

  重载：

  1.在同一个类或在一个子类中，方法名相同，参数列表不同的2个或多个方法构成方法的重载

  2.参数列表不同指参数类型，参数个数，参数顺序至少一项不同

  3.方法的返回类型、方法的修饰符、方法抛出的异常可以不同

  重写/覆写：

  1.在子类中可以根据需要对从父类中继承来的方法进行重写，但父类中被final修饰的方法不能被重写

  2.重写的方法和被重写的方法必须具有相同方法名称、参数列表和返回类型

  3.重写方法不能使用比被重写方法更严格的访问权限，但可以更广泛。即子类重写方法的访问权限必须大于等于父类被重写方法的访问权限。

  4.重写方法不能抛出新的异常或者比被重写方法声明的检查异常更广的检查异常。但是可以抛出更少，更有限或不抛出异常。

  5.如果一个方法不能被基础，则不能重写它。最典型的例子为，被覆盖的方法不能为private，否则在其子类中只是新定义了一个方法，并没有对其进行覆盖。

  6.如果想调用父类被覆盖的方法，用super关键字调用。

## 5.Java面向对象编程三大特性：封装 继承 多态

* **继承**

  子类重写父类方法时，方法的访问权限不能小于原访问权限，在接口中，方法的默认权限是public，所以子类重写后只能是public。

  A subclass inherits all the members (fields, methods, and nested classes) from its superclass. Constructors are not members, so they are not inherited by subclasses, but the constructor of the superclass can be invoked from the subclass.   [子类从其父类继承所有成员（字段，方法和嵌套类）。 构造函数不是成员，所以它们不被子类继承，但是可以从子类调用超类的构造函数。]来自Oracle官方文档https://docs.oracle.com/javase/tutorial/java/IandI/subclasses.html


## 6.线程安全与非线程安全

* Vector相当于一个线程安全的List。

* HashMap是非线程安全的，其对应的线程安全类是HashTable。

* ArrayList是非线程安全的，其对应的线程安全类是Vector。

* StringBuffer是线程安全的，其对应的非线程安全类是StringBuilder。

* Properties是线程安全的，因为Properties继承了HashTable，且HashTable是线程安全的。

* **拓展**
  * HashMap、TreeMap未进行同步考虑，是线程不安全的。

  * HashTbale和ConcurrentHashMap都是线程安全的，区别在于他们对加锁的范围不同，HashTable对整张表进行加锁，而ConcurrentHashMap将Hash表分为16桶（segment），每次只对需要的桶进行加锁。

  * Collection类提供了synchronizedXxx()方法，可以将指定的集合包装成线程同步的集合。例如：
    ```java
    List list = Collection.synchronizedList(new ArrayList());
    Set set = Collection.synchronizedSet(new HashSet());
    ```


## 7.接口、抽象类

* **接口**

  接口是一种约束和规范，是一种更加高级的抽象类，因为要给子类继承和使用，所以抽象类的方法必须是公开的，所以接口在实现时，定义的方法修饰符必须是public。因此子类在实现接口重写方法时的修饰符必须是public。接口中默认方法的修饰符为```public abstract```。

  接口中没有变量（既然是约束和规范，怎么能定义一个大家都可以修改的东西呢？），只能是常量。接口中定义常量的默认修饰符为```public static final```。

  **拓展**

  为什么是public static final？

  * 为什么是public：因为接口必然是要被实现的，如果不是public，这个属性就没有意义了。
  * 为什么是static：因为如果不是static，那么忧郁每个类可以继承多个接口，那么就会出现重名的情况。
  * 为什么是final：这是为了体现java的开闭原则，因为接口是一种模板，既然是模板，那就对修改关闭，对扩展开放。



* **抽象类**



* **对比**

  <table>
    <tr>
        <td><b>jdk版本</b></td>
        <td><b>接口</b></td>
        <td><b>抽象类</b></td>
   </tr>
    <tr>
        <td rowspan="7">jdk1.8之前</td>    
        <td >多实现</td>  
        <td>单继承</td>
    </tr>
    <tr>
        <td >变量类型默认且只能为public static final</td>  
        <td>变量类型不限（静态变量+非静态变量）</td>
    </tr>
    <tr>
        <td >函数类型默认且只能为public，只能有public类型的静态成员函数</td>
        <td>函数类型不限（静态函数+非静态函数）</td>
    </tr>
    <tr>
        <td >非静态成员函数没有方法体，静态成员函数有方法体</td>  
        <td>非静态函数包含没有方法体的抽象函数和有方法体的普通函数</td>
    </tr>
    <tr>
        <td >子类必须实现所有接口函数</td>  
        <td>子类可以不覆写父类的抽象方法，但子类也要声明为抽象类；子类可以选择覆写父类的非抽象方法</td>
    </tr>
    <tr>
        <td >可以有main方法；可以new一个接口，需要在方法体中实现所有接口函数</td>  
        <td>可以有main方法；不可以new一个抽象类</td>
    </tr>
    <tr>
        <td >没有构造器</td>  
        <td>可以有构造器</td>
    </tr>
    <tr>
        <td>jdk1.8</td>
        <td colspan="2">接口中可以有default类型的方法，实现类可以选择实现该方法。<br/>意义：默认方法的主要优势是提供一种拓展接口的方法，而不破坏现有代码。另一个优势为该方法是可选的，子类可以根据不同的需求Override或默认实现。</td>
    </tr>
    </table>


## 8.final、static、abstract、public、class、public static final、finally

* **final关键字**

  ①final修饰的类不能被继承；

  ②final定义的方法不能被子类重写，但是可以在本类中被重载；

  ③final定义的属性不能更改；

  ④final定义的方法里，不是必须要用final定义变量。

  ⑤final定义的**成员变量**而言，一旦有了初始值之后就不能被重新赋值，因此不可以在普通方法中对成员变量赋值。可以在代码块（类变量则在静态代码块，实例变量是普通代码块里）里初始化，也可以在构造器中初始化，也可以在声明变量时初始化。

  ⑥final的**局部变量**声明时不必马上初始化，但使用时必须初始化，且只能初始化一次。

  ⑦final定义变量，可用static也可以不用。

* **static关键字**
  * **特点**

    ①被static修饰的成员变量属于类，不属于这个类的某个对象。（也就是说，多个对象在访问或修改static修饰的成员变量时，其中一个对象将static成员变量值进行了修改，其他对象中的static成员变量值跟着改变，即多个对象共享一个static成员变量）

    ```Java
    class Demo {
      public static int num = 100;
    }

    class Test {
      public void main(String[] args) {
        Demo d1 = new Demo();
        Demo d2 = new Demo();
        d1.num = 200;
        System.out.println(d1.num);  // 结果为200
        System.out.println(d2.num);  // 结果为200
      }
    }
    ```

    ②被static修饰的成员变量可以且建议通过类名直接访问。访问成员的格式：

    ```java
    类名.静态成员变量名
    类名.静态成员方法名(参数)

    对象名.静态成员变量名 // 不建议使用该方式，会出现警告
    对象名.静态成员方法名(参数) // 不建议使用该方式，会出现警告
    ```

    ```java
    class Demo {
      //静态成员变量
      public static int num = 100;
      //静态方法
      public static void method() {
        System.out.println("静态方法");
      }
    }

    class Test {
      public void main(String[] args) {
        System.out.println(Demo.num);
        Demo.method();
      }
    }
    ```

  * **注意事项**

    ①静态内容是优先与对象存在，只能访问静态，不能使用this/super.静态修饰的内容存在于静态区。

    ```Java
    class Demo {
      //成员变量
	    public int num = 100;
      //静态方法
	    public static void method(){
        //不能使用this/super。
        System.out.println(this.num);  // 会报错
      }
    }
    ```

    ②同一个类中，静态成员只能访问静态成员

    ```Java
    class Demo {
      //成员变量
	    public int num = 100;
      //静态成员变量
	    public static int count = 200;
      //静态方法
      public static void method(){
        //System.out.println(num); 静态方法中，只能访问静态成员变量或静态成员方法
        System.out.println(count);
      }
    }
    ```

    ③main方法为静态方法仅仅为程序执行入口，它不属于任何一个对象，可以定义在任何类中。

* **abstract关键字**

  ①抽象类，位于继承树的抽象层，不能被实例化。

* **public关键字**

  ①共有类，可以在包外使用，此时源文件名必须和类名相同。

* **class关键字**

  ①只能在包内使用的类

  例子：

  ```java
  class A {
    int  i;
    static  String  s;
    void  method1() {   }
    static  void  method2()  {   }
  }
  //设 a 是 A 类同一个包下的一个实例
  A a = new A();
  ```

  **类中变量：** 除了private权限外，其他权限的变量（没有表示默认default），均可以用“对象.变量名”来调用。对于private变量，即使使用static，也不能用“类.变量名”来调用私有变量。只能通过类中的public get()方法来调用。

  **类中方法：** 除了private权限外，其他权限的方法（没有表示默认default），均可以用“对象.方法名”来调用。private方法可以用java反射机制调用。当然如果用private修饰方法，该方法只在类的内部调用。其中比较著名的就是单例模式中的私有构造方法。

  **static属性：** static方法在编译期就已经生成了，其他方法在运行期生成。非私有的static方法可以用“类.方法名”调用。但是私有的static变量和方法都是不可能被调用的，虽然private static这种写法很少见，但仍然存在，且编译期不会报错。上述代码块中```static void method2() {   }```的权限是默认权限，所以可以用“类.方法名”来调用，即通过“A.method2()”来调用。如果上述代码块中写出```private static void method2() {    }```,那么则不能通过“A.method2()”来调用。

* **public static final**

  * **作用：** 定义静态常量

  * **格式**

    ```Java
    public static final 数据类型 变量名 = 值; //变量名用全部大写，多个单词使用下划线连接
    class Demo {
      public static final String DEMO_NAME = "静态常量demo";
      public static void method() {
        System.out.println("一个静态方法");
      }
    }
    ```

  * **注意事项**

    ①当我们想使用类的静态成员时，不需要创建对象，直接使用类名来访问即可。
    ```Java
    System.out.println(Demo.DEMO_NAME); // 打印：静态常量demo
    Demo.method(); // 调用一个静态方法
    ```

    ② 接口中的每个成员变量都默认使用public staitc final修饰，即均为静态常量，由于接口没有构造方法，所以必须显示赋值。可以直接用接口名访问。

    ```Java
    interface Inter {
      public static final int COUNT = 100;
    }

    //访问接口中的静态常量
    Inter.COUNT
    ```

  * **finally关键字**
  在tray/catch/finally代码块中，如果finally块中有return语句的话，它将覆盖掉函数中其他return语句。

## 9.Java中的赋值与if()细节

Java中，赋值是有返回值的，赋什么值，就返回什么值。比如y=1；if(x=y);返回的是y的值1，即括号里的值为1。

**概要解析：**

Java与C语言在if判断时略有不同。
C中赋值后会与0比较，如果大于0，则返回true；而Java不会与0比较，而是直接把赋值后的结果放入括号中。

**详细解析：**

**C语言中，** 当if语句中的条件为赋值语句时，实际是将赋值后的结果与0比较（左值）
如：if(1)  实际括号内会执行如下判断：1>0，最后返回true到if的括号中执行if判断。

**Java语言中，** 虽然也用了左值，但是不进行与0比较这一步操作，而是直接将左值放到if的括号中执行if判断。但是int类型不能转换为boolean类型，所以会报错：“Type mismatch：cannot convert from int to boolean”

## 10.web.xml
web.xml文件是用来初始化配置信息，web.xml是放置在WEB-INF目录中

**拓展**

/WEB-INF/we.xml是部署描述文件

/WEB-INF/classes用来放置应用程序用到的自定义类(.class)，必须包括包(package)结构。

/WEB-INF/lib用来放置应用程序用到的JAR文件

## 11.常见易混淆api

* **Math**

  * ceil(x)

    大于等于x，并且与x最接近的整数（天花板数，向上取整）

    ceil 方法上有这么一段注释：If the argument value is less than zero but greater than -1.0, then the result is negative zero
如果参数小于0且大于-1.0，结果为 -0

  * floor(x)

    小于等于x，并且与x最接近的整数（地板数，向下取整）

    ceil 和 floor 方法 上都有一句话：If the argument is NaN or an infinity or positive zero or negative zero, then the result is the same as  the argument，意思为：如果参数是 NaN、无穷、正 0、负 0，那么结果与参数相同，
如果是 -0.0，那么其结果是 -0.0

* **线程**

  * run()

    用来执行线程体中具体的内容

  * start()

    用来启动线程对象，使其进入就绪状态

  * sleep()

    用来使线程进入睡眠状态，在此期间线程不消耗CPU资源

  * suspend()

    使线程挂起，如果想恢复线程，要通过resume()方法使其重新启动

## 12.反射

  * **反射的特点：**可以访问访问原类的私有方法，私有成员变量，因此，反射破坏了Java的封装性。

  * **mock对象：**也成为伪对象，在测试中利用mock对象来代替真实对象，方便测试的进行。

  * **java封装性：**指的是将对象的状态信息隐藏在对象内部，不允许外部程序直接访问对象内部信息，通过该类提供的方法实现对内部信息的操作访问。

  * **反射机制：**在运行状态中，对任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法和属性。

## 13.File

* **FileInputStream：**提供了对文件的字节读取

* **FileReader：**提供了对文件的字符读取

* **FileWriter：**提供了对文件的字符写入

* **File：**提供了对文件的基本操作，包括对删除，文件路径等操作

## 14.回收机制

Java的内存回收是自动的，GC在后台运行，不需要用户手动操作。内存回收线程可以释放无用的对象内存。

## 15.this()与super()

* 1.调用super()必须写在子类构造方法的第一行，否则编译不通过。每个子类构造方法的第一条语句，都是隐含地调用super()，如果父类没有这种形式的构造函数，那么在编译的时候就会报错。

* 2.super()和this()类似，区别是，super从子类中调用父类的构造方法，this()在同一类内调用其他方法。

* 3.super()和this()均需放在构造方法内第一行。

* 4.尽管可以用this调用一个构造器，但却不能调用两个。

* 5.this和super不能同时出现在一个构造函数里面，因为this必然会调用其他的构造函数，其他的构造函数必然也会有super语句的存在，这样在同一个构造函数里面就有了相同的语句，就失去了语句的意义，编译器也不会通过。

* 6.this()和super()都指的是对象，所以，均不可以在static环境中使用。包括：static变量、static方法、static语句块。

* 7.从本质上讲，this是一个指向本对象的指针，然而super是一个Java关键字。

## 16.Socket通信编程
* Socket套接字：源IP地址、目标IP地址、源端口号和目标端口号的组合

* 服务器端：SercerSocket提供的实例 ServerSocket server = new ServerSocket(端口号)

* 客户端：Socket提供的实例 Socket soc = new Socket(ip地址，端口号)

## 17.Integer的equals方法
```java
public boolean equals(Onject obj) {
  if(obj instanceof Integer) {
    return value == ((Integer)obj).intValue();
  }
  return false;
}
```
当传去的obj实参是Integer实例且value值也相等的情况下返回真，其他返回假。

## 18.Map的key和value问题

Map接口有两个经典的子接口分别是Hashtable和Hashmap。

Hashtable线程安全，不支持key和value为空，key不能重复，但value可以重复。

Hashmap非线程安全，支持key和value为空，key不能重复，但value可以重复。

## 19.各种数据类型及其默认值

| 数据类型 | short | int | long | float | double | char | boolean | 所有引用数据类型(如String) |
| :------: | :------: | :------: | :------: | :------: | :------: | :------: | :------: | :------: |
| **默认初始值** | 0 | 0 | 0L | 0.0f | 0 | 'u0000' | false | null |

```java
char[] chArr = new char[3];//默认空格
int[] intArr = new int[2];//默认0
String[] strArr = new String[2];//默认null
```

## 19.静态内部类和静态方法

* 1.静态内部类才可以声明静态方法

* 2.静态方法不可以使用非静态变量
