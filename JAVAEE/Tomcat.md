---





---

# Tomcat


### 1.CS与BS

   C/S: TCP/IP
        需要安装客户端, 更新需要重新下载客户端
        实时流量不需要太多, 网络带宽的要求会低很多
   B/S: http https
        不需要安装客户端, 浏览器, 更新服务器端更新同步到客户端
        实时流量很多, 带宽的要求比较高

http协议: 传输数据的规范
http请求: 从客户端发送给服务器的
		可能产生请求的几种方式:

*      直接浏览器输入地址访问
*      form表单提交(method = GET, POST)
*      点击超链接
*      JS来打开新的链接地址
*       跟随一个页面一起访问的js, css, jpg等等资源文件

![[./_resources/Tomcat.resources/msedge_unx0hDi9Yg.png]]
请求字面内容: url地址
      请求数据包含:

* 请求行: 请求方式(GET/POST)  请求地址URI(资源路径)  协议版本
* 请求头: Key-value(map), key是固定的, 值是客户端自行封装的
* (客户端信息)请求体: Post请求的请求参数(相对隐藏)
	* 请求参数: 发送请求的时候, 一起发送给服务器的数据(get请求的请求参数 uri (请求行))

    http响应: 从服务器发送给客户端的

* 响应行: 响应的状态码  http协议版本

				             200 响应成功   304 访问缓存   404 资源未找到
				             405方法不支持  500内部错误 302重定向

*  响应头: key-value(Map) 内容可以由程序员指定 / 由服务器引擎自动封装
* 响应体: 响应内容数据

![[./_resources/Tomcat.resources/chrome_OVI9S775by.png]]

### 2.apache-tomcat

    bin: 命令   startup  shutdown
    conf: 配置文件
    lib: 类库 jar文件
    logs: 日志文件
    webapps: web applications 应用文件夹
             一个文件夹, 就是一个web应用
    work: jsp的运行时产生的文件

    测试启动tomcat成功:http://localhost:8080/

![[./_resources/Tomcat.resources/chrome_NmGwEt6OfX.png]]
访问应用: http://localhost:8080/应用名/资源路径
添加web应用: (部署应用)

*   方式1: webapps里直接创建目录(hello) -> 应用

		        http://localhost:8080/hello
		        缺点: 安装, 卸载 需要重启服务器

*   方式2: 在桌面创建目录(hi), 打包hi.zip, 改名 hi.war

		        将hi.war文件直接放入到webapps中
		        优点: 全程tomcat不需要重启，安装、卸载都是操作war文件
		        缺点: webapps里面位置固定

*   方式3: 随便任意一个文件夹, 修改server.xml配置文件

		        <Context path="/kitty" docBase="应用的目录"/>
		        应用目录:自定义的应用名(虚拟目录)
		        缺点: 安装, 卸载 需要重启服务器
		        访问: http://localhost:8080/kitty(虚拟目录/应用名)

*   方法4: 随便任意一个文件夹, 新建一个xml配置文件

		        位置: conf/Catalina/localhost/xml文件
		        优点: 全程tomcat不需要重启
		        应用目录位置可以自定义
		        访问: http://localhost:8080/xml文件的名字(虚拟目录/应用名)
![[./_resources/Tomcat.resources/msedge_qL6ZANfEqf.png]]

