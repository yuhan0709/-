## node模块
通俗地说，一个js文件就是一个模块，如果想从一个js文件外使用其中的变量、函数，则需要export对象进行暴露
```
//fo.js
var msg = "你好";
exports.msg=msg

//04.js
var foo = require("fo.js");
console.log(msg);  //"你好"
```
如果想暴露一个类

则用module.export=构造函数名。暴露的这个类视为一个构造函数，可以直接用new 操作符。
```
export.js  (在node_modules的bar文件夹中，并且使用了package.json暴露)
function msg(word){  //这里function是一个类
    this.word=word;
}
msg.prototype = {
    sayHello:function(){   //msg的原型
        console.log(this.word);
    }
}
module.exports = msg;
```
引入这个类
```
var bar = require("bar");
var someword = new bar("你好node.js模块"); //相当于构造函数使用
someword.sayHello();
```

## js与js的两种合作关系
- 一个js提供了变量和函数，则只需要用export暴露。
- 一个js提供了类，则需要module.exports来暴露。

## 模块与文件夹
- 如果文件路径中不加“./”。
        
    那么Node.js将该文件视为node_modules目录下的一个文件

    - 注：==node\_modules==文件夹并不一定在同级目录里面，在任何直接祖先级目录中，都可以。甚至可以放到NODE_PATH环境变量的文件夹中。这样做的好处稍后你将知道：分享项目的时候，不需要带着modules一起给别人。

---

```
var fo = require("bar"); 
```
这时，既没有扩展名（.js）文件路径也没有“./”。node.js会去寻找node\_modules文件夹下的bar文件夹中的==index.js==。

- 但如果你不想用index.js做入口文件这时
```
//07.js
var fo = require("bar");
console.log(msg);

//app.js
var msg = "你好,我想用app.js作为入口文件";
exports.msg = msg;
```
这时，需要再在bar文件夹里写一个package.json文件
```
//package.json
{
    "name":"name",
    "version":"0.0.1",
    "main":"app.js" //在这里写入口文件
}
```