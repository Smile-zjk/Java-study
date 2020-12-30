# Static

实例字段在每个实例中都有自己的一个独立“空间”，但是**静态字段**只有一个**共享**“空间”，**所有实例都会共享该字段**。

不推荐用`实例变量.静态字段`去访问静态字段，因为在Java程序中，实例对象并没有静态字段。在代码中，实例对象能访问静态字段只是因为编译器可以根据实例类型自动转换为`类名.静态字段`来访问静态对象。

**注意**：因为**静态方法**属于`class`而不属于实例，因此，静态方法内部，无法访问`this`变量，也**无法访问实例字段**，它**只能访问静态字段**。

new一个实例时，执行顺序为  静态代码块 -> 匿名代码块 -> 构造方法

```java
public class Person {
    // 2. 可以用来赋初始值
    {
        System.out.println("匿名代码块");
    }
    // 1. 只执行一次
    static{
        System.out.println("静态代码块");
    }
    // 3.  
    public Person() {
        System.out.println("构造方法");
    }

    public static void main(String[] args) {
        //Person person = new Person();
        //当不new实例时，只执行静态代码块
     		 System.out.println("hello");
    }
}

```

**静态导入包**，可以不用加前面的类名，如果不加static会报错。

```java
import static java.lang.Math.random;

public class MyTest {
    public static void main(String[] args) {
        System.out.println(random());
    }
}

```

## 静态内部类和非静态内部类区别

1. **静态内部类**进行实例化的时候不需要先实例化其外部类。

2. **静态内部类**是独立类，拥有外部类的`private`访问权限，但是只能访问外部类的静态成员。

   ```java
   public class Hello {
       class Person{
           private String name;
           public Person(String name) {
               this.name = name;
           }
           
       }
   
       static class Teacher{
           private String name;
           public Teacher(String name) {
               this.name = name;
           }
       }
   
       public static void main(String[] args) {
           // 不能通过 new Person的形式实例化内部类，需要先实例化一个外部类
           Hello hello = new Hello();
           //也可以用Person person = hello.new Person("inner class");
           //但最好还是加上外部类的类名，结构层次比较清楚，不容易出错
           Hello.Person person = hello.new Person("inner class");
           Hello.Teacher teacher = new Teacher("static class");
         
       }
   }
   ```

   