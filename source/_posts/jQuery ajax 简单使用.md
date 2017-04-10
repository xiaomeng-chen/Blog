---
title: jQuery ajax 简单使用

tags: javascript jQuery

categories: code

---
```javascript
 $.ajax({
    type: 'get',
    url: "change" ,
    data: {
        name："lxc"
    } ,
    success: function(){
        alert("提交成功");
    }
 });
```
我在开发中就像上面这样用，下面简单介绍一下参数：
> 1. type
  get:以get的形式向目的url发送get请求类似如下
  http://localhost:8765/user/index/change?name=lxc&num=12&id=1
  post:其数据作为HTTP消息的实体形式发送请求,一般用于数据较多的时候
> 2. url
  必须，就是请求的接受地址，默认是当前界面的地址
> 3. data
  请求中发送的数据
> 4. success
  请求成功后置信地个回调函数
> 5. dataType
  可选，规定预期的服务器响应的数据类型。
  默认执行智能判断（xml、json、script 或 html）。
  
还有一些比较灵活的用法
比如get请求时将数据集成在url里面
```javascript
 $.ajax({
    type: 'get',
    url: "change?name=lxc&num=12&id=1",
    success: function(){
        alert("提交成功");
    }
 });
```



