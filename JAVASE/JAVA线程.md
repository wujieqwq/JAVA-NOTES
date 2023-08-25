---





---

# JAVA线程


1.多线程
1.1并发与并行

* 并发：指两个或多个事件在同一个时间段内发生
* 并发：指两个或多个事件在同一时刻发生（同时发生）

![[./_resources/JAVA线程.resources/msedge_sOEOHlUd3z.png]]
1.2线程与进程

* 进程：是指一个内存中运行的应用程序，每个进程都有一个独立的内存空间，一个应用程序可以同时运行多个线程；进程也是程序的一次执行过程，是系统运行程序的基本单位；系统运行一个程序即是一个进程从创建、运行到消亡的过程。
* 线程：线程是进程中的一个执行单元，责任当前进程中程序的执行，一个进程中至少有一个线程。一个进程中是可以有多个线程，这个应用程序也可以称之为多线程程序。

一个程序运行后至少有一个进程，一个进程中可以包含多个线程

线程调度

* 分时调度

				所有线程轮流使用CPU的使用权，平均分配每个线程占用CPU时间

* 抢占式调度

				优先让优先级高的线程使用CPU，如果线程优先级相同，会随机选择一个
				

1.3创建线程类
java.lang.Thread
1.定义Thread类的子类，重写run()方法，run()的方法体代表该线程需要完成的任务
2.创建Thread子类的实例，即线程对象
3.调用线程对象的start()方法启动该线程
线程类
```
public class MyThread extends Thread {
    // 定义指定线程名称的构造⽅法
    public MyThread(String name) {
        // 调⽤⽗类的String参数的构造⽅法，指定线程的名称
        super(name);
    }
    /**
    * 重写run⽅法，完成该线程执⾏的逻辑
    */
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
        System.out.println(getName() + "：正在执⾏！" + i);
        }   
    }
}
```
测试类
```
public class Demo01 {
    public static void main(String[] args) {
        // 创建⾃定义线程对象
        MyThread mt = new MyThread("新的线程！");
        // 开启新线程
        mt.start();
        // 在主⽅法中执⾏for循环
        for (int i = 0; i < 10; i++) {
            System.out.println("main线程！" + i);
        }
    }
}
```
多线程原理
```
public class MyThread extends Thread {
    /*
    * 利⽤继承中的特点
    * 将线程名称传递 进⾏设置
    */
    public MyThread(String name) {
        super(name);
    }
    /*
    * 重写run⽅法
    * 定义线程要执⾏的代码
    */
    public void run() {
        for (int i = 0; i < 20; i++) {
            //getName()⽅法 来⾃⽗亲
            System.out.println(getName() + i);
        }
    }
}
```

```
public class Demo {
    public static void main(String[] args) {
        System.out.println("这⾥是main线程");
        MyThread mt = new MyThread("⼩强");
        mt.start(); // 开启了⼀个新的线程
        for (int i = 0; i < 20; i++) {
            System.out.println("旺财:" + i);
        }
    }
}
```

![[./_resources/JAVA线程.resources/msedge_7BGE6BeWJ8.png]]![[./_resources/JAVA线程.resources/msedge_EJU9GhZHve.png]]
Thread类
```
构造方法
public Thread()：分配一个新的线程对象
public Thread(String name)：分配一个指定名字的线程对象
public Thread(Runnable target)：分配一个带有指定目标新的线程对象
public Thread(Runnable target,String name)：分配一个带有指定目标新的对象并指定名字

常用方法
public String getName()：获取当前线程名称
public void start()：导致此线程开始执行，jvm调用此线程run方法
public void run()：此线程要执行的任务
public static void sleep(long millis)：使当前正在执行的线程以指定的毫秒数暂停(暂停停止执行)
public static Thread currentThread()：返回对当前正在执行的线程对象的引用
```

1.5创建线程方式二
java.lang.Runnable 重写run方法
1.实现Runnable接口的实现类，并重写该接口的run()方法，该run()方法的方法体同样是该线程的线程知兴体
2.创建Runnable实现类的实例，并以此实例作为Thread的target来创建Thread对象，该Thread对象才是真正的线程对象
3.调用线程对象的start()方法来启动线程
```
public class MyRunnable implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            System.out.println(Thread.currentThread().getName() + " " + i);
        }
    }
}
```

```
public class Demo {
    public static void main(String[] args) {
        // 创建⾃定义类对象 线程任务对象
        MyRunnable mr = new MyRunnable();
        // 创建线程对象
        Thread t = new Thread(mr, "⼩强");
        t.start();
        for (int i = 0; i < 20; i++) {
          System.out.println("旺财 " + i);
        }
    }
}
```

### 1.6.Thread和Runnable的区别

如果一个类继承Thread，则不适合资源共享。但是如果实现了Runnable接口的话，则容易实现资源共享。
Runnable接口的优势
1.适合多个相同的程序代码的线程去共享同一个资源
2.可以避免java中的单继承局限性
3.增加程序的健壮性，实现解耦操作，代码可以被多个线程共享，代码和线程独立
4.线程池只能放入实现Runnable或Callable类线程，不能直接放入继承Thread的类
Tips：java中，每次程序运行至少启动2个线程。一个main，一个垃圾收集线程。每当java命令执行一个类的时候，实际上都会启动一个JVM,每个JVM在操作系统中启动了一个进程。

### 1.7匿名内部类实现线程创建

```
public class NoNameInnerClassThread {
    public static void main(String[] args) {
        // new Runnable() {
        //    public void run() {
        //        for (int i = 0; i < 20; i++) {
        //            System.out.println("张宇:" + i);
        //        }
        //    }
        // }; //‐‐‐这个整体 相当于new MyRunnable()
        Runnable r = new Runnable() {
            public void run() {
                for (int i = 0; i < 20; i++) {
                    System.out.println("张宇:" + i);
                }
            }
        };
        new Thread(r).start();
        for (int i = 0; i < 20; i++) {
            System.out.println("费⽟清:" + i);
        }
    }
}
```

### 2.线程安全

线程安全问题是由全局变量及静态变量引起的。若每个线程中对全局变量、静态变量只有读操作，一般来说，这个全局变量是线程安全的；若有多个线程同时执行写操作，一般都需要考虑线程同步。

线程同步（synchronized）
三种同步操作

* 同步代码块
* 同步方法
* 锁机制

2.1同步代码块
synchronized关键字可以用于方法中的某个区块中，表示只对这个区块的资源实行互斥访问
```
synchronized(同步锁) {
    需要同步操作的代码
}
```
2.2同步锁
对象的同步锁只是一个概念，可以想象为在对象上标记了一个锁
1.锁对象，可以是任意类型
2.多个线程对象，要使用同一把锁
Tips：在任何时候，最多允许一个线程拥有同步锁，拿到锁就进入代码块，其他线程等待(BLOCKED)
```
public class Ticket implements Runnable {
    private int ticket = 100;
    Object lock = new Object();
    /*
    * 执⾏卖票操作
    */
    @Override
    public void run() {
        // 每个窗⼝卖票的操作
        // 窗⼝ 永远开启
        while (true) {
            synchronized (lock) {
                if (ticket > 0) { // 有票 可以卖
                    // 出票操作
                    // 使⽤sleep模拟⼀下出票时间
                    try {
                        Thread.sleep(50);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    // 获取当前线程对象的名字
                    String name = Thread.currentThread().getName();
                    System.out.println(name + "正在卖: " + ticket‐‐);
                }
            }
        }
    }
}
```
2.3同步方法
同步方法：使用synchronized修饰的方法，为同步方法，保证A线程执行该方法的时候，其他线程只能等待
```
public synchronized void method() {
    可能会产⽣线程安全问题的代码
}
```

```
public class Ticket implements Runnable {
    private int ticket = 100;
    /*
    * 执⾏卖票操作
    */
    @Override
    public void run() {
        // 每个窗⼝卖票的操作
        // 窗⼝ 永远开启
        while (true) {
            sellTicket();
        }
    }
    /*
    * 锁对象 是 谁调⽤这个⽅法 就是谁
    * 隐含 锁对象 就是 this
    */
    public synchronized void sellTicket() {
        if (ticket > 0) { // 有票 可以卖
        // 出票操作
        // 使⽤sleep模拟⼀下出票时间
        try {
            Thread.sleep(100);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        // 获取当前线程对象的名字
        String name = Thread.currentThread().getName();
        System.out.println(name + "正在卖:" + ticket‐‐);
        }
    }
}
```
2.4Lock锁
java.util.concurrent.Locks.Lock提供了更广泛的锁定操作
```
public void lock()  加同步锁
public void unlock() 释放同步锁
```

```
public class Ticket implements Runnable {
    private int ticket = 100;
    Lock lock = new ReentrantLock();
    /*
    * 执⾏卖票操作
    */
    @Override
    public void run() {
        // 每个窗⼝卖票的操作
        // 窗⼝ 永远开启
        while (true) {
            lock.lock();
            if (ticket > 0) { // 有票 可以卖
            // 出票操作
            // 使⽤sleep模拟⼀下出票时间
            try {
                Thread.sleep(50);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            // 获取当前线程对象的名字
            String name = Thread.currentThread().getName();
            System.out.println(name + "正在卖:" + ticket‐‐);
            }
            lock.unlock();
        }
    }
}
```

### 3.线程状态

线程生命周期
![[./_resources/JAVA线程.resources/msedge_YQtGRfpTn1.png]]

