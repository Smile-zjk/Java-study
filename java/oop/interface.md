# 接口

**普通类**：只有具体实现

**抽象类**：具体实现和规范（抽象方法）都有

**接口**：只有规范，自己无法写方法

在Java开发中，通常将后台分成几层，常见的是三层`MVC`：model、view、controller，模型视图控制层三层，而impl通常处于controller层的service下，用来**存放接口的实现类**，**impl的全称为implement**，表示实现的意思。



类 可以实现接口，implement 接口

一个类可以实现多个`interface`

接口中的所以定义的方法其实都是**抽象的**  `public abstract`（只能是`public abstract`，其他修饰符都会报错）

接口中可以含有变量，但是接口中的变量会被隐式的指定为`public static final`变量（并且只能是`public`，用`private`修饰会报编译错误）。

抽象类和接口的对比如下：

|            | abstract class       | interface                   |
| :--------- | :------------------- | :-------------------------- |
| 继承       | 只能extends一个class | 可以implements多个interface |
| 字段       | 可以定义实例字段     | 不能定义实例字段            |
| 抽象方法   | 可以定义抽象方法     | 可以定义抽象方法            |
| 非抽象方法 | 可以定义非抽象方法   | 可以定义default方法         |

实现类可以不必覆写`default`方法。`default`方法的目的是，当我们需要给接口新增一个方法时，会涉及到修改全部子类。如果新增的是`default`方法，那么子类就不必全部修改，只需要在需要覆写的地方去覆写新增方法。



在接口中，可以定义`default`方法。`default`方法和抽象类的普通方法是有所不同的。因为`interface`没有字段，`default`方法无法访问字段，而抽象类的普通方法可以访问实例字段。

```java
public class Main {
    public static void main(String[] args) {
        Person p = new Student("Xiao Ming");
        p.run();
    }
}

interface Person {
    String getName();
    default void run() {
        System.out.println(getName() + " run");
    }
}

class Student implements Person {
    private String name;

    public Student(String name) {
        this.name = name;
    }

    public String getName() {
        return this.name;
    }
}

```

