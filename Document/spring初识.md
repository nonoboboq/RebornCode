# Spring
这里主要是记录11.14、15两天的学习与理解。不是很成系统。后续整理。
## 一、IOC控制反转
将类的创建，转移到外部使用的时候进行注入。减少代码之间的耦合。例如一个service逻辑类，需要不同类型的数据事物类。将事物数据类通过外部创建注入的方式，可以在数据事务改变的时候，不用改变service的逻辑。
```
//事务处理类
Public Interface  Dao{

}
class MySqlDao implement Dao{

}

class OracleDao Implement Dao{

}

//service逻辑处理
public ServiceCore{
    Dao d1 = new MySqlDao();
    ...
    //存在更改的可能性
    Dao d2 = new OracleDao();

    //-----若是通过IOC的方式
    private dao;
    void setDao(Dao d){
        this.Dao = d;  //可以随时通过外部进行更换
    }
}

public Test{
    ServiceCore ser = new ServiceCore();
    ...
    //外部注入
    Dao d = MySqlDao();
    ser.setDao(d);
    ...
}
```

## 二、Spring
### 1.jar包构建项目
&emsp;&emsp;  IDEA导入对应jar包进行
### 2.maven
&emsp;&emsp;配置maven，当项目中需要对应的jar包时，网上找相应的xml 修改pom文件进行自动下载导入。
### 3.Spring
&emsp;&emsp;通过ioc.xml控制相应的对象生成。代码解释：
```
         ApplicationContext a = new ClassPathXmlApplicationContext("ioc.xml");//读取IOC文件时，会根据对应的配置生成对象，
//        Person tmp = (Person) a.getBean("person");
//        System.out.println(tmp.toString());
//        Person tmp0 = a.getBean(Person.class);
//        System.out.println(tmp0);

        Person tmp  =  a.getBean("person2",Person.class);//根据ID 获取对象的过程
        System.out.println(tmp.toString());
```
重点理解：IOC主要在Spring里就是通过外部生成对象，getBean就是获取已经生成好的实例。  
ioc.xml文件：
```
spring框架根据不同class路径和生成具体的对象。id作为索引给外部索取对象。

    1.采用默认无参数构造方式。对象属性通过set方式设置
    <bean id = "person" class="com.mashibing.bean.Person">
        <property name="id" value="1"></property>
        <property name="age" value="20" ></property>
        <property name="gender" value="nan"></property>
        <property name="name" value="zhangsan"></property>
    </bean>
    2.通过含参数构造函数设置
    <bean id = "person2" class = "com.mashibing.bean.Person">
        <constructor-arg name="id" value="2"></constructor-arg>
        <constructor-arg name="name" value="lisi"></constructor-arg>
        <constructor-arg name="age" value="12"></constructor-arg>
        <constructor-arg name="gender" value="nv"></constructor-arg>
    </bean>
```
ioc.xml主要学习掌握就是不同的实例对象生成方式的xml书写方式，和调用的方法。

