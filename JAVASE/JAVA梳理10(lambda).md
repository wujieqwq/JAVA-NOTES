---





---

# JAVA梳理10(lambda)


### 1.lambda标准格式

* 一些参数
* 一个箭头
* 一段代码

```
(参数类型 参数名称) ‐> { 代码语句 }
```
格式说明

* 小括号内的语法与传统参数列表一致：无参数留空；多个参数则用逗号分隔
* \->代表指向动作
* 大括号内的语法与传统方法体要求基本一致

```
public interface Cook {
    void makeFood();
}
```

```
public class Demo05InvokeCook {
    public static void main(String[] args) {
        // 请在此使⽤Lambda【标准格式】调⽤invokeCook⽅法
    }
    private static void invokeCook(Cook cook) {
        cook.makeFood();
    }
}
```

```
public static void main(String[] args) {
    invokeCook(() ‐> {
        System.out.println("吃饭啦!");
    });
}
//Cook接口makeFood抽象方法参数为空，大括号为makeFood的方法体
```

### 2.lambda的参数和返回值

传统写法
```
import java.util.Arrays;
import java.util.Comparator;
public class Demo06Comparator {
    public static void main(String[] args) {
        // 本来年龄乱序的对象数组
        Person[] array = {
        new Person("古⼒娜扎", 19),
        new Person("迪丽热巴", 18),
        new Person("⻢尔扎哈", 20) };
        // 匿名内部类
        Comparator<Person> comp = new Comparator<Person>() {
            @Override
            public int compare(Person o1, Person o2) {
                return o1.getAge() ‐ o2.getAge();
            }
        };
        Arrays.sort(array, comp); // 第⼆个参数为排序规则，即Comparator接⼝实例
        for (Person person : array) {
            System.out.println(person);
        }
    }
}
```
lambda写法
```
import java.util.Arrays;
    public class Demo07ComparatorLambda {
        public static void main(String[] args) {
        Person[] array = {
        new Person("古⼒娜扎", 19),
        new Person("迪丽热巴", 18),
        new Person("⻢尔扎哈", 20) };
        Arrays.sort(array, (Person a, Person b) ‐> {
            return a.getAge() ‐ b.getAge();
        });
        for (Person person : array) {
            System.out.println(person);
        }
    }
}
```

### 3.lambda省略格式

```
public static void main(String[] args) {
    invokeCalc(120, 130, (a, b) ‐> a + b);
}
```
省略规则

* 小括号内参数类型可以省略
* 小括号内有且仅有一个参，则小括号可以省略
* 大括号内有且仅有一个语句，则无论是否有返回值，都可以省略大括号、return关键字及语句分号

### 4.lambda使用前提

1.必须有接口，且要求接口中有且仅有一个抽象方法
2.具有上下文推断，方法的参数或局部变量类型必须为lambda对应的接口类型

