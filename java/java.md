## 世界上有10种人，认识和不认识二进制的

1.整数类型  byte  1字节

​		short  2字节

​		int   4字节    default

​		long  8字节（带L）

当没超出int范围时long可以不加L

2.浮点型  float 4字节  精确到7位数字（后面带f）

​		double  8字节  精确到16位   default

char  2字节   boolean  4字节



3.自动类型提升：当容量小的数据类型向容量大的数据类型变量做运算时，结果自动提升为容量大的数据类型

byte、char、short---->  int  ---->  long  ---->  float  ---->  double

当byte、char、short三种类型的变量运算时，结果为int类型

4.强制类型转换，需要使用强转符，小心精度的丢失。

5.二进制（计算机组成原理   原反补码）



## 运算符

##### 算数运算  ：

i++：先运算，然后再自增1

++i：先自增1，然后再运算

```java
int a1 = 10;
int b1= a1++；   //a1=11,b1=10

int a2 = 10;
int b2 = ++a2;   //a2=11,b2=11
```

##### 逻辑运算：

&-逻辑与    &&-短路与  |-逻辑或   ||-短路或  !-逻辑非   ^-异或

![3-1](C:\Users\cb\Desktop\note\java\imgs\3-1.png)

&与&&运算结果相同 ，当符号左边为false时&&就不再去判断后面的内容

移位运算速度比乘除快  2*8-->  2<<3    8<<1       

三元运算符  int max = (m > n) ? m : n;    三元运算符比if-else运算效率高并且简洁

运算符的优先级（暂时不用考虑）



## 权限修饰符

![](C:\Users\cb\Desktop\note\java\imgs\修饰符.png)

javaBean是一种java语言写成的可重用组件，满足以下条件：

类是公共的，有一个无参的公共构造器，有属性且有对应的get和set方法

子类继承没有实现的方法使用this或者super一样

## 面向对象

封装  要给属性加入额外的限制条件，只能通过方法添加。并且需要避免用户再次适用对象.属性对属性进行赋值

继承（单继承） extends

多态：父类引用指向子类的对象  （只适用于方法，不适用于属性）

在编译期调用父类中声明的方法，但在运行期执行的是子类中重写的父类方法

## ==与equals

==如果比较的是基本数据类型，比较两个变量保存的数据是否相等；如果比较的是引用数据类型，则比较两个变量的地址值是否相同

equals（）方法  只能用于引用类型中  String、Data、File、包装类等都重写了Object类中的queals方法重写了，比较的是内容

Object中的==与equals方法的作用相同，都是比较地址值是否相同

## 自动装箱与自动拆箱

自动装箱：基本数据类型------>包装类

```java
int num = 10;
Integer in = num;
```

自动拆箱：包装类------>基本数据类型

```java
Integer in = 1；
int num = in;
```

## Static

静态变量随着类的加载而加载，通过“类.静态变量”的方式调用，静态变量在内存中只存在一份

静态方法中只能调用静态的方法或属性

在静态的方法中不能使用this和super关键字

静态代码块：

	>内部可以有输出语句
	
	>随着类的加载而执行
	
	>静态代码块的执行优先于非静态代码块的执行



非静态代码块：

	>内部可以有输出语句
	
	>随着对象的创建而执行
	
	>每创建一个对象就执行一次静态代码块
	
	>可以在创建对象时，对对象的属性进行初始化

## final修饰符

1.可以用于修饰类、方法和变量

2.用来修饰一个类：此类不能被其他类继承，比如System，String，StringBuffer

3.用于修饰一个方法：次方法不能被重写

4.修饰变量：此时的变量就相当于一个常量----可以显示初始化，在代码块中初始化，构造器中初始化

static final全局常量

## Abstract抽象

java允许类设计者指定：超类声明一个方法但不提供实现，该方法的实现由子类提供。这样的方法称为抽象方法。有一个或者多个抽象方法的类称为抽象类。

抽象类：

1.不能实例化   

2.有构造器便于子类实例化时调用

抽象方法：

1.只有方法的声明，没有方法体

2.包含抽象方法的类一定是抽象类

3.如果子类重写了父类中的所有抽象方法后，此类可以被实例化（即类前不用加abstract）

abstract的使用注意点：

1.不能用来修饰属性、构造器等结构

2.不能用来修饰私有方法、静态方法、final的方法、final的类

## 接口interface

java中：接口和类是并列的两个结构

jdk7及以前，只能定义全局变量和抽象方法

全局常量：public static final       抽象方法：public abstract

jdk8除了全局变量和抽象方法外，还可以定义

静态方法：可以通过接口直接调用该方法

默认方法：可以通过实现类的对象调用，如果实现类重写了默认方法则调用的是重写以后的方法

接口中不能定义构造器，意味着接口不能实例化

## 异常

编译时异常（checked）   编译器会提示

​	|----IOException

​		|----FileNotFouncException

​	|----ClassNotFoundException

运行时异常（unchecked）

​	|----NullPointerException

​	|----ArrayIndexOutOfBoundsException

​	|----ClassCastException  （类型强转异常）

​	|----NumberFormatException   （数值类型转换异常）

​	|----InputMismatchException   （输入不匹配，Scanner）

​	|----ArithmaticException    （算数异常，除数为0）

异常处理方式：

1.try-catch-finally  处理了编译时异常扔可能存在运行时异常

2.throws   只是把异常抛给了方法的调用者，并没有真正的将异常处理掉

## 多线程

程序：是为完成特定任务、用某种语言编写的一组指令的集合。即指一段静态的代码，静态对象。

进程：是程序的一次执行过程，或是正在运行的一个程序。是一个动态执行的过程，有它自身的产生、存在和消亡的过程。-------声明周期

线程：一个程序内部的一条执行路径

并行：多个CPU执行多个任务。如：多个人同时做不同的事情

并发：一个CPU同时执行多个任务。如：秒杀，多个人同时做同一件事

​		多线程的优点：

1.提高应用程序的相应。对图形化界面更有意义，可增强用户体验。

2.提高计算机系统CPU的利用率。

3.改善程序结构。将既长又复杂的进程分为多个线程，独立运行，利于理解和修改。	

##### 继承Thread

extends Thread    

​		常用方法：

start():启动当前线程；调用当前线程的run();

currentThread():静态方法，返回当前代码的线程;

yield():释放当前cpu的执行权

join():在线程a中调用线程b的join(),此时线程a就进入阻塞状态，直到线程b完全执行完以后，线程a才结束阻塞状态

stop():强制线程生命期结束，不推荐使用

sleep(long millitime):让当前线程“睡眠”指定的毫秒，在指定的时间内，当前线程是阻塞状态

​		线程的优先级：

1.MAX_PRIORITY:10     MIN_PRIORITY:1    NORM_PRIORITY:5--->默认优先级

2.如何获取和设置当前线程的优先级：

​	getPriority():获取线程的优先级

​	serPriority(int p):设置线程的优先级

​	说明：高优先级的线程要抢占低优先级线程cpu的执行权。但只是从概率上讲，高优先级的线程高概率的被执行。并不意味着只有当高优先级的线程执行完以后，低优先级的线程才执行。

给线程命名：

```java
//第一种命名方法
MyThread.setName();
//第二种通过构造器命名
public MyThread(String name) {
  super(name);
}

//卖票
private static int ticket = 100;  //加静态
```

##### 实现Runnable

没有getName方法

```java
Thread t1 = new Thread(new Runnable());
t1.start();   //调用了Runnable类型的target的run()
t1.setName("线程1");

//卖票
private int ticket = 100;  //不需要静态
Window w = new Window();   //Window相当于这三个线程的共享数据
Thread t1 = new Thread(w);
Thread t2 = new Thread(w);
Thread t3 = new Thread(w);
```

##### 两种创建方式的比较

开发中：优先选择Runnable接口继承的方式

原因：1.实现的方式没有类的单继承性的局限性

​	    2.实现的方式更适合来处理多个线程有共享数据的情况。

联系：public class Thread implements Runnable

相同点：两种方式都需要重写run（），将线程中要执行的逻辑声明在run（）方法中

![线程状态](C:\Users\cb\Desktop\note\java\imgs\线程状态.png)

##### 线程的安全问题

线程的同步解决了线程的安全问题----好处

操作同步代码时，只能有一个线程参与，其他线程等待。相当于是一个单线程的过程，效率低.

1.同步代码块：

```java
synchronized(同步监视器){
  //需要被同步的代码
}   
//操作共享数据的代码，即为需要被同步的代码
//共享数据：多个线程共同操作的变量    比如ticket就是共享数据
//同步监视器：俗称 锁。任何一个类的对象都可以充当锁
	要求：多个线程必须同用一把锁
     在实现Runnable接口创建多线程的方式中，我们可以考虑使用this充当同步监视器
```

2.同步方法：

​	如果操作共享数据的代码完整的声明在一个方法中，我们不妨将此方法声明同步的。

同步方法仍然涉及到同步监视器，只是不需要我们显式的声明

非静态的同步方法，同步监视器是：this

静态的同步方法，同步监视器是：当前类本身

3.使用lock锁：

```java
private ReentrantLock lock = new ReentrantLock();
在方法里
  try{
    lock.lock();
  }catch(){}finally{lock.unlock();}
```

面试题：synchronized与lock的异同

相同：二者都可以解决线程的安全问题

不同：synchronized机制在执行完相应的同步代码以后，自动的释放同步监视器

​	   lock需要手动的启动同步（lock（）），同时结束同步也需要手动的实现（unlock（））

面试题：sleep（）和wait（）的异同

相同点：一旦执行方法，都可以使得当前的线程进入阻塞状态。

不同点：Thread类中声明sleep（），Object类中声明wait（）

​		sleep（）可以在任何需要的场景下调用。wait（）必须使用在同步代码或同步方法中

​		如果两个方法都使用在同步代码块或同步方法中，sleep（）不会释放锁，wait（）会释放锁

##### 实现Callable接口创建线程

重写的call（）方法

![Callable](C:\Users\cb\Desktop\note\java\imgs\Callable.png)

##### 线程池

提高响应速度，降低资源消耗，便于线程管理![线程池](C:\Users\cb\Desktop\note\java\imgs\线程池.png)

## String类

面试题：String s = new String("abc")；方式创建对象，在内存中创建了几个对象？

​	两个：一个是堆空间中的new结构，另一个是char[]对应的常量池中的数据："abc"

##### 字符串的拼接

![字符串的拼接](C:\Users\cb\Desktop\note\java\imgs\字符串的拼接.png)

注意：final修饰的也是常量

##### String与基本数据类型的转换

字符串---->基本数据类型     Integer.parseInt（String s）

基本数据类型---->字符串     String.valueOf（int n）

##### String与char[]之间的转换

String---->char[]:调用String的toCharArray()

char[]---->String:调用String的构造器        String str = new String(arr);  

##### String与byte[]之间的转换

String---->byte[]:调用String的getBytes()

byte[]---->String:调用String的构造器    默认字符集UTF-8

##### Sting、StringBuffer和StringBuilder的异同

String:不可变字符序列；底层使用char[]存储

StringBuffer:可变字符序列；线程安全的（方法上加synchronized），效率低；底层使用char[]存储

StringBuilder:可变的字符序列；jdk5.0新增；线程不安全，效率高；底层使用char[]存储

## 日期时间API

##### System类中的currentTimeMillis()

```java
long time = System.currentTimeMillis();
//返回当前时间与1970年1月1日0时0分0秒之间以毫秒为单位的时间差   称为时间戳
```

##### Date类

Java.util.Date类    ------  java.sql.Date对应数据库中的日期类型的变量

```java
//构造器一：Date（）：创建一个对应当前时间的Date对象
Date date1 = new Date();
System.out.println(date1.toString()); //Thu Jul 18 11:34:00 GMT+08:00 2019
System.out.println(date1.getTime());  //1563420840626
//构造器二：创建指定毫秒数的Date对象
Date date2 = new Date(1563420840626L);
System.out.println(date2.toString());
```

##### java.text.SimpleDateFormat类

```java
SimpleDateFormat sdf = new SimpleDateFormat();
//日期----->字符串
Date date = new Date();   
String format = sdf.format(date);
System.out.println(format);  //2019/7/18 上午11:46(默认格式)

SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss");
Date parse = sdf.parse("2019-07-18 11:48:29");
```

##### java.util.Calendar类（抽象类）

```java
//实例化：方式一：创建其子类(GregorianCalendar)的对象
//方式二：调用其静态方法
Calendar calendar = Calendar.getInstance();
```

![日历类](C:\Users\cb\Desktop\note\java\imgs\日历类.png)

##### Java8中新增的Time类

```java
//now(): 获取当前的日期、时间、日期+时间
LocalDate localDate = LocalDate.now();
LocalTime localTime = LocalTime.now();
LocalDateTime localDateTime = LocalDateTime.now();

System.out.println(localDate);     //2019-07-18
System.out.println(localTime);     //12:06:08.241461400
System.out.println(localDateTime); //2019-07-18T12:06:08.241461400

//of():设置指定的年月日时分秒，没有偏移量
        LocalDateTime of = LocalDateTime.of(2020, 10, 6, 13, 43, 43);
        System.out.println(of);
```

##### Instant

![Instant](C:\Users\cb\Desktop\note\java\imgs\Instant.png)

##### DateTimeFormatter  类似于SimpleDateFormat



## 比较器

自然排序：java.lang.Comparable

定制排序：java.util.Comparator

##### Comparable接口

1.像String、包装类等实现了Comparable接口，重写了compareTo()方法，给出了两个对象大小的比较方式

2.像String、包装类重写CompareTo()方法以后，进行了从小到大的排列

3.重写CompareTo（obj）的规则：

​	如果当前对象this大于形参obj,则返回正整数；

​	如果当前对象this小于形参obj,则返回负整数；

​	如果当前对象this等于形参obj,则返回零；

4.对于自定义类来说，如果需要排序，我们可以让自定义类实现Comparable接口，重写CompareTo(obj)，在CompareTo（obj）方法中指名如何排序

```java
public int compareTo(object o) {
  if (o instanceof Goods) {
    Goods goods = (Goods)o;
    if(this.price > goods.price) {
      return 1;
    } else if (this.pricce < goods.price) {
      return -1;
    } else {
      return -this.name.compareTo(goods.name);
    }
  }
}
```

##### Comparator

Comparable接口的方式一旦一定，保证Comparable接口实现类的对象在任何都可以比较大小

Comparator接口属于临时性的比较

## 枚举类

类中的对象的个数是确定的，有限个

当需要定义一组常量时，强烈建议使用枚举类

## 注解

jdk8中的新特性：可重复注解，类型注解

```java
@MyAnnotation("abc")
@MyAnnotation("111")
public void tt(){}

class F<@MyAnnotation T>{}
```

## 集合

java集合可以分为Collection和Map两种体系

Collection接口：单列数据，定义了存取一组对象的方法的集合

​	List:元素有序、可重复的集合    

​		ArrayList  LinkedList  Vector

​	Set:元素无序、不可重复的集合

​		HashSet  LinkedHashSet  TreeSet

Map接口：双列数据，保存具有映射关系"key-value对"的集合
​	HashMap  LinkedHashMap  TreeMap  Hashtable  Properties

##### Iterator

Iterator对象称为迭代器，主要用于遍历Collection集合中的元素

Collection接口继承了java.lang.Iterable接口，该接口有一个iterator()方法，所有实现了Collection接口的集合类都有一个iterator()方法。

```java
Collection coll = new ArrayList();
Iterator it = coll.iterator();
while(it.hasNext()){
  System.out.println(it.next());
}
```

##### foreach

增强for循环

```java
//for(集合元素的类型 局部变量 ：集合对象)
//内部仍然使用了迭代器
for(Object obj : coll) {
  
}
```

##### ArrayList、LinkedList、Vector三者的异同

同：三个类都是实现了List接口，存储数据的特点相同：存储有序的、可重复的数据

不同：ArrayList：作为List接口的主要实现类；线程不安全的，效率高；底层使用Object[] elementData存储

LinkedList：对于频繁的插入、删除操作，使用此类效率比ArrayList高；底层使用双向链表存储

Vector：作为List接口的古老实现类；线程安全的，效率低；底层使用Object[] elementData存储

##### ArrayList

ArrayList  list = new ArryaList();//底层创建了长度是10的Object[] 数组 elementData

list.add(11)//如果此次的添加导致底层elementData数组容量不够，则扩容。

默认情况下，扩容为原来容量的1.5倍，同时需要将原有数组的数据复制到新数组中

jdk1.8的优化

​	list.add(123);//第一次调用add()时，底层才创建了长度为10的数组

##### LinkedList

```java
LinkedList list = new LinkedList();  内部声明了Node类型的first和last属性，默认值为null
```

##### vector

jdk7和jdk8中通过Vector()构造器创建对象时，底层都创建了长度为10的数组，扩容每次扩大为原来的2倍

##### HashSet

![HashSet](C:\Users\cb\Desktop\note\java\imgs\HashSet.png)

##### hashCode()和equals()

1.set接口中没有额外定义新的方法

2.要求：向Set中添加的数据，其所在的类一定要重写hashCode()和equals()

   要求：重写的hashCode()和equals()尽可能保持一致性：相等的对象必须具有相等的散列码

##### HashMap

![HashMap](C:\Users\cb\Desktop\note\java\imgs\HashMap.png)

```java
//遍历所有的key集：keySet()
Set set = map.keySet();
Iteratot it = set.iterator();
while(iterator.hasNext()){
  System.out.println(it.next());
}

//遍历所有的value集：values()
Coolection values = map.values();
for(Object obj : values) {
  System.out.println(obj);
}

//遍历所有的key-value  entrySet()
Set entrySet = map.entrySet();
Iterator it = entrySet.iterator();
while(it.hasNext()){
  //方式一：
  Object obj = it.next();
  Map.Entry entry = (Map.entry)obj;
  System.out.println(entry.getKey()+ "----->" + entry.getValue());
  
  //方式二：
  Object key = it.next();
  Object value = map.get(key);
  
}
```

##### properties

常用来处理配置文件，key和value都是String类型

##### Collections

 操作collection、Map的工具类

## 单例模式

```java
//饿汉式
public class Singleton{
  private static Singleton singleton = new Singleton ();
  private Singleton (){}
  public static Singleton getInstance(){return singletion;}
} 
```

```java
//懒汉式
public class Singleton{
            private static Singleton singleton = null;
            public static synchronized synchronized getInstance(){
                 if(singleton==null){
                     singleton = new Singleton();
                 }
                return singleton;
            }
       } 
```

饿汉式是线程安全的,在类创建的同时就已经创建好一个静态的对象供系统使用,以后不在改变

懒汉式如果在创建实例对象时不加上synchronized则会导致对对象的访问不是线程安全的（可以给变量加上volatile保证可见性）