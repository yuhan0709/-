# mongodb的安装
1. 配置环境变量
2. 一些命令
- mongo 使用数据库
- mongod 开机
- mongoimport 导入数据

## 开机
```
mongod --dbpath c:\mongo  // (开机,后面跟的是数据库的地址)

//dbpath 指的是数据库真实存在的位置
//以ns结尾的就是mongo的真实可见的数据库

```
## 使用数据库

**注意，一定要保持数据库是开机状态,所以最好新开一个cmd使用数据库**
```
直接输入mongo命令来链接数据库
```
### 命令行中mongo命令
1. show dbs :列出所有数据库
2. use 数据库名字：使用某个数据库
3. use 一个不存在的数据库：新建数据库
4. db: 查看当前所在数据库
5. db.一个位置的集合名字，这个集合将自动创建
```
 db.student.insert({"name":"xiaoming","age":"10","sex":"nan"})
//插入数据，其实就是插入json数据
//student相当于一个集合，集合中存储很多json
```
6. show collections：可以列出当前的集合
7. db.集合名字.find()：可以查看集合中的数据，也可以查询
```
db.student.find({"name":"yyh","age":17}) //查询条件
```
8. db.集合名字.insert()：插入数据

## 集合中的数据操作命令
[mongoDB教程](http://www.runoob.com/mongodb/mongodb-tutorial.html)
### 导入数据
直接导入多个json对象

可以现在外部写好json文件
```
例如在外部写好一个文件 db.json
在命令行中输入
mongoimport --db itcast --collection student --drop --file C:\Users\admin\Desktop\前端学习\node\db.json
```
其中

- --db itcast: 指的是数据库名字（本例是itcast)
- --collection student: 指的是数据库中集合的名字（本例是student)
- --drop 是清除集合中原有数据
- --file filepath :指的是导入的json文件的位置

---

### 查询条件
- 大于：(greater than)
```
db.student.find({"score.yuwen":{$gt:90}})
//查询语文成绩大于90的同学
```
- 大于或等于（>=） (greater than equal)
```
db.student.find({"score.yuwen":{$gte:90}})
```
- 小于 (less than)
```
db.student.find({"score.shuxue":{$lt:80}})
//查询数学成绩小于80分的同学
```
- 小于或等于（<=） (less than equal)

```
db.student.find({"score.shuxue":{$lte:80}})
```
- 等于 (equal)
```
db.student.find({"score.shuxue":{$eq:80}})
//查询数学成绩等于80的同学
```
- 不等于 (not equal)
```
db.student.find({"score.shuxue":{$ne:80}})
```
- 或查询
```
db.student.find({$or:[{"age":17},{"age":20}]})
//查询年龄为17岁或者20岁的同学

//若在可视化工具里可以按下面方法写：
db.student.find(
   {
      $or: [
         {key1: value1}, {key2:value2}
      ]
   }
)
```
- 且查询
```
db.student.find(
    {
        "score.yuwen":{$gt:85},
        "age":20
    }
)
```
---
### 排序
- (1升-1降)
```
db.student.find().sort({"score.yuwen":-1,"age":1})
//语文成绩降序，年龄升序
```

---
### 修改（更行）数据
```
db.col.update({'title':'MongoDB 教程'},{$set:{'title':'MongoDB'}})

//例子：把姓名为yyh的同学的语文成绩改为100
db.student.update({'name':'yyh'},{$set:{'score.yuwen':100}},{mutil:true})
//一般更新只会匹配一条数据，如果修改多条数据则需要把mutil的值设置为true
```
---
### 删除数据
```
db.student.remove({"score.shuxue":{$gt:80}})
//删除数学成绩大于80的学生

db.student.remove({"score.shuxue":{$gt:80}},{justOne:true})
//只删除一个数学成绩大于80的学生

db.student.remove({})
//删除一个集合的所有的数据
```
---
### 查询数据信息
```
db.student.stats()
```
