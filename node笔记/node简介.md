# node简介
- node.js是一个让JavaScript运行在服务器端的开发平台
-== node.js不是一种独立的语言==。与PHP,JSP,Python等“既是语言，也是平台”不同。它使用JavaScript进行编程。
- node.js不用建设在任何服务器之上。
### Node.js的特点
- 单线程
    - 优点：单线程对内容占用很少，而且也不会有  线程创建、取消的时间
    - 缺点：单线程中一个用户崩溃，整个线程其余用户也会崩溃。
- 非阻塞I/O
    - 在阻塞模式下，一个线程只能处理一项任务，要想提高吞吐量必须使用多线程。
    - 在非阻塞模式下，一个线程永远在进行计算，这个线程的CPU核心利用率永远是100% 
- 事件驱动
    - 在Node中，在一个时刻，只能执行一个事件回调函数。但是在执行这个回调函数的途中，可以转而执行其他事件。然后再执行原事件的回调函数。

## 一个简单的node.js
```
helloWorld.js
//require表示引包，引包就是引用自己的一个功能，内似与c预言中的#include stadio.h
var http = require("http");
//创建服务器，参数是一个回掉函数，表示如果有什么请求进来，要做什么
var server = http.createServer(function(req,res){
    //req表示请求，request; res表示响应，response
    //设置HTTP头部，状态码是200，文件类型是html,字符集是utf-8
    res.writeHead(200,{"Content-type":"text/html;charset=utf-8"});
    res.end("hello node.js");
})
//监听服务器
server.listen(8080);
```
## node.js没有根目录概念
它根本没有任何web容器，无法把静态页面放在node中。

根据你自己写得require('http')创建的服务器访问你的html页面（reddivNode.js），无法从网址判断html页面存在电脑的那个文件夹。（node.js无web容器）;

node服务器访问的URL与实际的文件的物理地址其实是没关系的

## node传递静态页面。
需要结合使用require('http'),require('fs')
```
createServer(function(req,res){
    fs.writeHead(function(err,data){
        
    })
})
```
