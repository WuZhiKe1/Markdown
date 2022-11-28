# **AJAX**

## 初识AJAX

 URL地址: 统一资源定位符,用于标识互联网上每个资源唯一存放位置
    
        组成 : 
           1. 客户端与服务之间的通讯协议
           2. 该资源的服务器名称
           3. 资源在服务器上的具体存放位置


​    通信过程

1. 请求
2. 处理
3. 响应 


​        网页中请求数据
​        let xhrObj = new XMLHttpRequest();
​        js 成员可以通过它请求服务器上的数据资源
​    

​         客户端请求服务器时
​         用get 和 post
​         get 用于从服务器获取资源
​         post 向服务器提交资源



 *AJAX : 在网页中利用 XMLHttpRequest 对象和服务器进行数据交互的方式*

​    *实先数据交互*



​    *应用场景*

​    *动态检测用户名查重*

​    *搜索提示*

​    *动态刷新表格数据*





## AJAX优缺点

### AJAX的优点:

1. 可以无需刷新页面与服务器端进行同信.
2. 允许根据用户事件来更新部分页面内容.

### AJAX缺点:

1. 没有浏览历史不能回退.
2. 存在跨域问题(同源).
3. SEO不友好.



## HTTP协议

HTTP ( hypretext transport protocol )  协议 [ 超文本传输协议 ] , 协议详细规定了浏览器和万维网服务器之间互相通信的规则 . 

### 请求报文

重点时格式与参数

http/1.1:协议版本

1. 行 : POST(GET请求体为空)   /   s?ie=utf-8   HTTP/1.1
2. 头 : Host : atguigu.com ...
3. 空行  : 必须有空行
4. 体 : username=admin&password=admin



### 响应报文

http/1.1:协议版本    200 : 响应状态表示OK.   OK:响应状态字符串.

1. 行 :  HTTP/1.1 200   OK
2. 头 : Host : atguigu.com ...
3. 空行   : 必须有空行
4. 体 : 

```html
<html>
  <head>
  </head>
  <body>
  	<h1>响应体</h1>
  </body>
</html>
```

## Express框架

在外层打开终端 输入npm init --yes 进行初始化

初始化后  安装Express框架:  终端输入 npm i express

```javascript
//1. 引入express
const express = require('express')

//2. 创建对象
const app = express();

//3. 创建路由规则
//request: 是对请求报文的封装
//response: 是对响应报文的封装
app.get('/', (request, response) => {
    //设置响应
    response.send('HELLO EXPRESS');
});

//4. 监听端口启动服务
app.listen(8000, () => {
    console.log("服务已经启动端口监听中...");
});
```

当前js文件打开终端输入 node + 文件名

网页输入: http://127.0.0.1:8000/ 就可以查看



