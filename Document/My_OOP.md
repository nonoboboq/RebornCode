# 1.面向对象
Object Oriented Programming  
面向对象是对实际事物的一种抽象，更符合人类的认知。  
对象的特征：属性、方法

# 2.Object类
一个类如果没有显式的继承另外一个类，则这个类就继承自Object类。
```
public class Person{

}
等同于
public class Person extends Object{

}
```
在object类中有一些**native**修饰的方法，是直接操作的内核进行的。
## 2.1 Object中的主要方法
### &emsp;1.getClass()

### &emsp;2.hashCode()
&emsp;&emsp;获取一个对象的哈希值，这里调用的是内核方法.将一些对象(String、int。。)通过哈希函数得到哈希值。自定义一个新的类的时候，一般需要从写hashCode()。
哈希函数中是将对象进行了哈希，得到的是int值，但转成了16进制进行了存储。

### &emsp;3.equal()
&emsp;&emsp;比较了两个对象的内容是否是相同的，与‘==’放在一起理解。
```
String s1 = new String("apple");
String s2 = new String("apple");
System.out.println(s1==s2);//false 这里是将是将s1、s2两个对象进行比较，对象地址不同。这里代表了两个不同的对象
System.out.println(s1.equal(s2));//true;这是由于两个对象都是引用相同的
```
![equal用法](https://github.com/nonoboboq/RebornCode/blob/master/.png/equal.PNG)
 
### &emsp;4.clone()

### &emsp;5.toString()

### &emsp;6.notify()
&emsp;&emsp;多线程时候会用到

### &emsp;7.wait()


**注意：抽象类中是可以定义构造函数的，但是无法进行实例化，抽象类多为在进行基于接口编程时候使用**



# 3.多态
对同一个指令，不同的对象给予不同的反应(不同的方法实现)。相同的引用类型，不用的实例执行可以执行不同的操作。 基于接口而非基于实现编程时候，多态可以提前约定好开发接口，这是一种自上而下的编程思想。  
使用方法：  
 &emsp;1.必须要有继承关系  
 &emsp;2.子类方法必须重写父类的方法  
 &emsp;3.父类引用指向子类对象  
表现形式：  
 &emsp;1.父类作为参数传递  
 &emsp;2.父类作为返回类型  
 父类型转换为子类型后，不安全操作。子类型可直接转换成父类型。

# 4.代码块
&emsp;1.普通代码块:直接在方法和语句中定义的代码块。{}中的代码    
&emsp;2.构造代码块：直接写在类中，类中的变量,每次运行的时候，会将构造代码块添加到构造函数中的前面。当使用this()方法时，另一个this方法中已经被添加过，不会被添加。   
&emsp;3.静态代码块：使用static{}括起来的叫静态代码块，在程序载入的时候就优先执行，例如：数据库连接等其他提前需要准备好的代码会放在static代码块中。类加载时会优先使用static代码块，多次载入也就只执行一次static代码块。  
&emsp;**“是在类初始化时进行，不是在创建对象时进行”且静态初始化块中代码不能访问非static成员变量**  
&emsp;4.同步代码块：在多线程时使用，用来给共享空间进行加锁操作。（？）  
**执行顺序**：静态、构造、普通代码块
```
public class Demo(){
    {
        System.out.println("hello");//构造代码块
    }
    public Demo(){
        System.out.println("hello");//构造代码块
    }

    public void test(){
        System.out.prinln("hello");//普通代码块 
    }
    public static void main(String[] args{
        this.test()
    }
}
```
# 5.package
解决类之间重名问题；为了便于管理类，合适的类位于合适的包。一般需要在文件第一行写上该类的名字：(例如：package com.xxx.xxx 域名倒写)  

完全限定名:包名+类名  
JDK中的主要包：  
&emsp;&emsp;java.lang: java语言中的核心类，如String、Math、Integer、System、Thread等.**不需要手动导入，自动加载**  
&emsp;&emsp;java.awt 包含了构成抽象窗口工具集  
&emsp;&emsp;util 工具包 
&emsp;&emsp;net 网络包  
&emsp;&emsp;io 输入输出流包  
# 6.import
当需要引入非lang包的其他java类的时候，需要使用import工具，如果不使用import，需要每次都要写入完全限定名字：  
用法：  
&emsp;&emsp;1. import.包名.类名  
&emsp;&emsp;2. import.*  
**注：** *当一个java文件需要使用多个同名类的时候，只能选择导入一个，另一个使用完全限定名字进行导入。*  
静态导包：当需要多次使用某个类时候，可使用该方法。  
```
import static java.lang.Math.*

System.out.println(Math.sqrt(2))
System.out.println(sqrt(2)) //简化成这样写。但同一个类中定义了sqrt()方法时，会优先使用本类中的同名方法。

```

# 7.封装 
将类中的某些属性通过private关键字隐藏到内部，不允许外部程序进行直接访问，可以通过类的自身方法进行访问和操作。
# 8.访问控制符
&emsp;&emsp;1.public  
&emsp;&emsp;2.protected 可以被当前类访问、当前的包中其他类访问、子类进行访问  
&emsp;&emsp;3.default 可以被当前类访问、当前的包中其他类访问  
&emsp;&emsp;4.private 可以被当前类访问  
**注**：构造方法也可能是private，在单例模式下使用。   
# 9.值传递与引用传递
java中区分基本类型：如整数、进行值传递，自定义类及其他(?)为引用传递。

# 10.super
&emsp;任何类的构造函数中，若构造函数的第一行没有显式的调用super()，**那么Java默认都会调用super()作为父类的初始化函数**。  
1.可以在子类中调用父类被子类覆盖的方法。super.父类方法名称  
2.当super在普通方法中使用的话，可以写在该方法中的任意位置。  
3.当super在构造方法中使用的话，会调用父类的构造方法、一定要将super放在第一行。  
4.在构造方法中super关键字和this()关键字不能同时出现  
5.父类中私有的属性和方法都不能被调用，包括构造方法  

# 11.局部变量和成员变量
局部变量：定义在方法中的变量，在整个方法中存在，只能在当前方法中使用。不包含初始化。   
成员变量：类内的变量叫成员变量(全局变量)作用域为整个类体中。成员变量包含初始值：int 0 ;String null  

# 12.引用类型
&emsp;基本类型：数值型(整数类型byte short long、浮点类型float double) 字符型(char) 布尔型(boolen)
&emsp;引用数据类型：类、接口、数组。与指针相比较而言，两个指针可以进行大小比较和相减运算，引用是不可以的。引用是对一个变量或对象的别名，指针是存储了一个对象的地址空间。  
# 13.static
修饰类成员变量的时候，表示该变量是类成员变量。与python对比来讲，python中的对象变量通过init函数进行定义与初始化，java中的类变量声明在类中，但对普通变量和static进行区分。

# 14.接口
java中的继承是单继承，但在使用接口类的时候可以通过implement进行“多重继承”.例子：  
```
public interface ATest{
    public void testFuc1(){};//没有实现
}

public interface BTest{
    public void testFuc2(){};//没有实现
}


public class Test implement ATest,BTest{
    @Override
    public void testFuc1(){
        System.out.println("");
    }

    @Override
    public void testFuc2(){
        System.out.println("");
    }

}

```
子类中对接口中的函数必须要全部实现。接口类不能实例化，接口类中的变量都是静态常量，不可进行修改，变量不写static修饰的话，默认为static。

# 15.内部类
把一个类定义在另一个类的内部称为内部类。  
创建内部类的方式：  
```
public class InnerClassDemo {
    public static void main(String[] args) {

    }
    class AInnerClass{
        String str = "abcaaa";
        public void show(){
            System.out.println("Innerclass str :"+this.str);
        }

    }
}
//测试类
public class TestInnerClass {
    public static void main(String[] args) {
        InnerClassDemo.AInnerClass tmp = new InnerClassDemo().new AInnerClass();//内部类的创建方法
        tmp.show();
    }
}
```
**注**：  
1.内部类可以访问外部类的私有属性，其实内部类可以看成外部类的中一个“方法”，外部类不能访问内部类的属性。  
2.内部类不能包含static成员 

## 匿名内部类：
当定义了一个内部类，实现了某个接口的时候，在使用的过程中只需要使用一次，可以不创建具体的类，采用new interface()
```
//测试类
public class TestInnerClass {
    public static void main(String[] args) {
        new Thread(new Runnable()//实例化了一个接口的实现类
            @Override
            public void run(){

            }
        )
    }
}
```
# 16.异常机制
**a.捕获异常**  
try catch,捕获异常后不会中断程序  
```
public class ExceptionDemo {
    public static void main(String[] args) {
        try{
            Scanner in = new Scanner(System.in);
            System.out.println("Please Input a:");
            int a = in.nextInt();
            System.out.println("Please Input b:");
            int b = in.nextInt();
            System.out.println("Please a/b:"+a/b);
        }catch (Exception e){
            //System.out.println(e);
            e.printStackTrace();//异常的调用栈
            System.out.println(e.getMessage());//异常提示
        }
    }
}
```
其中的Exception最能够细化捕捉：InputMismatchException输入不匹配、ArithmeticExceptio数学异常、NullPointerException空指针异常  
try catch finally:finally中的代码总会执行，finally中一般会包含：IO流的关闭操作；数据库连接关闭操作；  
```
public class ExceptionDemo {
    public static void main(String[] args) {
       System.out.println(test());
    }
    private static int test(){
        int num = 10;
        try {
            System.out.println("try");
            return num+=80; //num值改变后会优先执行finally语句，并在其中返回
        }catch (Exception e){
            System.out.println("erroe");
        }finally {
            if(num>20){
                System.out.println("num>20:"+num);
            }
            System.out.println("finally");
            num = 100;
            return num;
        }
    }
}
```
finally唯一不执行的情况是，调用了System.exit（1）的语句  
**b.声明异常**  
  
```
public class ThrowEdxception {
    public static void main(String[] args) {
        //在上层捕获异常
        try{
            test();
        }catch (Exception e){
            e.printStackTrace();
        }
        System.out.println("end");
    }
    //声明异常，多个异常用,隔开。向上抛出异常
    private static void test() throws Exception
    {
        System.out.println(1/0);
    }
}
```
在多个方法互相调用的过程中，需要在每个方法都使用Try catch.使用throws声明并抛出，到达最上层进行捕获，可以避免写多个try catch；

# 17.包装类
包装类是将基本类型封装到一个类中，包含了属性和方法，方便对象操作，包装类无语java.lang包中。
```
public class TestDemo {
    public static void main(String[] args) {
        int a = 10;
        Integer b = new Integer(10);
        //手动类型转换
        int b1 = b.intValue();//拆箱操作
        Integer a1 = Integer.valueOf(a);//装箱操作
        
        System.out.println(a==b);//True,调用了(Integer)a
    }
}
```
装箱：将基本数据类型转换成包装类  
拆箱：将包装类转换成基本数据类型  
常见包装类型：   
Boolean:  
Number:Byte,Short,Integer,Long,Float,Double  
Character:  
```
String s1 = new String("abc");
String s2 = "abc";
System.out.println(s1==s2);//false
System.out.println(s1.equals(s2));//true
s2 = s2,intern();
System.out.println(s1==s2);//true
System.out.println(s1.equals(s2));//true
```
集合框架分为（Set、List、Queue）、（Map）：  
![equal用法](../.png/集合框架1.png)

TreeSet:基于红黑树实现，支持有序操作

HashSet：基于哈希表实现，支持快速查找,基于HashMap实现。默认大小为16，装载因子为0.75,代表了当set中元素大于12个时，就需要开始扩容。
```
  public HashSet(int initialCapacity, float loadFactor) {
        map = new HashMap<>(initialCapacity, loadFactor);
    }
其中initialCapacity为初始容量，loadFactor为装载因子。
```
&emsp;**HashSet的装载原理**，当向HashSet中装载一个对象时，会调用该对象的HashCode()方法得到其hashCode值，然后根据hashCode值决定该对象的存储位置。HashSet存储成功的条件是：**1.两个对象equal()比较为FALSE 2.两个对象的HashCode()值不相等**
&emsp;**HashSet的查找原理**：将对象取hashcode()，再进行索引查找。    
HashSet的基本用法：
```
        HashSet<String> a1 = new HashSet<>();
        String s1 = "abc";
        a1.add(s1);
        a1.add("abc");
        a1.add("qwe");
        a1.add("tyu");

        System.out.println(a1.size());
        a1.remove("qwe");
        System.out.println(a1.size());
        System.out.println(a1.contains("qwe"));

        //两种遍历方式
        Iterator<String> it = a1.iterator();
        while (it.hasNext()){
            System.out.println(it.next());
        }

        for (String item:a1){
            System.out.println(item);
        }
结果：
3
2
false
tyu
abc
tyu
abc
```
LinkedHashSet:具有hashset的查找效率，内部使用双向链表维护元素的插入顺序
```

```

ArrayList：基于动态数组实现，支持随机访问,继承RandomAccess接口，数组默认大小为10，当其中元素多余容量时，会进行1.5倍的扩容，这是需要进行搬移复制操作。
```
public class ArrayList<E> extends AbstractList<E>
        implements List<E>, RandomAccess, Cloneable, java.io.Serializable
```
基本使用：
```
        ArrayList<String> a1 = new ArrayList<>(10);
        a1.add("abc");
        a1.add("ert");
        a1.add("opi");
        System.out.println(a1);
        a1.add(1,"www");
        System.out.println(a1);
        a1.remove("abc");
        System.out.println(a1);
        System.out.println(a1.size());
        System.out.println(a1.get(2));
        a1.set(1,"chen");
        System.out.println(a1);

结果：
[abc, ert, opi]
[abc, www, ert, opi]
[www, ert, opi]
3
opi
[www, chen, opi]
```

Vector:与ArrayList类似，但是是线程安全的

LinkedList:继续双向链表实现，只能顺序访问，可以快速的在链表中插入和删除元素，Linkedlist还可以用作栈、队列和双向队列

LinkedList：可以用来实现双向队列
PriorityQueue：基于堆结构实现，可以用它来实现优先队列

![equal用法](../.png/集合框架2.png)

TreeMap:红黑树实现

HashMap:基于哈希表实现

HashTable:线程安全的。(遗留类？)线程安全，应使用ConcurrentHashMap来支持线程安全。

LinkedHashMap:双向链表维护元素顺序，