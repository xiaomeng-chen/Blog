---
title: Koajs+sequelize+mysql环境搭建
tags: nodejs
categories: code

---

### 1.首先通过npm init 创建package.json文件
>$ npm init
### 2.安装Koajs
>$ npm install koa --save

在根目录下创建一个app.js的文件
```javascript
var koa = require('koa');
var app = koa();

app.use(function *(){
    this.body = 'Hello Lxc';
});

app.listen(3000);
```
### 3.启动服务器
>$ node --harmony app.js

我们在浏览器中输入 http://localhost:3000就可以看见正确的输出了
### 4.在工程中安装mysql和sequelize
>$ npm install mysql --save

>$  npm install sequelize --save
### 5.数据库配置
在根目录下新建一个models文件夹，在里面新建一个config.js的数据库配置文件
```javascript
module.exports = {
    db: {
        name: 'mysql',
        username: 'root',
        pwd: 'xxxxxx',
         host: '127.0.0.1',
        database: 'test',
        toString() {
            return `${this.name}://${this.username}:${this.pwd}@${this.host}/${this.database}`;
        }
    },
};
```
再新建一个db.js文件，引入config.js
```javascript
/**
 * Created by lxc on 16-3-3.
 */
var Sequelize = require('sequelize');
var configs = require('./config.js');
var sequelize = new Sequelize(configs.db.toString(), {
    logging: function () {}
});

sequelize.define('message', {
        title: Sequelize.TEXT,
        link: Sequelize.TEXT});

sequelize.sync({
    force: true
});

```
接下来我们在命令行中运行db.js
> node db.js

完成后我们去sql查看是否创建成功
>mysql> show columns from messages;
+-----------+----------+------+-----+---------+----------------+
| Field     | Type     | Null | Key | Default | Extra          |
+-----------+----------+------+-----+---------+----------------+
| id        | int(11)  | NO   | PRI | NULL    | auto_increment |
| title     | text     | YES  |     | NULL    |                |
| link      | text     | YES  |     | NULL    |                |
| createdAt | datetime | NO   |     | NULL    |                |
| updatedAt | datetime | NO   |     | NULL    |                |
+-----------+----------+------+-----+---------+----------------+
5 rows in set (0.00 sec)

看到这个结果就是创建成功了^-^

这个应用的结构还比较简单，正常开发的话肯定要比这复杂的多，项目的结构都要考虑，如果以后有时间再来补充吧。
 





