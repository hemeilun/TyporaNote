#                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     Spring5

<br/>

Spring概述：

1.Spring是轻量级的开源的JaveEE框架

2.Spring可以解决企业应用开发的复杂行

<br/>

3.Spring有两个核心部分：IOC和Aop

（1）IOC：控制反转，把创建对象的过程交给Spring来管理

（2）Aop：面向切面，不修改源代码进行功能增强

<br/>

4.Spring特点

（1）方便解耦，简化开发

（2）Aop编程支持

（3）方便程序测试

（4）方便进行事务操作

（5）方便和其他框架进行整合

（6）降低API开发难度

<br/>

5.此课程选取的是Spring5

<br/><br/><br/><br/><br/><br/><br/><br/>

## （一）IOC容器

<br/>

### 1.Spring简单入门

<br/>

项目结构：

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/spring1.png" alt="image-20211014144044662" style="zoom:80%;" />

<br/><br/>

步骤：

（1）配置MVC环境，创建Maven项目。

<br/>

（2）导包，共四个,并让几个版本相同：

- spring-beans
- spring-context
- spring-core
- spring-expression

```
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-beans</artifactId>
    <version>5.0.5.RELEASE</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.0.5.RELEASE</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
    <version>5.0.5.RELEASE</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-expression</artifactId>
    <version>5.0.5.RELEASE</version>
</dependency>
```

<br/>

（3）配置Spring相关插件

初始可能没有Spring的xml文件，需要先在 setting->Plugins->Installed中加入配置

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/spring2.png" alt="image-20211014145202915" style="zoom:80%;" />

<br/>

（4）配置applicationContext.xml文件

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/spring3.png" alt="image-20211014145509366" style="zoom:80%;" />

<br/>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="user" class="domain.User"></bean>
</beans>
```

<br/>

（5）创建主类进行测试

User：

```java
package domain;

public class User {
    public void add(){
        System.out.println("add~~~");
    }
}
```

<br/>

（6）创建测试类

测试类记得导junit包

```
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.9</version>
    <scope>test</scope>
</dependency>
```

```java
package Test;

import domain.User;
import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class test1 {

    @Test
    public void test1() {
        ApplicationContext applicationContext = new
                ClassPathXmlApplicationContext("applicationContext.xml");
        User user = applicationContext.getBean("user",User.class);
        user.add();
    }
}
```

<br/><br/><br/><br/><br/><br/><br/><br/>

### 2.概念和原理

<br/>

#### （1）什么是IOC

<br/>

IOC是一种思想，目的是：降低耦合度。

<br/>

控制反转:

把创建对象和对象之间的调用过程交给Spring进行管理。

解释：在以前，我们需要A类，就通过new来创建A类，当A中需要B类，我们就要再创建B类，这时控制创建什么类的权力在自己的手上（正转），可是这样就会遇到一个问题，因为代码中的耦合度会非常高，我们需要改B类时就要去代码中将B类的数据进行更改，会很复杂。

所以我们将创建对象的权力交给Spring进行管理，我们没有创建权只有调用权（反转），比如：我们需要A类，Spring就给我们A类，假如这个A类需要B类我们也不要关注，因为Spring读取配置文件时自行处理，当出现C类时（C类包含B类全部功能还比B类更好），我们仅仅需要将配置文件中的B类数据换成C类数据，就可以实现改变，耦合度大大降低。

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/spring4.png" alt="image-20211014175008620" style="zoom: 67%;" />

<br/><br/><br/><br/>

#### （2）IOC底层原理

<br/>

xml解析，工厂模式，反射

解释：

IOC思想基于IOC容器，IOC容器底层就是对象工厂。

首先创建IOC容器，再通过读取xml文件，将所需的对象放入容器，这时在容器中的存储类似于Map，然后将所需的对象通过反射进行创建，只是由于实现方式的不同，对象的创建时机有所不同，当程序需要具体的对象时，就从容器中直接进行获取。



在以前创建对象时，都是使用new来进行创建

<br/><br/><br/><br/>

#### （3）画图讲解IOC底层原理

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/spring5.png" alt="image-20211014175804838" style="zoom:80%;" />

<br/>

总共四步：

第一步：配置文件

第二步：创建工厂类（这个工厂类就是IOC容器的底层，其实这一步就是创建一个容器）

第三步：解析xml文件

第四步：通过反射创建对象

<br/><br/><br/><br/>

#### （4）IOC接口

<br/>

Spring提供IOC容器的两种实现方式（两个接口）：

① BeanFactory

IOC容器基本实现，是Spring内部的使用接口，不提供开发人员进行使用加载配置文件时候不会创建对象，在获取对象（使用）采取创建对象。

② ApplicationContext

BeanFactory接口的子接口，提供更多更强大的功能，一般由开发人员进行使用

加载配置文件时候就会把在配置文件对象进行创建

<br/><br/><br/><br/><br/><br/><br/><br/>

### 3.Bean管理

<br/>

#### （1）什么是Bean管理

<br/>

Bean管理指的是两个操作：

① Spring创建对象

② Spring注入属性

<br/>

Bean管理操作的两种方式：

① 基于xml配置文件方式实现

② 基于注解方式实现

<br/><br/><br/><br/>

#### （2）基于xml方式

<br/>

##### ① 创建对象

<br/>

```xml
<bean id="user" class="domain.User"></bean>
```

在Spring的配置文件中，使用bean标签，标签里面添加对应属性，就可以实现对象的创建

在bean标签中有很多属性，就可以实现属性的创建

- id：唯一标识
- class：类全路径

创建对象时，默认是执行无参构造方法完成对象的创建

<br/><br/><br/><br/>

##### ② 注入属性方法

<br/>

**DI**：依赖注入，就是注入属性

<br/>

两种方式：

<br/>

###### <1> set方法

<br/>

第一步：创建类并在类中创建set方法来设置属性

```java
package domain;

public class Book {
    private String bname;
    private String bauthor;



    //set方法注入依赖
    public void setBname(String bname) {
        this.bname = bname;
    }
    public void setBauthor(String bauthor) {
        this.bauthor = bauthor;
    }



    @Override
    public String toString() {
        return "Book{" +
                "bname='" + bname + '\'' +
                ", bauthor='" + bauthor + '\'' +
                '}';
    }
}
```

<br/><br/>

第二步：在applicationContext.xml中进行配置属性注入

```xml
    <bean id="book" class="domain.Book">
        <property name="bname" value="Spring5"/>
        <property name="bauthor" value="尚硅谷"/>
    </bean>
```

注：

- set方法配置属性为property
- name为属性名
- value为注入属性值

<br/><br/>

第三步：测试注入成果

```java
    @Test
    public void test2(){
        ApplicationContext applicationContext = new
                ClassPathXmlApplicationContext("applicationContext.xml");
        Book book = applicationContext.getBean("book",Book.class);
        System.out.println(book);
    }
    //输出：Book{bname='Spring5', bauthor='尚硅谷'}
```

<br/><br/><br/>

###### <2> 构造函数方法

<br/>

第一步：创建类并在类中创建有参构造方法设置属性

```java
package domain;

public class Orders {
    private String oname;
    private int age;

    //可以不写
    public Orders(){}



    //构造方法设置属性
    public Orders(String oname, int age) {
        this.oname = oname;
        this.age = age;
    }



    @Override
    public String toString() {
        return "Orders{" +
                "oname='" + oname + '\'' +
                ", age=" + age +
                '}';
    }
}
```

<br/><br/>

第二步：在applicationContext.xml中进行配置属性注入

```xml
    <bean id="orders" class="domain.Orders">
        <constructor-arg name="oname" value="Spring5"/>
        <constructor-arg name="age" value="18"/>
    </bean>
```

注：

- 有参构造方法配置属性为constructor-arg
- name为属性名
- value为注入属性值

<br/><br/>

第三步：测试注入成果

```java
    @Test
    public void test3(){
        ApplicationContext applicationContext = new
                ClassPathXmlApplicationContext("applicationContext.xml");
        Orders book = applicationContext.getBean("orders", Orders.class);
        System.out.println(book);
    }
    //Orders{oname='Spring5', age=18}
```

<br/><br/><br/>

###### <3> p命名空间注入

<br/>

实际上就是运用了set的方法，只是帮助我们简化了配置

<br/>

我们对Book进行修改（仅修改配置文件，其余操作不变）：

第一步：在application的配置文件头部加上

```java
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       //注意：这是新加的
       xmlns:p="http://www.springframework.org/schema/p"
           
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
```

<br/>

第二步：修改Book的配置文件

```xml
<bean id="book" class="domain.Book" p:bname="SpringMVC" p:bauthor="itcase"></bean>
```

<br/><br/><br/><br/>

##### ③ 注入属性

<br/>

**注意：**

注入属性时，如果类内有普通属性（非其他Bean），要么都注，要么都不注。

<br/>

将Book属性加一个address进行测试，现在Book属性为：

```java
private String bname;
private String bauthor;
private String address; 
```

<br/>

###### <1> 空值

将Bean改为：

```xml
    <bean id="book" class="domain.Book">
        <property name="bname" value="Spring5"/>
        <property name="bauthor" value="尚硅谷"/>
        
        <!--注入空值-->
        <property name="address">
            <null/>
        </property>
        
    </bean>
```

<br/><br/>

###### <2> 属性值包含特殊符号

第一种方法：转义字符实现

例如：

```
<property name="address" value="&lt;&lt;南京&gt;&gt;"></property>
```

在识别时，" < " ，" > "会报错，可以使用对应字母组合代替符号进行输出

<br/>

第二种方法：xml直接输出符<![CDATA[<<南京>>]]>

只能使用在<value></value>中，<property value="">一样会出错

可是，在<value></value>中可以直接写<>符号，**所以遇到特殊符号时，直接在value中写就行了。**

<br/><br/><br/>

###### <3> 注入外部bean

<br/>

就是一个类是另一个类的类内属性时，创建第一个类需要将另一个类进行注入，这就是注入Bean。

注入Bean有两种方法：

- 外部Bean
- 内部Bean

<br/>

**项目结构：**

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/spring6.png" alt="image-20211017125936038" style="zoom:80%;" />

<br/>

**第一步：创建对象**

```java
//UserService
package service;
import dao.UserDao;

public class UserService {
    private String name;
    private int age;

    private UserDao userDao;
    
    //set方法
    public void setName(String name) {
        this.name = name;
    }
    public void setAge(int age) {
        this.age = age;
    }
    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }

    @Override
    public String toString() {
        return "UserService{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", userDao=" + userDao +
                '}';
    }
}




//UserDao
package dao;

public interface UserDao {
    //现在这个没什么用
    void add(); 
}



//UserDaoImpl
package dao.impl;
import dao.UserDao;

public class UserDaoImpl implements UserDao {

    private String deparentment;

    public void setDeparentment(String deparentment) {
        this.deparentment = deparentment;
    }

    @Override
    public String toString() {
        return "UserDaoImpl{" +
                "deparentment='" + deparentment + '\'' +
                '}';
    }

    @Override
    public void add() {
        System.out.println("add~~~");
    }
}


```

<br/>

**第二步：创建配置文件，注入属性**

```xml
<!--applicationContext2.xml-->
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="userService" class="service.UserService">
        <property name="name" value="zhangsan"/>
        <property name="age" value="18"/>
        
        <!--外部Bean注入-->
        <property name="userDao" ref="userDao"></property>
    </bean>
    
    <bean id="userDao" class="dao.impl.UserDaoImpl">
        <property name="deparentment" value="技术部"></property>
    </bean>

</beans>

```

注：

- name：类内属性名称
- ref：     引入外部Bean的id

<br/>

**第三步：测试**

```java
@Test
    public void test4(){
        ApplicationContext applicationContext = new
                ClassPathXmlApplicationContext("applicationContext2.xml");
        UserService userService = applicationContext.getBean("userService", UserService.class);
        System.out.println(userService);
        //UserService{name='zhangsan', age=18, userDao=UserDaoImpl{deparentment='技术部'}}
    }
```

<br/><br/><br/>

###### <4> 注入内部Bean

<br/>

注入内部Bean与注入外部Bean的区别只有配置xml文件时不同：

配置文件：

```xml
 <bean id="userService" class="service.UserService">
        <property name="name" value="zhangsan"/>
        <property name="age" value="18"/>
        
        <!--注入内部Bean-->
        <!--只有这个地方不同-->
        <property name="userDao">
            <bean id="userDao2" class="dao.impl.UserDaoImpl">
                <property name="deparentment" value="研发部"/>
            </bean>
        </property>
        
    </bean>
```

<br/><br/><br/>

###### <5> 注入普通集合

<br/>

集合内属性为基本数据类型

<br/>

**第一步：创建对象**

```java
package domain;

import java.util.*;

public class stu {
    private String[] array;
    private List<String> list;
    private Map<Integer,String> map;
    private Set<String> set;

    public void setArray(String[] array) {
        this.array = array;
    }
    public void setList(List<String> list) {
        this.list = list;
    }
    public void setMap(Map<Integer, String> map) {
        this.map = map;
    }
    public void setSet(Set<String> set) {
        this.set = set;
    }

    @Override
    public String toString() {
        return "stu{" +
                "array=" + Arrays.toString(array) +
                ", list=" + list +
                ", map=" + map +
                ", set=" + set +
                '}';
    }
}
```

<br/>

**第二步：创建配置文件applicationContext3.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="stu" class="domain.stu">
        
        <!--数组-->
        <property name="array">
            <array>
             <value>zhangsan</value>
             <value>lisi</value>
            </array>
        </property>

        <!--List集合-->
        <property name="list">
            <list>
                <value>chinese</value>
                <value>math</value>
            </list>
        </property>

        <!--Map集合-->
        <property name="map">
            <map>
                <entry key="30" value="java"></entry>
                <entry key="7" value="Spring"></entry>
            </map>
        </property>

        <!--Set集合-->
        <property name="set">
            <set>
                <value>mysql</value>
                <value>redis</value>
            </set>
        </property>
        
        <!--Properties集合-->
        <property name="properties">
          <props>
            <prop key="p1">aaa</prop>
            <prop key="p2">bbb</prop>
            <prop key="p3">ccc</prop>
          </props>
        </property>


    </bean>
</beans>
```

<br/>

**第三步：测试**

```java
    @Test
    public void test5(){
        ApplicationContext applicationContext = new
                ClassPathXmlApplicationContext("applicationContext3.xml");
        stu s = applicationContext.getBean("stu", stu.class);
        System.out.println(s);
        //stu{array=[zhangsan, lisi], list=[chinese, math], map={30=java, 7=Spring}, set=[mysql, redis]}
    }
```

<br/><br/><br/>

###### <6> 注入特殊集合

<br/>

集合内属性为其他类或集合

<br/>

**第一步：创建对象**

```java

//Course
package domain;
import java.util.Map;

public class Course {
    
    private Map<Integer,String> map;
    public void setMap(Map<Integer, String> map) {
        this.map = map;
    }

    @Override
    public String toString() {
        return "Course{" +
                "map=" + map +
                '}';
    }
}


 //在stu中加入
 private List<Course> course;
 public void setCourse(List<Course> course) {
        this.course = course;
    }
```

<br/>

**第二步：applicationContext3.xml中加入**

```xml

<!--这个是stu的内部成员，所以应该写在stu的bean的里面-->
<property name="course" >
    <list>
    <!--引入外部用ref标签-->
    <ref bean="course1"/>
    <ref bean="course2"/>
    </list>
</property>


<!--这个需要写在stu的bean的外面-->
<bean id="course1" class="domain.Course">
      <property name="map">
      <map>
         <entry key="30" value="java"></entry>
         <entry key="7" value="Spring"></entry>
       </map>
       </property>
</bean>
<bean id="course2" class="domain.Course">
       <property name="map">
       <map>
          <entry key="20" value="javaWeb"></entry>
          <entry key="9" value="SpringMVC"></entry>
       </map>
       </property>
</bean>
```

<br/>

**第三步：测试**

```java
    @Test
    public void test5(){
        ApplicationContext applicationContext = new
                ClassPathXmlApplicationContext("applicationContext3.xml");
        stu s = applicationContext.getBean("stu", stu.class);
        System.out.println(s);
        //stu{array=[zhangsan, lisi], list=[chinese, math], map={30=java, 7=Spring}, set=[mysql, redis], course=[Course{map={30=java,              7=Spring}}, Course{map={20=javaWeb, 9=SpringMVC}}]}
    }
```

<br/><br/><br/>

###### <7> 提取集合

<br/>

目的：将集合进行提取，使其可以被多个对象使用

<br/>

**第一步：修改applicationContext3.xml**

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
     
       xmlns:util="http://www.springframework.org/schema/util"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           
                           http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util.xsd">

    <!--新加了两行-->
    <!--xmlns:util="http://www.springframework.org/schema/util"
    http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util.xsd-->
    
```

<br/>

**第二步：在bean中引入**

```xml
        <property name="map">
           <ref bean="map1"/>
        </property>
```

<br/><br/><br/><br/>

##### ④ 工厂bean

<br/>

Spring中有两种bean类型：

- 普通bean：在配置文件中定义的bean类型就是返回类型
- 工厂bean：在配置文件中定义的bean类型可以和返回值类型不同

<br/>

步骤：

**第一步：创建类，并让这个类作为工厂bean，实现接口FactoryBean**

```java
package domain;

import org.springframework.beans.factory.FactoryBean;

public class light implements FactoryBean<String> {
    @Override
    public String getObject() throws Exception {

        return "这是工厂bean";
    }

    @Override
    public Class<?> getObjectType() {
        return null;
    }

    @Override
    public boolean isSingleton() {
        return false;
    }
}
```

<br/>

第二步：创建配置文件applicationContext4

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="light" class="domain.light"></bean>
</beans>
```

<br/>

第三步：测试

```java
    @Test
    public void test6(){
        ApplicationContext applicationContext = new
                ClassPathXmlApplicationContext("applicationContext4.xml");
        String light = applicationContext.getBean("light",String.class);
        System.out.println(light);
        //这是工厂bean
    }
```

<br/><br/><br/><br/>

##### ⑤ bean的作用域

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/spring7.png" alt="image-20211018195604457" style="zoom:80%;" />

<br/>

scope:指对象的配置范围

在bean中存在属性scope，分为单实例和多实例：

- 单实例：（默认）singleton
- 双实例：prototype

<br/>

单多实例之间的区别：

- 单实例：加载配置文件时候就会创建单实例对象

  ​               当调用此对象时，不论在哪里调用都是同一个对象

  ​         Bean的生命周期：

  ​         对象创建：当应用加载，创建容器时，对象就被创建了

  ​         对象运行：只要容器在，对象一直活着

  ​         对象销毁：当应用卸载，销毁容器时，对象就被销毁了

- 多实例：加载配置文件时候不会创建多实例对象，只有调用时     

  ​               才会创建

  ​               当调用此对象时，调用的是不同的对象
  
  ​           Bean的生命周期：
  
  ​           对象创建：当使用对象时，创建新的对象实例
  
  ​           对象运行：只要对象在使用中，就一直活着
  
  ​           对象销毁：当对象长时间不用时，被 Java 的垃圾回收器回收了

```xml
 <bean id="light" class="domain.light" scope="singleton"></bean>
```

<br/><br/><br/><br/>

##### ⑥ bean的生命周期

<br/>

步骤：

- 第一步：通过构造器创建bean实例
- 第二步：通过set方法为bean的属性设置值和对其他bean的引用
- 第三步：把bean实例传递给bean后置处理器的方法postProcessBeforeInitialization
- 第四步：调用bean的初始化方法（需要配置初始化方法）
- 第五步：把bean实例传递给bean后置处理器的方法postProcessAfterInitialization
- 第六步：bean可以使用了
- 第七步：当容器关闭时，调用bean的销毁方法

<br/>

后置处理器：

创建类引用BeanPostProcessor接口，并重写postProcessBeforeInitialization和postProcessAfterInitialization方法，再在xml文件中进行配置（程序中自己是有的，为了展示出bean的生命周期才自己写上的）。

<br/>

例子：

第一步：创建对象

```java
package domain;

public class phone {

    private String s;

    public phone(){
        System.out.println("第一步：通过构造器创建bean实例");
    }

    public void setS(String s) {
        this.s = s;
        System.out.println("第二步：通过set方法为bean的属性设置值和对其他bean的引用");
    }

    public void init(){
        System.out.println("第四步：调用bean的初始化方法");
    }

    public void destroy(){
        System.out.println("第七步：当容器关闭时，调用bean的销毁方法");
    }
}
```

<br/>

第二步：配置后置处理器

```java
package MyBeanPost;

import org.springframework.beans.BeansException;
import org.springframework.beans.factory.config.BeanPostProcessor;

public class MyBeanPost implements BeanPostProcessor {
    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("第三步：把bean实例传递给bean后置处理器的方法postProcessBeforeInitialization");
        return bean;
    }

    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("第五步：把bean实例传递给bean后置处理器的方法postProcessAfterInitialization");
        return bean;
    }
}
```

<br/>

第三步：配置配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">


    <bean id="phone" class="domain.phone" init-method="init" destroy-method="destroy">
        <property name="s" value="sss"></property>
    </bean>

    <bean id="beanpost" class="MyBeanPost.MyBeanPost"/>
</beans>
```

第四步：测试，查看生命周期

```java
    @Test
    public void test7(){
        ApplicationContext applicationContext = new
                ClassPathXmlApplicationContext("applicationContext4.xml");
        phone phone1 = applicationContext.getBean("phone",phone.class);
        System.out.println("第六步：bean可以使用了");
        System.out.println(phone1);
        ((ClassPathXmlApplicationContext) applicationContext).close();
        /*第一步：通过构造器创建bean实例
        第二步：通过set方法为bean的属性设置值和对其他bean的引用
        第三步：把bean实例传递给bean后置处理器的方法postProcessBeforeInitialization
        第四步：调用bean的初始化方法（需要配置初始化方法）
        第五步：把bean实例传递给bean后置处理器的方法postProcessAfterInitialization
        第六步：bean可以使用了
        domain.phone@32eff876
        第七步：当容器关闭时，调用bean的销毁方法*/
    }

```

<br/><br/><br/><br/>

##### ⑦ xml自动装配

<br/>

定义：根据指定装配规则（属性名称或者属性类型），Spring自动将匹配的值进行注入

<br/>

bean标签属性autowrite，配置自动装配

autowrite属性常用的两个值：

- byName：根据属性名进行注入，注入值bean的id值要和类的属性名称一致，例：类的属性名为dept，那此类bean注入时，id就要为dept
- byType：根据属性类型注入，例：一个类中属性类型为Book，那Book的bean注入时，就不能有两个Book的Bean注入。

<br/><br/><br/><br/>

##### ⑧ 外部文件引入

<br/>

applicationContext.xml加载jdbc.properties配置文件获得连接信息。

**第一步**：需要引入context命名空间和约束路径：

命名空间：xmlns:context="http://www.springframework.org/schema/context"

约束路径：http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd

 

**第二步**：Spring容器加载properties文件

<context:property-placeholder location="xx.properties"/>

<property name="" value="${key}"/>



完成后，文件就已经成功被加载进去了。

<br/>

代码解释：

第一步：导入数据库连接池包和mysql驱动包

```xml
        
        <!--druid--> 
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.1.10</version>
        </dependency>

        <!--C3P0-->
        <dependency>
           <groupId>c3p0</groupId>
           <artifactId>c3p0</artifactId>
           <version>0.9.1.2</version>
        </dependency>

        <!--mysql驱动包-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.32</version>
        </dependency>
```

第二步：创建配置文件druid.properties

```properties
pool.driverClass=com.mysql.jdbc.Driver
pool.url=jdbc:mysql:///travel
pool.username=root
pool.password=root
```

第三步：编辑配置文件applicationContext5.xml

druid连接池：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

      <!--引入外部属性文件-->
      <context:property-placeholder location="druid.properties"></context:property-placeholder>

      <!--配置druid连接池-->
      <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
          <property name="driverClassName" value="${pool.driverClass}"></property>
          <property name="url" value="${pool.url}"></property>
          <property name="username" value="${pool.username}"></property>
          <property name="password" value="${pool.password}"></property>
      </bean>
</beans>
```

C3P0连接池：

```xml

<bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
    <property name="driverClass" value="${jdbc.driver}"/>
    <property name="jdbcUrl" value="${jdbc.url}"/>
    <property name="user" value="${jdbc.username}"/>
    <property name="password" value="${jdbc.password}"/>
</bean>

```

第四步：测试

```java
    @Test
    public void test8() throws SQLException {
          ApplicationContext applicationContext = new
                  ClassPathXmlApplicationContext("applicationContext5.xml");
        DataSource dataSource = applicationContext.getBean("dataSource", DataSource.class);
        Connection connection = dataSource.getConnection();
        System.out.println(connection);
        //com.mysql.jdbc.JDBC4Connection@4f0f2942
    }
```

<br/><br/><br/><br/>

#### （3）基于注解方式

<br/>

加上注解后记得在applicationContext.xml中加上注解的组件扫描

<context:component-scan base-package="dao,service"></context:component-scan>

base-package后面的是要扫描的文件夹名

加载外部文件：

 <context:property-placeholder location="druid.properties"></context:property-placeholder>

location后面的是要加载的文件名

<br/>

##### ① 原始注解

<br/>

Spring是轻代码而重配置的框架，配置比较繁重，影响开发效率，所以注解开发是一种趋势，注解代替xml配置文件可以简化配置，提高开发效率。

**Spring原始注解主要是代替<bean>的配置**

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/spring8.png" alt="image-20211018210729449" style="zoom:80%;" />

<br/>

@Component：用来代替<bean>，但由于其阅读性不强，一般不用

@Contraller（web层），@Service（service层），@Repository（dao层），这三个作用与@Component是一样的，只是可读性更强

@Autowired与@Qualifier一般一起用，用来在一个类中注入另一个类，相当于注入<bean>

<br/>

代码解释：

<br>

项目结构：

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/spring9.png" alt="image-20211018225553562" style="zoom:80%;" />

<br/>

第一步：创建类

```java
//MangerService
package service;

import dao.MangerDao;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Scope;
import org.springframework.stereotype.Service;

//代替<bean id="mangerService" class="service.MangerService">注入bean</bean>
@Service("mangerService")

//代替bean中的scope="singleton"
@Scope("singleton")
public class MangerService {

    @Value("${pool.driverClass}")
    private String s;

    //代替注入bean，<bean name="mangerDao" ref="mangerDao"><bean>
    @Autowired
    //如果Qualifier不加，就会直接通过属性的类型，在Spring容器中去找相同属性类型的值进行注入
    @Qualifier("mangerDao")
    private MangerDao mangerDao;
    //通过注解方式，set方法是可以不写的
    public void setMangerDao(MangerDao mangerDao) {
        this.mangerDao = mangerDao;
    }

    public void delete(){
        System.out.println(s);
        mangerDao.save();
    }
}



//MangerDao
package dao;
public interface MangerDao {
    void save();
}


//MangerDaoImpl
package dao.impl;

import dao.MangerDao;
import org.springframework.stereotype.Repository;

@Repository("mangerDao")
public class MangerDaoImpl implements MangerDao {

    public void save(){
        System.out.println("save~~~");
    }
}
```

第二步：创建配置文件applicationContext6.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

    <!--注解的组件扫描-->
    <context:component-scan base-package="dao,service"></context:component-scan>
    <!--引入外部文件-->
    <context:property-placeholder location="druid.properties"></context:property-placeholder>
</beans>
```

第三步：测试

```java
    @Test
    public void test9(){
        ApplicationContext applicationContext = new
                ClassPathXmlApplicationContext("applicationContext6.xml");
        MangerService mangerService = applicationContext.getBean("mangerService", MangerService.class);
        mangerService.delete();
        //com.mysql.jdbc.Driver
        //save~~~
    }
```

<br/><br/><br/><br/>

##### ② 新注解

<br/>

原始注解并不能将配置文件中的内容全部替代，所以需要使用到新注解

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/spring10.png" alt="image-20211020165419872" style="zoom:80%;" />

<br/>

Spring中加载核心类的类为：AnnotationConfigApplicationContext

代码解释：

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/spring11.png" alt="image-20211020170033411" style="zoom:80%;" />

<br/>

第一步：创建核心配置类SpringConfigTxt

```java
package configTxt;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Import;

//设置核心配置文件
@Configuration

//配置要扫描的文件
//代替：<context:component-scan base-package="dao,service"></context:component-scan>
@ComponentScan("dao")
@ComponentScan("service")

//导入外部包
@Import({SpringContextJdbc.class})

public class SpringConfigTxt {
    
}
```

第二步：创建数据库配置类SpringContextDdbc

```java
package configTxt;

import com.alibaba.druid.pool.DruidDataSource;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.PropertySource;
import javax.sql.DataSource;


//配置要加载的文件
//代替：<context:property-placeholder location="druid.properties"></context:property-placeholder>
@PropertySource("classPath:druid.properties")
public class SpringContextJdbc {

    @Value("${pool.driverClass}")
    private String driverClass;

    @Value("${pool.url}")
    private String url;

    @Value("${pool.username}")
    private String username;

    @Value("${pool.password}")
    private String password;

    //将方法的返回值放入Spring容器中，并以指定名称命名
    @Bean(name="dataSource")
    public DataSource getDataSource(){

        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setDriverClassName(driverClass);
        dataSource.setUrl(url);
        dataSource.setUsername(username);
        dataSource.setPassword(password);
        return dataSource;
    }
    
}
```

第三步：测试（其余实体类和上面原始注解是一样的）

```java
    @Test
    public void test10(){
        ApplicationContext applicationContext = new
                AnnotationConfigApplicationContext(SpringConfigTxt.class);
        MangerService mangerService = applicationContext.getBean("mangerService", MangerService.class);
        mangerService.delete();
        //com.mysql.jdbc.Driver
        //save~~~
    }
```

<br/><br/><br/><br/><br/><br/><br/><br/>

## （二）AOP

<br/>

### 1.概念和原理

<br/>

#### （1）概念

<br/>

面向切面编程，利用AOP对业务的各个部分进行分离，从而使得业务逻辑的耦合度降低，提高程序的重用性，同时提高了开发的效率。

通俗描述：不通过修改源代码的方式，在主干功能里面添加新功能。

举例：

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/spring12.png" alt="image-20211021150816464" style="zoom:67%;" />

<br/>

AOP代理主要分为动态代理和静态代理，

- 静态代理的代表为AspectJ
- 动态代理的代表为Spring AOP

<br/>

① AsectJ

AspectJ是静态代理的增强，采用编译时生成生成AOP代理类，因此也称为编译时增强，具有良好的性能

缺点：需要使用特定的编译器进行处理

② Spring AOP

Spring AOP使用的是动态代理，运行时生成AOP代理类，所谓的动态代理就是说AOP框架不会去修改字节码，而是在内存中临时为方法生成一个AOP对象，这个AOP对象包含了目标对象的全部方法，并且在特定的切点做了增强处理，并调用源对象的方法

缺点：每次在运行时生成AOP代理，因此性能要差一点



<br/><br/><br/><br/>

#### （2）底层原理

<br/>

Spring底层使用动态代理

有两种方式的动态代理：

第一种：有接口，使用JDK动态代理

​              创建接口的实现对象，增强类的方法  

第二种：没有接口，使用CGLIB动态代理

​              创建子类的代理对象，增强类的方法

<br/><br/>

###### ① JDK动态代理

<br/>

  JDK动态代理通过反射来接收被代理的类，并且要求被代理的类必须实现一个接口，JDK动态代理的核心是InvacationHandler接口和Proxy类

<br/>

**Proxy中存在方法newPorxyInstance：**

<br/>

![image-20211021160217875](https://cdn.jsdelivr.net/gh/hemeilun/picture/spring13.png)

<br/>

- loader：类加载器

- interfances：增强方法所在类实现的接口，接口可以是多个的，用法：实现类.getClass().getInterfaces()

- h：实现这个接口InvocationHandler，创建代理对象，写增强方法,

  ​       存在两种方式：匿名内部类：

  

  ```java
                new InvocationHandler() {
                      @Override
                      public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                          方法前要加的新功能；
                          Object o = method.invoke();
                          方法后要加的新功能；
                          return o;
                          //这个o就是增强后的proxy，内部方法全部变为{}中不包含return的内容
                      }
                  });
  ```

​              第二种方式：自己创建类继承InvocationHandler接口，重写有参构造，传递要增强的类

```java
   Proxy.newProxyInstance(paperimpl.class.getClassLoader(), paper1.getClass().getInterfaces(),new MyInvocationHander(paper1));
```

<br/>

**InvocationHandler：**

<br/>

![image-20211021160924283](https://cdn.jsdelivr.net/gh/hemeilun/picture/spring15.png)

<br/>

- 返回值就是通过method.invock()后得到的对象，现在这个对象中的方法就是整个invock中的内容
- proxy:调用该方法的代理实例,比如：要增强类paper的方法，这个proxy就是paper
- method：调用方法的方法实例，比如：调用的是add方法，这个method就是add方法
- args：调用方法的参数

<br/><br/>

**代理过程**：

第一步：存在具体的接口，并存在实现类实现了该接口

第二步：在具体操作中使用了Proxy的newProxyInstance

第三步：找到newInstance的InvocationHandle的实现类，将代理的类传进去，通过invoke对代理类中的方法进行增强，然后返回代理类

第四步：调用接口中的具体方法，现在走的就是增强后的方法

<br/><br/>

代码实现：

第一步：创建接口和实现类

```java
//paper接口
package JDKProxy;

public interface paper {
    int add(int a,int b);
    void update();
}


//paperImpl
package JDKProxy;

public class paperimpl implements paper{
    @Override
    public int add(int a, int b) {
        System.out.println("这是是实现类中加法");
        return a+b;
    }

    @Override
    public void update() {
        System.out.println("这是实现类中的更新");
    }
}

```

第二步：创建类实现InvocationHandler

```java
package JDKProxy;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;

public class MyInvocationHander implements InvocationHandler {

    public Object target;
    public MyInvocationHander(Object o){
        target = o;

    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("执行前的方法");
        Object invoke = method.invoke(target, args);
        System.out.println("执行后的方法");
        return invoke;
    }
}
```

第三步：测试

```java
//继承InvocationHandler接口   
@Test
    public void test11(){
        paper paper1 = new paperimpl();
        paper o = (paper) Proxy.newProxyInstance(paperimpl.class.getClassLoader(), paper1.getClass().getInterfaces(),new MyInvocationHander(paper1));
        o.add(1,2);
        o.update();
    }

//匿名内部类
    @Test
    public void test12(){
        paper paper1 = new paperimpl();
        paper o = (paper) Proxy.newProxyInstance(paperimpl.class.getClassLoader(), paper1.getClass().getInterfaces(), new InvocationHandler() {
            @Override
            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                System.out.println("执行前的方法");
                Object invoke = method.invoke(paper1, args);
                System.out.println("执行后的方法");
                return invoke;
            }
        });
        o.add(1,2);
        o.update();
        //执行前的方法
        //这是是实现类中加法
        //执行后的方法
        //执行前的方法
        //这是实现类中的更新
        //执行后的方法
    }
```

<br/><br/><br/><br/><br/><br/><br/><br/>

### 2.AOP操作术语

<br/>

连接点：类中哪些方法可以倍增强，这些方法称为连接点

切入点：实际被增强的方法

通知（增强）：实际增强逻辑的部分，比如：给add方法增加了权限判断，那权限判断的部分就是通知

切面：把通知应用到切入点的过程

<br/>

通知的类型：

- 前置通知：放在增强的方法的前面的通知
- 后置通知
- 环绕通知：前后都有通知
- 异常通知：产生异常后的通知
- 最终通知：相当于tyr...cache...finnaly中的finnaly的通知

<br/><br/><br/><br/>

### 3.AspectJ

<br/>

```xml
<!--开启aspect生成代理对象-->
<aop:aspectj-autoproxy></aop:aspectj-autoproxy>
```

<br/>

Spring框架一般是基于AspectJ实现AOP操作

定义：AspectJ不是Spring的组成部分，是独立的AOP框架，一般把AspectJ和Spring框架一起使用，进行AOP操作

基于AspectJ实现AOP操作：

- 基于xml配置文件实现
- 基于注解方式实现

<br/>

使用时需要先导包：

```xml
 <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-aop</artifactId>
        <version>5.0.5.RELEASE</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-aspects</artifactId>
        <version>5.0.5.RELEASE</version>
    </dependency>
    
    <!--aspectj需要用到的依赖-->
    <dependency>
        <groupId>aopalliance</groupId>
        <artifactId>aopalliance</artifactId>
        <version>1.0</version>
    </dependency>
    <dependency>
        <groupId>org.aspectj</groupId>
        <artifactId>aspectjweaver</artifactId>
        <version>1.9.6</version>
    </dependency>
    <dependency>
        <groupId>net.sourceforge.cglib</groupId>
        <artifactId>com.springsource.net.sf.cglib</artifactId>
        <version>2.2.0</version>
    </dependency>
```


<br/><br/><br/>

####  （1）切入点表达式

<br/>

作用：对具体类的具体方法进行增强

语法结构：

execution（【访问修饰符】 方法返回值类型  【类全路径】 代理的方法(参数)  【抛出异常类型】  ）

*：可以在方法返回值类型，类路径，代理的方法中使用

..：方法中的参数就是..

例：execution(* ajsectj.compu.add(..))

<br/><br/><br/><br/>

#### （2）基于注解方式

<br/>

##### ① 基本使用

一些注解解释：

- Aspect：生成代理对象

- Order(数值>=0)：有多个类在同一个方法上增强，数值越小，优先级越高，越早执行

- Before：前置通知

- After：最终通知，出现异常也会执行它的内容

- AfterReturning：后置通知，出现异常不会执行它的内容

- AfterThrowing：异常通知

- Around：环绕通知，要注意一下arround，和其他几个不一样

  ​                 proceedingJoinPoint.proceed();



第一步：创建类和增强类

```java

//compu
package ajsectj;
import org.springframework.stereotype.Component;

@Component("compu")
public class compu {
    public void add(){
        System.out.println("add~~~");
    }
}

//compuPlus
package ajsectj;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.*;
import org.springframework.stereotype.Component;

@Component("compuPlus")
@Aspect
public class compuPlus {

    @Before("execution(* ajsectj.compu.add(..))")
    public void before(){
        System.out.println("before~~~");
    }

    @After("execution(* ajsectj.compu.add(..))")
    public void after(){
        System.out.println("after~~~");
    }

    @AfterReturning("execution(* ajsectj.compu.add(..))")
    public void afterReturning(){
        System.out.println("afterReturning~~~");
    }

    @AfterThrowing("execution(* ajsectj.compu.add(..))")
    public void afterThrowing(){
        System.out.println("afterThrowing~~~");
    }

    @Around("execution(* ajsectj.compu.add(..))")
    public void around(ProceedingJoinPoint proceedingJoinPoint) throws Throwable{
        System.out.println("around之前~~~");
        proceedingJoinPoint.proceed();
        System.out.println("around之后~~~");
    }

}


```

第二步：创建配置文件安平plicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
                           http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">

    <!--开启组件扫描-->
    <context:component-scan base-package="ajsectj"></context:component-scan>

    <!--开启aspect生成代理对象-->
    <aop:aspectj-autoproxy></aop:aspectj-autoproxy>

</beans>
```

第三步：测试

```java
@Test
public void test13(){
    ApplicationContext applicationContext = new
            ClassPathXmlApplicationContext("applicationContext7.xml");
    compu c = applicationContext.getBean("compu", compu.class);
    c.add();
    //around之前~~~
    //before~~~
    //add~~~
    //around之后~~~
    //after~~~
    //afterReturning~~~
}
```

<br/><br/><br/><br/>

##### ② 切入点抽取

<br/>

当存在多种通知的切入点表达式相同，可以进行抽取

注释：Pointcut(切入点表达式)

代码：

@Pointcut(切入点表达式)

public void pointdemo(){}

@Before("pointdemo()")

public void before(){

System.out.println("before...."); }

<br/><br/><br/><br/>

##### ③ 全注解开发

<br/>

创建配置类替代配置文件

<br/>

```java
package ajsectj;


import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.EnableAspectJAutoProxy;

@Configuration
@ComponentScan("ajsectj")
@EnableAspectJAutoProxy(proxyTargetClass = true)
public class ConfigAop {
}
```

<br/><br/><br/><br/>

#### （3）基于xml文件方式

了解即可：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">


    <bean id="compu" class="ajsectj.compu"/>
    <bean id="compuPlus" class="ajsectj.compuPlus"/>

    <!--配置AOP增强-->
    <aop:config>
        <!--切入点-->
        <aop:pointcut id="p" expression="execution(* ajsectj.compu.add(..))"/> 

        <!--配置切面-->
        <aop:aspect ref="compuPlus">
            <!--增强作用在具体的方法上-->
            <aop:before method="before" pointcut-ref="p"/>
        </aop:aspect>
    </aop:config>
</beans>
```

<br/><br/><br/><br/><br/><br/><br/><br/>

## （三）JdbcTemplate

<br/>

利用Spring框架对JDBC进行封装，实现对数据库的操作

template中的方法和之前在web中学的是一样的

这里说明三个新的：

- batchAdd(String sql,List<Object[]> batchArgs)   ，批量添加

- batchUpdate(String sql,List<Object[]> batchArgs)   ，批量添加

- batchDelete(String sql,List<Object[]> batchArgs)   ，批量添加

  

<br/>

具体操作：

第一步：导入template相关包

```xml
<!--template使用要用到的-->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.1.10</version>
</dependency>
<!--mysql的依赖-->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.32</version>
</dependency>
<!--jdbc相关依赖-->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.0.5.RELEASE</version>
</dependency>
<!--针对事务的一些相关操作依赖-->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-tx</artifactId>
    <version>5.0.5.RELEASE</version>
</dependency>
<!--现在可以没有，但整合其他框架，如：hibernate,mybatis等需要有这个-->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-orm</artifactId>
    <version>5.0.5.RELEASE</version>
</dependency>
```

第二步：创建实体类Users

```java
package domain;

public class Users {

    private int id;
    private String username;
    private String password;

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    @Override
    public String toString() {
        return "Users{" +
                "id=" + id +
                ", username='" + username + '\'' +
                ", password='" + password + '\'' +
                '}';
    }
}
```

第三步：配置applicationContext9.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                          http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

    <context:property-placeholder location="druid.properties"/>
    <context:component-scan base-package="dao.impl"/>

    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${pool.driverClass}"/>
        <property name="url" value="${pool.url}"/>
        <property name="username" value="${pool.username}"/>
        <property name="password" value="${pool.password}"/>
    </bean>

    <bean id="template" class="org.springframework.jdbc.core.JdbcTemplate">
        <property name="dataSource" ref="dataSource"></property>
    </bean>

</beans>



<!--这是properties中的内容，不是xml文件的-->
pool.driverClass=com.mysql.jdbc.Driver
pool.url=jdbc:mysql:///test
pool.username=root
pool.password=root
```

第四步：配置相关dao层（我只写了dao层，其他注解方式都和这个一样）

```java
package dao.impl;

import domain.Users;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.jdbc.core.BeanPropertyRowMapper;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.stereotype.Repository;

import java.util.List;

@Repository("usersDaoimpl")
public class UsersDaoimpl {

    @Autowired
    @Qualifier("template")
    private JdbcTemplate template;

    public void querry(){
        String sql="select * from users";
        List<Users> query = template.query(sql, new BeanPropertyRowMapper<Users>(Users.class));
        System.out.println(query);
    }
}
```

第五步：测试

```java
@Test
public void test16(){
    ApplicationContext applicationContext = new
            ClassPathXmlApplicationContext("applicationContext9.xml");
    UsersDaoimpl c = applicationContext.getBean("usersDaoimpl", UsersDaoimpl.class);
    c.querry();
    //[Users{id=1, username='zhangsan', password='123'}, Users{id=2, username='李四', password='123'}]
}
```

<br/><br/><br/><br/><br/><br/><br/><br/>

## （四）事务

<br/>

```xml
<!--开启事务注解-->
<tx:annotation-driven transaction-manager="dataSourceTransactionManager"/>

<!--注入事务管理对象-->
<bean id="dataSourceTransactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
     <property name="dataSource" ref="dataSource"></property>
</bean>
```

<br/>

### 1.概念

<br/>

定义：事务是数据库操作最基本单元，逻辑上为一组操作，要么都成功，如果有一个失败所有操作都失败

事务的四个特性：

- 原子性
- 一致性
- 隔离性
- 持久性

金典运用场景：

银行转账：A向B转100元，A先减100元，B再加100元，如果要完成就都完成，如果出现异常，就要回滚

<br/><br/><br/><br/>

### 2.事务操作

<br/>

事务注解添加到三层架构的Service层（业务逻辑层）

注解：**@Transactional**

添加到类上：这个类中的所有对象都是事务

添加到方法上：这个方法是一个事务

参数：

有多个参数，用逗号隔开

传播行为：@Transactional(propagation = Propagation.MANDATORY)

隔离级别：@Transactional(isolation = Isolation.READ_COMMITTED)

timeout：@Transactional(timeout = 10)

readOnly：@Transactional(readOnly = true)

rollbackFor：@Transactional(rollbackFor = RuntimeException.class)

noRollbackFor：@Transactional(noRollbackFor = RuntimeException.class)

<br/>

两种方式：

- 编程式事务管理：就是类似自己通过try...cache...实现事务管理
- 声明式事务管理

<br/>

声明式事务管理：

- 基于注解方式
- 基于xml配置文件方式

<br/>

底层原理：

在Spring进行声明式事务管理，底层使用AOP原理

<br/>

Spring事务管理API

- 提供一个接口，代表事务管理工具，这个接口针对不同的框架提供不同的实验类

<br/><br/>

步骤：

第一步：创建实体类

```java

//pingpangService
package service;

import dao.pingpangDao;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

@Service
@Transactional
public class pingpangService {

    @Autowired
    @Qualifier("pingpangDao")
    private pingpangDao pingpangdao;

    public void account(){
        pingpangdao.delete();
        pingpangdao.add();
    }
}


//pingpangDao
package dao;

public interface pingpangDao {
    void add();
    void delete();
}


//pingpangDaoimpl
package dao.impl;

import dao.pingpangDao;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.stereotype.Repository;

@Repository("pingpangDao")
public class pingpangDaoimpl implements pingpangDao {

    @Autowired
    @Qualifier("template")
    private JdbcTemplate template;

    @Override
    public void add() {
        String sql = "update users set id=id+10 where username='zhangsan' ";
        template.update(sql);
    }

    @Override
    public void delete() {
        String sql = "update users set id=id-10 where username='李四' ";
        template.update(sql);
    }
}
```

第二步：配置文件applicationContext9.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                          http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
                          http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd">

    <context:property-placeholder location="druid.properties"/>
    <context:component-scan base-package="dao,service"/>

    <!--注入事务管理对象-->
    <bean id="dataSourceTransactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"></property>
    </bean>

    <!--开启事务注解-->
    <tx:annotation-driven transaction-manager="dataSourceTransactionManager"/>
    
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${pool.driverClass}"/>
        <property name="url" value="${pool.url}"/>
        <property name="username" value="${pool.username}"/>
        <property name="password" value="${pool.password}"/>
    </bean>

    <bean id="template" class="org.springframework.jdbc.core.JdbcTemplate">
        <property name="dataSource" ref="dataSource"></property>
    </bean>


</beans>
```

第三步：测试

```java
@Test
public void test17(){
    ApplicationContext applicationContext = new
            ClassPathXmlApplicationContext("applicationContext9.xml");
    pingpangService c = applicationContext.getBean("pingpangService", pingpangService.class);
    c.account();
}
```

<br/><br/><br/><br/>

### 3.传播行为

<br/>

propagation：事务传播行为

定义：多事务方法直接进行调用，这个过程中事务进行管理的过程

事务方法：对数据库表数据进行变化的操作。



事务传播级别：事务的控制范围。通俗点说，执行到某段代码时，对已存在事务的不同处理方式。

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/spring16.png" alt="image-20211023221716367" style="zoom: 67%;" />

<br/>

​      作者：uzip柚子皮
​      链接：https://www.jianshu.com/p/760399781b78
​      来源：简书
​      著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

- **PROPAGATION_REQUIRED**，需要事务处理。有则使用，无则新建。这是 Spring 默认的事务传播行为。该级别的特性是，如果 Context 中已经存在事务，那么就将当前需要使用事务的代码加入到 Context 的事务中执行，如果当前 Context 中不存在事务，则新建一个事务执行代码。这个级别通常能满足大多数的业务场景。

- **PROPAGATION_SUPPORTS**，支持事务处理。该级别的特性是，如果 Context 存在事务，则将代码加入到 Context 的事务中执行，如果 Context 中没有事务，则使用 **非事务** 的方式执行。

- **PROPAGATION_MANDATORY**，强制性要求事务。该级别的特性是，当要以事务的方式执行代码时，要求 Context 中必须已经存在事务，否则就会抛出异常！使用 MANDATORY 强制事务，可以有效地控制 “必须以事务执行的代码，却忘记给它加上事务控制” 这种情况的发生。举个简单的例子：有一个方法，对这个方法的要求是一旦被调用，该方法就必须包含在事务中才能正常执行，那么这个方法就适合设置为 PROPAGATION_MANDATORY 强制事务传播行为，从而在代码层面加以控制。

- **PROPAGATION_REQUIRES_NEW**，每次都新建一个事务。该级别的特点是，当执行到一段需要事务的代码时，先判断 Context 中是否已经有事务存在，如果不存在，就新建一个事务；如果已经存在，就 suspend 挂起当前事务，然后创建一个新事务去执行，直到新事务执行完毕，才会恢复先前挂起的 Context 事务。

- **PROPAGATION_NOT_SUPPORTED**，不支持事务。该级别的特点是，如果发现当前 Context 中有事务存在，则挂起该事务，然后执行逻辑代码，执行完毕后，恢复先前挂起的 Context 事务。这个传播行为的事务，可以缩小事务处理过程的范围。举个简单例子，在一个事务中，需要调用一段非核心业务的逻辑操作 1000 次，如果将这段逻辑放在事务中，会导致该事务的范围变大、生命周期变长，为了避免因事务范围扩大、周期变长而引发一些的事先没有考虑到的异常情况发生，可以将这段逻辑设置为 NOT_SUPPORTED 不支持事务传播行为。

- **PROPAGATION_NEVER**，对事务要求更严格，不能出现事务！该级别的特点是，设置了该级别的代码，在执行前一旦发现 Context 中有事务存在，就会抛出 Runtime 异常，强制停止执行，有我无他！

- **PROPAGATION_NESTED**，嵌套事务。该级别的特点是，如果 Context 中存在事务 A，就将当前代码对应的事务 B 加入到 事务 A 内部，嵌套执行；如果 Context 中不存在事务，则新建事务执行代码。换句话说，事务 A 与事务 B 之间是父子关系，A 是父，B 是子。理解嵌套事务的关键点是：save point。

    父、子事务嵌套、save point 的说明：

​               父事务会在子事务进入之前创建一个 save point；

​               子事务 rollback ，父事务只会回滚到 save point，而不会回滚整个父事务；

​               父事务 commit 之前，必须先 commit 子事务。

代码说明：

```java
class ServiceA {
     void methodA() {
         ServiceB.methodB();
     }
}

class ServiceB {
     void methodB() {
     }
}    
```

- 若 `ServiceB.methodB()` 的传播行为定义为 `PROPAGATION_REQUIRED` , 那么在执行 `ServiceA.methodA()` 的时候，若 `ServiceA.methodA()` 已经开启了事务，这时调用 `ServiceB.methodB()`，`ServiceB.methodB()` 将会运行在 `ServiceA.methodA()` 的事务内部，而不再开启新的事务。而假如 `ServiceA.methodA()` 运行的时候发现自己没有在事务中，就会为它分配一个新事务。这样，在 `ServiceA.methodA()` 或者在 `ServiceB.methodB()` 内的任何地方出现异常，事务都会被回滚。即使 `ServiceB.methodB()` 的事务已经被
   提交，但是 `ServiceA.methodA()` 在接下来的过程中 fail 要回滚，`ServiceB.methodB()` 也会跟着一起回滚。

- 假如 `ServiceA.methodA()` 的传播行为设置为 `PROPAGATION_REQUIRED`，`ServiceB.methodB()` 的传播行为为 `PROPAGATION_REQUIRES_NEW`，那么当执行到 `ServiceB.methodB()` 的时候，`ServiceA.methodA()` 所在的事务就会挂起，而 `ServiceB.methodB()` 会起一个新的事务，等待 `ServiceB.methodB()` 的事务完成以后，A的事务才会继续执行。`PROPAGATION_REQUIRED`与 `PROPAGATION_REQUIRES_NEW` 的事务区别在于事务的回滚程度。因为 `ServiceB.methodB` 是新起一个事务，那么就是存在两个不同的事务。如果 `ServiceB.methodB` 已经提交，那么 `ServiceA.methodA` 失败回滚，`ServiceB.methodB` 是不会回滚的。如果 `ServiceB.methodB` 失败回滚，如果它抛出的异常被 `ServiceA.methodA` 捕获，`ServiceA.methodA` 事务仍然可能会提交。

- 假如 `ServiceA.methodA` 的事务传播行为是 `PROPAGATION_REQUIRED`，而 `ServiceB.methodB` 的事务传播行为是 `PROPAGATION_NOT_SUPPORTED`，那么当执行到 `ServiceB.methodB` 时，`ServiceA.methodA` 的事务挂起，而`ServiceB.methodB` 以非事务的状态运行完之后，再继续 `ServiceA.methodA` 的事务。

- 假如 `ServiceA.methodA` 的事务传播行为是 `PROPAGATION_REQUIRED`， 而 `ServiceB.methodB` 的事务级别是 `PROPAGATION_NEVER` ，那么 `ServiceB.methodB` 执行时就会抛出异常。

<br/>

 PROPAGATION_REQUIRES_NEW和PROPAGATION_NESTED的区别：

使用 PROPAGATION_REQUIRES_NEW时，内层事务与外层事务就像两个独立的事务一样，一旦内层事务进行了提交后，外层事务不能对其进行回滚。两个事务互不影响。两个事务不是一个真正的嵌套事务。同时它需要JTA事务管理器的支持。

使用PROPAGATION_NESTED时，外层事务的回滚可以引起内层事务的回滚。而内层事务的异常并不会导致外层事务的回滚，它是一个真正的嵌套事务。

<br/><br/><br/><br/>

### 4.隔离级别

<br/>

事务之间具有隔离性，多事务之间的操作不会产生影响。

<br/>

三种读问题：

- 脏读：一个未提交事务读取了另一个未提交事务的数据，但是另一个事务发生回滚，就会出现脏读。

  ​           比如说：

  ​            张三工资：5000

  ​            主管A：开启事务A

  ​            主管B：开启事务B，修改张三工资为3000

  ​            主管A：读取张三工资，为3000

  ​            主管B：rollback

  ​            这时，张三工资任然为5000，可是主管A读取的是3000，出现了脏读

- 不可重复读：在一次事务中两次读取的数据不一样

  ​            比如说：

  ​            张三工资：5000

  ​            主管A：开启事务A，查询张三工资为5000

  ​            主管B：开启事务B，修改张三工资为3000，提交事务B

  ​            主管A：再次查询张三工资为3000

  ​            同一事物，两次读取工资不一样，出现不可重复读

- 幻读：一个事务进行时，另一事务添加或删除数据并提交，这时第一个事务对数据进行修改，会发现修改数据数量与自己看到的数据数量不一致，出现幻读。

  ​            比如说：

  ​            张三工资：5000，李四工资：5000

  ​            主管A：开启事务A，查询张三工资为5000，李四工资5000

  ​            主管B：开启事务B，添加新员工王五工资10000，提交事务

  ​            主管A：修改所有员工工资为6000，这时发现修改了三个人的数据，可实际自己看到的只有两个人

  ​            主管A看到的是两个人，可是修改时提醒修改了三个人 ，这时就出现了幻读。

注：脏读是严重错误，一定不能出现

<br/>

隔离级别：

大多数数据库默认是**Read Committed**

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/spring17.png" alt="image-20211024140921604" style="zoom:80%;" />

<br/>

### 5.transactional的其他属性

<br/>

① timeout

事务需要在一定的时间内进行提交，如果不提交就进行回滚

默认值为-1，设置时间以秒为单位。

<br/>

② readOnly

事务内只允许查询操作

readOnly的默认值为false，标识查询，，修改都可以

设置为true后，只能查询

<br/>

③ rollbackFor

设置出现哪些异常进行回滚，默认遇到runtimeException会回滚

<br/>

④ noRollbackFor

设置出现哪些异常不进行事务回滚

<br/><br/><br/><br/>

### 6.基于xml方式实现事务管理

<br/>

声明式事务底层使用的是AOP原理，所以在配置时处理基本的事务通知配置之外，还要通过AOP将事务通知引入

<br/>

xml实现只需将注解中的@Transactional和开启事务注解去掉。

```xml
<!--配置事务通知-->
<!--这个通知说明的是切入点和具体执行事务的细节-->
<tx:advice transaction-manager="dataSourceTransactionManager" id="active">
    <tx:attributes>
        <tx:method name="add" propagation="REQUIRED"/>
        <tx:method name="delete" propagation="REQUIRED"/>
    </tx:attributes>
</tx:advice>

<!--通过这一步将事务通知配置到指定的类或方法中，让spring自动对目标进行代理-->
<aop:config>
    <!--切入点，这个就是一个大概，具体细节在事务通知中-->
    <aop:pointcut id="pc" expression="execution(* service.pingpangService.*(..))"/>

    <!--配置切面-->
    <aop:advisor advice-ref="active" pointcut-ref="pc"/>
</aop:config>
```

<br/><br/><br/><br/>

### 7.全注解配置

<br/>
@EnableTransactionManagement：开启事务注解

代替： <tx:annotation-driven transaction-manager="dataSourceTransactionManager"/>

<br/>

```java
package configTxt;


import com.alibaba.druid.pool.DruidDataSource;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.PropertySource;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.datasource.DataSourceTransactionManager;
import org.springframework.transaction.annotation.EnableTransactionManagement;

import javax.sql.DataSource;

@Configuration
@ComponentScan("service")
@ComponentScan("dao")
@PropertySource("druid.properties")
//开启事务注解
@EnableTransactionManagement
public class newConfig {

    @Value("${pool.driverClass}")
    private String driverClass;

    @Value("${pool.url}")
    private String url;

    @Value("${pool.username}")
    private String username;

    @Value("${pool.password}")
    private String password;


    //将方法的返回值放入Spring容器中，并以指定名称命名
    @Bean(name="dataSource")
    public DataSource getDataSource(){

        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setDriverClassName(driverClass);
        dataSource.setUrl(url);
        dataSource.setUsername(username);
        dataSource.setPassword(password);
        return dataSource;
    }

    //因为上面已经将Datasource放入了Spring容器中，这个地方就会根据数据类型去找
    @Bean(name="template")
    public JdbcTemplate template(DataSource dataSource){
        JdbcTemplate template = new JdbcTemplate(dataSource);
        return template;
    }

    @Bean(name="dataSourceTransactionManage")
    public DataSourceTransactionManager getManger(DataSource dataSource){
        DataSourceTransactionManager manger= new DataSourceTransactionManager(dataSource);
        return manger;
    }

}
```

<br/><br/><br/><br/><br/><br/><br/><br/>



## （五）其他

<br/>

### 1.日志

(我弄了，没有生效)

Spring5框架已经自带了通用的日志封装

- Spring5已经移除了Log4jConfigListener，官方建议使用Log4j2
- Spring5框架整合了Log4j2

<br/>

第一步：导包

```xml
<dependency>
    <groupId>org.apache.logging.log4j</groupId>
    <artifactId>log4j-api</artifactId>
    <version>2.13.3</version>
</dependency>
<dependency>
    <groupId>org.apache.logging.log4j</groupId>
    <artifactId>log4j-core</artifactId>
    <version>2.13.3</version>
</dependency>
<dependency>
    <groupId>org.apache.logging.log4j</groupId>
    <artifactId>log4j-slf4j-impl</artifactId>
    <version>2.13.3</version>
</dependency>
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-api</artifactId>
    <version>1.7.30</version>
</dependency>
```

第二步：配置log4j2.xml（名字固定）

```xml
 1  <?xml version="1.0" encoding="UTF-8"?>
 2  <Configuration status="WARN">
 3    <Appenders>
 4      <Console name="Console" target="SYSTEM_OUT">
 5        <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
 6      </Console>
 7    </Appenders>
 8    <Loggers>
 9      <Root level="error">
10        <AppenderRef ref="Console"/>
11      </Root>
12    </Loggers>
13  </Configuration>
```

<br/><br/><br/><br/>

### 2.@Nullable

<br/>

（1）放在方法上面，方法返回值可以为空

@Nullable

String getId();

<br/>

（2）放在方法的参数里面，说明参数可以为空

void add(@Nullable int a,int b)：a可以没有

<br/>

（3）放在属性上面，属性值可以为空

@Nullable

private String name;

<br/><br/><br/><br/>

### 3.GenericApplicationContext

<br/>

直接在函数中将对象保存到Spring容器中

<br/>

```java
@Test
public void test19(){
    //1.创建GenericApplicationContext对象
    GenericApplicationContext context = new GenericApplicationContext();
    //2.调用context的方法进行调用
    context.refresh();
    context.registerBean("users",Users.class,() -> new Users());
    //3.获取在Spring注册的对象
    Users users = context.getBean("users",Users.class);
    System.out.println(users);
}
```

<br/><br/><br/><br/>

### 4.Spring集成Junit4

<br/>

应该整合junit5，但我不想写了，感觉用不上

（1）原始Junit测试Spring的问题

在测试类中，每个测试方法都有以下两行代码： 

ApplicationContext ac = new ClassPathXmlApplicationContext("bean.xml");

  IAccountService as = ac.getBean("accountService",IAccountService.class);



这两行代码的作用是获取容器，如果不写的话，直接会提示空指针异常。所以又不

 能轻易删掉。

<br/>

（2）上述问题解决思路

让SpringJunit负责创建Spring容器，但是需要将配置文件的名称告诉它

将需要进行测试Bean直接在测试类中进行注入

<br/>

（3）Spring集成Junit步骤

 

<1>导入spring集成Junit的坐标

```xml
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.13.1</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-test</artifactId>
      <version>5.3.9</version>
    </dependency>
```

<2>使用@Runwith注解替换原来的运行期

<3>使用@ContextConfiguration指定配置文件或配置类

<4>使用@Autowired注入需要测试的对象

<5>创建测试方法进行测试

```java
@RunWith(SpringJUnit4ClassRunner.class)
//指定配置类
//@ContextConfiguration(classes = {SpringConfiguration.class})
//加载配置文件
@ContextConfiguration("classpath:application2.xml")
public class SpringJunitTest {
    @Autowired
    private UserService userService;
    @Test
    public void testUserService(){
        userService.save();
    }
}

```

<br/><br/><br/>

这个视频后面还有一个Webflux，就先等一等吧。