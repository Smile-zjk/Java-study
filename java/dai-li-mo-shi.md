# 代理模式

为什么要学习代理模式？因为这就是SpringAOP的底层！【**SpringAOP**和**SpringMVC**】

代理模式的分类：

* 静态代理
* 动态代理

## 静态代理

角色分析：

* 抽象角色：一般会使用接口或者抽象类来决解
* 真实角色：被代理的角色
* 代理角色：代理真实角色，代理真实角色后，我们一般会做一些附属操作
* 客户：访问代理对象的人

代理步骤：

1. 接口

   ```java
   //租房
   public interface Rent {
       public void rent();
   }
   ```

2. 真实角色

   ```java
   //房东
   public class Host implements Rent{
   
       public void rent() {
           System.out.println("房东要出租房子");
       }
   }
   ```

3. 代理角色

   ```java
   public class Proxy implements Rent{
       private Host host;
   
       public Proxy() {
   
       }
       public Proxy(Host host) {
           this.host = host;
       }
   
   
       public void seeHouse(){
           System.out.println("中介带你看房");
       }
   
       public void fare(){
           System.out.println("收中介费");
       }
   
       public void rent() {
           seeHouse();
           this.host.rent();
           fare();
       }
   }
   ```

4. 客户端访问代理角色

   ```java
   public class Client {
       public static void main(String[] args) {
           Host host = new Host();
           Proxy proxy = new Proxy(host);
   
           proxy.rent();
       }
   }
   ```

   

代理模式的好处：

* 可以使真实角色的操作更加纯粹，不用去关注一些公共的业务
* 公共业务就交给代理角色，实现了业务的分工
* 公共业务发生扩展的时候，方便集中管理

缺点：

* 一个真实角色就会产生一个代理角色；代码量会翻倍～开发效率变低