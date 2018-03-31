## 通过案例了解http模块
```
//引用模块
var http = require('http');
//创建一个服务器，回调函数表示接收到请求之后做的事情
var server = http.createServer(function(req,res){
    //req参数表示请求，res表示响应
    //设置一个响应头(纯文本为text/plain)
    res.writeHead('200',"Content-Type":"text/html;charset = UTF-8");
    //这两个语句相等。但第一种用的比较多。
    res.setHeader("Content-Type","text/html");
    res.write("可以在这里写语句，会在服务器显示"); //end结束之后不能再写write语句。
    res.end(""); //必须要在createServer中加入end（结束请求）
    //http里的end必须写字符串格式。（可用toString()方法转换成为字符串）
})
//监听端口
端口号，访问路径
server.listen(3000,"127.0.0.1")
```
## http中req（request）里面能够使用的东西
最关键的就是**req.url属性**，表示用户请求的URL地址

所有的路由设计，都是通过req.url来实现的。
```
var http = require('http');
var server = http.createSever(function(req,res){
    console.log(req.url);
    res.end();
})
server.listen(8080);
```
运行之后，网址输入"localhost:8080"    //输出/

输入localhost:8080/img       //输出/img

输入loaclhost:8080/img#abc?id=123  //输出/img   (无法访问#之后的内容，除此之外都可以)

### 如何识别req.url
识别URL用到两个新模块。
- url模块
- querystring模块
    - querystring.parse(string);  接受一个查询字符串返回一个对象
    ```
    querysring.parse('foo=bar&baz=qux&baz=quux&corge');
    retuen //{foo:'bar',baz:['qux','quxx'],corge:''}
    ```
    - querystring.stringfy()；等方法（可去查帮助手册）

再用URL的parse()方法把一个完整的路径拆分成很多方法（查看帮助手册）