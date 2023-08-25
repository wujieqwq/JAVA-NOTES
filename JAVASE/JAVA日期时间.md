---





---

# JAVA日期时间


**1.旧版**
Date类
构造方法：
```
public Date()  分配Date对象并初始化此对象，以表示分配它的时间(精确到毫秒)
public Date(long date)  表示从标准基准时间(历元(epoch),即1970年1月1日00:00:00 GMT)以来的指定毫秒数
```
常用方法：
```
public long getTime() 把日期对象转换成对应的时间毫秒值
```

DateFormat类
![[./_resources/JAVA日期时间.resources/msedge_cE6wjKyYMT.png]]

```
import java.text.DateFormat;
import java.text.SimpleDateFormat;
public class Demo02SimpleDateFormat {
public static void main(String[] args) {
    // 对应的⽇期格式如：2018-01-16 15:06:38
    SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
}
}
```

![[./_resources/JAVA日期时间.resources/msedge_yHGkHkKre6.png]]

```
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Date;
/*
把Date对象转换成String
*/
public class Demo03DateFormatMethod {
public static void main(String[] args) {
    Date date = new Date();
    // 创建⽇期格式化对象,在获取格式化对象时可以指定⻛格
    SimpleDateFormat df = new SimpleDateFormat("yyyy年MM⽉dd⽇");
    String str = df.format(date);
    System.out.println(str); // 2008年1⽉23⽇

    String str1 = "2019年12⽉11⽇";
    Date date = df.parse(str1);
    System.out.println(date); // Tue Dec 11 00:00:00 CST 2019

}
}
```

Calendar类
万年历
静态方法：public static Calendar getInstance() 使用默认时区和语言环境获得一个日历
![[./_resources/JAVA日期时间.resources/msedge_NeoEQ9AQ0K.png]]
get/set方法
```
import java.util.Calendar;
public class CalendarUtil {
    public static void main(String[] args) {
        // 创建Calendar对象
        Calendar cal = Calendar.getInstance();
        // 设置年
        int year = cal.get(Calendar.YEAR);
        // 设置⽉
        int month = cal.get(Calendar.MONTH) + 1;
        // 设置⽇
        int dayOfMonth = cal.get(Calendar.DAY_OF_MONTH);
        System.out.print(year + "年" + month + "⽉" + dayOfMonth + "⽇");
    }
}
```

```
import java.util.Calendar;
public class Demo07CalendarMethod {
    public static void main(String[] args) {
        Calendar cal = Calendar.getInstance();
        cal.set(Calendar.YEAR, 2020);
        System.out.print(year + "年" + month + "⽉" + dayOfMonth + "⽇"); // 2020年1⽉ 17⽇
    }
}
```
add方法
```
import java.util.Calendar;
public class Demo08CalendarMethod {
    public static void main(String[] args) {
        Calendar cal = Calendar.getInstance();
        System.out.print(year + "年" + month + "⽉" + dayOfMonth + "⽇"); // 2019年1⽉17⽇
        // 使⽤add⽅法
        cal.add(Calendar.DAY_OF_MONTH, 2); // 加2天
        cal.add(Calendar.YEAR, -3); // 减3年
        System.out.print(year + "年" + month + "⽉" + dayOfMonth + "⽇"); // 2016年1⽉ 19⽇;
    }
}
```
getTime方法
```
import java.util.Calendar;
import java.util.Date;
public class Demo09CalendarMethod {
    public static void main(String[] args) {
        Calendar cal = Calendar.getInstance();
        Date date = cal.getTime();
        System.out.println(date); // Tue Jan 16 16:03:09 CST 2019
    }
}
```
西方周日为一周开始
Calendar总0~11表示1~12月
日期有大小关系，靠后的日期大
旧版线程不安全

**2.新版**[参考博客](https://www.cnblogs.com/ciel717/articles/16292649.html)
`**Java 8**`推出了全新的日期时间`**API**`。不同于老版本，新`**API**`基于`**ISO**`标准日历系统，`**java.time**`包下的所有类都是不可变类型而且线程安全。

`**ZoneId**`：时区`**ID**`，用来确定`**Instant**`和`**LocalDateTime**`互相转换的规则。

`**Instant**`：瞬时实例，用来表示时间线上的一个点（瞬时）。

`**LocalDate**`：表示没有时区的日期, 不包含具体时间，`**LocalDate**`是不可变并且线程安全的。

`**LocalTime**`：表示没有时区的时间, 不包含日期，`**LocalTime**`是不可变并且线程安全的。

`**LocalDateTime**`：表示没有时区的日期时间,组合了日期和时间，`**LocalDateTime**`是不可变并且线程安全的。

`**ZonedDateTime**`：最完整的日期时间，包含时区和相对`**UTC**`或格林威治的时差。

`**Clock**`：用于访问当前时刻、日期、时间，用到时区。

`**Duration**`：用秒和纳秒表示时间的数量（长短），用于计算两个日期的“时间”间隔。

`**Period**`：用于计算两个“日期”间隔。

`**TemporalAccessor**`：`**LocalDateTime**`、`**LocalDate**`、`**LocalTime**`等类的顶级接口。

* * *

其中，LocalDate、LocalTime、LocalDateTime是新API里的基础对象。新API还引入了ZoneOffSet和ZoneId类，使得解决时区问题更为简便。解析、格式化时间的DateTimeFormatter类也全部重新设计。

说明：如果是JDK8的应用，可以使用Instant代替Date，LocalDateTime代替Calendar，DateTimeFormatter代替SimpleDateFormat。

获取当前时间
```
/**
* 获取当前时间
*/
public void localDateCreate() {

    LocalDate localDate = LocalDate.now();
    LocalTime localTime = LocalTime.now();
    LocalDateTime localDateTime = LocalDateTime.now();
    System.out.println("年月日: " + localDate);
    System.out.println("时分秒毫秒: " + localTime);
    System.out.println("年月日时分秒毫秒: " + localDateTime);

    /*输出：
        年月日: 2020-10-16
        时分秒毫秒: 09:55:49.448
        年月日时分秒毫秒: 2020-10-16T09:55:49.448
    */
}
```
获取日期
```
/**
* 获取日期的年月日周时分秒
*/
public void getDateInfo() {
    LocalDateTime localDateTime = LocalDateTime.now();
    //本年当中第多少天
    int dayOfYear = localDateTime.getDayOfYear();
    //本月当中第多少天
    int dayOfMonth = localDateTime.getDayOfMonth();
    //本周中星期几(英文)
    DayOfWeek dayOfWeek = localDateTime.getDayOfWeek();
    //本周中星期几(数字)
    int value = dayOfWeek.getValue();
    //本周中星期几(汉字)
    String dayOfWeekCN = dayOfWeek.getDisplayName(TextStyle.FULL, Locale.CHINA);
    //当天开始时间
    LocalDateTime minTime = LocalDateTime.of(localDateTime, LocalTime.MIN);
    //当天结束时间
    LocalDateTime maxTime = LocalDateTime.of(localDateTime, LocalTime.MAX);
    System.out.println("今天是" + localDateTime + "\n"
            + "本年当中第" + dayOfYear + "天" + "\n"
            + "本月当中第" + dayOfMonth + "天" + "\n"
            + "本周中星期" + value + "-即" + dayOfWeek + "-即" + dayOfWeekCN + "\n");   

    int year = localDateTime.getYear();              //年
    Month month = localDateTime.getMonth();          //月
    int monthValue = localDateTime.getMonthValue();  //直接获取
    int dayOfMonth1 = localDateTime.getDayOfMonth(); //日
    int hour = localDateTime.getHour();              //时 
    int minute = localDateTime.getMinute();          //分 
    int second = localDateTime.getSecond();          //秒
    int nano = localDateTime.getNano();              //纳秒

    System.out.println("今天是" + localDateTime + "\n"
            + "年： " + year + "\n"
            + "月： " + monthValue + "-即 " + month + "\n"
            + "日： " + dayOfMonth1 + "\n"
            + "时： " + hour + "\n"
            + "分： " + minute + "\n"
            + "秒： " + second + "\n"
            + "纳秒： " + nano + "\n"
    );
}
```
自定义日期
```
/**
* 设置自定义日期
*/
public void setDate() {
    LocalDate localDate = LocalDate.of(2020, 10, 15);
    LocalTime localTime = LocalTime.of(10, 10, 10);
    LocalDateTime localDateTime = LocalDateTime.of(2020, 10, 15, 10, 10);
    System.out.println("自定义的年月日: " + localDate);
    System.out.println("自定义时分秒毫秒: " + localTime);
    System.out.println("自定义年月日时分秒毫秒: " + localDateTime);

    /*输出:
        自定义的年月日: 2020-10-15
        自定义时分秒毫秒: 10:10:10
        自定义年月日时分秒毫秒: 2020-10-15T10:10
    */
}
```
日期时间加减
```
/**
* 日期时间的加减
*/
public void lessOrAddDate() {

    System.out.println("######################### >>> LocalDate <<< #########################");

    LocalDate localDate = LocalDate.now();
    System.out.println("当前时间: " + localDate);

    System.out.println("*********添加 操作*********");
    LocalDate addOneDay = localDate.plusDays(1); //添加一日
    LocalDate addOneMonths = localDate.plusMonths(1);//添加一月
    LocalDate addOneYears = localDate.plusYears(1);//添加一年
    LocalDate addOneWeeks = localDate.plusWeeks(1);//添加一周

    System.out.println("添加一日: " + addOneDay);
    System.out.println("添加一月: " + addOneMonths);
    System.out.println("添加一年: " + addOneYears);
    System.out.println("添加一周: " + addOneWeeks);

    System.out.println("*********减 操作*********");
    LocalDate delOneDay = localDate.minusDays(1); //减去一日
    LocalDate delOneMonths = localDate.minusMonths(1);//减去一月
    LocalDate delOneYears = localDate.minusYears(1);//减去一年
    LocalDate delOneWeeks = localDate.minusWeeks(1);//减去一周

    System.out.println("减去一日: " + delOneDay);
    System.out.println("减去一月: " + delOneMonths);
    System.out.println("减去一年: " + delOneYears);
    System.out.println("减去一周: " + delOneWeeks);

    System.out.println("######################### >>> LocalTime <<< #########################");

    LocalTime localTime = LocalTime.now();
    System.out.println("当前时间: " + localTime);

    System.out.println("*********添加 操作*********");
    LocalTime addOneHours = localTime.plusHours(1); //添加1小时
    LocalTime addOneMinutes = localTime.plusMinutes(1);//添加1分钟
    LocalTime addOneSeconds = localTime.plusSeconds(1);//添加1秒
    LocalTime addOneNanos = localTime.plusNanos(1);//添加1纳秒

    System.out.println("添加1小时: " + addOneHours);
    System.out.println("添加1分钟: " + addOneMinutes);
    System.out.println("添加1秒: " + addOneSeconds);
    System.out.println("添加1纳秒: " + addOneNanos);

    System.out.println("*********减 操作*********"); 
    LocalTime delOneHours = localTime.minusHours(1); //减去1小时
    LocalTime delOneMinutes = localTime.minusMinutes(1);//减去1分钟
    LocalTime delOneSeconds = localTime.minusSeconds(1);//减去1秒
    LocalTime delOneNanos = localTime.minusNanos(1);//减去1纳秒

    System.out.println("减去1小时: " + delOneHours);
    System.out.println("减去1分钟: " + delOneMinutes);
    System.out.println("减去1秒: " + delOneSeconds);
    System.out.println("减去1纳秒: " + delOneNanos);

    /*
    输出：
        ######################### >>> LocalDate <<< #########################
        当前时间: 2020-10-16

        *********添加 操作*********
        添加一日: 2020-10-17
        添加一月: 2020-11-16
        添加一年: 2021-10-16
        添加一周: 2020-10-23

        *********减 操作*********
        减去一日: 2020-10-15
        减去一月: 2020-09-16
        减去一年: 2019-10-16
        减去一周: 2020-10-09

        ######################### >>> LocalTime <<< #########################
        当前时间: 10:20:22.164

        *********添加 操作*********
        添加1小时: 11:20:22.164
        添加1分钟: 10:21:22.164
        添加1秒: 10:20:23.164
        添加1纳秒: 10:20:22.164000001

        *********减 操作*********
        减去1小时: 09:20:22.164
        减去1分钟: 10:19:22.164
        减去1秒: 10:20:21.164
        减去1纳秒: 10:20:22.163999999
    */
}
```
`**LocalDateTime**`满足以上所有`**LocalDate**`和`**LocalTime**`的操作日期时间方法。方法名称和`**LocalDate**`、`**LocalTime**`也都相同。

计算时间、日期间隔
```
/**
* 计算时间日期间隔
* <p>
* Duration: 用于计算两个“时间”间隔
* Period: 用于计算两个“日期”间隔
*/
public void durationOrPeriod() {
    LocalDateTime now = LocalDateTime.now();
    System.out.println("duration当前时间：" + now);

    LocalDateTime of = LocalDateTime.of(2020, 10, 15, 10, 24);
    System.out.println("duration自定义时间：" + of);

    //Duration:用于计算两个“时间”间隔
    Duration duration = Duration.between(now, of);

    System.out.println(now + " 与 " + of + " 间隔  " + "\n"
            + " 天 :" + duration.toDays() + "\n"
            + " 时 :" + duration.toHours() + "\n"
            + " 分 :" + duration.toMinutes() + "\n"
            + " 毫秒 :" + duration.toMillis() + "\n"
            + " 纳秒 :" + duration.toNanos() + "\n"
    );

    LocalDate nowDate = LocalDate.now();
    System.out.println("period当前时间：" + now);

    LocalDate ofDate = LocalDate.of(2020, 10, 15);
    System.out.println("period自定义时间：" + of);

    //Period：用于计算两个“日期”间隔
    Period period = Period.between(nowDate, ofDate);
    System.out.println("Period相差年数： " + period.getYears());
    System.out.println("Period相差月数： " + period.getMonths());
    System.out.println("Period相差日数： " + period.getDays());

    //还可以这样获取相差的年月日
    System.out.println("-------------------------------");

    long years = period.get(ChronoUnit.YEARS);
    long months = period.get(ChronoUnit.MONTHS);
    long days = period.get(ChronoUnit.DAYS);
    System.out.println("Period相差的年月日分别为 ： " + years + "," + months + "," + days);

    //注意，当获取两个日期的间隔时，并不是单纯的年月日对应的数字相加减，而是会先算出具体差多少天，
    //    再折算成相差几年几月几日的

    /*
    输出：
        duration当前时间：2020-10-16T14:41:40.235
        duration自定义时间：2020-10-15T10:24
        2020-10-16T14:41:40.235 与 2020-10-15T10:24 间隔
        天 :-1
        时 :-28
        分 :-1697
        毫秒 :-101860235
        纳秒 :-101860235000000

        period当前时间：2020-10-16T14:41:40.235
        period自定义时间：2020-10-15T10:24
        Period相差年数 ： 0
        Period相差月数 ： 0
        Period相差日数 ： -1
        -------------------------------
        Period相差的年月日分别为 ： 0,0,-1
    */
}
```

修改时间
```
/**
* 将年、月、日等修改为指定的值，并返回新的日期（时间）对象
* 析： 其效果与时间日期相加减差不多，如今天是2018-01-13，要想变为2018-01-20有两种方式
* a. localDate.plusDays(20L) -> 相加指定的天数
* b. localDate.withDayOfYear(20) -> 直接指定到哪一天
*/
public void directDesignationTime() {
    LocalDate localDate = LocalDate.now();
    System.out.println("当前时间: " + localDate);

    LocalDate addDay = localDate.plusDays(4);
    System.out.println("添加4天后的日期: " + addDay);

    LocalDate directDesignationDate = localDate.withDayOfMonth(20);
    System.out.println("直接指定到当月第几号: " + directDesignationDate);

    LocalDate directDesignationYearDate = localDate.withDayOfYear(20);
    System.out.println("直接指定到当年第几天: " + directDesignationYearDate);

    LocalDate directDesignationYear = localDate.withYear(2000);
    System.out.println("当前时间直接指定年份: " + directDesignationYear);

    LocalDate directDesignationMonth = localDate.withMonth(6);
    System.out.println("当前时间直接指定月份: " + directDesignationMonth);

    LocalTime localTime = LocalTime.now();
    LocalTime directDesignationHour = localTime.withHour(2);
    System.out.println("直接指定到小时: " + directDesignationHour);

    LocalTime directDesignationMinute = localTime.withMinute(2);
    System.out.println("直接指定到分钟: " + directDesignationMinute);
}
```

