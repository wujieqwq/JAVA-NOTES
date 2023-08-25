---





---

# ServletResponse


### Java设计模式

		单例模式: 整个应用运行期间，只有一个对象的类，就是单例的。
		web应用的单例: Servlet，ServletContext，DataSource。
		分类:

* 懒汉模式(用时初始化对象)
* 饿汉模式(一开始创建对象)

		弊端: 因为单例模式只有一个对象，多线程的时候，一定是共享的资源，导致线程不安全。
		解决方法:

1. 加锁
2. 成员变量变为方法参数

### 302重定向

特点：
		1.地址栏发生变化
		2.可以访问其他服务器
		3.是两次请求，无法通过request对象来共享数据
```
// 常用的重定向代码  setStatus(302) setHeader("location","")
response.sendRedirect(this.getServletContext().getContextPath() + "/context/get");
```

```
// 响应行的操作, 可以设置状态码
response.setStatus(302); // 302 -> 重定向(又发送了一次请求)
// location固定的key, value: 就是一个资源地址 uri /应用名/资源名
response.setHeader("location", this.getServletContext().getContextPath()+"/context/get");
```

### HttpServletResponse

![[./_resources/ServletResponse.resources/msedge_e88HViYGrO.png]]
方法
设置响应行
状态码
setStatus(int sc)

设置响应头
常见响应头：

1. Content-Type:服务器告诉客户端本次响应体的数据格式及其编码
2. Content-dispositon:服务器告诉客户端以什么格式打开响应体
	* in-line:默认值，当前页面打开
	* attachment;filename=XXX ：以附件形式打开响应体，文件下载
3. location(重定向)

添加
addHeader(String name,String value)
addIntHeader(String name,int value)
addDateHeader(String name,long value)
设置
setHeader(String name,String value)
setDateHeader(String name,long value)
setIntHeader(String name,int value)

设置响应体
getOutputStream()
PrintWriter getWriter() 获得字符流，write()写入到response缓冲区，Tomcat将缓冲区内容组装成Http响应返回给浏览器端
设置缓冲区编码
setCharacterEncoding(String charset)
设置页面编码
中文乱码处理
setContentType("text/html;charset=UTF-8")
```
// 设置response缓冲区的字符集, 默认字符集ISO8859-1
// 缓冲区字符集不代表客户端字符集，最终编码取决于客户端
//response.setCharacterEncoding("UTF-8");

response.setContentType("text/html;charset=utf-8");
```

```
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        String filename = "美女.jpg"; // 以后要下载的文件名是请求参数动态传递

        ServletContext application = this.getServletContext();

        // response是有格式的/文件类型, 如果不设定类型和打开方式, 会自动识别(浏览器自动解析)

        // 先根据要下载的文件名, 获得对应的文件类型

        String mimeType = application.getMimeType(filename);

        // 1.告诉浏览器, 文件类型是什么

        response.setContentType(mimeType); // mime类型 -> 修改的是响应头信息

        // response.setHeader("Content-Type", mimeType);

        // 2.通知浏览器, 文件打开方式是什么 (附件形式打开)

        // 处理中文乱码

        String agent = request.getHeader("User-Agent");

        String name = getFileName(agent, filename);

        response.setHeader("Content-Disposition", "attachment;filename=" + name);

        // URLDecoder  浏览器的解码器

        // URLEncoder  编码器, 将中文 -> %E7

        // 要下载的文件 web/resource/a.mp3

        String filePath = application.getRealPath("/resource/" + filename);

        ServletOutputStream out = response.getOutputStream();

        BufferedInputStream bis = new BufferedInputStream(new FileInputStream(filePath));

        byte[] bs = new byte[1024];

        int i;

        while ((i = bis.read(bs)) != -1) {

            out.write(bs, 0, i);

        }

        bis.close();

    }
```

