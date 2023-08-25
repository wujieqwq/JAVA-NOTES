---





---

# JAVA梳理11(文件操作，IO流)


### 1.File类

java.io.FIle
构造方法
```
推荐D:/aaa.txt写法
// ⽂件路径名
String pathname = "D:\\aaa.txt";
File file1 = new File(pathname);

// ⽂件路径名
String pathname2 = "D:\\aaa\\bbb.txt";
File file2 = new File(pathname2);

// 通过⽗路径和⼦路径字符串
String parent = "d:\\aaa";
String child = "bbb.txt";
File file3 = new File(parent, child);

// 通过⽗级File对象和⼦路径字符串
File parentDir = new File("d:\\aaa");
String child = "bbb.txt";
File file4 = new File(parentDir, child);
```
常用方法
```
public class FileGet {
    public static void main(String[] args) {
        File f = new File("d:/aaa/bbb.java");
        System.out.println("⽂件绝对路径:" + f.getAbsolutePath());
        System.out.println("⽂件构造路径:" + f.getPath());
        System.out.println("⽂件名称:" + f.getName());
        System.out.println("⽂件⻓度:" + f.length() + "字节");
        File f2 = new File("d:/aaa");
        System.out.println("⽬录绝对路径:" + f2.getAbsolutePath());
        System.out.println("⽬录构造路径:" + f2.getPath());
        System.out.println("⽬录名称:" + f2.getName());
        System.out.println("⽬录⻓度:" + f2.length());
    }
}
输出结果：
⽂件绝对路径:d:\aaa\bbb.java
⽂件构造路径:d:\aaa\bbb.java
⽂件名称:bbb.java
⽂件⻓度:636字节
⽬录绝对路径:d:\aaa
⽬录构造路径:d:\aaa
⽬录名称:aaa
⽬录⻓度:4096
```
文件路径:
 绝对路径: C:\\Users\\xx\\Desktop\\note.txt     /Users/XX/Desktop/note.txt
 相对路径: 相对参数值(当前目录) 不确定的
 . 当前目录
 .. 上一级目录
 通过相对路径, 获得程序中的文件目前对应的绝对路径
 类路径: java文件 -> 编译class文件 -> 运行
 程序src目录编译后的文件夹, 目录结构和src完全相同

\# 相对的是工作目录 File file = new File("hello.txt") 
\# 相对的是class文件所在的根目录 URL resource = ClassPathDemo.class.getResource("/"); 
\# 相对的是ClassPathDemo.class所在的目录 URL resource = ClassPathDemo.class.getResource("a/b/c"); 
\# 相对的是class文件所在的根目录，并且一定不能加斜杠 URL resource = ClassPathDemo.class.getClassLoader().getResource("hello.txt");

 windows操作系统: 文件a 目录a 文件A -> 同时存在
 linux操作系统: 文件a 目录a 文件A -> 三选一

判断功能的方法
```
public class FileIs {
    public static void main(String[] args) {
        File f = new File("d:\\aaa\\bbb.java");
        File f2 = new File("d:\\aaa");
        // 判断是否存在
        System.out.println("d:\\aaa\\bbb.java 是否存在:" + f.exists());
        System.out.println("d:\\aaa 是否存在:" + f2.exists());
        // 判断是⽂件还是⽬录
        System.out.println("d:\\aaa ⽂件?:" + f2.isFile());
        System.out.println("d:\\aaa ⽬录?:" + f2.isDirectory());
    }
}
输出结果：
d:\aaa\bbb.java 是否存在:true
d:\aaa 是否存在:true
d:\aaa ⽂件?:false
d:\aaa ⽬录?:true
```

创建删除功能
```
public class FileCreateDelete {
    public static void main(String[] args) throws IOException {
        // ⽂件的创建
        File f = new File("aaa.txt");
        System.out.println("是否存在:" + f.exists()); // false
        System.out.println("是否创建:" + f.createNewFile()); // true
        System.out.println("是否存在:" + f.exists()); // true

        // ⽬录的创建
        File f2= new File("newDir");
        System.out.println("是否存在:" + f2.exists()); // false
        System.out.println("是否创建:" + f2.mkdir()); // true
        System.out.println("是否存在:" + f2.exists()); // true
        // 创建多级⽬录
        File f3= new File("newDira\\newDirb");
        System.out.println(f3.mkdir()); // false
        File f4= new File("newDira\\newDirb");
        System.out.println(f4.mkdirs()); // true
        // ⽂件的删除
        System.out.println(f.delete()); // true
        // ⽬录的删除
        System.out.println(f2.delete()); // true
        System.out.println(f4.delete()); // false
    }
}
```

目录的遍历
```
public String[] list() 返回一个String数组，表达该File目录中的所有子文件或目录
public File[] listFiles() 返回一个File数组，表示该File目录中的所有子文件或目录
```

```
public class FileFor {
    public static void main(String[] args) {
        File dir = new File("d:\\java_code");
        // 获取当前⽬录下的⽂件以及⽂件夹的名称。
        String[] names = dir.list();
        for (String name : names) {
            System.out.println(name);
        }
        // 获取当前⽬录下的⽂件以及⽂件夹对象，只要拿到了⽂件对象，那么就可以获取更多信息
        File[] files = dir.listFiles();
        for (File file : files) {
            System.out.println(file);
        }
    }
}
```

### 2.文件过滤器

java,io,FileFilter是一个接口，FIle的过滤器
listFiles(FileFilter) 作为参数
boolean accept(File pathname) pathname是否包含在当前目录中
```
public class DiGuiDemo4 {
    public static void main(String[] args) {
        File dir = new File("D:\\aaa");
        printDir2(dir);
    }
    public static void printDir2(File dir) {
        // 匿名内部类⽅式,创建过滤器⼦类对象
        File[] files = dir.listFiles(new FileFilter() {
          @Override
          public boolean accept(File pathname) {
                return pathname.getName().endsWith(".java") || pathname.isDirectory();
            }
        });
        // 循环打印
        for (File file : files) {
            if (file.isFile()) {
                System.out.println("⽂件名:" + file.getAbsolutePath());
            } else {
                printDir2(file);
            }
        }
    }
}
```
lambda简化
```
()->{ }
```

```
public static void printDir3(File dir) {
    // lambda的改写
    File[] files = dir.listFiles(f ->{
        return f.getName().endsWith(".java") || f.isDirectory();
    });
    // 循环打印
    for (File file : files) {
        if (file.isFile()) {
            System.out.println("⽂件名:" + file.getAbsolutePath());
        } else {
            printDir3(file);
        }
    }
}
```

### 3.IO

![[./_resources/JAVA梳理11(文件操作，IO流).resources/msedge_25jVmPqfkx.png]]![[./_resources/JAVA梳理11(文件操作，IO流).resources/msedge_EjUmcPRzPn.png]]

### 4.字节流

```
java.io.OutputStream
public void close() 关闭此输出流并释放与此流相关联的任何系统资源
public void flush() 刷新此输出流并强制任何缓冲的输出字节被写出
public void write(byte[] b) 将b.length字节从指定的字节数组写入此输出流
public void write(byte[] b，int off,int len) 从指定字节数组写入len字节，从偏移量off开始输出到此输出流
public abstract void write(int b) 将指定的字节输出流
```
tips:完成流操作时，必须close()，释放系统资源

FileOutputStream类
构造
```
public class FileOutputStreamConstructor throws IOException {
    public static void main(String[] args) {
        // 使⽤File对象创建流对象
        File file = new File("a.txt");
        FileOutputStream fos = new FileOutputStream(file);
        // 使⽤⽂件名称创建流对象
        FileOutputStream fos = new FileOutputStream("b.txt");
    }
}
```

写出字节数据
```
public class FOSWrite {
    public static void main(String[] args) throws IOException {
        // 使⽤⽂件名称创建流对象
        FileOutputStream fos = new FileOutputStream("fos.txt");
        // 写出数据
        fos.write(97); // 写出第1个字节
        fos.write(98); // 写出第2个字节
        fos.write(99); // 写出第3个字节
        // 关闭资源
        fos.close();
    }
}
输出结果：
abc

public class FOSWrite {
    public static void main(String[] args) throws IOException {
        // 使⽤⽂件名称创建流对象
        FileOutputStream fos = new FileOutputStream("fos.txt");
        // 字符串转换为字节数组
        byte[] b = "abcde".getBytes();
        // 写出从索引2开始，2个字节。索引2是c，两个字节，也就是cd。
        fos.write(b, 2, 2);
        // 关闭资源
        fos.close();
    }
}
输出结果：
cd
```
数据追加续写
true表示追加数据，false表示清空原有数据
public FileOutputStream(File file,boolean append)
public FileOutputStream(String name,boolean append)
```
public class FOSWrite {
    public static void main(String[] args) throws IOException {
        // 使⽤⽂件名称创建流对象
        FileOutputStream fos = new FileOutputStream("fos.txt"，true);
        // 字符串转换为字节数组
        byte[] b = "abcde".getBytes();
        // 写出从索引2开始，2个字节。索引2是c，两个字节，也就是cd。
        fos.write(b);
        // 关闭资源
        fos.close();
    }
}
⽂件操作前：cd
⽂件操作后：cdabcde
```
Tips:回车符\\r和换行符\\n

* 回车符：回到一行开头
* 换行符：下一行

windows \\r\\n
liunx \\n
FileInputStream类
构造
```
public class FileInputStreamConstructor throws IOException{
    public static void main(String[] args) {
        // 使⽤File对象创建流对象
        File file = new File("a.txt");
        FileInputStream fos = new FileInputStream(file);
        // 使⽤⽂件名称创建流对象
        FileInputStream fos = new FileInputStream("b.txt");
    }
}
```

读取字节数据
```
public class FISRead {
    public static void main(String[] args) throws IOException{
        // 使⽤⽂件名称创建流对象
        FileInputStream fis = new FileInputStream("read.txt");
        // 读取数据，返回⼀个字节
        int read = fis.read();
        System.out.println((char) read);
        read = fis.read();
        System.out.println((char) read);
        read = fis.read();
        System.out.println((char) read);
        read = fis.read();
        System.out.println((char) read);
        read = fis.read();
        System.out.println((char) read);
        // 读取到末尾,返回-1
        read = fis.read();
        System.out.println( read);
        // 关闭资源
        fis.close();
    }
}
输出结果：
a
b
c
d
e
-1
```
Tips:读取字节自动提升为int类型

### 5.字符流

字符输入流Reader
FileReader类
构造时用系统默认的字符编码和默认字节缓冲区(一个字节数组，临时存储字节数据)
构造方法
```
public class FileReaderConstructor throws IOException{
    public static void main(String[] args) {
        // 使⽤File对象创建流对象
        File file = new File("a.txt");
        FileReader fr = new FileReader(file);
        // 使⽤⽂件名称创建流对象
        FileReader fr = new FileReader("b.txt");
    }
}
```
读取字符数据
```
//
read()每次读取一个字符，提升为int类型，读到末尾返回-1
public class FRRead {
    public static void main(String[] args) throws IOException {
        // 使⽤⽂件名称创建流对象
        FileReader fr = new FileReader("read.txt");
        // 定义变量，保存数据
        int b;
        // 循环读取
        while ((b = fr.read()) != -1) {
        System.out.println((char)b);
        }
        // 关闭资源
        fr.close();
    }
}
输出结果：
程
序
员
//read(char[] cbuf)每次读b的长度个字符到数组，返回读到有效的字符个数，读到末尾返回-1
public class FRRead {
    public static void main(String[] args) throws IOException {
        // 使⽤⽂件名称创建流对象
        FileReader fr = new FileReader("read.txt");
        // 定义变量，保存有效字符个数
        int len;
        // 定义字符数组，作为装字符数据的容器
        char[] cbuf = new char[2];
        // 循环读取
        while ((len = fr.read(cbuf)) != -1) {
            System.out.println(new String(cbuf));
        }
        // 关闭资源
        fr.close();
    }
}
输出结果：
程序
员序
```
字符输出流Writer
FileWriter类
构造方法
```
public class FileWriterConstructor {
    public static void main(String[] args) throws IOException {
        // 使⽤File对象创建流对象
        File file = new File("a.txt");
        FileWriter fw = new FileWriter(file);
        // 使⽤⽂件名称创建流对象
        FileWriter fw = new FileWriter("b.txt");
    }
}
```
写出数据
```
public class FWWrite {
    public static void main(String[] args) throws IOException {
        // 使⽤⽂件名称创建流对象
        FileWriter fw = new FileWriter("fw.txt");
        // 写出数据
        fw.write(97); // 写出第1个字符
        fw.write('b'); // 写出第2个字符
        fw.write('C'); // 写出第3个字符
        fw.write(30000); // 写出第4个字符，中⽂编码表中30000对应⼀个汉字。
        /*
        *【注意】关闭资源时,与FileOutputStream不同。
        * 如果不关闭,数据只是保存到缓冲区，并未保存到⽂件。
        */
        // fw.close();
    }
}
输出结果：
abC⽥
```

存在内置缓冲区，如果不关闭输出流，无法写出字符到文件中；关闭流对象，是无法继续写出数据的。想写出数据，又想继续使用流，就需要flush方法。
flush:刷新缓冲区，流对象可以继续使用
close:先刷新缓冲区，然后通知系统释放资源
```
public class FWWrite {
    public static void main(String[] args) throws IOException {
        // 使⽤⽂件名称创建流对象
        FileWriter fw = new FileWriter("fw.txt");
        // 写出数据，通过flush
        fw.write('刷'); // 写出第1个字符
        fw.flush();
        fw.write('新'); // 继续写出第2个字符，写出成功
        fw.flush();
        // 写出数据，通过close
        fw.write('关'); // 写出第1个字符
        fw.close();
        fw.write('闭'); // 继续写出第2个字符,【报错】java.io.IOException: Stream closed
        fw.close();
    }
}
```
写出字符数组
```
public class FWWrite {
    public static void main(String[] args) throws IOException {
        // 使⽤⽂件名称创建流对象
        FileWriter fw = new FileWriter("fw.txt");
        // 字符串转换为字节数组
        char[] chars = "程序员".toCharArray();
        // 写出字符数组
        fw.write(chars); // 程序员
        // 写出从索引1开始，2个字符。索引1是'序'，两个字符，也就是'序员'。
        fw.write(b, 2, 2); // 序员
        // 关闭资源
        fos.close();
    }
}
```
写出字符串
```
public class FWWrite {
    public static void main(String[] args) throws IOException {
        // 使⽤⽂件名称创建流对象
        FileWriter fw = new FileWriter("fw.txt");
        // 字符串
        String msg = "程序员";
        // 写出字符数组
        fw.write(msg); //程序员
        // 写出从索引1开始，2个字符。索引1是'序'，两个字符，也就是'序员'。
        fw.write(msg, 2, 2); // 序员
        // 关闭资源
        fos.close();
    }
}
```
续写换行同FileOutputStream

