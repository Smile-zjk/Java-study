# 多线程

一个Java程序实际上是一个JVM进程，JVM进程用一个主线来执行`main()`方法，在`main()`方法内部，我们可以启动多个线程。此外，JVM还有负责垃圾回收的其他工作线程等。

## 方法一：

 从`Thread`派生一个自定义类，然后覆写`run()`方法。`start()`方法会在内部自动调用实例的`run()`方法。

**注意：**直接调用`run()`方法，相当于调用了一个普通的Java方法，当前线程并没有任何改变，也不会启动新线程。必须调用`Thread`实例的`start()`方法才能启动新线程，如果我们查看`Thread`类的源代码，会看到`start()`方法内部调用了一个`private native void start0()`方法，`native`修饰符表示这个方法是由JVM虚拟机内部的C代码实现的，不是由Java代码实现的。

```java
public class Main {
    public static void main(String[] args) {
        Thread t = new MyThread();
        t.start(); // 启动新线程
    }
}

class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("start new thread!");
    }
}
```

## 方法二：

实现`Runnable`接口，推荐使用`Runnable`对象，因为**Java单继承的局限性**。

```java
public class Main {
    public static void main(String[] args) {
        // 创建Runnable接口的实现类对象
      	MyRunnable myrunnable = new MyRunnable();
      
        // 创建线程对象，通过线程对象来开启我们的线程，代理
        Thread t = new Thread(myrunnable);
      
        t.start(); 
    }
}

class MyRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("start new thread!");
    }
}
```

或者用Java8引入的lambda语法进一步简写为：

```java
public class Main {
    public static void main(String[] args) {
        Thread t = new Thread(() -> {
            System.out.println("start new thread!");
        });
        t.start(); // 启动新线程
    }
}
```

