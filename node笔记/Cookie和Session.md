## 关于Cookie

**cookie是在res中设置的,req中读取的**。第一次访问没有cookie

cookie的存储大小有限，kv对儿。对用户可见，用户可以禁用，清除cookie。
```
var express = require('express');
var cookieParser = require('cookie-parser');
var app = express();

//使用cookie必须要使用cookie-parse中间件
app.use(cookieParser());

app.get("/",function(req,res){
//maxAge以毫秒为单位
//发送cookie
    res.cookie('xihao','tfboys',{maxAge:10000,httpOnly:true});
//返回cookie    
    res.send(req.cookies);
    
})
app.listen(3000);
```

## 关于session
Session就是利用cookie,实现的“会话”，就是第一次访问的时候，可以在服务器上为这个用户缓存一些信息

别的用户不能看见，服务器会下发一个密钥（cookie），客户端每次访问都携带这个密钥。

**express中读取还是设置都是在req中**。
```
var express = require("express");
var app();
var session = require("express-session");
app.use(session({
    secret:'keyborad cat',
    resave:false,
    saveUniniy\tialized:true;
}))
app.get("/",function(req,res){
    if(req.session.login){
        res.send("成功登陆");
    }else{
        res.send("尚未登陆");
    }
})
//登陆页面
app.get("/login",function(req,res){
//给浏览器发送session;
    req.session.login = true;
    
})
```