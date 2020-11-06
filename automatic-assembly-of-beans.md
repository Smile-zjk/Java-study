# Autowire

* 自动装配是Spring满足bean依赖的一种方式。
* Spring会在上下文中自动寻找，并自动给bean装配属性。

在Spring中有三种装配的方式

1. 在xml中显示的配置
2. 在java中显示配置
3. **隐式的自动装配bean**【重要】

## 测试

环境搭建：一个人有两个宠物

## ByName自动装配

```markup
<bean id="cat" class="com.casuall.pojo.Cat"/>
<bean id="dog" class="com.casuall.pojo.Dog"/>
<!-- byName: 通过属性的名字来自动装配 -->
<bean id="people" class="com.casuall.pojo.People" autowire="byName">
    <property name="name" value="casuall" />
</bean>
```

## ByType自动装配

```markup
<bean class="com.casuall.pojo.Cat"/>
<bean class="com.casuall.pojo.Dog"/>
<!-- byType: 通过属性的类型来自动装配 -->
<bean id="people" class="com.casuall.pojo.People" autowire="byType">
    <property name="name" value="casuall" />
</bean>
```

注意：byType需要保证属性的所有类型都是唯一的（没有重复的）。

## 使用注解实现自动装配

要使用注解须知：

1. 导入约束
2. 配置注解的支持

```markup
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <context:annotation-config/>

</beans>
```

`@Autowired`：先通过byType找，找不到再通过byName

直接在属性上使用即可，也可以在set方法上使用，也可以用在构造器上。

使用Autowired我们可以不用编写set方法来，前提是你这个自动装配的属性在IOC容器中存在，且符合名字byname。

