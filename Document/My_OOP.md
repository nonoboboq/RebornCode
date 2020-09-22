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
&emsp;&emsp;2.protected  
&emsp;&emsp;3.default  
&emsp;&emsp;4.private    