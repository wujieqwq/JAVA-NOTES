---





---

# Java For循环tips


## [Java](https://www.delftstack.com/zh/howto/java/for-loop-with-two-variables-java/#java-for-%E5%BE%AA%E7%8E%AF%E4%B8%AD%E4%BD%BF%E7%94%A8%E5%A4%9A%E4%B8%AA%E7%9B%B8%E5%90%8C%E7%B1%BB%E5%9E%8B%E7%9A%84%E5%8F%98%E9%87%8F) `for` 循环中使用多个相同类型的变量

我们在 `int` 类型的 `for` 循环中使用了两个变量。第一个 `;` 之前的部分是初始化部分，在这里我们可以初始化多个用逗号隔开的变量，第二个 `;` 之前的部分是条件部分，之后是操作部分。`&&`和`||`运算符可以用来创建条件。

```
public class ForLoop {
    public static void main(String[] args) {
        for (int i = 0, j = 10; i < 10 && j > 0; i++, j--) {
            System.out.println("i = " + i + " :: " + "j = " + j);
        }
    }
}
```

