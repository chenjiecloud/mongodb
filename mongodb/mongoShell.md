#　运行MongoDbB服务端：
- windows安装好MongoDB数据库后，启动服务的命令为：mongod
- 执行mongod，你会发现服务并没有启动，报了一个exception，服务停止了
- 新建文件夹：出息上边的错误，是因为我们没有简历mongodb需要的文件夹，一般是安装盘的跟目录，建立data/db，这两个文件
- 运行mongod：这时候服务就可以开启了，链接默认端口是27017

- 查看存在数据库命令：show dbs
- 查看数据库版本命令：db.version()

# mongo基本命令：
```mongodb
var x = print('hello world')
print(x)

<!-- 还可以定义函数 -->
function calc() {
    return 10
}
```
- 很像javaScript的语法

- show dbs：显示已有数据库，如果你刚安装好，会默认有local、admin(config)，这是MongoDB的默认数据库，我们在新建库时是不允许起这些名称的。
- use admin： 进入数据，也可以理解成为使用数据库。成功会显示：switched to db admin。
- show collections：显示数据库中的集合（关系型中叫表，我们要逐渐熟悉）。
- db：显示当前位置，也就是你当前使用的数据库名称，这个命令算是最常用的，因为你在作任何操作的时候都要先查看一下自己所在的库，以免造成操作错误。

## 数据操作基础命令：
- use db(建立数据库)：use不仅可以进入一个数据库，如果你敲入的库不存在，它还可以帮你建立一个库。但是在没有集合前，它还是默认为空。
- db.集合.insert()：新建数据集合和插入文件（数据），当集合没有时，这时候就可以新建一个集合，并向里边插入数据。Demo：db.user.insert({'name':'hello'})
- db.集合.find()：查询所有数据，这条命令会列出集合下的所有数据，可以看到MongoDB是自动给我们加入了索引值的。Demo：db.user.find()
- db.集合.findOne()：查询第一个文件数据，这里需要注意的，所有MongoDB的组合单词都使用首字母小写的驼峰式写法。
- db.集合.update({查询}, {修改})：修改文件数据，第一个是查询条件，第二个是要修改成的值。这里注意的是可以多加文件数据项的，比如下面的例子。
```mongodb
db.user,update({'name': 'Asaki'}, {'name': 'Asaki1', 'age': '18'})
```
- db.集合.remove(条件)：删除文件数据，注意的是要跟一个条件。Demo:db.user.remove({'name': 'asaki'})
- db.集合.drop()：删除整个集合，这个在实际工作中一定要谨慎使用，如果是程序，一定要二次确认。
- db.dropDatabase()：删除整个数据库，在删除库时，一定要先进入数据库，然后再删除。实际工作中这个基本不用，实际工作可定需要保留数据和痕迹的。

## MongoDB的存储结构：
- 关系型数据库的数据结构都是顶层是库，库下面是表，表下面是数据。但是MongoDB有所不同，库下面是集合，集合下面是文件，可以看下面这张图进行了解一下。
![MongoDB的存储结构](http://59.110.165.66/static/upload/20180824/j1ZWi5on7n8hoDodtVFt.png) 
## 用js写mongo命令：
#### 现在模拟一个用户登录日志表的信息，用JS进行编写。新在一个新建的目录下，比如D:/mongoShell/，新建一个goTask.js文件。文件内容如下：
- goTask.js
```javaScript
var userName = 'Asaki';      // 声明一个登录名
var timeStamp = Date.parse(new Date());     // 声明登录时的时间戳
var jsonDatabase = {'loginUser': userName, 'loginTime': timeStamp};  // 组成JSON字符串
var db = connect('log');    // 链接数据库
db.login.insert(jsonDatabase);  // 插入数据

print('[demo]log print success')    // 没有错误显示成功
```
- 执行js文件
+ mongo goTask.js

## 批量插入的正确方式：