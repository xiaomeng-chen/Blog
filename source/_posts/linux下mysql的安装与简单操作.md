---
title: linux下mysql的安装与简单操作

tags: mysql

categories: code

---
### 1.安装命令如下
> sudo apt-get install mysql-server
然后按照提示输入数据库密码即可


### 2.启动mysql命令
> service mysql start
这时系统会提示输入密码，正确输入后没有报错就是启动成功了

### 3.关闭mysql服务
> service mysql stop

### 4.连接数据库
>mysql -u root -p
这时系统会提示输入密码，正确输入后会进去mysql命令行下

### 5.查看数据库
>show databases;
需要注意的是mysql命令后面一定要加分号，否则不会运行

### 6.创建数据库
>create database name;

### 7.创建表
>create table user(id int(3) auto_increment not null primary key, name char(8));







