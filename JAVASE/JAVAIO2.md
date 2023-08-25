---





---

# JAVAIO2


IO:
   字节流: InputStream  OutputStream
        FileInputStream
        BufferedInputStream  ->  文件复制
        ObjectInputStream -> 对象序列化, 持久化
   字符流: Reader  Writer
        FileReader
        InputStreamReader
        BufferedReader  PrintWriter  ->  内容读写
   read  write
   print println readLine flush

Properties: extends Hashtable(HashMap)
   key-value: String
   load(reader/inputStream)   getProperty(key)
   store(writer/outputStream) setProperty(key, value)

* * *

文件IO:
  File: listFiles
  路径: 相对路径  绝对路径
  JUnit: 相对值 当前 module
  Main方法: 相对值 当前 工程

IO:
  读: read \* 3
  写: write \* 3

输出流: 如果文件不存在, 就创建新的文件; 文件存在, 默认清空文件写入
      缓冲区(缓存, 硬盘)
输入流: read 方法, 返回-1标志着读到文件末尾

字节流: InputStream  OutputStream: 抽象类
  FileInputStream  FileOutputStream
  缓冲流: BufferedInputStream  BufferedOutputStream

字符流: Reader  Writer
  FileReader  FileWriter -> 只能默认字符集
  转换流: InputStreamReader  OutputStreamWriter
  文件的读写: BufferedReader  PrintWriter

适用场景:
  字节流: 文件复制, 例如: 文件的上传, 文件的下载
          BufferedInputStream BufferedOutputStream
  字符流: 文本文件的内容读写, 字符集 UTF-8 GBK
          BufferedReader PrintWriter

IO流构造器的规律:
  1.传文件名 String 的参数, 都可以替换成 File 对象
  2.流的关系: 字节流 < 字符流
            底层流(字节流, 字符流) < 缓冲流/打印流

对象流: 读写对象
  ObjectInputStream  ObjectOutputStream

    writeObject(): NotSerializableException

    序列化: 对象 -> 字节数组  Serializable: 为了表示可序列化
    反序列化: 字节数组 -> 对象
    经过序列化和反序列化后的对象, 属于深克隆
    需要使用版本号进行类型的匹配 serialVersionUID

属性集: Properties  持久化
    Properties 可保存在流中或从流中加载。属性列表中每个键及其对应值都是一个字符串。
    load(Reader/InputStream)  getProperty(key)
    store(Writer/OutputStream) setProperty(key, value)

异常的处理:
    FileNotFoundException
    IOException
    ClassNotFoundException
    EOFException: 读到文件末尾  End Of File
                  剩余字节数, 不够
                  和read()方法返回 -1 进行区分

