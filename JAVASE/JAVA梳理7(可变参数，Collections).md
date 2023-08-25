---





---

# JAVA梳理7(可变参数，Collections)


### 可变参数

定义一个方法需要接收多个参数，并且参数类型一致可简化成
```
修饰符 返回值类型 ⽅法名(参数类型... 形参名) { }
```
||
```
修饰符 返回值类型 ⽅法名(参数类型[] 形参名) { }
```

```
public class ChangeArgs {
    public static void main(String[] args) {
        int[] arr = { 1, 4, 62, 431, 2 };
        int sum = getSum(arr);
        System.out.println(sum);
        // 6 7 2 12 2121
        // 求 这⼏个元素和 6 7 2 12 2121
        int sum2 = getSum(6, 7, 2, 12, 2121);
        System.out.println(sum2);
    }
        /*
        * 完成数组 所有元素的求和 原始写法
    public static int getSum(int[] arr) {
        int sum = 0;
        for (int a : arr) {
            sum += a;
        }
        return sum;
    }
        */
        // 可变参数写法
        public static int getSum(int... arr) {
            int sum = 0;
            for (int a : arr) {
                sum += a;
            }
            return sum;   
        }
}
```

* * *

### Collections

* 常用功能

![[./_resources/JAVA梳理7(可变参数，Collections).resources/msedge_XMjAeOmfeS.png]]

* Comparator比较器

```
public int compare(String o1, String o2) //比较两个参数的顺序
```
升序排序
o1<o2返回负数，相等返回0，o1>o2返回正数
降序排序
o1<o2返回正数，相等返回0，o1>o2返回负数
```
public class CollectionsDemo3 {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<String>();
        list.add("cba");
        list.add("aba");
        list.add("sba");
        list.add("nba");
        // 排序⽅法 按照第⼀个单词的降序
        Collections.sort(list, new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                return o2.charAt(0) - o1.charAt(0);
            }
        });
        System.out.println(list);
    }
}
```

