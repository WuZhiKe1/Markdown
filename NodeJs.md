# 初始 Node.js

Node.js® is a <font color='#DA924A'>JavaScript runtime</font> built on Chrome's V8 JavaScript engine.

<font color='#DA924A'>Node.js</font> 是一个基于 Chrome V8 引擎的 <font color='#DA924A'>JavaScript 运行环境。</font>

[<font color='cornflowerblue'>Node.js 中文网</font>](http://nodejs.cn/)



注意：

1. 浏览器是 JavaScript 的前端运行环境。
2. Node.js 是 JavaScript 的后端运行环境。
3. Node.js 中无法调用 DOM 和 BOM 等浏览器内置 API。

​	



<font color='#DA924A'>Node.js可以做什么</font>

1. [<font color='cornflowerblue'>基于 Express 框架</font>](http://www.expressjs.com.cn/)，可以快速构建 Web 应用。
2. [<font color='cornflowerblue'>基于 Electron 框架</font>](https://electronjs.org/)，可以构建跨平台的桌面应用。
3. [<font color='cornflowerblue'>基于 restify 框架</font>](http://restify.com/)，可以快速构建 API 接口项目。
4. 读写和操作数据库、创建实用的命令行工具辅助前端开发、etc…。





<font color='#DA924A'>在Node.js环境中执行JavaScript 代码</font>

1. 打开终端。
2. 输入 node 要执行的js文件的路径。



<font color='#DA924A'>终端中的快捷键</font>



在 <font color='#DA924A'>Windows</font> 的 <font color='#DA924A'>powershell </font>或 <font color='#DA924A'>cmd</font><font color='#DA924A'> 终端中</font>，我们可以通过如下<font color='#DA924A'>快捷键</font>，来提高终端的操作效率：

​    ①使用 ↑ 键，可以快速定位到上一次执行的命令。

​    ②使用 tab 键，能够快速补全路径。

​    ③使用 esc 键，能够快速清空当前已输入的命令。

​    ④输入 cls 命令，可以清空终端。





----



# fs 文件系统模块



fs 模块是 Node.js 官方提供的、<font color='#DA924A'>用来操作文件的模块</font>。它提供了一系列的方法和属性，用来满足用户对文件的操作需求。

例如：

<font color='#DA924A'>fs.readFile()</font> 方法，用来读取指定文件中的内容。

<font color='#DA924A'>fs.writeFile() </font>方法，用来向指定的文件中写入内容。



如果要在 JavaScript 代码中，使用 fs 模块来操作文件，则需要使用如下的方式先导入它：

```js
const fs = require('fs');
```





## **读取**指定文件中的内容

使用<font color='#DA924A'> fs.readFile() 方法</font>，可以读取指定文件中的内容

```js
//  fs.readFile(path [ , options] callback);
```

<font color='#DA924A'>参数解读</font>：

参数1：必选参数，字符串，表示文件的路径。

参数2：可选参数，表示以什么编码格式来读取文件。

参数3：必选参数，文件读取完成后，通过回调函数拿到读取的结果。

```js
//导入 fs 模块，来操作文件
const fs = require('fs');
// 调用fs.readFile() 方法读取文件
// 文件格式默认utf-8

fs.readFile('./files/1.txt', 'utf-8', function (err, dataStr) {
  //err代表失败
  console.log(err);   //如果读取成功输出null    读取失败输出 错误对象  
  console.log('----------');
  // dataStr代表成功
  console.log(dataStr);    //读取成功输出111     读取失败输出  undefined

});
```





<font color='#DA924A'> 判断文件是否读取成功</font>

可以判断 err 对象是否为 null，从而知晓文件读取的结果：

```js
const fs = require('fs')

fs.readFile('./files/11.txt', 'utf8', function(err, dataStr) {
  if (err) {
    return console.log('读取文件失败！' + err.message)
  }
  console.log('读取文件成功！' + dataStr)
})
```



----

##  向指定的文件中写入内容



使用 <font color='#DA924A'>fs.writeFile() 方法</font>，可以向指定的文件中写入内容，语法格式如下：

```js
//fs.writeFile(file,data[, options],callback); 
```

<font color='#DA924A'>参数解读</font>： 

1. 参数1：必选参数，需要指定一个文件路径的字符串，表示文件的存放路径。
2. 参数2：必选参数，表示要写入的内容。 
3. 参数3：可选参数，表示以什么格式写入文件内容，默认值是 utf-8。
4. 参数4：必选参数，文件写入完成后的回调函数。

```js
// 1. 导入 fs 文件系统模块
const fs = require('fs');

// 2. 调用 fs.writeFile() 方法，写入文件的内容
//    参数1：表示文件的存放路径
//    参数2：表示要写入的内容
//    参数3：回调函数
fs.writeFile('./files/3.txt', 'ok123', function(err) {
  // 2.1 如果文件写入成功，则 err 的值等于 null
  // 2.2 如果文件写入失败，则 err 的值等于一个 错误对象
  // console.log(err)

  if (err) {
    return console.log('文件写入失败！' + err.message)
  };
  console.log('文件写入成功！')
});
```





<font color='#DA924A'> 路径动态拼接的问题</font>：

​	在使用 fs 模块操作文件时，如果提供的操作路径是以 <font color='#DA924A'>./ 或 ../ </font>开头的相对路径时，很容易出现路径动态拼接错误的问题。

 原因：代码在运行的时候，会以执行 node 命令时所处的目录，动态拼接出被操作文件的完整路径。

 解决方案：在使用 fs 模块操作文件时，直接提供完整的路径，<font color='#DA924A'>不要提供 ./ 或 ../ 开头的相对路径</font>，从而防止路径动态拼接的问题。



<font color='#DA924A'>绝对路径不利于维护，所以使用   __dirname   表示当前文件所处的目录</font>

```js
const fs = require('fs')
fs.readFile(__dirname + '/files/1.txt', 'utf8', function(err, dataStr) {
  if (err) {
    return console.log('读取文件失败！' + err.message)
  }
  console.log('读取文件成功！' + dataStr)
})
```



----

# path 路径模块

path 模块是 Node.js 官方提供的、用来处理路径的模块。它提供了一系列的方法和属性，用来满足用户对路径的处理 需求。

 例如： 

1. <font color='#DA924A'>path.join() 方法</font>，用来将多个路径片段拼接成一个完整的路径字符串 。
2. <font color='#DA924A'>path.basename() 方法</font>，用来从路径字符串中，将文件名解析出来。

如果要在 JavaScript 代码中，使用 path 模块来处理路径，则需要使用如下的方式先导入它

```js
const path = require('path');
```





## 路径拼接path.join() 



使用 <font color='#DA924A'>path.join() 方法</font>，<font color='#DA924A'>可以把多个路径片段拼接为完整的路径字符串</font>，语法格式如下：

```js
//path.join([...paths])
```

参数解读：

1. ...paths <string> 路径片段的序列 
2. 返回值: <string>

```js
const path = require('path');
const fs = require('fs');

 //注意：  ../ 会抵消前面的路径
const pathStr = path.join('/a', '/b/c', '../../', './d', 'e');
console.log(pathStr);  // \a\d\e


fs.readFile(path.join(__dirname, './files/1.txt'), 'utf8', function (err, dataStr) {
  if (err) {
    return console.log(err.message)
  };
  console.log(dataStr)
});
```

<font color='#DA924A'>注意</font>：凡是涉及到路径拼接的操作，都要使用 path.join() 方法进行处理。不要直接使用 + 进行字符串的拼接。





## 获取路径中的文件名. path.basename() 



使用 <font color='#DA924A'>path.basename() 方法</font>，可以获取路径中的最后一部分，经常通过这个方法获取路径中的文件名，语法格式如下：

```js
path.basename(path[ ,ext]);	
```

<font color='#DA924A'>参数解读</font>： 

1. path  必选参数，表示一个路径的字符串 。	
2. ext  可选参数，表示文件扩展名 。
3. 返回:  表示路径中的最后一部分。

```js
const path = require('path')

// 定义文件的存放路径
const fpath = '/a/b/c/index.html'

// const fullName = path.basename(fpath)
// console.log(fullName)     index.html

const nameWithoutExt = path.basename(fpath, '.html')      //去除文件后缀'.html'  
console.log(nameWithoutExt)   //index

```



## 获取路径中的文件扩展名 path.extname()

使用 <font color='#DA924A'>path.extname() 方法</font>，可以获取路径中的扩展名部分，语法格式如下：

```js
path.extname(path);
```

参数解读： 

1. path 必选参数，表示一个路径的字符串 。
2. 返回:  返回得到的扩展名字符串。

```javascript
const path = require('path')

// 这是文件的存放路径
const fpath = '/a/b/c/index.html'

const fext = path.extname(fpath)
console.log(fext)    // .html

```



----

#  http 模块

在网络节点中，负责消费资源的电脑，叫做客户端；<font color='#DA924A'>负责对外提供网络资源</font>的电脑，叫做服务器。

<font color='#DA924A'>http 模块</font>是 Node.js 官方提供的、用来<font color='#DA924A'>创建 web 服务器</font>的模块。

通过 http 模块提供的 <font color='#DA924A'>http.createServer() </font>方法，就 能方便的把一台普通的电脑，变成一台 Web 服务器，从而对外提供 Web 资源服务。

如果要希望使用 http 模块创建 Web 服务器，则需要先导入它：

```js
const http = require('http')
```





服务器和普通电脑的区别在于，服务器上安装了<font color='#DA924A'> web 服务器软件</font>，例如：IIS、Apache 等。通过安装这些服务器软件， 就能把一台普通

的电脑变成一台 web 服务器。 

在 Node.js 中，我们不需要使用 IIS、Apache 等这些第三方 web 服务器软件。因为我们可以基于 Node.js 提供的 http 模块，通过几行

简单的代码，就能轻松的手写一个服务器软件，从而对外提供 web 服务。





## IP 地址

<font color='#DA924A'>IP 地址</font>就是互联网上<font color='#DA924A'>每台计算机的唯一地址</font>，因此 IP 地址具有唯一性。如果把“个人电脑”比作“一台电话”，那么“IP地 址”就相当于“电话号

码”，只有在知道对方 IP 地址的前提下，才能与对应的电脑之间进行数据通信。 IP 地址的格式：通常用“点分十进制”表示成（a.b.c.d）的

形式，其中，a,b,c,d 都是 0~255 之间的十进制整数。例如：用 点分十进表示的 IP地址（192.168.1.1）。



 

<font color='#DA924A'>注意</font>：

 ① 互联网中每台 Web 服务器，都有自己的 IP 地址，例如：大家可以在 Windows 的终端中运行 ping www.baidu.com 命 令，即可查看到

百度服务器的 IP 地址。

 ② 在开发期间，自己的电脑既是一台服务器，也是一个客户端，为了方便测试，可以在自己的浏览器中输入 

127.0.0.1 这个 IP 地址，就能把自己的电脑当做一台服务器进行访问了。









## 域名和域名服务器

尽管 IP 地址能够唯一地标记网络上的计算机，但IP地址是一长串数字，<font color='#DA924A'>不直观</font>，而且不便于<font color='#DA924A'>记忆</font>，于是人们又发明了另一套 字符型的地址方案，即所谓的<font color='#DA924A'>域名（Domain Name）地址</font>。

<font color='#DA924A'> IP地址</font>和<font color='#DA924A'>域名</font>是<font color='#DA924A'>一一对应的关系</font>，这份对应关系存放在一种叫做<font color='#DA924A'>域名服务器</font>(DNS，Domain name server)的电脑中。使用者 只需通过好记的域名访问对应的服务器即可，对应的转换工作由域名服务器实现。因此，<font color='#DA924A'>域名服务器就是提供 IP 地址和域名 之间的转换服务的服务</font><font color='#DA924A'>器</font>。 

注意： 

① 单纯使用 IP 地址，互联网中的电脑也能够正常工作。但是有了域名的加持，能让互联网的世界变得更加方便。 

② 在开发测试期间，<font color='#DA924A'> 127.0.0.1</font> 对应的域名是 <font color='#DA924A'>localhost</font>，它们都代表我们自己的这台电脑，在使用效果上没有任何区别。







## 端口号

每个 web 服务都对应一个唯一的端口号。客户端发送过来的 网络请求，通过端口号，可以被准确地交给对应的<font color='#DA924A'> web 服务</font>进行处理。



<font color='#DA924A'>注意：</font>

① 每个端口号不能同时被多个 web 服务占用。 

② 在实际应用中，URL 中的 80 端口可以被省略。





## 创建最基本的 web 服务器

1. 导入 http 模块 
2.  创建 web 服务器实例 
3. 为服务器实例绑定 request 事件，监听客户端的请求 
4. 启动服务器

<font color='#DA924A'>Ctrl + c 停止服务器</font>

```js
// 1. 导入 http 模块
const http = require('http');

// 2. 调用 http.createServer() 方法，即可快速创建一个 web 服务器实例
const sever = http.createServer();

// 3. 为服务器实例绑定 request 事件，即可监听客户端发送过来的网络请求
sever.on('request', (req, res) => {
    // req是请求对象，它包含了与客户端相关的数据和属性，例如:
    // req.url 是客户端请求的URL地址
    // req.method 是客户端的method请求类型

    //这里不是引号  是左上角的 `
    const str = `You request url is ${req.url}, and request method is ${req.method}`;


    // res是响应对象，它包含了与服务器相关的数据和属性，例如:
    //要发送到客户端的字符串
    // res. end() 方法的作用:
    //向客户端发送指定的内容，并结束这次请求的处理过程
    // 为了防止中文显示乱码的问题，需要设置响应头Content -Type 的值为text/html; charset=utf-8
    res.setHeader('Content-Type', 'text/html; charset=utf-8');

    res.end(str);
});

//4.  调用服务器实例的 .listen() 方法，即可启动当前的 web 服务器实例
sever.listen(80, () => {
    console.log('http sever running at http:127.0.0.1');   //:80 可以省略
});
```



## 根据不同的 url 响应不同的 html 内容



1. 获取请求的 url 地址 
2. 设置默认的响应内容为 404 Not found 
3. 判断用户请求的是否为 / 或 /index.html 首页 
4. 判断用户请求的是否为 /about.html 关于页面 
5. 设置 Content-Type 响应头，防止中文乱码 
6. 使用 res.end() 把内容响应给客户端

```js
// 导入 http 模块
const http = require('http');

// 调用 http.createServer() 方法，即可快速创建一个 web 服务器实例
const sever = http.createServer();

// 为服务器实例绑定 request 事件，即可监听客户端发送过来的网络请求
sever.on('request', (req, res) => {
    // req是请求对象，它包含了与客户端相关的数据和属性，例如:
    // req.url 是客户端请求的URL地址
    // req.method 是客户端的method请求类型

    //这里不是引号  是左上角的 `
    const str = `You request url is ${req.url}, and request method is ${req.method}`;


    // res是响应对象，它包含了与服务器相关的数据和属性，例如:
    //要发送到客户端的字符串
    // res. end() 方法的作用:
    //向客户端发送指定的内容，并结束这次请求的处理过程
    // 为了防止中文显示乱码的问题，需要设置响应头Content -Type 的值为text/html; charset=utf-8
    res.setHeader('Content-Type', 'text/html; charset=utf-8');

    res.end(str);
});

// 调用服务器实例的 .listen() 方法，即可启动当前的 web 服务器实例
sever.listen(80, () => {
    console.log('http sever running at http:127.0.0.1');   //:80 可以省略
});
```



<font color='#DA924A'>补全用户输入的 url</font>

```js
//导入 http 模块
const http = require('http');
//导入 fs 模块
const fs = require('fs');
//导入path 模块
const path = require('path');


//创建Web 服务器
const sever = http.createServer();
//监听服务器的 request 事件
sever.on('request', (req, res) => {
    //获取用户请求的 url 地址
    const url = req.url
    //把 请求的 url 地址 ，映射为本地文件的存放路径
    //预义一个空白的文件存放路径 
    let fpath = ''
    if (url === '/') {              //如果用户输入的是根路径就 手动帮用户拼接首页路径
        fpath = path.join(__dirname, './clock/index.html')
    } else {                       //如果用户输入的不是根路径就补全路径
        fpath = path.join(__dirname, '/clock', url)
    }

    //根据映射过来的文件路径古曲文件
    fs.readFile(fpath, 'utf-8', (err, dataStr) => {
        //读取失败向用户返回固定信息
        if (err) return res.end('404 Not fount.')
        //读取成功将读取的内容响应给客户端  
        res.end(dataStr)
    })

});
//启动服务器
sever.listen(80, () => {
    console.log('sever running at http://127.0.0.1');
});
```



----

# 模块化

<font color='#DA924A'>模块化</font>是指解决一个<font color='#DA924A'>复杂问题</font>时，自顶向下逐层<font color='#DA924A'>把系统划分成若干模块的过程</font>。对于整个系统来说，<font color='#DA924A'>模块是可组 合、分解和更换的单</font>

<font color='#DA924A'>元。</font>

Node.js 中根据模块来源的不同，将模块分为了<font color='#DA924A'> 3 大类</font>，分别是： 

1. <font color='#DA924A'>内置模块</font>（内置模块是由 Node.js 官方提供的，例如 fs、path、http 等） 。
2. <font color='#DA924A'>自定义模块</font>（用户创建的每个 .js 文件，都是自定义模块） 。
3.  <font color='#DA924A'>第三方模块</font>（由第三方开发出来的模块，并非官方提供的内置模块，也不是用户创建的自定义模块，使用前需要先下载）。

使用强大的 <font color='#DA924A'>require() 方法</font>，可以加载需要的<font color='#DA924A'>内置模块</font>、<font color='#DA924A'>用户自定义模块</font>、<font color='#DA924A'>第三方模块</font>进行使用

使用 require() 方法加载其它模块时，会执行被加载模块中的代码。

```js
// 加载内置的 fs 模块
const fs = require('fs')

//加载自定义模块
const custom = require('./custom.js')

//加载第三方模块
const moment = require('moment')
```







## 模块作用域

和<font color='#DA924A'>函数作用域</font>类似，在自定义模块中定义的<font color='#DA924A'>变量</font>、<font color='#DA924A'>方法</font>等成员，<font color='#DA924A'>只能在当前模块内被访问</font>，这种模块级别的访问限制，叫做<font color='#DA924A'>模块作用域</font>。

防止了全局变量污染的问题



##  向外共享模块作用域中的成员



### module 对象

在每个 .js 自定义模块中都有一个 module 对象，它里面存储了和当前模块有关的信息。



### module.exports 对象

在自定义模块中，可以使用 module.exports 对象，将模块内的成员共享出去，供外界使用。 外界用 <font color='#DA924A'>require() 方法导入</font>自定义模块时，得到的就是 module.exports 所指向的对象。



使用 require() 方法导入模块时，导入的结果，<font color='#DA924A'>永远以 module.exports 指向的对象为准。</font>



### exports 对象

 由于 module.exports 单词写起来比较复杂，为了<font color='#DA924A'>简化向外共享成员的代码</font>，Node 提供了 exports 对象。默认情况 下，<font color='#DA924A'>exports 和 </font><font color='#DA924A'>module.exports 指向同一个对象</font>。最终共享的结果，还是以 <font color='#DA924A'>module.exports 指向的对象为准</font>。

<font color='#D26B6B'> exports 和 module.exports 的使用误区</font>



时刻谨记，require() 模块时，得到的永远是 module.exports 指向的对象：

<font color='#D26B6B'>注意</font>：为了防止混乱，建议大家不要在同一个模块中同时使用 exports 和 module.exports





Node.js 遵循了 CommonJS 模块化规范，CommonJS 规定了<font color='#DA924A'>模块的特性</font>和<font color='#DA924A'>各模块之间</font><font color='#DA924A'>如何相互依赖。</font>

 CommonJS 规定：

​    ①  每个模块内部，<font color='#DA924A'>module 变量</font>代表当前模块。 

​    ②  module 变量是一个对象，它的 exports 属性（即 <font color='#DA924A'>module.exports</font>）<font color='#DA924A'>是对外的接口</font>。 

​    ③  加载某个模块，其实是加载该模块的 module.exports 属性。<font color='#DA924A'>require() 方法用于加载模块</font>。



```js
// 自定义模块
//在自定义模块中，默认情况下    module.exports = {}

//向 module.exports 对象上挂载 username属性
module.exports.username = 'zs'

//挂载  sayHello方法
module.exports.sayHello = function () {
    console.log('Hello')
}
const age = 20    //只有挂载后age 才可以外部调用 
module.exports.age = age   //age 成为非私有成员 

// 永远以 module.exports 指向的对象为准。
module.exports = {
    username: 'wu',
    sayhello: function () {
        console.log('hello')
    },
    ages: 22
}
module.exports.age = age   //module.exports.age = age    //可以添加
exports.agee = age        //无法添加
```

```js
const custom = require('./13-自定义模块custom')
console.log(custom);
//输出       { username: 'wu', sayhello: [Function: sayhello], ages: 22, age: 20 }
```









----

# npm与包

Node.js 中的第三方模块又叫做包。 就像电脑和计算机指的是相同的东西，<font color='#DA924A'>第三方模块和包指的是同一个概念</font>，只不过叫法不同。



不同于 Node.js 中的内置模块与自定义模块，<font color='#DA924A'>包是由第三方个人或团队开发出来的</font>，免费供所有人使用。 

<font color='#DA924A'>注意</font>：Node.js 中的包都是免费且开源的，不需要付费即可免费下载使用。





<font color='#DA924A'> 为什么需要包 </font>

​     由于 Node.js 的内置模块仅提供了一些底层的 API，导致在基于内置模块进行项目开发的时，效率很低。 

<font color='#DA924A'>包是基于内置模块封装出来的</font>，提供了更高级、更方便的 API，<font color='#DA924A'>极大的提高了开发效率</font>。 

<font color='#DA924A'>包和内置模块之间</font>的关系，类似于 jQuery 和 浏览器内置 API 之间的关系。



[<font color='cornflowerblue'>网站上搜索自己所需要的包</font>](https://www.npmjs.com/)    <font color='#DA924A'>查看包的文档</font>

[<font color='cornflowerblue'>服务器上下载自己需要的包</font>](https://registry.npmjs.org/)

<font color='#DA924A'>npm, Inc.</font> 公司提供了一个包管理工具，我们可以使用这个包管理工具，从 https://registry.npmjs.org/ 服务器把需要 的包下载到本地使

用。

 这个包管理工具的名字叫做 <font color='#DA924A'>Node Package Manager</font>（简称 npm 包管理工具），这个包管理工具随着 Node.js 的安 装包一起被安装

到了用户的电脑上。 

在终端中执行<font color='#DA924A'> npm -v</font> 命令，来查看自己电脑上所安装的 npm 包管理工具的版本号：





## 格式化时间的传统做法

1. 创建格式化时间的自定义模块 
2. 定义格式化时间的方法 
3. 创建补零函数 
4. 从自定义模块中导出格式化时间的函数 
5. <font color='#DA924A'> 导入格式化时间的自定义模块 </font>
6.  <font color='#DA924A'>调用格式化时间的函数</font>

```js
function dateFormat(dtStr) {
    const dt = new Date(dtStr)

    const y = dt.getFullYear()
    const m = padZero(dt.getMonth() + 1)
    const d = padZero(dt.getDate())

    const hh = padZero(dt.getHours())
    const mm = padZero(dt.getMinutes())
    const ss = padZero(dt.getSeconds())
    return `${y}-${m}-${d} ${hh}:${mm}:${ss}`
}

//补零’
function padZero(n) {
    return n > 9 ? n : '0' + n
}


module.exports = {
    dateFormat
}

```

```js
const TIME = require('./15传统格式化时间')

//调用方法进行时间的格式化
const dt = new Date()
const newDT = TIME.dateFormat(dt)
console.log(newDT);

```







## 格式化时间的高级做法 

1. <font color='#DA924A'>使用 npm 包管理工具，在项目中安装格式化时间的包 moment </font>
2. 使用 require() 导入格式化时间的包
3. 参考 moment 的官方 API 文档对时间进行格式化

```js
//导入moment包
const moment = require('moment')
//参考moment 官方API文档，调用对应的方法，对时间进行格式化
//调用moment() 方法，得到当前的时间
//针对当前的时间，调用format() 方法，按照指定的格式进行时间的格式化
const dt = moment().format( 'YYYY-MM-DD HH:mm:sS ' )
console.log(dt) //输出2020-01-12 17:23:48
```







##  在项目中安装包的命令

```c
npm install  包的完整名称
#简写
npm i 完整的包名称
```







##  初次装包后多了哪些文件

初次装包完成后，在项目文件夹下多一个叫做 node_modules 的文件夹和 package-lock.json 的配置文件。 

其中：

<font color='#DA924A'>node_modules 文件</font>夹用来<font color='#DA924A'>存放所有已安装到项目中的包</font>。require() 导入第三方包时，就是从这个目录中查找并加载包。 

<font color='#DA924A'>package-lock.json配置文件</font> 用来<font color='#DA924A'>记录 node_modules 目录下的每一个包的下载信息</font>，例如包的名字、版本号、下载地址等。 

注意：程序员不要手动修改 node_modules 或 package-lock.json 文件中的任何代码，npm 包管理工具会自动维护它们。





## 安装指定版本的包

默认情况下，使用 npm install 命令安装包的时候，<font color='#DA924A'>会自动安装最新版本的包</font>。如果需要安装指定版本的包，可以在包 名之后，通过 <font color='#DA924A'>@ 符</font>号指定具体的版本。

```c
npm i moment@2.22.2
```

<font color='#DA924A'>包的语义化版本规范</font>



包的版本号是以“点分十进制”形式进行定义的，总共有三位数字，例如 2.24.0 

其中每一位数字所代表的的含义如下： 

第1位数字：<font color='#DA924A'>大版本 </font>

第2位数字：<font color='#DA924A'>功能版本</font> 

第3位数字：<font color='#DA924A'>Bug修复版本</font>

<font color='#DA924A'>版本号提升的规则</font>：只要前面的版本号增长了，则后面的版本号<font color='#DA924A'>归零</font>。





## 包管理配置文件



npm 规定，在<font color='#DA924A'>项目根目录</font>中，必须提供一个叫做 <font color='#DA924A'>package.json</font> 的包管理配置文件。

用来记录与项目有关的一些配置 信息。

1. 项目的名称、版本号、描述等 
2. 项目中都用到了哪些包 
3. 哪些包只在开发期间会用到 
4. 那些包在开发和部署时都需要用到



<font color='#DA924A'>多人协作的问题</font>

整个项目的体积是 30.4M 

第三方包的体积是 28.8M 

项目源代码的体积 1.6M 

<font color='#DA924A'>遇到的问题：</font>第三方包的体积过大，不 方便团队成员之间共享项目源代码。

<font color='#DA924A'> 解决方案</font>：共享时剔除node_modules





## 如何记录项目中安装了哪些包

在项目根目录中，创建一个叫做<font color='#DA924A'> package.json 的配置文件</font>，即可用来记录项目中安装了哪些包。从而方便剔除 node_modules 目录之

后，在团队成员之间共享项目的源代码。

<font color='#DA924A'>注意</font>：今后在项目开发中，一定要把 node_modules 文件夹，添加到 .gitignore 忽略文件中。





## 快速创建 package.json

npm 包管理工具提供了一个快捷命令，可以在执行命令时所处的目录中，<font color='#DA924A'>快速创建 package.json </font>这个包管理 配置文件：

```c
#在执行命令所处的目录中，快速创建 package.json 文件
npm init -y
```



注意： 

1. 上述命令只能在<font color='#DA924A'>英文的目录下成功运行</font>！所以，项目文件夹的名称一定要使用英文命名，不要使用中文，不能出现空格。
2. 运行 npm install 命令安装包的时候，npm 包管理工具会<font color='#DA924A'>自动把包的名称和版本号，记录到 package.json 中</font>。





##  dependencies 节点

package.json 文件中，有一个 <font color='#DA924A'>dependencies 节点</font>，专门用来记录您使用 npm install  命令安装了哪些包。

## 一次性安装所有的包

当我们拿到一个剔除了 node_modules 的项目之后,需要先把所有的包下载到项目中,才能将项目运行起来。否则会报类似于下面的错误：

```js
//由于项目运行依赖 moment 这个包 如果没有安装这包，就会报出以下错误
Error: Cannot find module 'moment'
//可以运行 npm install 命令（或 npm i）一次性安装所有的依赖包：
//执行 npm install 命令时 ，npm 包管理工具会先读取 package.json 中的 dependencies 节点
//读取到记录的所有依赖包名称和版本号之后，npm 包管理工具会把这些包一次性下载到项目中
npm install
```



## 卸载包

可以运行<font color='#DA924A'> npm uninstall</font> 命令，来卸载指定的包：

```c
npm uninstall 具体包名
```



注意：npm uninstall 命令执行成功后，会把卸载的包，自动从 package.json 的 dependencies 中移除掉。





## devDependencies 节点

如果某些包<font color='#DA924A'>只在项目开发阶段会用到</font>，<font color='#DA924A'>在项目上线之后不会用到，</font>则建议把这些包记录到 devDependencies 节点中。 

与之对应的，如果某些包在开发和项目上线之后都需要用到，则建议把这些包记录到 dependencies 节点中。

```c
#安装指定的包，并记录到 devDependencies 节点中
npm install 包名 --save-dev
#简写
npm i 包名 -D
```





##  解决下包速度慢的问题



切换 npm 的下包镜像源 下包的镜像源，指的就是下包的服务器地址。

```c
#查看当前的下包镜像源
npm config get registry 
#将下包的镜像源切换为淘宝镜像源
npm config set registry=https://registry .npm. taobao. org/
#检查镜像源是否下载成功
npm config get registry 
```





##  包的分类

使用 npm 包管理工具下载的包，共分为两大类，分别是：<font color='#DA924A'>项目包 全局包</font>



### 项目包

那些被安装到<font color='#DA924A'>项目</font>的 node_modules 目录中的包，都是项目包。

<font color='#DA924A'>项目包又分为两类</font>，分别是：

1.  <font color='#DA924A'>开发依赖包</font>（被记录到 devDependencies 节点中的包，只在开发期间会用到)
2. <font color='#DA924A'>核心依赖包</font>（被记录到 dependencies 节点中的包，在开发期间和项目上线之后都会用到）

```c
npm i 包名-D
#开发依赖包(会被记录到devDependencies节点下)
npm i包名
#核心依赖包(会被记录到dependencies 节点下)
```





### 全局包

在执行 npm install 命令时，如果提供了<font color='#DA924A'> -g </font>参数，则会把包安装为<font color='#DA924A'>全局包</font>。

 全局包会被安装到 C:\Users\用户目录\AppData\Roaming\npm\node_modules 目录下。



```c
npmi包名-g
#全局安装指定的包
npm uninstall 包名-g
#卸载全局安装的包，
```



注意:

1. 只有<font color='#DA924A'>工具性质的包</font>，才有全局安装的必要性。因为它们提供了好用的终端命令。
2. 判断某个包是否需要全局安装后才能使用，可以<font color='#DA924A'>参考官方提供的使用说明即可</font>。





### i5ting_toc

i5ting_ toc 是一一个可以把md文档转为html页面的小工具，使用步骤如下:
```c
 #将i5ting toc 安装为全局包
 npm install -g i5ting toc
 #调用i5ting toc, 轻松实现md转html的功能
 i5ting toc -f要转换的md文件路径-0
```



## 规范的包结构

一个规范的包，它的组成结构,必须符合以下3点要求:

1. 包必须以<font color='#DA924A'>单独的目录</font>而存在
2. 包的顶级目录下要必须包含<font color='#DA924A'>package.json</font>这个包管理配置文件
3. package.json 中必须包含<font color='#DA924A'>name, version, main 这三个属性</font>，分别代表包的<font color='#DA924A'>名字、版本号、包的入口</font>。



<font color='#DA924A'>注意:</font>

以上3点要求是-个规范的包结构必须遵守的格式，关于更多的约束，可以参考如下网址:
https://yarnpkg.com/zh-Hans/docs/package-json



# 模块的加载机制																																								

<font color='#DA924A'>优先从缓存中加载</font>

<font color='#DA924A'>模块在第一次加载后会被缓存</font>。 这也意味着多次调用 require() 不会导致模块的代码被执行多次。 

注意：

不论是内置模块、用户自定义模块、还是第三方模块，它们都会优先从缓存中加载，从而<font color='#DA924A'>提高模块的加载效率</font>。





<font color='#DA924A'> 内置模块的加载机制</font>

内置模块是由 Node.js 官方提供的模块，<font color='#DA924A'>内置模块的加载优先级最高。</font>





<font color='#DA924A'>自定义模块的加载机制</font>

使用 require() 加载自定义模块时，必须指定以 <font color='#DA924A'>./ </font>或 <font color='#DA924A'>../ </font>开头的<font color='#DA924A'>路径标识符</font>。在加载自定义模块时，如果没有指定 ./ 或 ../  这样的路径标识

符，则 node <font color='#DA924A'>会把它当作内置模块或第三方模块</font>进行加载。



同时，在使用 require() 导入自定义模块时，如果省略了文件的扩展名，则 Node.js 会按顺序分别尝试加载以下的文件：

1. 按照确切的文件名进行加载
2. 补全 .js 扩展名进行加载 
3. 补全 .json 扩展名进行加载
4. 补全 .node 扩展名进行加载 
5. 加载失败，终端报错



<font color='#DA924A'>第三方模块的加载机制</font>

如果传递给 require() 的模块标识符不是一个内置模块，也没有以 ‘./’ 或 ‘../’ 开头，则 Node.js 会从当前模块的父 目录开始，尝试从 /node_modules 文件夹中加载第三方模块。

<font color='#DA924A'>如果没有找到对应的第三方模块，则移动到再上一层父目录中，进行加载，直到文件系统的根目录。</font>



 <font color='#DA924A'>目录作为模块</font>

当把目录作为模块标识符，传递给 require() 进行加载的时候，有三种加载方式： 

1.  在被加载的目录下查找一个叫做 package.json 的文件，并寻找 main 属性，作为 require() 加载的入口 
2.  如果目录里没有 package.json 文件，或者 main 入口不存在或无法解析，则 Node.js 将会试图加载目录下的 index.js 文件。
3.  如果以上两步都失败了，则 Node.js 会在终端打印错误消息，报告模块的缺失：Error: Cannot find module 'xxx'



----

#  Express

<font color='#DA924A'>Express </font>是基于 Node.js 平台，快速、开放、极简的 Web 开发框架。 

通俗的理解：Express 的作用和 Node.js 内置的 http 模块类似，是专门用来创建 Web 服务器的。 

Express可以方便、快速的创建 <font color='#DA924A'>Web 网站的服务器或 API 接口的服务器</font>。

Express 的本质：就是一个 npm 上的第三方包，提供了快速创建 Web 服务器的便捷方法。 

[<font color='cornflowerblue'>Express 的中文官网</font>](http://www.expressjs.com.cn/)



## Express安装

```c
npm i express 
```



## 创建基本的 Web 服务器

```js
//1.导入express
const express = require(' express ' )
// 2.创建web服务器
const
app =express( )
//3.调用app.listen( 端口号，启动成功后的回调函数) ,启动服务器 
app.listen(80, () => {
console. log( 'express server running at http://127.0.0.1')
})
```



## 监听 GET 请求

```js
//参数1:客户端请求的URL地址
//请求对应的处理函数

//req:请求对象(包含了与请求相关的属性与方法)
//res:响应对象(包含了与响应相关的属性与方法)
app. get( '请求URL'，function(req, res) { /*处理函数*/ })
```

## 监听 POST 请求

```js
//参数1:客户端请求的URL地址
//请求对应的处理函数

//req:请求对象(包含了与请求相关的属性与方法)
//res:响应对象(包含了与响应相关的属性与方法)
app . post( '请求URL '，function(req, res) { /*处理函数*/ }
```







## 整体流程

```js
// 1. 导入 express
const express = require('express')
// 2. 创建 web 服务器
const app = express()

// 4. 监听客户端的 GET 和 POST 请求，并向客户端响应具体的内容
app.get('/user', (req, res) => {
    // 调用 express 提供的 res.send() 方法，向客户端响应一个 JSON 对象
    res.send({ name: 'zs', age: 20, gender: '男' })
})
app.post('/user', (req, res) => {
    // 调用 express 提供的 res.send() 方法，向客户端响应一个 文本字符串
    res.send('请求成功')
})
app.get('/', (req, res) => {
    // 通过 req.query 可以获取到客户端发送过来的 查询参数
    // 注意：默认情况下，req.query 是一个空对象
    //客户端使用?name=zs&age=20 这种查询字符串形式，发送到服务器的参数，
    //可以通过req . query 对象访问到，例如:
    // req. query . name      req.query.age

    console.log(req.query)
    res.send(req.query)
})
// 注意：这里的 :id 是一个动态的参数
app.get('/user/:id/:username', (req, res) => {
    // req.params   是动态匹配到的 URL 参数 

    //动态查询客户端输入的参数  id 输入1 服务器响应 对象id ： 1  id是属性名

    // 冒号是固定写法  属性名不是  还可以多个匹配参数  比如 /：username 

    //用户输入的是http://127.0.0.1/3/zs        就响应 id：3   username：'zs'
    //默认也是一个空对象
    console.log(req.params)
    res.send(req.params)
})

// 3. 启动 web 服务器
app.listen(80, () => {
    console.log('express server running at http://127.0.0.1')
})
```



## 托管静态资源

### 创建静态资源express.static()

以将 public 目录下的图片、CSS 文件、JavaScript 文件对外开放访问

```js
const express = require('express')
const app = express()
//在这里，调用express . static()方法，快速的对外提供静态资源
app.use(express.static('clock'))      //use(注册全局中间件)
app.listen(80, () => {
    console.log('express sever running at http://127.0.0.1');
})
```

输入   http://127.0.0.1/index.html     http://127.0.0.1/index.js    http://127.0.0.1/index.css   就可以查询<font color='#DA924A'>clock</font>文件夹里的静态资源





### 托管多个静态资源目录

如果要托管多个静态资源目录，请<font color='#DA924A'>多次调用 </font>express.static() 函数：

访问静态资源文件时，express.static() 函数会根据目录的添加顺序查找所需的文件。



### 挂载路径前缀

如果希望在托管的<font color='#DA924A'>静态资源访问路径之前</font>，<font color='#DA924A'>挂载路径前缀</font>，则可以使用如下的方式：

```js
app.use('/clock'express.static('clock'))
```

输入   http://127.0.0.1<font color='#DA924A'>/clock/</font>index.html     http://127.0.0.1/<font color='#DA924A'>/clock/</font>index.js    http://127.0.0.1/<font color='#DA924A'>/clock/</font>index.css   就可以查询<font color='#DA924A'>clock</font>文件夹里的静态资源





##  nodemon

在编写调试 Node.js 项目的时候，如果修改了项目的代码，则需要频繁的手动 close 掉，然后再重新启动，非常繁琐。 现在，我们可以使

用 nodemon（https://www.npmjs.com/package/nodemon） 这个工具，它能够监听项目文件 的变动，当代码被修改后，nodemon <font color='#DA924A'>会自动</font>

<font color='#DA924A'>帮我们重启项目</font>，极大方便了开发和调试。

在终端中，运行如下命令，即可将 nodemon 安装为全局可用的工具：

```c
npm install -g nodemon
```



当基于 Node.js 编写了一个网站应用的时候，传统的方式，是运行 node app.js 命令，来启动项目。这样做的坏处是： 代码被修改之后，

需要手动重启项目。 现在，我们可以将 node 命令替换为 nodemon 命令，使用 nodemon app.js 来启动项目。这样做的好处是：代码 被

修改之后，会被 nodemon 监听到，从而实现自动重启项目的效果

```c
node app.js
#将上面的终端命令，替换为下面的终端命令，即可实现自动重启项目的效果
nodemon app.js 
```



<font color='#D26B6B'>报错无权限</font>

打开文件所在文件夹，点击左上角的“文件”选项，鼠标放到“打开Windows powershell”，选择以管理员身份打开，输入 set-ExecutionPolicy RemoteSigned，Y

-----

# Express 路由

<font color='#DA924A'>路由就是映射关系。</font>

<font color='#DA924A'>现实生活中的路由</font>

拨打10086时

按键 1 -> 业务查询 

按键 2 -> 手机充值 

按键 3 -> 业务办理 

按键 4 -> 密码服务与停复机                                          在这里，路由是按键与服务之间的映射关系

按键 5 -> 家庭宽带

 按键 6 -> 话费流量

 按键 8 -> 集团业务

 按键 0 -> 人工服务 



在 Express 中，路由指的是<font color='#DA924A'>客户端的请求与服务器处理函数之间的映射关系。</font> Express 中的路由分 3 部分组成，分别是<font color='#DA924A'>请求的类型</font>、<font color='#DA924A'>请</font>

<font color='#DA924A'>求的 URL 地址</font>、<font color='#DA924A'>处理函数</font>

```js
app.METHOD(PATH,HANDLER)
```



<font color='#DA924A'>路由的匹配过程</font>

每当一个请求到达服务器之后，<font color='#DA924A'>需要先经过路由的匹配</font>，只有匹配成功之后，才会调用对应的处理函数。

在匹配时，会按照路由的顺序进行匹配，如果<font color='#DA924A'>请求类型</font>和<font color='#DA924A'>请求的 URL 同时匹配成功</font>，则 Express 会将这次请求，转 交给对应的 function 

函数进行处理。





|        |                  |          路由          | 分发 |                 处理函数                  |
| :----: | :--------------: | :--------------------: | :--: | :---------------------------------------: |
|        |                  |   app.get(/'. funA)    | 分发 |  funA(req, res) { /处理并响应这次请求"/)  |
| 客户端 | 从上到下进行匹配 |  app.post('/', funB)   | 分发 | funB(req, res) { /*处理并响应这次请求"/ } |
|        |                  |  app.post('/', funB)   | 分发 |  funC(req, res) {/处理并响应这次请求*/)   |
|        |                  | app.post(/user'. funD) | 分发 | funD(req, res) {/*处理并响应这次请求*/ }  |
|        |                  |        其它路由        |      |                                           |



<font color='#DA924A'>路由匹配的注意点</font>：

1.  按照定义的<font color='#DA924A'>先后顺序</font>进行匹配
2. <font color='#DA924A'>请求类型和请求的URL同时匹配成功</font>， 才会调用对应的处理函数





在 Express 中使用路由最简单的方式，就是把路由挂载到 app 

```js
const express = require('express')
const app = express()

//挂载路由
app.get('/',(req,res) =>{res.send('hello')})
app.post('/',(req,res) =>{res.send('Hello')})

app.listen(80,() =>{console.log('sever running at http://127.0.0.1')})
```





## 模块化路由

为了方便对路由进行模块化的管理，Express<font color='#DA924A'> 不建议</font>将路由直接挂载到 app 上，而是<font color='#DA924A'>推荐将路由抽离为单独的模块</font>。 

将路由抽离为单独模块的。

1. 创建路由模块对应的 .js 文件 
2. 调用 express.Router() 函数创建路由对象 
3. 向路由对象上挂载具体的路由 
4. 使用 module.exports 向外共享路由对象 
5. 使用 app.use() 函数注册路由模块



<font color='#DA924A'>创建路由</font>

```js
//导入express
const express = require('express')
//创建路由对像
const router = express.Router()

//挂载获取用户列表路由
router.get('/user/list', (req, res) => {
    res.send('Get user list')
})

//挂载添加用户路由
router.post('/user/add', (req, res) => {
    res.send('Add new user')
})

//向外导出路由
module.exports = router
```



<font color='#DA924A'>注册路由</font>

```js
const express = require('express')
const app = express()

//导入路由模块
const router = require('./03-express路由.js')

//使用app.use() 注册路由模块
app.use('api',router)    //api 在访问时要在前面加api  api/user/list        use(注册全局中间件)

app.listen(80, () => { console.log('sever running at http://127.0.0.1') })
```



# 中间件

<font color='#DA924A'>中间件</font>（Middleware ），特指业务流程的中间处理环节。

<font color='#DA924A'>Express 中间件</font>

next 函数是实现<font color='#DA924A'>多个中间件连续调用的关键</font>，它表示把流转关系转交给下一个中间件或路由。

Express 的中间件，本质上就是一个 f<font color='#DA924A'>unction 处理函数</font>，Express 中间件的格式如下：

```js
const express = require('express')
const app = express()

const mw = function (req, res, next) {   // mw 指向的就是中间件函数
    console.log('先调用')
    //当中间件的业务处理完比后必需调用 next() 函数
    //表示把关系转给下一个中间件或路由
    next()
}

//注册为全局生效的中间件
app.use(mw)

app.get('/', (req, res) => {
    console.log('后调用');
    res.send('Home page')
})
app.get('/User', (req, res) => {
    res.send('User page')
})

app.listen(80, () => { console.log('sever running at http://127.0.0.1') })
```

<font color='#DA924A'>注意</font>：中间件函数的形参列表中，必须包含 next 参数。而路由处理函数中只包含 req 和 res。

<font color='#DA924A'>简化写法</font>

```js
app.use((req,res,nest) =>{
    console.log('简化写法')
    next()
})
```





## 中间件的作用

多个中间件之间，共享同一份 req 和 res。基于这样的特性，我们可以在上游的中间件中，<font color='#DA924A'>统一</font>为 req 或 res 对象<font color='#DA924A'>添加自定义的属性或方</font>

<font color='#DA924A'>法</font>，供<font color='#DA924A'>下游</font>的中间件或路由进行使用。



## 定义多个全局中间件

可以使用 app.use() <font color='#DA924A'>连续定义多个</font>全局中间件。客户端请求到达服务器之后，会按照中间件定义的先后<font color='#DA924A'>顺序依次进行</font> <font color='#DA924A'>调用</font>





## 局部生效的中间件

不使用 app.use() 定义的中间件，叫做局部生效的中间件

```js
const express = require('express')
const app = express()

const wm = function (req, res, next) {
    console.log('局部中间件');
    next()
}

app.get('/', wm, (req, res) => {

    res.send('Home page')
})
// 多个中间件  wm1,wm2    第一种写法
//            [ wm1,wm2]    第二种写法


app.get('/User', (req, res) => {
    res.send('User page')
})

app.listen(80, () => { console.log('http://127.0.0.1') })

```





<font color='#D26B6B'>注意事项</font>

1. 一定要在路由之前注册中间件 
2. 客户端发送过来的请求，可以连续调用多个中间件进行处理 
3. 执行完中间件的业务代码之后，不要忘记调用 next() 函数 
4. 为了防止代码逻辑混乱，调用 next() 函数后不要再写额外的代码
5. 连续调用多个中间件时，多个中间件之间，共享 req 和 res 对象





##  中间件的分类

1. <font color='#DA924A'>应用级别</font>的中间件 
2.  <font color='#DA924A'>路由级别</font>的中间件 
3.  <font color='#DA924A'>错误级别</font>的中间件 
4.  <font color='#DA924A'>Express 内置</font>的中间件 
5.  <font color='#DA924A'>第三方</font>的中间件





### 应用级别的中间件

通过 app.use() 或 app.get() 或 app.post() ，<font color='#DA924A'>绑定到 app 实例上的中间件</font>，叫做应用级别的中间件

```js
//全局
app.use((req, res, next) =>{
    next()
})

//局部
app.ge('/',wm,(req, res, next) =>{
	next()
})
```







### 路由级别的中间件

绑定到 express.Router() 实例上的中间件，叫做路由级别的中间件。它的用法和应用级别中间件没有任何区别。只不 过，<font color='#DA924A'>应用级别中间</font><font color='#DA924A'>件是绑定到 app 实例上，路由级别中间件绑定到 router 实例上</font>

```js
const express = require('express')
const router = express.Router()

router.use((req, res, next) =>{
	next()
})

app.use('/',router)
```







### 错误级别的中间件

错误级别中间件的<font color='#DA924A'>作用</font>：专门用来捕获整个项目中发生的异常错误，从而防止项目异常崩溃的问题。

格式：错误级别中间件的 function 处理函数中，<font color='#DA924A'>必须有 4 个形参</font>，形参顺序从前到后，分别是 (err, req, res, next)。

注意：错误级别的中间件， 必须注册在所有路由之后！



```js
const express = require('express')
const app = express()

app.get('/', (req, res) => {            //路由
    throw new Error('服务器发生了错误')   //抛出一个自定义错误
    res.send('Home page')
})

app.use((err,req, res, text) => {               //错误级别的中间件
    console.log('发生了错误' + err.message) //在服务器打印错误消息
    res.send('Error' + err.message)        //请客户端响应错误信息
})
app.listen(80, () => { console.log('http://127.0.0.1') })
```







### Express内置的中间件

<font color='#DA924A'>Express 内置了 3 个常用的中间件</font>

1. express.static 快速托管静态资源的内置中间件，例如： HTML 文件、图片、CSS 样式等（无兼容性）
2. express.json 解析 JSON 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用）
3.  express.urlencoded 解析 URL-encoded 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用）



```js
//1配置解析application/ json 格式数据的内置中间件
app.use(express.json())
// 配置解析 application/ x-Ww- form-ur lencoded格式数据的内置中间件
app.use(express.urlencoded({ extended: false}))
```

```js
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()

// 注意：除了错误级别的中间件，其他的中间件，必须在路由之前进行配置
// 通过 express.json() 这个中间件，解析表单中的 JSON 格式的数据
app.use(express.json())
// 通过 express.urlencoded() 这个中间件，来解析 表单中的 url-encoded 格式的数据
app.use(express.urlencoded({ extended: false }))

app.post('/user', (req, res) => {
  // 在服务器，可以使用 req.body 这个属性，来接收客户端发送过来的请求体数据
  // 默认情况下，如果不配置解析表单数据的中间件，则 req.body 默认等于 undefined
  console.log(req.body)
  res.send('ok')
})

app.post('/book', (req, res) => {
  // 在服务器端，可以通过 req,body 来获取 JSON 格式的表单数据和 url-encoded 格式的数据
  console.log(req.body)
  res.send('ok')
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(80, function () {
  console.log('Express server running at http://127.0.0.1')
})
```







### 第三方的中间件

在 express@4.16.0 之前的版本中，经常使用 <font color='#DA924A'>body-parser 这个第三方中间件</font>，来解析请求体数据。

1. 运行 npm install body-parser 安装中间件 
2. 使用 require 导入中间件 
3. 调用 app.use() 注册并使用中间件

<font color='#DA924A'>注意</font>：Express 内置的 express.urlencoded 中间件，就是基于 body-parser 这个第三方中间件进一步封装出来的。









## 自定义中间件

自己<font color='#DA924A'>手动模拟</font>一个类似于 express.urlencoded 这样的中间件，来<font color='#DA924A'>解析 POST 提交到服务器的表单数据</font>。

1. 定义中间件 
2.  监听 req 的 data 事件 
3. 监听 req 的 end 事件 
4. 使用 querystring 模块解析请求体数据 
5.  将解析出来的数据对象挂载为 req.body 
6. 将自定义中间件封装为模块



 ```js
 //导入处理 querystring 的 node.js 内置模块
 const qs = require('querystring')
 
 const bodyParser = (req, res, next) => {
     // 定义中间件具体业务逻辑
     //在中间件中，需要监听req对象的data事件，来获取客户端发送到服务器的数据。
     //如果数据量比较大，无法- -次性发送完毕， 则客户端会把数据切割后，分批发送到服务器。所以data事件可能会触
     //发多次，每一次触发data事件时，获取到数据只是完整数据的一部分，需要手动对接收到的数据进行拼接。
 
     //1. 定义一个str 字符串，储存客户端发送过来的请求体数据
     let str = ''
 
     //2. 监听req的data 事件
     req.on('data', (chunk) => {
         str += chunk
     })
 
     //当请求体数据接收完毕之后，会自动触发req的end事件。
     //因此，我们可以在req的end事件中，拿到并处理完整的请求体数据.
 
     //3. 监听req的end 事件
     req.on('end', () => {
         //在 str 中存放的时完整的请求体数据
 
         //TODO：把字符串格式额请求体数据转换为对象格式
         const body = qs.parse(str)
         //上游的中间件和下游的中间件及路由之间，共享同一份req和res。因此，我们可以将解析出来的数据,挂载为req
         //的自定义属性，命名为req.body,供下游使用.
         req.body = body
         next()
 
 
     })
 
 }
 module.exports = bodyParser
 ```



```js
const express = require('express')
const app = express()

//导入自己封装的中间件模块
const customBodyParser = require('./08-custom-body-parser')
//将自定义的中间函数，注册为全局可用中间件
app.use(customBodyParser)
app.post('/user', (req, res) => {
    res.send(req.body)
})

app.listen(80, () => { console.log('http://127.0.0.1'); })
```







# 使用 Express 写接口



1. <font color='#DA924A'>创建基础服务器</font>

```js
//导入express 模块
const express = require('express')
const app = express()
const apiRouter = require('./09-路由模块')

//配置解析表单数据的中间件
app.use(express.urlencoded({ extended: false }))

//注册路由
app.use('/api', apiRouter)

//启动服务器
app.listen(80, () => { console.log('http://127.0.0.1') })
```



2. <font color='#DA924A'>创建  api  模块 </font>

```js
const express = require('express')
const apiRouter = express.Router()

apiRouter.get('/get', (req, res) => {
    //获取用户通过请查询符串，发送到服务器的数据
    const query = req.query
    //调用send 方法，把数据返回客户端
    res.send({
        status: 0,           //状态 0 表示成功 1 表示失败
        msg: 'GET请求成功',  //状态描述
        data: query,      //响应给客户端具体数据
    })
})

apiRouter.post('/post', (req, res) => {
    //获取用户通过请求体，发送到服务器的 URL-encoded 数据
    const body = req.body
    //调用send 方法，把数据返回客户端
    res.send({
        status: 0,           //状态 0 表示成功 1 表示失败
        msg: 'POST请求成功',  //状态描述
        data: body,           //响应给客户端具体数据
    })
})

module.exports = apiRouter
```



-----

# 接口的跨域问题

刚才编写的 GET 和 POST接口，存在一个很严重的问题：<font color='#DA924A'>不支持跨域请求。</font> 

解决接口跨域问题的方案主要有两种： 

1. CORS（主流的解决方案，推荐使用） 
2.  JSONP（有缺陷的解决方案：只支持 GET 请求）

##  使用 cors 中间件解决跨域问题

<font color='#DA924A'>使用步骤:</font>

1. 运行 npm install cors 安装中间件
2. 使用 const cors = require('cors') 导入中间件 
3. 在路由之前调用 app.use(cors()) 配置中间件



<font color='#DA924A'>CORS 的注意事项</font>

1. CORS 主要在<font color='#DA924A'>服务器端</font>进行配置。客户端浏览器<font color='#DA924A'>无须做任何额外的配置</font>，即可请求开启了 CORS 的接口。 

2. CORS 在浏览器中<font color='#DA924A'>有兼容性</font>。<font color='#DA924A'>只有支持 XMLHttpRequest Level2 的浏览器</font>，才能正常访问开启了 CORS 的服 务端接口（例如：

   IE10+、Chrome4+、FireFox3.5+）

## CORS 响应头部 - Access-Control-Allow-Origin 

响应头部中可以携带一个 Access-Control-Allow-Origin 字段

```js
Access-Control-Allow-Origin: <origin> | *
```

<font color='#DA924A'>其中，origin 参数的值指定了允许访问该资源的外域 URL</font>。

```js
res.setHeader('Access-Control-Allow-Origin','http://127.0.0.1')
```



如果指定了 Access-Control-Allow-Origin 字段的值为通配符 *，表示允许来自任何域的请求

```js
res.setHeader('Access-Control-Allow-Origin','*')
```



默认情况下，CORS仅支持客户端向服务器发送如下的9个请求头:

Accept、Accept-Language、 Content-Language、 DPR、 Downlink、 Save-Data、 Viewport-Width、 Width 、

Content-Type (值仅限于 text/plain、 multipart/form-data、 application/x-www-form-urlencoded 三者之一)

如果客户端向服务器发送了额外的请求头信息，则需要在服务器端，通过Access-Control- Allow-Headers对额外

的请求头进行声明，否则这次请求会失败!

```js
//允许客户端额外向服务器发送Content-Type 请求头和X-Custom-Header 请求头
//注意:多个请求头之间使用英文的逗号进行分割
res.setHeader( ' Access -Control -Allow-Headers'，' Content-Type, X-Custom-Header' )
```



默认情况下，CORS仅支持客户端发起<font color='#DA924A'>GET、POST、HEAD</font>请求。

如果客户端希望通过PUT、DELETE 等方式请求服务器的资源，则需要在服务器端，通过Access-Control-Alow-Methods

来<font color='#DA924A'>指明实际请求所允许使用的HTTP方法</font>。

```js
//只允许POST、GET、 DELETE、 HEAD请求方法
res. setHeader( ' Access-Control-Allow-Methods', 'POST, GET, DELETE, HEAD')
//允许所有的HTTP请求方法
res. setHeader( ' Access -Control -Allow- Methods'，'')
```

 



## CORS请求的分类

客户端在请求 CORS 接口时，根据请<font color='#DA924A'>求方式和请求头的不同</font>，可以将 CORS 的请求分为<font color='#DA924A'>两大类</font>，

分别是： 

1.  简单请求 
2. 预检请求

<font color='#DA924A'>简单请求</font>

同时满足以下两大条件的请求，就属于简单请求： 

1. 请求方式：GET、POST、HEAD 三者之一 

2. HTTP 头部信息不超过以下几种字段：无自定义头部字段、Accept、Accept-Language、Content-Language、DPR、 Downlink、

   Save-Data、Viewport-Width、Width 、Content-Type（只有三个值application/x-www-formurlencoded、multipart/form-data、text/plain

<font color='#DA924A'>预检请求</font>

只要符合以下任何一个条件的请求，都需要进行预检请求：

1. 请求方式为 GET、POST、HEAD 之外的请求 Method 类型 

2. 请求头中包含自定义头部字段 

3. 向服务器发送了 application/json 格式的数据 

   

在浏览器与服务器正式通信之前，浏览器<font color='#DA924A'>会先发送 OPTION 请求进行预检，以获知服务器是否允许该实际请求</font>，所以这一 次的 OPTION 请求称为“预检请求”。<font color='#DA924A'>服务器成功响应预检请求后，才会发送真正的请求，并且携带真实数据</font>。

简单请求和预检请求的<font color='#DA924A'>区别</font> 

<font color='#DA924A'>简单请求的特点：</font>

客户端与服务器之间只会发生一次请求。 



<font color='#DA924A'>预检请求的特点：</font>

客户端与服务器之间会发生两次请求，OPTION 预检请求成功之后，才会发起真正的请求。





## JSONP 接口

概念：浏览器端通过 ,<script>标签的 src 属性，请求服务器上的数据，同时，服务器返回一个函数的调用。这种请求数据 的方式叫做 JSONP。

<font color='#DA924A'>特点：</font>

1. JSONP 不属于真正的 Ajax 请求，因为它没有使用 XMLHttpRequest 这个对象。 
2. JSONP 仅支持 GET 请求，不支持 POST、PUT、DELETE 等请求。

<font color='#DA924A'>创建 JSONP 接口的注意事项 </font>

如果项目中<font color='#DA924A'>已经配置了 CORS</font> 跨域资源共享，为了<font color='#DA924A'>防止冲突</font>，<font color='#DA924A'>必须在配置 CORS 中间件之前声明 JSONP 的接口</font>。否则 JSONP 接口会

被处理成开启了 CORS 的接口。示例代码如下

<font color='#DA924A'>实现 JSONP 接口的步骤 </font>

1. 获取客户端发送过来的回调函数的名字 
2. 得到要通过 JSONP 形式发送给客户端的数据 
3. 根据前两步得到的数据，拼接出一个函数调用的字符串 
4. 把上一步拼接得到的字符串，响应给客户端的 

```js
app.get(' /api/jsonp, (req,res) => {
// 1.获取客户端发送过来的回调函数的名字
const funcName = req. query . callback
// 2.得到要通过JSONP形式发送给客户端的数据
const data = { name :'zs'age: 22 }
//根据前两步得到的数据， 拼接出一个函数调用的字符串
const scriptStr =`${funcName}(${JSON.stringify(data)})`
// 4.把上一步拼接得到的字符串，响应给客户端的<script> 标签进行解析执行
res. send(scriptStr)
})
```







# 解决跨域

<font color='#DA924A'>cors方法</font>

```js
//在路由之前配置cors 这个中间件，解决跨域问题
const cors = require('cors')
app.use(cors())
```



-----



# MySQL

## 数据库的基本概念

数据库（database）是用来<font color='#DA924A'>组织</font>、<font color='#DA924A'>存储</font>和管理<font color='#DA924A'>数据</font>的仓库。

为了方便管理互联网世界中的数据，就有了<font color='#DA924A'>数据库管理系统的概念</font>（简称：数据库）。用户可以对数据库中的数 据进行<font color='#DA924A'>新增</font>、<font color='#DA924A'>查询</font>、<font color='#DA924A'>更</font>

<font color='#DA924A'>新</font>、<font color='#DA924A'>删除</font>等操作。





## 常见的数据库及分类

1. MySQL 数据库（目前使用最广泛、流行度最高的开源免费数据库；Community + Enterprise） 
2. Oracle 数据库（收费） 
3. SQL Server 数据库（收费） 
4.  Mongodb 数据库（Community + Enterprise）



其中，MySQL、Oracle、SQL Server 属于<font color='#DA924A'>传统型数据库</font>（又叫做：<font color='#DA924A'>关系型数据库</font> 或<font color='#DA924A'> SQL 数据库</font>），这三者的 设计理念相同，用法比较类似。



而 Mongodb 属于<font color='#DA924A'>新型数据库</font>（又叫做：<font color='#DA924A'>非关系型数据库 或 NoSQL 数据库</font>），它在一定程度上弥补了传统型 数据库的缺陷。







## 传统型数据库的数据组织结构

<font color='#DA924A'>数据的组织结构</font>：指的就是数据以什么样的结构进行存储。



传统型数据库的数据组织结构，与 Excel 中数据的组织结构 比较类似。

在传统型数据库中，数据的组织结构分为<font color='#DA924A'>数据库</font>(database)、<font color='#DA924A'>数据表</font>(table)、<font color='#DA924A'>数据行</font>(row)、<font color='#DA924A'>字段</font>(field)这 4 大部分组成。





### 实际开发中库、表、行、字段的关系

1. 在实际项目开发中，一般情况下，每个项目都对应独立的数据库。 
2. 不同的数据，要存储到数据库的不同表中，例如：用户数据存储到 users 表中，图书数据存储到 books 表中。
3. 每个表中具体存储哪些信息，由字段来决定，例如：我们可以为 users 表设计 id、username、password 这 3 个 字段。 
4. 表中的行，代表每一条具体的数据。





## 安装并配置 MySQL

安装 MySQL Server 和 MySQL Workbench 这两个软件，就能满足开发的需要了。

1. <font color='#DA924A'>MySQL Serve</font>r：专门用来提供数据存储和服务的软件。 
2. <font color='#DA924A'>MySQL Workbench</font>：可视化的 MySQL 管理工具，通过它，可以方便的操作存储在 MySQL Server 中的数据。

只需要运行 <font color='#DA924A'>mysql-installer-community-8.0.19.0.msi 这个安装包</font>，就能一次 性将 MySQL Server 和 MySQL Workbench 安装到自己的电脑上。



##  使用 MySQL Workbench 管理数据库

![屏幕截图 2022-06-25 144800](D:\JAVAWeb\WbeNotes\图片\node\屏幕截图 2022-06-25 144800.png)

![屏幕截图 2022-06-25 145139](D:\JAVAWeb\WbeNotes\图片\node\屏幕截图 2022-06-25 145139.png)





![屏幕截图 2022-06-25 145240](D:\JAVAWeb\WbeNotes\图片\node\屏幕截图 2022-06-25 145240.png)





![屏幕截图 2022-06-25 145332](D:\JAVAWeb\WbeNotes\图片\node\屏幕截图 2022-06-25 145332.png)



![屏幕截图 2022-06-25 145413](D:\JAVAWeb\WbeNotes\图片\node\屏幕截图 2022-06-25 145413.png)



MySQL Workbench删除数据库表

右击要删除的实例表，点击【drop table..】

在弹出的对话框中，点击【drop now】

## 使用 SQL 管理数据库

SQL（英文全称：Structured Query Language）是<font color='#DA924A'>结构化查询语言</font>，专门用来<font color='#DA924A'>访问和处理数据库</font>的编程语言。能够让 我们以<font color='#DA924A'>编程的形式，操作数据库里面的数据</font>。



1. SQL 是一门数据库编程语言 
2. 使用 SQL 语言编写出来的代码，叫做 SQL 语句 
3. SQL 语言只能在关系型数据库中使用（例如 MySQL、Oracle、SQL Server）。非关系型数据库（例如 Mongodb） 不支持 SQL 语言



<font color='#DA924A'>作用：</font>

1. 从数据库中查询数据
2.  向数据库中插入新的数据 
3.  更新数据库中的数据 
4. 从数据库删除数据 
5.  可以创建新数据库 
6.  可在数据库中创建新表 
7. 可在数据库中创建存储过程、视图 
8.  etc...



### SQL 的 SELECT 语句

<font color='#DA924A'>SELECT </font>语句用于<font color='#DA924A'>从表中查询数据</font>。执行的结果被存储在一个<font color='#DA924A'>结果表</font>中（称为结果集）。

```sql
--这是注释
--从FROM指定的[表中] ,查询出[所有的]数据。 *表示[所有列]
SELECT * FROM 表名称
--从FROM指定的[表中] ,查询出指定列名称(字段) 的数据。
SELECT 列名称 FROM 表名称
```

<font color='#DA924A'>注意</font>：SQL 语句中的关键字对<font color='#DA924A'>大小写不敏感</font>。SELECT 等效于 select，FROM 等效于 from。





###  SQL 的 INSERT INTO 语句

<font color='#DA924A'>INSERT INTO </font>语句用于向数据表中插入新的数据行

```sql
--语法解读:向指定的表中，插入如下几列数据，列的值通过values —— 指定
--注意:列和值要对应， 多个列和多个值之间，使用英文的逗号分隔
INSERT INTO 表名 (列1, 列2,...) VALUES (值1, 值2.....) 
```





### SQL 的 UPDATE 语句

<font color='#DA924A'>Update</font>语句用于修改表中的数据。

```mysql
--语法解读:
--1.用UPDATE指定要更新哪个表中的数据
--2.用SET指定列对应的新值
--3.用WHERE指定更新的条件
UPDATE 表名称 SET 列名称 = 新值可以同时更改多个，列名称 = 新值 WHERE 列名称=某值    --id = 2 修改第二行
```



### SQL 的 DELETE 语句

<font color='#DA924A'>DELETE </font>语句用于删除表中的行。

```mysql
--语法解读:
--从指定的表中，根据WHERE条件，删除对应的数据行
DELETE FROM 表名称 WHERE 列名称 = 值   //id = 4  删除第四行
```





###  SQL 的 WHERE 子句

WHERE 子句用于限定选择的标准。在 SELECT、UPDATE、DELETE 语句中，皆可使用 WHERE 子句来限定选择的标准。

```mysql
--查询语句中的 WHERE 条件
SELECT 列名称 FROM 表名称 WHERE 列运算符值
--更新语句中的 WHERE 条件
UPDATE 表名称 SET 列 = 新值 WHERE 列 运算符 值
--删除语句中的 WHERE 条件
DELETE FROM 表名称 WHERE 列 运算符 值
```

<font color='#DA924A'>WHERE 可以使用的运算符</font>

| 操作符  | 描述         |
| ------- | ------------ |
| =       | 等于         |
| <>      | 不等于       |
| >       | 大于         |
| <       | 小于         |
| <=      | 小于等于     |
| >=      | 大于等于     |
| BETWEEW | 在某个范围   |
| LIKE    | 搜索某种模式 |

<font color='#DA924A'>注意：</font>在某些版本的 SQL 中，操作符 <> 可以写为 !=



<font color='#DA924A'>WHERE 子句示例</font>

```mysql
--查询 status 为1的所有用户
SELECT * FROM users WHERE status = 1 
--查询 id 大于 2 的所有用户
SELECT * FROM users WHERE id > 2 
查询 username 不等于 admin 的所有用户
SELECT * FROM users WHERE username<> 'admin'
```





### SQL 的 AND 和 OR 运算符

AND 和 OR 可在 <font color='#DA924A'>WHERE 子语句中把两个或多个条件结合起来。 </font>

AND <font color='#DA924A'>表示必须同时满足多个条件</font>，相当于 JavaScript 中的 && 运算符，例如 <font color='#DA924A'>if (a !== 10 && a !== 20)</font>

OR 表示<font color='#DA924A'>只要满足任意一个条件即可</font>，相当于 JavaScript 中的 || 运算符，例如<font color='#DA924A'> if(a !== 10 || a !== 20)</font>





### SQL 的 ORDER BY 子句

ORDER BY 语句用于根据指定的列对结果集进行排序。 

ORDER BY 语句<font color='#DA924A'>默认按照升序</font>对记录进行排序。<font color='#DA924A'>升序ORDER BY ASC</font> 

如果您希望按照<font color='#DA924A'>降序</font>对记录进行排序，可以使用 <font color='#DA924A'>DESC</font> 关键字。

```mysql
--按照 id 的升序排列
SELECT * FROM users OREDER BY id
SELECT * FROM users OREDER BY id ASC
--按照降序
SELECT * FROM users PREDER BY id DESC
```



### ORDER BY 子句 – 多重排序

```mysql
--先按照 id 排序 在按照 status 排序
SELECT * FROM users OREMDER BY id DESC, status ASC
```





###  SQL 的 COUNT(*) 函数

 <font color='#DA924A'>COUNT(*)</font>函数用于返回<font color='#DA924A'>查询结果的总数据条数</font>

```mysql
SELECT COUNT(*) FROM 表名
```

查询 users 表中 status 值为 0 的总数据条数

```mysql
SELECT COUNT(*) FROM users WHERE status = 0   //status = 0 的有几个
--返回  列名 COUNT 值 3
```

<font color='#DA924A'>使用 AS 为列设置别名</font>

```mysql
--使用 AS 为列设置别名
SELECT COUNT(*) AS total FROM users WHERE status = 0
--返回 列名 total 值 3
```





## 在项目中操作 MySQL



1. 安装操作 MySQL 数据库的第三方模块（mysql） 
2. 通过 mysql 模块连接到 MySQL 数据库 
3. 通过 mysql 模块执行 SQL 语句

在使用 mysql 模块操作 MySQL 数据库之前，必须先对 mysql 模块进行必要的配置

```js
//导入MySQL 模块
const mysql = require('mysql')
//建立于数据库的链接
const db = mysql.createPool({
    host: '127.0.0.1',  //数据库的 IP 地址
    user: 'root',       //登录数据库的账号
    password: 'admin123', //登录数据库密码
    database: 'my_demo_01' //指定要操作的数据库
})

```



### 测试 mysql 模块能否正常工作

```js
db.query('SELECT 1', (err,results) =>{   // 1 指定属性索引 只是测试用
    if(err) return console.log(err.message)
    console.log(results)  //输出
})	
```



### 查询数据

```js
// 查询 users 表中的所有用户数据
db.query('SELECT * FROM users', (err,results) =>{
	//查询失败
    if(err) return console.log(err.message)
    //查询成功
    console.log(results)
})
```





### 插入数据

向 users 表中新增数据， 其中 username 为 Spider-Man，password 为 pcc321。

```js
//要插入到 users 表中的数据
const user = {username: 'Spider-Man',password: 'pcc321'}
//执行 SQL 语句，其中 ？ 表示占位符
const sqlStr = 'INSERT INTO users (username, password) VALUES (?, ?)'
//使用数组的形式。依次 ？ 占位符指定具体的值
//注意： 如果SQL 语句中有多个占位符，则必需使用数组为每个占位符指定具体的值
//       如果SQL 语句中只有一个占位符，则可以省略数组
db.query(sqlStr,[user.username, user.password], (err, results) =>{
    if(err) return console.log(err.message)  //失败
    if(results.affectedRows === 1) {console.log('插入数据成功')}  //成功
})   //results.affectedRows  判断  const sqlStr = 'INSERT INTO users (username, password) VALUES (?, ?)'  
//    影响的hang'shu
```



###  插入数据的便捷方式

向表中新增数据时，如果数据对象的<font color='#DA924A'>每个属性</font>和<font color='#DA924A'>数据表的字段一一对应</font>，则可以通过如下方式快速·插入数据：

```js
//要插入到 users 表中的数据
const user = {username: 'Spider-Man',password: 'pcc4321'}
//执行 SQL 语句，其中 ？ 表示占位符
const sqlStr = 'INSERT INTO users SET ?'
//使用数组的形式。依次 ？ 占位符指定具体的值
db.query(sqlStr,user, (err, results) =>{
    if(err) return console.log(err.message)  //失败
    if(results.affectedRows === 1) {console.log('插入数据成功')}  //成功
})
```





###  更新数据

```js
//更新数据
const user = { id: 6, username: 'aaa', password: '40000' }
//执行 SQL 语句，其中 ？ 表示占位符
const sqlStr = 'UPDATE users SET username=?,password=? WHERE id=?'
//使用数组的形式。依次 ？ 占位符指定具体的值
db.query(sqlStr, [user.username, user.password, user.id], (err, results) => {
    if (err) return console.log(err.message)  //失败
    if (results.affectedRows === 1) { console.log('插入数据成功') }  //成功
})
```







### 更新数据的便捷方式

更新表数据时，如果数据对象的每个属性和数据表的字段一一对应，则可以通过如下方式快速更新表数据：

```js
//更新数据
const user = { id: 6, username: 'aaa', password: '000' }
//执行 SQL 语句，其中 ？ 表示占位符
const sqlStr = 'UPDATE users SET ? WHERE id=?'
//使用数组的形式。依次 ？ 占位符指定具体的值
db.query(sqlStr, [user, user.id], (err, results) => {
    if (err) return console.log(err.message)  //失败
    if (results.affectedRows === 1) { console.log('插入数据成功') }  //成功
})
```



### 删除数据

在删除数据时，推荐<font color='#DA924A'>根据 id </font>这样的唯一标识，来<font color='#DA924A'>删除对应的数据。</font>

```js
//要执行的 sql 语句
const sqlStr = 'DELETE FROM users WHERE id=?'
//调用 db.query() 执行 SQL 语句同时，为占位符指定具体值
db.query(sqlStr, 6, (err, results) => {
    if (err) return console.log(err.message)  //失败
    if (results.affectedRows === 1) { console.log('删除数据') }  //成功
})
```

### 标记删除

1. 使用 DELETE 语句，会把真正的把数据从表中删除掉。

2. 为了保险起见，推荐使用标记删除的形式，来模拟删除的动作。 

3. 所谓的标记删除，就是在表中设置类似于 status 这样的状态字段，来标记当前这条数据是否被删除。 

4. 当用户执行了删除的动作时，我们并没有执行 DELETE 语句把数据删除掉，而是执行了 UPDATE 语句，将这条数据对应 的 status 

​       字段标记为删除即可。



```js
db.query('UPDATE users SET status=1 WHERE id=?', 6, (err, results) =>{
    if(err) return console.log(err.message)  //失败
    if(results.affectedRows === 1) {console.log('插入数据成功')}  //成功
})
```



---

# Web 开发模式

服务端渲染的 Web 开发模式

<font color='#DA924A'>服务端渲染的概念</font>：服务器<font color='#DA924A'>发送给客户端的 HTML 页面</font>，是在<font color='#DA924A'>服务器通过字符串的拼接，动态生</font><font color='#DA924A'>成的</font>。因此，客户端不 需要使用 Ajax 这

样的技术额外请求页面的数据。



目前主流的 Web 开发模式有两种，分别是：

​     ① 基于<font color='#DA924A'>服务端渲染</font>的传统 Web 开发模式 

​     ② 基于<font color='#DA924A'>前后端分离</font>的新型 Web 开发模式





## 服务端渲染的 Web 开发模式



<font color='#DA924A'>服务端渲染的概念：</font>

服务器发送给客户端的 HTML 页面，是在服务器通过字符串的拼接，动态生成的。因此，客户端不 需要使用 Ajax 这样的技术额外请求页面的数据。

```js
app . get( '/index.html', (req, res) => {
// 1.要渲染的数据
const user = { name:'ZS',age:20 }
// 2.服务器端通过字符串的拼接，动态生成HTML内容
const html =`<h1>姓名: ${user . name},年龄: ${user . age}</h1>`
// 3.把生成好的页面内容响应给客户端。因此，客户端拿到的是带有真实数据的HTML页面
res. send(html )
})
```



<font color='#DA924A'>优点:</font>

1. 前端耗时少。因为服务器端负责动态生成HTML内容,浏览器只需要直接渲染页面即可。尤其是移动端，更省电。
2. 有利于SEO. 因为服务器端响应的是完整的HTML页面内容，所以爬虫更容易爬取获得信息，更有利于SEO。
   

<font color='#DA924A'>缺点:</font>

1. 占用服务器端资源。 即服务器端完成HTML页面内容的拼接,如果请求较多，会对服务器造成一定的访问压力。
2. 不利于前后端分离，开发效率低。使用服务器端渲染,则无法进行分工合作，尤其对于前端复杂度高的项目，不利于
   项目高效开发。





## 前后端分离的 Web 开发模式

前后端分离的概念：前后端分离的开发模式，<font color='#DA924A'>依赖于 Ajax 技术的广泛应用</font>。

简而言之，前后端分离的 Web 开发模式， 就是<font color='#DA924A'>后端只负责提供 API 接口，前端使用 Ajax 调用接口的开发模式。</font>





<font color='#DA924A'>优点:</font>

​    ①开发体验好。前端专注于UI页面的开发,后端专注于api的开发，且前端有更多的选择性。

​    ②用户体验好。 Ajax 技术的广泛应用，极大的提高了用户的体验，可以轻松实现页面的局部刷新。

​    ③减轻了服务器端的渲染压力。因为页面最终是在每个用户的浏览器中生成的。

<font color='#DA924A'>缺点:</font>

​    ①不利于 SEO。因为完整的HTML页面需要在客户端动态拼接完成，所以爬虫无法爬取页面的有效信息。(解决方

​    案:利用Vue、React 等前端框架的SSR (server side render)技术能够很好的解决SEO问题! )



## 身份认证

<font color='#DA924A'>身份认证</font>（Authentication）又称“身份验证”、“鉴权”，是指<font color='#DA924A'>通过一定的手段，完成对用户身份的确认</font>。 

​     ⚫ 日常生活中的身份认证随处可见，例如：高铁的验票乘车，手机的密码或指纹解锁，支付宝或微信的支付密码等。 

​     ⚫ 在 Web 开发中，也涉及到用户身份的认证，例如：各大网站的手机验证码登录、邮箱密码登录、二维码登录等。



身份认证的目的，是为了<font color='#DA924A'>确认当前所声称为某种身份的用户，确实是所声称的用户</font>。



对于服务端渲染和前后端分离这两种开发模式来说，分别有着不同的身份认证方案： 

​     ① <font color='#DA924A'>服务端渲染</font>推荐使用 Session 认证机制 

​     ② <font color='#DA924A'>前后端分离</font>推荐使用 JWT 认证机制







## Session 认证机制

<font color='#DA924A'>HTTP 协议的无状态性</font>

指的是客户端的<font color='#DA924A'>每次 HTTP 请求都是独立的</font>，连续多个请求之间没有直接的关系，<font color='#DA924A'>服务器不会 主动保留每次 HTTP 请求的状态</font>。

现实生活中的会员卡身份认证方式，在 Web 开发中的专业术语叫做 <font color='#DA924A'>Cookie</font>。

### Cookie

Cookie 是<font color='#DA924A'>存储在用户浏览器中的一段不超过 4 KB 的字符串</font>。它由一个<font color='#DA924A'>名称</font>（Name）、一个<font color='#DA924A'>值</font>（Value）和其它几个用 于控制 Cookie <font color='#DA924A'>有</font><font color='#DA924A'>效期、安全性、使用范围的可选属性组成</font>。

不同域名下的 Cookie 各自独立，每当客户端发起请求时，会<font color='#DA924A'>自动</font>把<font color='#DA924A'>当前域名下</font>所有<font color='#DA924A'>未过期的</font> Cookie 一同发送到服务器。

 Cookie的几大特性：

​     ① 自动发送 

​     ② 域名独立 

​     ③ 过期时限

​     ④ 4KB 限制



客户端第一次请求服务器的时候，服务器<font color='#DA924A'>通过响应头的形式</font>，向客户端发送一个身份认证的 Cookie，客户端会自动 将 Cookie 保存在浏览器中。

随后，当客户端浏览器每次请求服务器的时候，浏览器会<font color='#DA924A'>自动</font>将身份认证相关的 Cookie，通过<font color='#DA924A'>请求头的形式发送给 服务器</font>，服务器即可验明客户端的身份。

<font color='#DA924A'>Cookie 不具有安全性</font>

由于 Cookie 是存储在浏览器中的，而且<font color='#DA924A'>浏览器也提供了读写 Cookie 的 API</font>，因此 <font color='#DA924A'>Cookie 很容易被伪造</font>，不具有安全 性。因此不建议服务器将重要的隐私数据，通过 Cookie 的形式发送给浏览器。

<font color='#DA924A'>注意</font>：千万不要使用 Cookie 存储重要且<font color='#D26B6B'>隐私的数据</font>！





### Session 的工作原理

![屏幕截图 2022-06-27 164201](D:\JAVAWeb\WbeNotes\图片\node\屏幕截图 2022-06-27 164201.png)

Session 认证机制需要<font color='#DA924A'>配合 Cookie 才能实现</font>。由于 Cookie 默认<font color='#DA924A'>不支持跨域访问</font>，所以，当涉及到前端跨域请求后端接 口的时候，需要

做<font color='#DA924A'>很多额外的配置</font>，才能实现跨域 Session 认证。

<font color='#DA924A'>注意</font>： 

1.  当前端请求后端接口<font color='#DA924A'>不存在跨域问题的时候</font>，推荐使用 Session 身份认证机制。
2.  当前端需要跨域请求后端接口的时候，不推荐使用 Session 身份认证机制，推荐使用 JWT 认证机制。

## 在 Express 中使用 Session 认证

1. 安装 express-session 中间件

```c
npm install express-session
```



2. 配置 express-session 中间件

```js
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()

// TODO_01：请配置 Session 中间件
const session = require('express-session')
app.use(
  session({       //secret 属性的值可以是任意字符
    secret: 'itheima',   	//固定写法
    resave: false,
    saveUninitialized: true,   	//固定写法
  })  
)
```

3. 向 session 中存数据

```js
// 托管静态页面
app.use(express.static('./pages'))
// 解析 POST 提交过来的表单数据
app.use(express.urlencoded({ extended: false }))

// 登录的 API 接口
app.post('/api/login', (req, res) => {
  // 判断用户提交的登录信息是否正确
  if (req.body.username !== 'admin' || req.body.password !== '000000') {
    return res.send({ status: 1, msg: '登录失败' })
  }

  // TODO_02：请将登录成功后的用户信息，保存到 Session 中
  // 注意：只有成功配置了 express-session 这个中间件之后，才能够通过 req 点出来 session 这个属性
  req.session.user = req.body // 用户的信息
  req.session.islogin = true // 用户的登录状态

  res.send({ status: 0, msg: '登录成功' })
})
```





4. 从 session 中取数据

```js
// 获取用户姓名的接口
app.get('/api/username', (req, res) => {
  // TODO_03：请从 Session 中获取用户的名称，响应给客户端
  if (!req.session.islogin) {
    return res.send({ status: 1, msg: 'fail' })
  }
  res.send({
    status: 0,
    msg: 'success',
    username: req.session.user.username,
  })
})
```



5. 清空 session

调用 <font color='#DA924A'>req.session.destroy() 函数</font>，即可清空服务器保存的 session 信息。

```js
// 退出登录的接口
app.post('/api/logout', (req, res) => {
  // TODO_04：清空 Session 信息
  req.session.destroy()
  res.send({
    status: 0,
    msg: '退出登录成功',
  })
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(80, function () {
  console.log('Express server running at http://127.0.0.1:80')
})
```





## JWT 认证机制

### JWT（英文全称：JSON Web Token）

是目前<font color='#DA924A'>最流行的跨域认证解决方案</font>。

![屏幕截图 2022-06-27 200316](D:\JAVAWeb\WbeNotes\图片\node\屏幕截图 2022-06-27 200316.png)



<font color='#DA924A'>总结</font>：用户的信息通过 Token 字符串的形式，保存在客户端浏览器中。服务器通过还原 Token 字符串的形式来认证用户的身份。

JWT 通常由三部分<font color='#DA924A'>组成</font>，<font color='#DA924A'>分别是 Header（头部</font>）、<font color='#DA924A'>Payload（有效荷载）</font>、<font color='#DA924A'>Signature（签名）</font>。

<font color='#DA924A'>三者之间使用英文的      “ . ”    分隔</font>

```c
Header.Payload.Signature
```





<font color='#DA924A'>JWT 字符串的示例</font>

```c
eyJhbGci0i JIUzI1NiIsInR5cCI6IkpXVCJ9. eyJpZCI6MSwidXN1cm5hbwUi0i JhZG1pbiIs InBhc3N3b3 JkIjoiIiwibmlja25
hbWUi0iLms6Xlt7Tlt7QiLC J1bWF pbC I6 Im5pYmF iYUBpdGNhc3QUY24iLC J1c2VyX3BpYyI6IiIs Im1hd I6MTU3ODAzNjY4Miw
iZXhwI joxNTc4MDcyNjgy fQ . Mwq7GqCx JPK- EA8LNr tMG041lKdZ3359KBL 3XeuBxuI
```



### JWT 的三个部分各自代表的<font color='#DA924A'>含义</font>:

1. <font color='#DA924A'>Payload</font> 部分才是<font color='#DA924A'>真正的用户信息</font>，它是用户信息经过加密之后生成的字符串。 
2. Header 和 Signature 是<font color='#DA924A'>安全性相关</font>的部分，只是为了保证 Token 的安全性。



### JWT 的使用方式

客户端收到服务器返回的 JWT 之后，通常会将它储存在 <font color='#DA924A'>localStorage </font>或 <font color='#DA924A'>sessionStorage</font> 中。

此后，客户端每次与服务器通信，都要带上这个 JWT 的字符串，从而进行身份认证。推荐的做法是把 <font color='#DA924A'>JWT 放在 HTTP  请求头的</font> <font color='#DA924A'>Authorization 字段</font>中

```c
Authorization: Bearer <token>
```





### 在 Express 中使用 JWT

1. 运行如下命令，安装如下两个 JWT 相关的包：

```c
npm install jsonwebtoken express-jwt
# jsonwebtoken 用于生成 JWT 字符串
# express-jwt 用于将 JWT 字符串解析还原成 JSON 对象
```

2. 

```js
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()

// TODO_01：安装并导入 JWT 相关的两个包，分别是 jsonwebtoken 和 express-jwt
const jwt = require('jsonwebtoken')
const expressJWT = require('express-jwt')
// 允许跨域资源共享
const cors = require('cors')    //安装了cors包
app.use(cors())

// 解析 post 表单数据的中间件
const bodyParser = require('body-parser')    //安装了body-parser 包
app.use(bodyParser.urlencoded({ extended: false }))  
```



3. 定义 secret 密钥

>为了<font color='#DA924A'>保证 JWT 字符串的安全性</font>，防止 JWT 字符串在网络传输过程中被别人破解，我们需要专门定义一个用于<font color='#DA924A'>加密</font>和<font color='#DA924A'>解密</font> 的 secret 密钥： 
>
>① 当生成 JWT 字符串的时候，需要使用 secret 密钥对用户的信息<font color='#DA924A'>进行加密</font>，最终得到加密好的 JWT 字符串 
>
>② 当把 JWT 字符串解析还原成 JSON 对象的时候，需要使用 secret 密钥进行<font color='#DA924A'>解密</font>

```js
// TODO_02：定义 secret 密钥，建议将密钥命名为 secretKey
const secretKey = 'itheima No1 ^_^'
```

4. 将 JWT 字符串还原为 JSON 对象

>客户端每次在访问那些有权限接口的时候，都需要主动<font color='#DA924A'>通过请求头中的 Authorization 字段</font>，将 Token 字符串发 送到服务器进行身份认证。
>
>此时，服务器可以通过 express-jwt 这个中间件，自动将客户端发送过来的 Token 解析还原成 JSON 对象

```js
// TODO_04：注册将 JWT 字符串解析还原成 JSON 对象的中间件
// 注意：只要配置成功了 express-jwt 这个中间件，就可以把解析出来的用户信息，挂载到 req.user 属性上
//使用app.use()来注册中间件
// expressJWT({ secret: secretKey })就是用来解析Token的中间件
// .unless({ path: [/^\/api\//] })用来指定哪些接口不需要访问权限
app.use(expressJWT({ secret: secretKey }).unless({ path: [/^\/api\//] })
```





5. 在登录成功后生成 JWT 字符串

调用 jsonwebtoken 包提供的<font color='#DA924A'> sign() 方法</font>，将用户的信息加密成 JWT 字符串，响应给客户端

```js
// 登录接口
app.post('/api/login', function (req, res) {
  // 将 req.body 请求体中的数据，转存为 userinfo 常量
  const userinfo = req.body
  // 登录失败
  if (userinfo.username !== 'admin' || userinfo.password !== '000000') {
    return res.send({
      status: 400,
      message: '登录失败！',
    })
  }
  // 登录成功
  // TODO_03：在登录成功之后，调用 jwt.sign() 方法生成 JWT 字符串。并通过 token 属性发送给客户端
  // 参数1：用户的信息对象
  // 参数2：加密的秘钥
  // 参数3：配置对象，可以配置当前 token 的有效期
  // 记住：千万不要把密码加密到 token 字符中
  const tokenStr = jwt.sign({ username: userinfo.username }, secretKey, { expiresIn: '30s' })   //有效时间 30s
  res.send({
    status: 200,
    message: '登录成功！',
    token: tokenStr, // 要发送给客户端的 token 字符串
  })
})
```





6. 使用 req.user 获取用户信息

```js
// 这是一个有权限的 API 接口
app.get('/admin/getinfo', function (req, res) {
  // TODO_05：使用 req.user 获取用户信息，并使用 data 属性将用户信息发送给客户端
  console.log(req.user)
  res.send({
    status: 200,
    message: '获取用户信息成功！',
    data: req.user, // 要发送给客户端的用户信息
  })
})
```



7. 捕获解析 JWT 失败后产生的错误

> 当使用 express-jwt 解析 Token 字符串时，如果客户端发送过来的 Token 字符串<font color='#DA924A'>过期或不合法</font>，会产生一个<font color='#DA924A'>解析失败 </font>的错误，影响项目
>
> 的正常运行。我们可以通过<font color='#DA924A'> Express 的错误中间件</font>，捕获这个错误并进行相关的处理



```js
// TODO_06：使用全局错误处理中间件，捕获解析 JWT 失败后产生的错误
app.use((err, req, res, next) => {
  // 这次错误是由 token 解析失败导致的
  if (err.name === 'UnauthorizedError') {
    return res.send({
      status: 401,
      message: '无效的token',
    })
  }
  res.send({
    status: 500,
    message: '未知的错误',
  })
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(8888, function () {
  console.log('Express server running at http://127.0.0.1:8888')
})
```

