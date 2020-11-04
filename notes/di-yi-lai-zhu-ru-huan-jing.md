# DI依赖注入环境



## DI  依赖注入

### 1 构造器注入



### 2 set方式注入【重点】

* 依赖注入：set注入！
  * 依赖：bean对象的创建依赖于容器
  * 注入：备案对象中的所有属性，由容器来注入

【环境搭建】

1. 复杂类型

   ```java
   public class Address {
       private  String address;
   
       public void setAddress(String address) {
           this.address = address;
       }
   
       public String getAddress() {
           return address;
       }
   }
   ```

   

2. 真是测试对象

   ```java
   public class Student {
       private String name;
       private Address address;
       private String[] books;
       private List<String> hobbys;
       private Map<String, String> card;
       private Set<String> games;
       private String wife;
       private Properties info;
   ```

3. beans.xml

   ```html
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
   
   
       <bean id="student" class="com.casuall.pojo.Student">
           <property name="name" value="casuall"/>
       </bean>
   </beans>
   ```

4. 测试类

   ```java
   public class MyTest {
       public static void main(String[] args) {
           ApplicationContext context = new ClassPathXmlApplicationContext();
   
           Student stduent = (Student) context.getBean("student");
           System.out.println(stduent.getName());
       }
   }
   ```

   

5. 完善注入信息

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
   
   
       <bean id="student" class="com.casuall.pojo.Student">
           <property name="name" value="casuall"/>
           <property name="address" ref="address"/>
           <property name="books">
               <array>
                   <value>红楼梦</value>
                   <value>西游记</value>
                   <value>水浒传</value>
                   <value>三国演义</value>
               </array>
           </property>
           <property name="hobbys">
               <list>
                   <value>听歌</value>
                   <value>看电影</value>
                   <value>敲代码</value>
               </list>
           </property>
           <property name="card">
               <map>
                   <entry key="身份证" value="1234"/>
                   <entry key="银行卡" value="465"/>
               </map>
           </property>
           <property name="games">
               <set>
                   <value>LOL</value>
                   <value>CF</value>
                   <value>DNF</value>
               </set>
           </property>
           <property name="wife">
               <null/>
           </property>
           <property name="info">
               <props>
                   <prop key="学号">2018</prop>
                   <prop key="性别">男</prop>
               </props>
           </property>
       </bean>
   
       <bean id="address" class="com.casuall.pojo.Address">
           <property name="address" value="hbu"/>
       </bean>
   </beans>
   ```

#### 命名空间

**p-namespace**允许使用`bean`元素的**属性**（而不是嵌套 `<property/>`元素）来描述协作bean的属性值，也可以同时使用两者。

与具有p-namespace的XML Shortcut相似，在Spring 3.1中引入的**c-namespace**允许使用内联属性来配置**构造函数参数**，而不是嵌套`constructor-arg`元素

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
  
		<!-- 通过p命名空间，实际上是一种简化，实质还是setter注入-->
    <bean id="user" class="com.casuall.pojo.User" p:age="18" p:name="cc"/>
    <!-- 等价于下面-->
  	<bean id="user" class="com.casuall.pojo.User">
        <property name="age" value="18"/>
        <property name="name" value="cc"/>
    </bean>
  
  	<!-- 通过c命名空间，实质上是constructor注入-->
    <bean id="user2" class="com.casuall.pojo.User" c:age="22" c:name="dd"/>
    <!-- 等价于 -->
  	<bean id="user2" class="com.casuall.pojo.User">
        <constructor-arg name="age" value="22"/>
        <constructor-arg name="name" value="dd"/>
    </bean>
</beans>
```



注意点：**p命名**和**c命名**空间不能直接使用，需要导入xml约束！

```xml
xmlns:c="http://www.springframework.org/schema/c"
xmlns:p="http://www.springframework.org/schema/p"
```



### 3 拓展方式