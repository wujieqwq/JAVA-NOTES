---





---

# JAVASE回顾6 异常


Throwable类
——Error类：严重错误Error,无法通过处理的错误，只能避免
——Exception类：表示异常，可以通过代码的方式纠正，使程序继续运行，是必须要处理的

Throwable常用方法
```
//打印异常详细信息，包括异常的类型，异常的原因，异常出现的位置
public void printStackTrace()

//获取发生异常的原因
public String getMessage()

//获取异常的类型和异常描述信息
public String toString()
```
1.异常分类

* 编译时期异常：checked异常，编译时期检查，出错则编译失败
	* IOException                            输入输出流异常
	* FileNotFoundException          文件找不到的异常
	* ClassNotFoundException      类找不到异常
	* DataFormatException            数据格式化异常
	* NoSuchFieldException          没有匹配的属性异常
	* NoSuchMethodException      没有匹配的方法异常
	* SQLException                        数据库操作异常
	* TimeoutException                  执行超时异常
* 运行时期异常：runtime异常，运行时期检查
	* ArrayIndexOutofBoundsException    数组越界异常
	* ClassCastException                          类型转换异常
	* NullPointerException                          空指针异常 
	* IllegalAccessException                      非法的参数异常
	* InputMismatchException                    输入不匹配异常

2.异常处理

* 抛出异常throw
	* 用在方法内抛出一个异常对象

```
throw new 异常类名(参数)；
```

* Objects非空判断

```
//查看指定引用对象是不是null
public static <T> T requireNonNull(T obj)
```

```
//源码
public static <T> T requireNonNull(T obj) {
    if (obj == null)
    throw new NullPointerException();
    return obj;
}
```

* 声明异常throws
	* 用在方法声明之上，用于表示当前方法不处理异常，提醒方法的调用者来处理异常

```
修饰符 返回值类型 ⽅法名(参数) throws 异常类名1, 异常类名2 … { }
```

```
public class ThrowsDemo {
    public static void main(String[] args) throws FileNotFoundException {
        read("a.txt");
    }
    // 如果定义功能时有问题发⽣需要报告给调⽤者。可以通过在⽅法上使⽤throws关键字进⾏声明
    public static void read(String path) throws FileNotFoundException {
        if (!path.equals("a.txt")) { // 如果不是 a.txt这个⽂件
            // 我假设 如果不是 a.txt 认为 该⽂件不存在 是⼀个错误 也就是异常 throw
            throw new FileNotFoundException("⽂件不存在");
        }
    }
}
```

* 捕获异常try...catch
	* 多个catch中的异常不能相同
	* 如果异常有父子类关系则子类先放上面处理

```
try {
    编写可能会出现异常的代码
} catch(异常类型 e) {
    处理异常的代码
    //记录⽇志/打印异常信息/继续抛出异常
}
```

* finally代码块
	* 特定代码块无论异常是否发生，都需要执行
	* finally不能单独使用
	* 当在try或者catch中调用退出JVM的相关方法，此时finally不会执行
* 自定义异常
	* 自定义编译期异常类 继承于 java.lang.Exception
	* 自定义运行期异常类 继承于 java.lang.RuntimeException

```
// 业务逻辑异常
public class RegisterException extends Exception {
    /**
    * 空参构造
    */
    public RegisterException() {
    }
    /**
    * @param message 表示异常提示
    */
    public RegisterException(String message) {
        super(message);
    }
}
```

```
public class Demo {
    // 模拟数据库中已存在账号
    private static String[] names = {"bill", "hill", "jill"};
    public static void main(String[] args) {
        // 调⽤⽅法
        try {
            // 可能出现异常的代码
            checkUsername("nill");
            System.out.println("注册成功"); // 如果没有异常就是注册成功
        } catch(RegisterException e) {
            // 处理异常
            e.printStackTrace();
        }
    }
    // 判断当前注册账号是否存在
    // 因为是编译期异常，⼜想调⽤者去处理 所以声明该异常
    public static boolean checkUsername(String uname) throws LoginException {
        for (String name : names) {
            if (name.equals(uname)) {//如果名字在这⾥⾯ 就抛出登陆异常
                throw new RegisterException("亲" + name + "已经被注册了！");
            }   
        }
        return true;
    }
}
```

![[./_resources/JAVASE回顾6_异常.resources/异常的检查与不检查.png]]

