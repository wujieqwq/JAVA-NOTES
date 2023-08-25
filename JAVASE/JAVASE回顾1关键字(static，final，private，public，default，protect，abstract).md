---





---

# JAVASE回顾1关键字(static，final，private，public，default，protect，abstract)


1.static

* static方法
	* 静态方法中不能访问非静态成员方法和非静态成员变量，

				 但是在非静态成员方法中是可以访问静态成员方法和静态成员变量

* static方法是属于类的，非实例对象，在JVM加载类时，就已经存在内存中，不会被虚拟机GC回收掉，这样内存负荷会很大，但是非static方法会在运行完毕后被虚拟机GC掉，减轻内存压力
* 静态方法中不能使用this
* 属于类，被类本身和类实例化的对象调用

* static变量
	* 静态变量被所有对象共享，在内存中只有一个副本，在类初次加载的时候才会初始化
	* static成员变量初始化顺序按照定义的顺序来进行初始化
* static代码块
		静态初始化块，用于类的初始化操作
		
		在静态初始化块中不能直接访问非staic成员
		
	static内部类
	* 只有静态内部类才能够定义静态的成员变量与成员方法
	* 只能引用外部类中的静态的成员（变量或方法）
	* 创建静态内部类时不需要将静态内部类的实例绑定在外部类的实例上

```
package innerClass; 
public class OutClass1 { 
    public int oid; 
    public String oname; 
    public static class InnerStaticClass1{ 
        public int iid; 
        public String iname; 
    } 
} 
package innerClass; 
import innerClass.OutClass1.InnerStaticClass1; 
public class Test1 { 
    public static void main(String[] args) { 
        OutClass1 oc=new OutClass1(); 
        InnerStaticClass1 ic=new InnerStaticClass1();  //不依赖与外部类的实例
    } 
}
```

2.final(代表不可改变)

* final类
	* 被修饰的类不能被继承
	* final 和 abstract 这两个关键字是反相关的，final 类就不可能是 abstract 的
* final变量
	* 被修饰的变量不能被重新赋值
	* 与static一起使用常作为常量
	* 引用类型的变量则为地址不可更改，其中的属性可以更改例如数组
	* final 成员变量必须在声明的时候初始化或者在构造器中初始化
	* 同类型final变量相加时不会改变类型(例byte类型相加会变为int类型，两个final byte)
* final方法
	* 被修饰的方法不能被重写

3.abstract

* abstract方法
	* 抽象方法只包含方法名(修饰符，返回值，参数列表)，没有方法体
	* 抽象方法必须为public或者protected（因为如果为private，则不能被子类继承，子类便无法实现该方法），缺省情况下默认为public
* abstract类
	* 如果有抽象方法则该类一定为抽象类
	* 抽象类不能被实例化
	* 有自己的构造方法
	* 抽象类不能使用final关键字修饰，因为final修饰的类是无法被继承
	* 抽象类可以有成员变量（可以是私有的）

4.修饰符范围
![[./_resources/JAVASE回顾1关键字(static，final，private，public，default，protect，abstract).resources/msedge_q6yP5jNEWT.png]]

