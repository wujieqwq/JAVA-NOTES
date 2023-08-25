---





---

# JAVASE回顾2 IO层级


1.java.io.File类
		是文件和目录路径名的抽象表示，主要用于文件和目录的创建，查找和删除
		判断方法

* exits()
* isDirectory()
* isFile()

		创建删除

* boolean createNewFile()
* boolean delete() 如果删除目录则目录必须为空
* boolean mkdir()
* boolean mkdirs()

		目录遍历

* String\[\]  list()
* File\[\]  listFiles()

2.IO
		顶层父类
![[./_resources/JAVASE回顾2_IO层级.resources/msedge_QdPo6P7SAk.png]]

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
|     | 1.基础子类<br>构造器传FIle或文件名 | 2.缓冲流，构造器传1或3 | 3.转换流，构造器传1的字节流<br>指定字符编码 | 4.序列化<br>构造器传1 | 5.打印流<br>顶层java.io.PrintStream<br>构造器传文件名或1或3 |
| 字节输入 | FileInputStream | BufferedInputStream |     | ObjectInputStream |     |
| 字节输出 | FileOutputStream<br>可指定是否向文件中继续添加内容 | BufferedOutputStream |     | ObjectOutputStream |     |
| 字符输入 | FileReader<br>读取字符自动升为int | BufferedReader | InputStreamReader |     |     |
| 字符输出 | FileWriter<br>有缓冲区 | BufferedWriter | OutputStreamWriter |     | PrintStream<br>可指定自动刷新缓冲流和字符编码 |

