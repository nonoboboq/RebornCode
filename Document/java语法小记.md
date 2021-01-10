## static
static修饰的变量、函数、是属于类所有，在static函数内，不能访问非静态函数或者变量。因为非静态函数或者变量是依赖于对象生存的。  
static变量可以，减少不必要的内存。因为所有static和类有关，所有对象依赖共用一份变量。  
在类加载的时候，存在以下顺序：  
**先是static代码块、普通类语句、构造函数。**同时main函数也为static，在对象生成之前就存在。
```
public class Test{

    Person p = new Person();

    static{
        private int a = 10;
        private int b = 13;
        System.out.println("static");
    }

    public Test(){
        System.out.println("Constuctor");
    }

    public static void main(){
        System.out.println("main");
    }

}

class Person(){
    public Person(){
        System.out.constructor("Person Constructor");
    }
}

输出：
static
main
Person Constructor
Construnctor
```
static不会影响作用域范围。可以做的是就是将不太会改变函数或变量设为static