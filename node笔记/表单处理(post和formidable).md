## post表单处理
案例：
```
var http = require("http");
var query = require("querystring");
var alldata = "";
var server = http.createServer(function(req,res){
    if(req.url=="/check"&&req.method.toLowerCase()=="post") {
        req.addListener("data",function (chunk) {
            alldata += chunk;
        })
    }
    req.addListener("end",function(){
        var dataString  = alldata.toString();
        res.end("success");
        //console.log(dataString);
        var OBJ = query.parse(dataString);
        console.log(OBJ);
        console.log(OBJ.username);
       console.log(OBJ.sex);
        for(var i=0;i<OBJ.hobby.length;i++){
            console.log(OBJ.hobby[i]);
       }
    })
})
server.listen(8000,"127.0.0.1");
```
post所发送的数据会被分成一小块一小块的==chunk==进行接受，这体现了node的==非阻塞IO==的特点

Node.js会将POST数据拆分成很多小的数据块，然后通过触发特定的事件，将这些小数据块传递给回调函数。这里的特定的事件有data事件（表示新的小数据块到达了）以及end事件（表示所有的数据都已经接收完毕）。”

[http://nodejs.cn/api/querystring.html](http://note.youdao.com/) （查看nodejs开发文档）

这里queryString模块的parse方法用于把字符串解析成为键值对的形式。

## formidable
[https://www.npmjs.com/package/formidable](http://note.youdao.com/) 

formidable也是用于解析表单，尤其是文件上传

==注意== 当涉及到上传文件的时候，form表单里一定要加上 enctype="multipart/form-data"
```
    <form action="http://localhost:8000/check" method="post" enctype="multipart/form-data">
```

### formidable的安装
- npm install formidable  -g下载formidable;
- var formidable=require formidable

### formidable中的一些方法
- 创建一个新的上传表单（Create a new Incoming form）
```
var form = formidable.IncomingForm();

```
- 设置表单域的编码格式
```
from.encoding = "utf-8";
```
- 设置上传文件的路径
```
form.uploadDir = "/my/dir";
```
- 设置该属性为true可以使得上传的文件保持原来的文件的扩展名
```
form.keepExtension = fales;
```
更多方法可以看开发文档

