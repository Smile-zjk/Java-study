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

   \`\`\`xml &lt;?xml version="1.0" encoding="UTF-8"?&gt;

 \`\`\` 4. 测试类 \`\`\`java public class MyTest { public static void main\(String\[\] args\) { ApplicationContext context = new ClassPathXmlApplicationContext\(\); Student stduent = \(Student\) context.getBean\("student"\); System.out.println\(stduent.getName\(\)\); } } \`\`\` 5. 完善注入信息 \`\`\`xml红楼梦西游记水浒传三国演义听歌看电影敲代码LOLCFDNF2018男

 \`\`\` \#\#\#\# 命名空间 \*\*p-namespace\*\*允许使用\`bean\`元素的\*\*属性\*\*（而不是嵌套 \`\`元素）来描述协作bean的属性值，也可以同时使用两者。 与具有p-namespace的XML Shortcut相似，在Spring 3.1中引入的\*\*c-namespace\*\*允许使用内联属性来配置\*\*构造函数参数\*\*，而不是嵌套\`constructor-arg\`元素 \`\`\`xml

```text
<bean id="user2" class="com.casuall.pojo.User" c:age="22" c:name="dd"/>
<!-- 等价于 -->
  <bean id="user2" class="com.casuall.pojo.User">
    <constructor-arg name="age" value="22"/>
    <constructor-arg name="name" value="dd"/>
</bean>
```

&lt;/beans&gt;

```text
注意点：**p命名**和**c命名**空间不能直接使用，需要导入xml约束！

```xml
xmlns:c="http://www.springframework.org/schema/c"
xmlns:p="http://www.springframework.org/schema/p"
```

### 3 拓展方式

### 4 bean的作用域

| Scope | Description |
| :--- | :--- |
| singleton | \(Default\) Scopes a single bean definition to a single object instance for each Spring IoC container. |
| prototype | Scopes a single bean definition to any number of object instances. |
| request | Scopes a single bean definition to the lifecycle of a single HTTP request. That is, each HTTP request has its own instance of a bean created off the back of a single bean definition. Only valid in the context of a web-aware Spring `ApplicationContext`. |
| session | Scopes a single bean definition to the lifecycle of an HTTP `Session`. Only valid in the context of a web-aware Spring `ApplicationContext`. |
| application | Scopes a single bean definition to the lifecycle of a `ServletContext`. Only valid in the context of a web-aware Spring `ApplicationContext`. |
| websocket | Scopes a single bean definition to the lifecycle of a `WebSocket`. Only valid in the context of a web-aware Spring `ApplicationContext`. |

1. 单例模式（Spring默认机制）

```markup
<bean id="user" class="com.casuall.pojo.User" scope="singleton"/>
```

1. 原型模式：每次从容器中get的时候，都会产生一个新对象

```markup
<bean id="accountService" class="com.something.DefaultAccountService" scope="prototype"/>
```

1. 其余的request、session、application这些只能在web开发中使用到！

