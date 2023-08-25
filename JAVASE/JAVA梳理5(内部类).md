---





---

# JAVA梳理5(内部类)


![[./_resources/JAVA梳理5(内部类).resources/内部类.png]]

内部类
1.成员内部类：定义在类中方法外的类

* 内部类可直接访问外部类的成员，包括私有成员
* 外部内要访问内部类的成员，必须要建立内部类的对象

2.匿名内部类：带具体实现的 父类或父接口 匿名的子类对象
```
new ⽗类名或者接⼝名() {
// ⽅法重写
@Override
public void method() {
// 执⾏语句
}
};

public class InnerDemo2 {
public static void main(String[] args) {
/*
* 1.等号右边:定义并创建该接⼝的⼦类对象
* 2.等号左边:是多态，接⼝类型引⽤指向⼦类对象
*/
FlyAble f = new FlyAble() {
public void fly() {
System.out.println("我⻜了~~~");
}
};
// 将f传递给showFly⽅法中
showFly(f);
}
public static void showFly(FlyAble f) {
f.fly();
}
}


```
3.静态内部类

