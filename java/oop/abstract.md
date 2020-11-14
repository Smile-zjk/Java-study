# 抽象类

如果父类的方法本身不需要实现任何功能，仅仅是为了定义方法签名，**目的是**让子类去覆写它，那么，可以把父类的方法声明为**抽象方法**：

```java
class Person {
    public abstract void run();
}
```

把一个方法声明为`abstract`，表示它是一个抽象方法，本身没有实现任何方法语句。因为这个抽象方法本身是无法执行的，所以，`Person`类也**无法被实例化**。编译器会告诉我们，无法编译`Person`类，因为它包含抽象方法。

必须把`Person`类本身也声明为`abstract`，才能正确编译它：

```
abstract class Person {
    public abstract void run();
}
```

**抽象类**本身被设计成**只能用于被继承**，因此，抽象类可以**强迫子类实现其定义的抽象方法**，否则编译会报错。因此，抽象方法实际上相当于定义了“规范”。

例如，`Person`类定义了抽象方法`run()`，那么，在实现子类`Student`的时候，就必须覆写`run()`方法：

```java
public class Main {
    public static void main(String[] args) {
        Person p = new Student();
        p.run();
    }
}

abstract class Person {
    public abstract void run();
}

class Student extends Person {
    @Override
    public void run() {
        System.out.println("Student.run");
    }
}

```

面向抽象编程的本质就是：

- 上层代码只定义规范（例如：`abstract class Person`）；
- 不需要子类就可以实现业务逻辑（正常编译）；
- 具体的业务逻辑由不同的子类实现，调用者并不关心。

### 小结

- 通过`abstract`定义的方法是抽象方法，它只有定义，没有实现。抽象方法定义了子类必须实现的接口规范；
- 定义了抽象方法的class必须被定义为抽象类，从抽象类继承的**子类必须实现抽象方法**；
- 如果不实现抽象方法，则该子类仍是一个抽象类；
- 面向抽象编程使得调用者只关心抽象方法的定义，不关心子类的具体实现；
- 抽象类里面可以有普通方法，但是不能该抽象类不能被实例化。