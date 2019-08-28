---
layout: post
title: "Node.js 操作 MongoDB"
date: 2019-08-28
tag: 学习
---



## 1 Native Driver （官方驱动）

### 1.1 安装

```
npm install mongodb --save
```



### 1.2 连接MongoDB服务

#### 示例

```javascript
//导入模块
const MongoClient = require('mongodb').MongoClient;

// 定义 连接url
const url = 'mongodb://localhost:27017';

// 定义数据库
const dbName = 'myproject';

// 连接MongoDB服务器
MongoClient.connect(url, function(err, client) {
  if (err) throw err;
  
  //选择数据库
  const db = client.db(dbName);

  client.close();
});
```

#### 连接需要验证的服务

```javascript
//导入模块
const MongoClient = require('mongodb').MongoClient;
const util = require('util');

//声明用户名 密码
const user = encodeURIComponent('dave');
const password = encodeURIComponent('abc123');

// 定义 URL
const url = util.format('mongodb://%s:%s@localhost:27017/',
  user, password);

// 连接服务
MongoClient.connect(url, function(err, client) {
  if (err) throw err;
  
  //选择数据库
  const db = client.db(dbName);
    
  client.close();
});
```



### 1.3 集合操作

#### 创建集合

```javascript
db.createCollection(coolName, { "capped": true, "size": 100000, "max": 5000},
    function(err, results) {
      if (err) throw err;
      //results 是表示集合的对象
      console.log("集合创建成功.");
    }
);
```

#### 删除集合

```Javascript
db.dropCollection(coolName, (err, result) => {
    if (err) throw err;
    console.log('删除成功');
})
```



### 1.4 CURD 增删改查 （Create Update Retrieve Delete）

#### 1.4.1 添加文档

```javascript
// 添加一条文档
db.collection('collName').insertOne({a:1}, function(err, r) {
    if (err) throw err;
    console.log(r.insertedCount);
});

// 添加多条文档
db.collection('collName').insertMany([{a:2}, {a:3}], function(err, r) {
    if (err) throw err;
    console.log(r.insertedCount);
});
```

* MongoDB 会自动创建集合



#### 1.4.2 更新文档

```javascript
const col = db.collection('collName');

//更新一条文档
col.updateOne({a:3}, {$set: {b: 1}}, {
     upsert: true
 }, function(err, r) {
     if (err) throw err;
     console.log(r.matchedCount);
     console.log(r.upsertedCount);
 });

//更新多条文档
  col.updateMany({a:2}, {$set: {b: 1}}, function(err, r) {
        if (err) throw err;
        console.log(r.matchedCount);
        console.log(r.modifiedCount);
  })

```

#### 1.4.3 删除文档

```javascript
const col = db.collection('collName');

//删除一条文档
col.deleteOne({a:1}, function(err, r) {
    if (err) throw err;
    console.log(r.deletedCount);
});

// 删除多条文档
col.deleteMany({a:2}, function(err, r) {
    if(err) throw err;
    console.log(r.deletedCount);
});
```

#### 1.4.4 查询文档

```javascript
const col = db.collection('collName');

//查询满足条件的一条数据
col.findOne({a:100}, function(err, result) { // 返回集合中所有数据
	if (err) throw err;
	console.log(result);
});

//查询满足条件的所有数据
col.find({}).toArray(function(err, result) { // 返回集合中所有数据
	if (err) throw err;
	console.log(result);
});

//查询并修改
col.findOneAndUpdate({a:1}, {$set: {b: 1}}, {
    returnOriginal: false
    , sort: [[a,1]]
    , upsert: true
}, function(err, r) {
    if (err) throw err;
    console.log(r.value); //r.value是修改前的文档
})
    
//查询并且删除
col.findOneAndDelete({a:2}, function(err, r) {
    if (err) throw err;
    console.log(r.value); //返回被删掉的文档
});

//排序
col.find().sort().toArray()

//数量限制
col.find().skip().limit().toArray()
col.find().limit().toArray()
```







## 2 mongoose 

### 2.1 安装以及使用mongoose 连接MongoDB服务

#### 关于mongoose

* 优雅的MongoDB文档模型 （elegant mongodb object modeling for node.js）

* 官方文档 http://mongoosejs.com/docs/index.html

#### 安装和导入

```
npm install mongoose --save
```

```javascript
const mongoose = request('mongoose');
```

#### 连接MongoDB

```javascript
//语法
mongoose.connect(uri, options, (err) => {
    
});
//或者
mongoose.connect(uri options).then(() => {
    
}, (err) => {
    
});
```

* options 选项

  >bufferCommands   是否启用缓存
  >
  >user  用户名
  >
  >pass  密码
  >
  >dbName  数据库名
  >
  >autoReconnect  自动重新连接
  >
  >autoIndex  自动创建索引

* uri

  >```
  >mongodb://localhost/myapp
  >mongodb://username:password@host:port/database?options...
  >```



```
// 导入 mongoose
const mongoose = require('mongoose');

// 连接 mongodb
mongoose.connect('mongodb://mydbuser:123456@localhost:27017/mydb')

// 连接对象
const conn = mongoose.connection;

//监听事件
conn.on('error',()=>{
	console.log('连接失败')
})

conn.on('open',()=>{
	console.log('连接成功')
})
```



#### connection 对像

* db
* host
* port
* user
* pass
* createCollection()  创建集合
* dropCollection()   删除集合
* dropDatabase()    删除数据库





### 2.2 mongoose 基本概念

#### Schema

Mongoose的一切都始于一个Schema。每个schema映射到MongoDB的集合(collection)和定义该集合(collection)中的文档的形式。 Schemas不仅定义了文档和属性的结构，还定义了文档实例方法、静态模型方法、复合索引和文档被称为中间件的生命周期钩子。

```javascript
var blogSchema = new Schema({
  title:  String,
  author: String,
  body:   String,
  comments: [{ body: String, date: Date }],
  date: { type: Date, default: Date.now },
  hidden: Boolean,
  meta: {
    votes: Number,
    favs:  Number
  }
});
```

Schema的类型

- String
- Number
- Date
- Buffer
- Boolean
- Mixed
- ObjectId
- Array
- Map
- Decimal128



```
const mongoose = require('mongoose')

// 连接
mongoose.connect('mongodb://mybdUser:123456@localhost:27017/mydb')

const conn = mongoose.connection
conn.on('error', () => {
    console.error('连接失败');
})

conn.on('open', () => {
    console.log('连接成功');
    
})

// 定义 Schema
const membersSchema = new mongoose.Schema({
    name: String,
    nickName: String,
    age: Number,
    team: String
})

// 定义模型
const membersModel = mongoose.model('members',membersSchema)
```



 #### Model

使用schema定义，我们需要schema转成可以用的模型

```javascript
var BlogModel = mongoose.model('Blog', blogSchema);
```

* 查询 Model.find()
* 删除 remove()
* 更新 update()



#### Document

* Document对象是Model的实例，表示集合中的一个文档
* save() 保存

```javascript
const user = new userModel({
	firstName:'zhang',
    lastName:'san',
    age:56,
    info:'none'
})
user.save((err,res)=>{
    if (err) throw err;
    console.log('添加成功')
	console.log(res)
})
```



### 2.3 mongoose CURD 

#### 模块

* http
* ejs
* mongoose
* url
* formidable



#### 目录结构

```
|-- views 模板目录
|---- index.ejs
|---- add.ejs
|---- edit.ejs
|-- app.js  
|-- article.model.js  

```



### 2.4 Schema

#### 索引

在 mongoose 中，我们在 Schema 中定义索引



#### 实例方法

```javascript
// 定义一个 schema
const kittySchema = mongoose.Schema({
  name: String
});

// 为 事例 添加一个方法
kittySchema.methods.speak = function () {
  var greeting = this.name
    ? "Meow name is " + this.name
    : "I don't have a name";
  console.log(greeting);
}
```

- 重写 mongoose 的默认方法会造成无法预料的结果
- **不要**在自定义方法中使用 ES6 箭头函数，会造成 this 指向错误。

#### 静态方法

```javascript
// assign a function to the "statics" object of our animalSchema
animalSchema.statics.findByName = function(name, cb) {
   return this.find({ name: new RegExp(name, 'i') }, cb);
};

var Animal = mongoose.model('Animal', animalSchema);
Animal.findByName('fido', function(err, animals) {
   console.log(animals);
});
```

- 不要在静态方法中使用 ES6 箭头函数



#### 虚拟值

```javascript
personSchema.virtual('fullName').get(function () {
  return this.name.first + ' ' + this.name.last;
});
```



#### 别名

```javascript
var personSchema = new Schema({
  n: {
    type: String,
    // Now accessing `name` will get you the value of `n`, and setting `n` will set the value of `name`
    alias: 'name'
  }
});
```



#### 选项

* autoIndex  应用启动时，Mongoose 自动发送 createIndex 指令， schema 里的每个 index 都会被创建
* bufferCommands
* capped 设置集合的容量
* collection 自定义集合名称
* id  Mongoose 会默认生成一个虚拟值 id，指向文档的 _id 字段。 如果你不需要 id 虚拟值，可以通过这个选项禁用此功能。
* _id Mongoose 默认给你的 Schema 赋值一个 _id。 这个值的类型是 ObjectId，这与MongoDB的默认表现一致。 如果你不需要 _id，可以通过这个选项禁用此功能。
* minimize  Mongoose 默认不保存空对象。  如果把 minimize 选项设为 false，Mongoose 将保存空对象。
* strict  Strict 选项默认为 true，这意味着你不能 save schema 里没有声明的属性。  
* versionKey   versionKey 是 Mongoose 在文件创建时自动设定的。 这个值包含文件的内部修订号。 versionKey 是一个字符串，代表版本号的属性名， 默认值为 __v。如果这个值与你的计划冲突，你可以设定为其他名称
* timestamps   如果设置了 timestamps 选项, mongoose 会在你的 schema 自动添加 createdAt 和 updatedAt 字段， 其类型为 Date。 这两个字段的默认名是 createdAt 和 updatedAt， 你可以通过设定 timestamps.createdAt 和 timestamps.updatedAt 自定义字段名称



### 2.5 查询

#### 查询方法

* model.find()
* model.findOne()
* model.findById()
* model.distinct()
* model.count()
* Model.findOneAndDelete()
* Model.findOneAndRemove()
* Model.findOneAndUpdate()
* Model.findByIdAndDelete()
* Model.findByIdAndRemove()
* Model.findByIdAndUpdate()
* 支持回调和promise的用法



#### Query 对象 (链式调用)

以上查询方法，返回的是Query对象

##### 查询条件

* where() 
* equals() / ne()
* gt() / gte()
* lt() / lte()
* in() / nin()
* regex()
* and
* or

##### 指定字段

* select()

##### 数量限制

* skip()
* limit()

##### 排序

* sort()

##### 执行

* exec()



#### 其他增删改方法

* model.create()
* model.update()
* model.updateOne()
* model.updateMany()
* model.replaceOne()
* model.remove()
* model.deleteOne()
* model.deleteMany()





### 2.8 Aggregate

#### aggregate表达式

* $project：修改输入文档的结构。可以用来重命名、增加或删除域，也可以用于创建计算结果以及嵌套文档。对应project()方法
* $match：用于过滤数据，只输出符合条件的文档。$match使用MongoDB的标准查询操作。对应match()。
* $limit：用来限制MongoDB聚合管道返回的文档数。对应limit()方法
* $skip：在聚合管道中跳过指定数量的文档，并返回余下的文档。对应skip()。
* $unwind：将文档中的某一个数组类型字段拆分成多条，每条包含数组中的一个值。对应unwind()方法
* $group：将集合中的文档分组，可用于统计结果。对应group()方法
* $sort：将输入文档排序后输出。对应sort()方法
* $geoNear：输出接近某一地理位置的有序文档。对应near()。
* $sample：随机选择N个
* $lookup：连接操作符，用于连接同一个数据库中另一个集合，并获取指定的文档，类似于populate

#### $group 表达式

* $sum 计算总和。
* $avg 计算平均值 
* $min 获取集合中所有文档对应值得最小值。
* $max 获取集合中所有文档对应值得最大值。
* $push 在结果文档中插入值到一个数组中。
* $addToSet 在结果文档中插入值到一个数组中，但不创建副本。
* $first 根据资源文档的排序获取第一个文档数据。
* $last 根据资源文档的排序获取最后一个文档数据

#### aggregate 对象方法

* aggregate.group()
* aggregate.sort()
* aggregate.exec()
* .....





### 2.9 联表

#### aggregate $lookup

```javascript
teamsModel.aggregate([
    {$lookup: {from:'members', localField: 'name',foreignField:'team', as:'members'}},
    {$project: {name:1, introduction:1,power:1,'members.name':1,'members.nickName':1}},
    {$match:{name:'复仇者'}}
], (err, res) => {
    if (err) throw err;
    console.log(res[0]);
})
```

```javascript
membersModel.aggregate([
    {$lookup: {from:'teams', localField:'team', foreignField:'name', as:'teams'}},
    {$project: {_id:0, nickName:1, teamName:'$team', teamIntroduction:'$teams.introduction'}}
], (err, res) => {
    console.log(res);
})
```

* from    需要关联的集合名
* localField    本集合中需要查找的字段
* foreignField    另外一个集合中需要关联的字段
* as    输出的字段名



#### populate

在一个Collection(articles)中定义一个指向另一个Collection(users)的_id字段的字段(by)

```javascript
//定义Schema
const membersSchema = new mongoose.Schema({
    name: String,
    nickName: String,
    age: Number,
    team: {type:mongoose.Schema.Types.ObjectId, ref: 'teams'}
});
const teamsSchema = new mongoose.Schema({
    name: String,
    introduction: String,
    power: Number
});

//查询使用
membersModel
    .find({})
    .populate('team', 'name -_id')
    .exec((err, res) => {
        if (err) throw err;
        console.log(res);
    })

```





### 2.10 验证（Validate）

#### 验证器规则

* 验证是在SchemaType上定义的。
* 验证是中间件。Mongoose 验证器作为pre('save')前置钩子在每个模式默认情况下执行。
* 你可以手动使用document运行验证。validate(callback) 或 doc.validateSync()。
* 验证程序不运行在未定义的值上，除了required验证器。
* 验证异步递归；当你调用Model#save，子文档验证也可以执行。如果出现错误，你的 Model#save回调接收它。
* 验证是可自定义的。

#### 内置验证器

- 所有的`SchemaType`都有内置的`required`验证器。所需的验证器使用`SchemaType`的`checkrequired()`函数确定值是否满足所需的验证器。
- 数值（ Numbers ）有最大（`man`）和最小（`min`）的验证器。
- 字符串（String）有`enum`，`match`，`maxLength`和`minLength`验证器。

```javascript
const UsersSchema = new mongoose.Schema({   
  name: {   
    type: String,   
    unique: true,
    required: true,   
    minlength: 3,   
    maxlength: 6   
  },   
  age: {   
    type: Number,   
    min: [18, '未成年人禁止入内'],   
    max: 30,   
    required: true   
  },   
  sex: {   
    type: String,   
    enum: {   
      values: ['male', 'female'],   
      message: '`{PATH}` 是 `{VALUE}`， 您必须确认您的性别!'   
    },   
    required: true   
  }  
});   

```

`{PATH}` 和 `{VALUE}` 是错误提示中的变量

> `{PATH}`： 键名
>
> `{VALUE}`： 当前键值
>
> `{TYPE}`：验证器类型，比如min，regexp等
>
> `{MIN}`： 最小值，只存在数值
>
> `{MAX}`：最大值，只存在数值



#### 自定义验证器

```Javascript
const UsersSchema = new Schema({   
  ...   
  phone: {   
    type: String,   
    validate: {   
    	validator: function(v){
    		return /1[3|5|7|8]\d{9}/.test(v);   	
		},   
      	message: '`{PATH}` 必须是有效的11位手机号码!'   
    },   
    required: true   
  }  
});  
```

也可以使用数组添加多个验证器

```
validate: [  
  {   
    validator: fn,   
    message: ''   
  },
  {   
    validator: fn,   
    message: ''   
  }
]
```



#### 进行验证

* 进行save()操作的时候进行验证，回调函数第一个参数

* document.validate()  进行验证 回调得到错误对象

  ```
  user.validate((err) => {
      console.log(err);
  })
  ```

* document.validateSync() 同步验证，返回err对象

* 验证失败，返回`ValidatorError`对象,  改对象的errors 属性，下包含每个字段的错误。每个字段的错误都包含一下属性

  > kind   验证器类型，比如min，regexp等
  >
  > path  键名(属性名)
  >
  > value  值
  >
  > message  错误信息

* 默认情况下，验证器都是只有save操作才会触发，但是在 Mongoose 4.x后，我们也可以开启update()和findoneandupdate()的验证器，只需将runValidators设为true(默认是false)：

  ```javascript
  const opts = { runValidators: true };   
  UsersModel.update({}, { name: 'Superman' }, opts, (err) => { });
  ```

  

### 2.11 中间件

中间件（也称为前置和后置钩子）是异步函数执行过程中传递的控制的函数。`中间件`是在`schema`级别上指定的

#### ① 中间件类型

#####document 中间件， 

支持下列操作（ `this` 指向当前 document）

- document.validate()
- document.save()
- document.remove()

 ##### query 中间件 

支持下列操作 （`this` 指向当前 query）

- Model.count()
- Model.find()
- Model.findOne()
- Model.findOneAndRemove()
- Model.findOneAndUpdate()
- Model.update()

##### aggregate 中间件 

作用于 `MyModel.aggregate()` 它会在你对 aggregate 对象调用 `exec()` 时执行。 对于 aggregate 中间件，`this` 指向当前aggregation 对象

##### model 中间件，

`this` 指向当前 model。 Model 中间件支持以下 Model 操作：

- Model.insertMany()

#### ② 前置钩子 (pre)

##### 串行

串行中间件一个接一个地执行。具体来说， 上一个中间件调用 `next` 函数的时候，下一个执行。

```Javascript
var schema = new Schema(..);
schema.pre('save', function(next) {
  // do stuff
  next();
});
```

##### 并行

并行中间件提供细粒度流控制。

 ```javascript
var schema = new Schema(..);

// `true` means this is a parallel middleware. You **must** specify `true`
// as the second parameter if you want to use parallel middleware.
schema.pre('save', true, function(next, done) {
  // calling next kicks off the next middleware in parallel
  next();
  setTimeout(done, 100);
});
 ```

在这个例子里，`save` 方法将在所有中间件都调用了 `done` 的时候才会执行。

##### 使用场景

- 复杂的数据校验
- 删除依赖文档（删除用户后删除他的所有文章）

#### ③ 后置钩子 (post)

[post](https://mongoosedoc.top/docs/api.html#schema_Schema-post) 中间件在方法执行*之后* 调用，这个时候每个 `pre` 中间件都已经完成

```Javascript
schema.post('validate', function(doc) {
  console.log('%s has been validated (but not saved yet)', doc._id);
});
schema.post('save', function(doc) {
  console.log('%s has been saved', doc._id);
});
schema.post('remove', function(doc) {
  console.log('%s has been removed', doc._id);
});
```

如果你给回调函数传入两个参数，mongoose 会认为第二个参数是 `next()` 函数，你可以通过 next 触发下一个中间件

 

### 2.12 插件

#### 语法

```javascript
ArticlesSchema.plugin(function(schema, options){
    schema.add({lastMod: Date});
    schema.pre('save', function(next){
        this.lastMod = Date.now();
        next();
    })
}, [option])
```

#### 全局插件

mongoose单独有一个plugin()功能为每一个schema注册插件：

```
mongoose.plugin(pluginsFn);
```



#### 第三方插件

http://plugins.mongoosejs.io/





































 

 

 