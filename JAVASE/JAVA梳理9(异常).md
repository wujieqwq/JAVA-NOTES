---





---

# JAVA梳理9(异常)


1.异常

1.1异常概念：程序在执行的过程中，出现的非正常的情况，最终会导致JVM的非正常停止。

1.2异常体系
![[./_resources/JAVA梳理9(异常).resources/msedge_Se1o9lmYcC.png]]

* Error:严重错误，无法通过处理的错误
* Exception:表示异常，异常产生后程序员可以通过代码的方式纠正，使程序继续运行，是必须要处理的

![[./_resources/JAVA梳理9(异常).resources/msedge_7CLfcsR9Dx.png]]
1.3异常分类

* 编译时期异常：checked异常。编译时期就会检查，如果没有处理异常编译失败
* 运行时期异常：runtime异常。在运行时期检查异常

![[./_resources/JAVA梳理9(异常).resources/msedge_MuYg5IJNwb.png]]
2.异常的处理
2.1抛出异常throw
```
throw new 异常类名(参数);
```
2.2 Objects非空判断
```
public static <T> T requireNonNull(T obj)
```

```
public static <T> T requireNonNull(T obj) {
    if (obj == null)
        throw new NullPointerException();
    return obj;
}
```
2.3声明异常throws
```
修饰符 返回值类型 ⽅法名(参数) throws 异常类名1, 异常类名2 … { }
```

```
public class ThrowsDemo2 {
    public static void main(String[] args) throws IOException {
        read("a.txt");
    }
    public static void read(String path)throws FileNotFoundException, IOException {
        if (!path.equals("a.txt")) { // 如果不是 a.txt这个⽂件
            // 我假设 如果不是 a.txt 认为 该⽂件不存在 是⼀个错误 也就是异常 throw
            throw new FileNotFoundException("⽂件不存在");
        }
        if (!path.equals("b.txt")) {
            throw new IOException();
        }
    }
}
```
2.4捕获异常try...catch
```
try {
    编写可能会出现异常的代码
} catch(异常类型 e) {
    处理异常的代码
    //记录⽇志/打印异常信息/继续抛出异常
}
```

![[./_resources/JAVA梳理9(异常).resources/msedge_yiyC7GLR2z.png]]
2.5 finally代码块
语法try...catch...finally          finally代码块一定会执行
Tips:只有在try或catch调用退出JVM的相关方法，finally才不会执行
2.6异常注意事项
多个异常
```
try {
    编写可能会出现异常的代码
} catch(异常类型A e) { 当try中出现A类型异常,就⽤该catch来捕获.
    处理异常的代码
    // 记录⽇志/打印异常信息/继续抛出异常
} catch(异常类型B e) { 当try中出现B类型异常,就⽤该catch来捕获.
    处理异常的代码
    // 记录⽇志/打印异常信息/继续抛出异常
}
```

* 多个catch中异常不能相同，若多个异常中有子父类的关系，那么子类异常要在最上面的catch中处理
* 运行时异常被抛出可以不处理
* finally有return语句，永远返回finally中的结果
* 如果父类抛出多个异常，子类重写父类方法时，抛出和父类相同的异常或者是父类异常的子类或者不抛出异常
* 父类方法没有抛出异常，子类重写时也不可抛出异常，子类产生该异常只能捕获处理不能声明抛出

3.自定义异常
异常类定义：
1.自定义编译期异常，类继承于java.lang.Exception
2.自定义运行期异常，类继承于java.lang.RuntimeException

