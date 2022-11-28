# 初识AJAX

 URL地址: 统一资源定位符,用于标识互联网上每个资源唯一存放位置。
     <font color='#D26B6B'>URL组成</font> : 

          1. 客户端与服务之间的通讯协议
          2. 该资源的服务器名称
          3. 资源在服务器上的具体存放位置




| 通信过程: |
| :-------- |
| 请求      |
| 处理      |
| 响应      |

​        网页中请求数据
​        let xhrObj = new XMLHttpRequest();
​        js 成员可以通过它请求服务器上的数据资源
————————————————————————​    

​         客户端请求服务器时
​         用get 和 post
​         get 用于从服务器获取资源
​         post 向服务器提交资源

————————————————————————​    



 *AJAX : 在网页中利用 XMLHttpRequest 对象和服务器进行数据交互的方式*。

​    *实先数据交互*

————————————————————————​    



​    *应用场景*

​    *动态检测用户名查重*

​    *搜索提示*

​    *动态刷新表格数据*

------

# Jquery中的AJAX

## <u><font color='#D26B6B'>GET请求</font></u>

<font color='#DA924A'>get 用于从服务器获取资源</font>

 **$.get(url,[data],[callback])**

| url :      | 地址                       |
| ---------- | -------------------------- |
| data:      | 请求资源要携带的参数  可选 |
| callback : | 请求成功时的回调函数  可选 |



```javascript
//<button id="btnGET">按钮</button>
$(function () {   //on可以注册多个事件
            $('#btnGET').on('click', function () {                    //res 接受服务器返回的数据
                $.get('http://www.liulongbin.top:3006/api/getbooks', function (res) {
                    console.log(res);
                })
            })
            //带参数
            $('#btnGET1').on('click', function () {           //请求id 为1的参数信息    //res 接受服务器返回的数据
                $.get('http://www.liulongbin.top:3006/api/getbooks', { id: 1 }, function (res) {
                    console.log(res);
                })
            })
        })
```



## <u><font color='#D26B6B'>post请求</font></u>

<font color='#DA924A'>post 向服务器提交资源</font>

***$.post(url,[data],[callback])***

| url :      | 地址                           |
| ---------- | ------------------------------ |
| data:      | 要提交的数据  可选             |
| callback : | 数据提交成功时的回调函数  可选 |



```javascript
//<button id="btnPOST">按钮</button>
$(function () {
            $('#btnPOST').on('click', function () {
                $.post('http://www.liulongbin.top:3006/api/addbook',  //d地址
                    { bookname: '请w求', author: '吴', publisher: '上海w河南' },  //提交的数据
                    function (res) {   //回调函数
                        console.log(res);
                    }
                )
            })
        })
```





## <u><font color='#D26B6B'>JQ独有的AJAX</font></u>

*$.ajax(type,url,[data],[callback])  功能综合的函数*

| type:    | *请求方式,例如 get和post  type:'get'* |
| -------- | ------------------------------------- |
| url :    | *地址*                                |
| data:    | 携带的数据                            |
| success: | *请求成功时的回调函数  可选*          |



## <u><font color='#D26B6B'>GET请求</font></u>

比如登录如果密码错误result.success的值就是false一般还会有一个msg=‘密码错误’ 如果密码和账号正确就会返回result.success=true执行后续的代码。这个数据结构是前后端一起协商定义的格式

```javascript
//<button id="btnGET">按钮</button>
$(function () {
            $('#btnGET').on('click', function () {
                $.ajax({
                    type: 'GET',
                    url: 'http://www.liulongbin.top:3006/api/getbooks',
                    data: {
                        id: 1
                    },
                    success: function (res) {//success  请求成功后回调函数。这个方法有两个参数：服务器返回数据，返回状态
                        console.log(res);
                    }
                });
            });
        });
```





## <u><font color='#D26B6B'>POST请求</font></u>

```javascript
//<button id="btnPOST">POST按钮</button>
$(function () {
            $('#btnPOST').on('click', function () {
                $.ajax({
                    type: 'POST',
                    url: 'http://www.liulongbin.top:3006/api/addbook',
                    data: {
                        bookname: '我请求',
                        author: '我吴',
                        publisher: '我我河南'
                    },
                    success: function (res) {
                        console.log(res);
                    }
                });
            });
        });
```

------



# <u><font color='#D26B6B'>接口</font></u>

使用AJAX请求数据时, 被请求的URL地址, 就叫数据接口 ( 简称接口 ) . 同时每个接口必需有请求方式。

例如:

http://www.liulongbin.top:3006/api/getbooks             获取图书列表的接口 ( GET请求 )

http://www.liulongbin.top:3006/api/addbook              添加图书的接口 ( POST请求 ) 



## <u><font color='#D26B6B'>接口请求过程</font></u>

用户与网页交互  → ← 网页发起请求  →  服务器响应请求   ↓

​                                                                                 ←返回数据

接口测试工具  :   [PostMan](https://www.postman.com/)     [Apipost](https://www.apipost.cn/)

## <u><font color='#D26B6B'>GET接口测试</font></u>

新建接口 选择GET 输入接口

![image-20220610151451223](C:\Users\小柯\AppData\Roaming\Typora\typora-user-images\image-20220610151451223.png)

查询 di为 1的请求

![image-20220610151627661](C:\Users\小柯\AppData\Roaming\Typora\typora-user-images\image-20220610151627661.png)

发送请求

输出

![image-20220610151653994](C:\Users\小柯\AppData\Roaming\Typora\typora-user-images\image-20220610151653994.png)

## <u><font color='#D26B6B'>POST接口测试</font></u>

与GET相似  但是要在Body下选择 x-www-from-urlencoded 。

![image-20220610152214741](C:\Users\小柯\AppData\Roaming\Typora\typora-user-images\image-20220610152214741.png)



## <u>接口文档</u>

接口的说明文档

<font color='#DA924A'>文档组成</font>：

1. 接口名称:  用来表示各个接口的简单说明, 如登录接口, 获取图书列表接口。
2. 接口URL:  接口的调用地址。
3. 接口的调用方式:  如GET和POST。
4. 参数格式:  接口需要传递的参数, 每个参数必需包括:  参数名称 、参数类型  、是否必选  、参数说明这4项内容。
5. 响应格式：接口的返回值的详细描述，一般包括数据名称、数据类型、说明这3项。
6. 返回示例（可选）：通过对象的形式，例举服务器返回数据的结构。



------



# from表单

表单在网页中主要负责数据采集功能。HTML from 标签，就是用于采集用户输入信息，并通过<from>标签的提交操作，把采集到的信息

提交给服务器端进行处理。

## <u>表单的基本组成</u>：

1. 表单标签  <form></form>。
2. 表单域  <input></input>。
3. 表单按钮<button></button>。

## <u>form属性</u>

form标签是用来采集数据，属性是用来规定如何把采集到的数据发送到服务器。

| 属性    | 值                                                           | 描述                                    |
| ------- | ------------------------------------------------------------ | --------------------------------------- |
| action  | URL地址                                                      | 规定当提交表单时，向何处发送表单数据    |
| method  | get或post                                                    | 规定一种方式把表单数据提交到 action URL |
| enctype | application/x-www-form-urlencoded     multipart/form-data   text/plain | 规定在发送表单数据之前如何对其进行编码  |
| target  | _blank   _self   _parent   _top   framename                  | 规定在何处打开 action URL               |





### <u>action</u>：

后端提供URL地址，负责接收提交的数据   ， 未指定URL默认当前页面。 

表单提交后会立即跳转action 指定的URL地址





### <u>target</u> ：

默认的值是 _self ，表示在相同框架中打开action URL。

| 值        | 描述                                         |
| --------- | -------------------------------------------- |
| _blank    | 在新窗口打开。                               |
| _self     | 默认的值在相同框架（窗口）中打开action URL。 |
| _parent   | 在父框架中打开。（很少用）                   |
| _top      | 在整个窗口中打开。（很少用）                 |
| framename | 在指定框架打开。（很少用）                   |





### <u>method</u>：

规定（get或post）一种方式把表单数据提交到 action URL。

默认get 表示通过URL地址的形式，把表单数据提交到action URL。

get适用于少量简单的数据。



post：更加安全 在URL中看不到数据。

post适用于大量的复杂的、或包含文件数据上传。





### <u>enctype</u>：

| 值                                | 描述                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| application/x-www-form-urlencoded | 发送前编码所有字符（默认）。                                 |
| multipart/form-data               | 不对字符编码 ，在使用包含文件上传控件的表单时，必需使用该值。 |
| text/plain                        | 空格转换为  '+'  加号，但不对特殊字符编码（很少用）。        |





```html
<body>
     <form action="/login" target="_blank" method="post" enctype="application/x-www-form-urlencoded">
        <input type="text" name="email_or_mobile" />
        <input type="password" name="password" />
        <button type="submit">提交</button> <!-- submit 发送表单支持键盘提交 -->
    </form>
</body>
```





## <u>表单的同步提交</u>

<u>点击submit 按钮，触发表单提交操作，从而使页面跳转到 action URL 的行为，叫表单的同步提交</u>。

1. 表单提交后整个页面会发生跳转，用户体验差。
2. 页面之前的状态和数据会丢失。

**解决方案：表单只负责采集数据，Ajax负责将数据提交到服务器。**



## <u>AJAX提交表单数据</u>

1. 阻止表单提交后默认的跳转行为，可调用事件对象的  event.preventDefaukt（）函数，阻止跳转。
2. 快速获取表单中的数据 JQuery提供了serialize() 函数  一次型获取表单中所有的数据。

```html
<body>
    <form action="/login" id="f1">
        <input type="text" name="username" />
        <input type="password" name="password" />
        <button type="submit">提交</button>
    </form>

    <script>

        $(function () {
            //第一种方式
            // $('#f1').submit(function () {
            //     alert(1);
            // e.preventDefault(); //阻止默认提交后跳转
            // let data = $(this).serialize();  //获取数据
            // console.log(data);
            // })

            //第二种方式
            $('#f1').on('submit', function (e) {
                alert(1);
                e.preventDefault();  //阻止默认提交后跳转
                let data = $(this).serialize();  //获取数据
                console.log(data);
            });
        });
    </script>
</body>
```



------



# 模板引擎

指定的模板结构和数据， 自动生成一个完整的HTML页面

模板引擎优点:

1. 减少了字符串的拼接操作。
2. 使代码结构清晰。
3. 便于阅读。

### [<u>**<font color='cornflowerblue'>art-template模板引擎</font>**</u>](http://aui.github.io/art-template/zh-cn/docs/installation.html)

1. 下载后导入   在 window 全局,多一个函数, 叫做template('模板ID',需要渲染的数据对象)。
2. 定义数据。
3. 定义模板，   模板的HTML 结构 ,必需定义到 script 中         ↓
4. 调用函数templatel。                                                            ↓
5. 渲染HTML结构。                                                                 ↓

```html
 <script type="text/javascript">
     //都有一个type属性
     //type="text/javascript"   默认将script内的代码当成js代码
     //type="text/html"         模板结构应写这里
</script>
```



```html
<head>
    <!-- 1. 导入模板引擎 -->
    <!-- 在 window 全局,多一个函数, 叫做template('模板ID',需要渲染的数据对象) -->
    <script src="template-web.js"></script>
</head>

<body>
    <!--5.1填充template返回的值-->
    <div class="container"></div>

    <!-- 3. 定义模板 -->
    <!-- 3.1 模板的HTML 结构 ,必需定义到 script 中 -->
    <!-- {{占位符 name:属性}} -->
    <script type="text/html" id="h">
        <h1>{{name}}123{{age}}</h1>  
    </script>


    <script >
        //2. 定义需要渲染的数据
        let data = {
            name: 'wz',
            age: 1
        };


        //4. 调用template函数 template('模板ID',需要渲染的数据对象)
        let htmlStr = template('h', data);  //将占位符{{}}替换;
        console.log(htmlStr);   // 输出<h1>wz1231</h1> 

        //5.渲染html
        document.querySelector('.container').innerHTML = htmlStr;

    </script>
</body>

</html>
```

art-template 提供了{{ }} 这中语法格式，在{{ }}内可以进行<u>**变量输出**</u>，或<u>**循环数组**</u>等操作，这中{{ }}语法在art-template 中称为标注语法。

在{{ }}语法中，我们可以进行变量的输出、对象的输出、三元表达式输出、逻辑或输出、加减乘除等表达式输出。

**{{ valus }}      {{ obj.key }}         {{ obj [ 'key' ] }}   {{a ? b : c }}     {{a || b }}          {{a + b }}**

------

### <u>标准语法——原文输出</u>

语法：**{{ @ value }}**

如果要输出的 value 值中，包含了HTML标签，则需使用**<u>原文输出</u>**语法，才能保证HTML标签正常被渲染。

```html
<div class="container"></div>
<script type="text/html" id="h"> 
        {{@ test}}     //加@
</script>
 <script>
        let data = {    
            test: '<h3>测试原文输出</h3>'
        };
        document.querySelector('.container').innerHTML =template('h', data);
</script>
```



------

### <u>标准语法——条件输出</u>

**{{ if value1}}**

**输出的内容**

**{{ /if }}**

**—————————**

**{{ if value}}**

**输出的内容**

**{{ else if value2}}**

**输出的内容**

**{{ /if }}**

```html
<div class="container"></div>
<script type="text/html" id="h"> 
        <div>
            {{if flag === 0}}
            flag等于0
            {{/if}}
        </div>
</script>
 <script>
        let data = {    
            flag: 0,
        };
        document.querySelector('.container').innerHTML =template('h', data);
</script>
```



### <u>标准语法——循环输出</u>

要实现循环输出，则可以再{{}}内，通过**each**语法循环数组，当前循环的索引**$index** 进行访问，

当前的循环项使用 **$value** 进行访问。$value是所有的循环项       $value.key   可以输出数组里对象的值

**{{each arr}}**

​     	**{{ $index }}  {{ $value }}**

**{{/each}}**

```html
<div class="container"></div>
<script type="text/html" id="h"> 
        <ul>
            {{each hobby}}
            <li>索引是:{{$index}}, 循环项是: {{$value}}</li>
            {{/each}}
        </ul>
</script>
<script>
        let data = {    
            hobby: ['唱', '跳', 'rap', '篮球'],
        };
        document.querySelector('.container').innerHTML =template('h', data);
</script>
```

------



### <u>标准语法——过滤器</u>

过滤器的本质就是function函数

**{{value | filterName}}**                   value: 参数 传递给函数filterName

定义过滤器的基本语法：

```javascript
template.defaults.imports.filterName = function(value) {/*return处理结果*/}
```

```html
<div class="container"></div>
<script type="text/html" id="h"> 
       <h3>{{regTime | dateFormat}}</h3>
</script>
<script>
     //定义过滤器
        template.defaults.imports.dateFormat = function (date) {
            let y = date.getFullYear();
            let m = date.getMonth() + 1;
            let d = date.getDate();
            return y + '-' + m + '-' + d;
        }
        let data = {    
            regTime: new Date(),
        };
        document.querySelector('.container').innerHTML =template('h', data);
</script>
```

------



# 模板引擎的事项原理

————————————————————————————**正则与字符串操作**————————————————————————

## 1 .基本语法

exec()  函数用于**检索字符串**中的正则表达式的匹配。

如果字符串中有匹配的值，**则返回改匹配值**，否则返回 **null**。

```javascript
//RegExpObject.exec(string);
let str = 'hello';
let pattern = /o/;
console.log(pattern.exec(str));
//输出结果
// 0: "o"
// groups: undefined
// index: 4
// input: "hello"
// length: 1
```



## 2. 分组

正则表达式中 （） 包起来的内容是一个分组，可以通过分组来 **提取自己想要的内容**

```javascript
let str = '<div>我是{{name}}</div>';
let pattern = /{{([a-zA-Z]+)}}/;
console.log(pattern.exec(str));
//得到name的相关信息
// 0: "{{name}}"    
// 1: "name"                // 索引为1 匹配的内容
// groups: undefined
// index: 7
// input: "<div>我是{{name}}</div>"
// length: 2
```



## 3. 字符串的replace函数

**replace（）函数用于在字符串中<u>替换</u>另一些字符：**

```javascript
let result= '123456'.replace('123','abc'); //得到result的值为字符串'abc456'
```

```javascript
let str = '<div>我是{{name}}</div>';
let pattern = /{{([a-zA-Z]+)}}/;
let patternResult = pattern.exec(str);
//上一节输出的值
//patternResult[0]  "{{name}}"     
//patternResult[1] ' name'
str = str.replace(patternResult[0], patternResult[1]);  //replace 函数返回值为替换后的新字符串
//输出的内容是: <div>我是name</div>
console.log(str);
```



**可以多次提取：**

```javascript
 let str = '<div>我是{{name}}{{age}}</div>';
 let pattern = /{{\s*([a-zA-Z]+)\s*}}/; 
 let patternResult = pattern.exec(str);
 str = str.replace(patternResult[0], patternResult[1]); 
 patternResult = pattern.exec(str);
 str = str.replace(patternResult[0], patternResult[1]); 
 console.log(str);   
 //输出的内容是: <div>我是nameage</div>
```

**多次提取简化：**

```javascript
let str = '<div>我是{{name}}{{age}}</div>';
let pattern = /{{\s*([a-zA-Z]+)\s*}}/;
let patternResult = null;
while (patternResult = pattern.exec(str)) {
    str = str.replace(patternResult[0], patternResult[1]);
};
console.log(str); //输出的内容是: <div>我是nameage</div>
```

**替换值：**

```javascript
let data = {
    name: 'wu',
    age: '18',
}
let str = '<div>我是{{name}}{{age}}</div>';
let pattern = /{{\s*([a-zA-Z]+)\s*}}/;
let patternResult = null;
while (patternResult = pattern.exec(str)) {    //data[patternResult[1]] = data['name']
    str = str.replace(patternResult[0], data[patternResult[1]]);
};
console.log(str); //输出的内容是: <div>我是wu18</div>
```



------



# XMLHttpRequest

XMLHttpRquest 简称xhr  是浏览器提供的Javascript 对象，通过它，可以 **请求服务器上的数据资源**。

Jqery中的AJAX函数就是，基于xhr对象封装的。

### <u>XMLHttpRequest 对象方法</u>

| new XMLHttpRequest()                        | 创建新的 XMLHttpRequest 对象                                 |
| ------------------------------------------- | ------------------------------------------------------------ |
| abort()                                     | 取消当前请求                                                 |
| getAllResponseHeaders()                     | 返回头部信息                                                 |
| getResponseHeader()                         | 返回特定的头部信息                                           |
| open(*method*, *url*, *async**user*, *psw*) | 规定请求                                                                                                                                               method：请求类型 GET 或 POST                                                                                                                      url：文件位置                                                                                                                                async：true（异步）或 false（同步）                                                                                                 user：可选的用户名称 psw：可选的密码 |
| send()                                      | 将请求发送到服务器，用于 GET 请求                            |
| send(*string*)                              | 将请求发送到服务器，用于 POST 请求                           |
| setRequestHeader()                          | 向要发送的报头添加标签/值对                                  |



### <u>XMLHttpRequest 对象属性</u>

| **属性**           | **描述**                                                     |
| ------------------ | ------------------------------------------------------------ |
| onreadystatechange | 定义当 readyState 属性发生变化时被调用的函数                 |
| readyState         | 保存 XMLHttpRequest 的状态。                                                                                                                          0：请求未初始化UNSENT                               XMLHttpRequest 对象以被创建，但未调用open方法                                                                                                                                       1：服务器连接已建立OPENED                        open方法以被调用                                                                                                                                  2：请求已收到 HEDAERS_RECEIVED           send方法以被调用，响应头也已经被接收                                                                                                                                  3：正在处理请求 LOADING                              数据接收中，此时response属性已包含部分数据                                                                                                                           4：请求已完成且响应已就绪 DONE                   Ajax请求完成，意味着传输已彻底完成或失败 |
| responseText       | 以字符串返回响应数据                                         |
| responseXML        | 以 XML 数据返回响应数据                                      |
| status             | 返回请求的状态号                                                                                                                                                    200: "OK"                                                                                                                                                                    403: "Forbidden"                                                                                                                                                         404: "Not Found"                                                                                                                                                               如需完整列表请访问 [Http 消息参考手册](https://www.w3school.com.cn/tags/html_ref_httpmessages.asp) |
| statusText         | 返回状态文本（比如 "OK" 或 "Not Found"）                     |



## URL编码与解码

URL 地址中，只允许出现英文相关的字母、标点符号、数字，因此，在URL地址中不允许出现中文字符。

出先中文字符，要对其**编码**（转义）

**URL编码原则**：使用安全的字符（没有特殊用途或特殊意义的可打印的字符）去表示那些不安全的字符。

URL编码原则： 使用**英文字符**去表示**非英文字符**

浏览器会自动编码，无序关心

endcodeURI()  编码函数

decodeURI() 解码函数

```javascript
console.log(encodeURI('及你太美'));
console.log(decodeURI('%E5%8F%8A%E4%BD%A0%E5%A4%AA%E7%BE%8E'));
```



## 发起GET请求

1. **创建  XHR  对象。**

​      var xhr = new XMLHttpRequest();

2. **调用  open  函数，指定请求方式  与URL地址。**

​    xhr.open('GET','URl')； 

3. **调用 send 函数发起AJAX请求。**

​    xhr.send();

4. **监听 onreadystatechange  事件**

​    xhr.onreadystatechange = function() {

​             4.1 **监听 xhr 对象的<u>请求状态</u> readyState ； 与服务器的<u>响应状态</u> status**
​            if(xhr.readyState === 4 && status === 200){

​				**4.2 打印服务器响应回来的数据**

​				console.log(xhr.responseText);

​	 };

};

```javascript
let xhr = new XMLHttpRequest();
xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks');
xhr.send();
xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && status === 200) {
        console.log(xhr.responseText)
    };
};
```

### 发起带参数的GET请求

只需在调用open函数期间，为URL指定地址即可

```javascript
xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks?id=1');
//?id=1  叫做   查询字符串  多个参数用 & 拼接
```



## 发起POST请求

相较于GET多了：

 设置**Content-Type** 属性

调用send()函数,同时将数据以 查询字符串的形式,提交给服务器

```javascript
let xhr = new XMLHttpRequest();
xhr.open('POST', 'http://www.liulongbin.top:3006/api/addbook');

//设置Content-Type 属性 (固定写法)
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')

//调用send()函数,同时将数据以 查询字符串的形式,提交给服务器
xhr.send('bookname=鸡你太美&author=坤坤&publisher=篮球');
xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && status === 200) {
        console.log(xhr.responseText)
    };
};
```



------

# 数据交换格式

**数据交换格式，就是服务器端与客户端之间进行数据传输与交换的格式。**
**前端领域，经常提及的两种数据交换格式分别是XML和JSON。其中XML用的非常少,所以,重点要学**
**习的数据交换格式就是JSON。**



## <u>XML</u>

**XML**的英文全称是EXtensible Markup Language,即**可扩展标记语言**。因此，XML和HTML类似,
也是一种标记语言。

XML和HTML的区别：
XML和HTML虽然都是标记语言,但是,它们两者之间没有任何的关系。
   ●HTML被设计用来描述网页上的**内容**,是网页内容的载体。
   ●XML被设计用来**传输和存储数据**，是数据的载体。

XML缺点：

1. 格式臃肿，和数据无关的代码过多，体积大，传输效率低。
2. Javascript中解析 XML 麻烦。



## <u>JSON</u>

**概念：**

1. **JSON**的英文全称是Javascript Object Notation, 即**Javascript 对象表示法**。

2. **JSON**就是Javascript **对象和数组**的**字符串**表示法，它使用文本	表示一个J**S对象或数组信息**。

3. **JSON的本质是字符串**。

**作用：**

JSON是一种**轻量级的文本数据交换格式**，在作用上类似 XML，专门用于储存和传输数据，但是JSON比XML**更小、更快、更容易解析**。

## JSON的两种结构

JSON就是用字符串来表示Javascript的对象和数组。所以，JSON中包含**对象**和**数组**两种结构,通过这
两种结构的相互**嵌套**，可以表示各种复杂的数据结构。



### 对象结构

对象结构:对象结构在JSON中表示为 { } 括起来的内容。数据结构为{ key: value, key: value, .. }的键
值对结构。其中，key 必须是使用**英文的双引号包裹**的字符串，value的数据类型可以是**数字、字符串、**
**布尔值、null、 数组、对象**6种类型。

```javascript
{
    "name" : "wuwu",
     "age" : 20，
     "hobby" : ["篮球","rap"]
    //不允许出现 undefined  function 函数
}
```



### 数组结构

数组结构在JSON中表示为 [ ] 括起来的内容。数据结构为[ "java", "javascript", 30, true ..1.
数组中数据的类型可以是数字、字符串、布尔值、null、 数组、 对象6种类型。

```javascript
[ "java", "python", "php" ]
[ 100， 200, 300.5 ]
[ true, false, null ]
[{"name":"zs"，"age": 20},{ "name": "ls","age": 30}]
[ ["苹果"，"榴莲"，"椰子”] , [4,50,5] ]
```



## JSON语法注意事项

1. 属性名必须使用双引号包裹
2. 字符串类型的值必须使用双引号包裹
3. JSON 中不允许使用单引号表示字符串
4. JSON 中不能写注释
5. JSON的最外层必须是对象或数组格式
6. 不能使用undefined或函数作为JSON的值

JSON的作用:在计算机与网络之间存储和传输数据。



## JSON和JS对象的关系

JSON是JS对象的字符串表示法，它使用文本表示一个JS对象的信息，本质是一个字符串
```javascript
//这是一个对象
let obj = {a: 'Hello', b: 'World' };
//这是一个JSON 字符串，本质是一个字符串
let jsonk= '{"a": "Hello", "b": "World"}';
```



## JSON和JS对象的互转

序列化和反序列化
把数据对象转换为字符串的过程，叫做序列化,例如:调用JSON.stringify0函数的操作，叫做JSON序列化。
把字符串转换为数据对象的过程，叫做反序列化，例如:调用JSON.parse0函数的操作,叫做JSON反序列化。

```javascript
//要实现从JSON字符串转换为JS对象，使用JSON.parse0方法:
let obj = JSON.parse(' {"a": "Hello", "b": "World"} ')
console.log(obj);
//结果是{a:'Hello', b: 'World' }
```

**JS转JSON JSON.stringify();**

```javascript
let obj =  JSON.stringify({ a: 'Hello', b: 'World' });
console.log(obj);
```



## JSON发送Ajax请求

```javascript
let xhr = new XMLHttpRequest();
xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks');
xhr.send();
xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && xhr.status === 200) {
        console.log(xhr.responseText);
        let result = JSON.parse(xhr.responseText)
        console.log(result);
    };
};    
```



------

# 封装原生AJAX

```javascript
function resolveData(data) {
        let arr = [];
        for (let k in data) {
            let str = k + '=' + data[k];
            arr.push(str);
        };
        return arr.join('&'); //在数组的每个元素之间添加 & 进行连接成字符串
        // split(&)  //通过 & 分割字符串 转成数组
};

    // let res = resolveData({
    //     name: 'wz',
    //     age: 18,
    // });
    // console.log(res);

function wu(options) {
    let xhr = new XMLHttpRequest();
    //把外界传来的参数  转化为  查询字符串
    let qs = resolveData(options.data);
    //options.method   老版本的是options.Type 输入的请求  ;  toUpperCase() 转为大写
    if (options.method.toUpperCase() === 'GET') {
        //发起GET请求
        xhr.open('GET', options.url + '?' + qs);
        xhr.send();
    } else if (options.method.toUpperCase() === 'POST') {
            //发起POST请求
            xhr.open('POST', option.url);
            xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
            xhr.send(qs);
    };
    xhr.onreadystatechange = function () {
            if (xhr.readyState === 4 && xhr.status === 200) {
                let result = JSON.parse(xhr.responseText);
                options.success(result);

            };
    };

};


//测试
wu({
    method: 'get',
    url: 'http://www.liulongbin.top:3006/api/getbooks',
    data: {
        id: 1,
    },
    success: function (res) {
        console.log(res);
    }

})
```



------

# XMLHttpRequest Level2新特性

**旧版XMLHttpRequest的缺点：**

1. 只支持文本数据的传输，无法用来读取和上传文件。
2. 传送和接收数据时，没有进度信息，只能提示有没有完成。

**XMLHttpRequest Level2的新功能：**

1. 可以设置HTTP请求的时限。
2. 可以使用FormData对象管理表单数据。
3. 可以上传文件。
4. 可以获得数据传输的进度信息。



## timeout属性

有时，Ajax 操作很耗时,而且无法预知要花3少时间。如果网速很慢,用户可能要等很久。新版本的
XML HttpRequest对象,增加了timeout属性,可以设置HTTP请求的时限:

```javascript
xhr. timeout = 3000；
```

上面的语句，将最长等待时间设为3000毫秒。过了这个时限，就自动停止HTTP请求。与之配套的还有一个
timeout事件，用来指定回调函数:

```javascript
xhr. ontimeout = function (event) {
alert('请求超时! ')
```

```javascript
let xhr = new XMLHttpRequest();
//设置超时事件
xhr. timeout = 3000；
//超时后会执行 ontimeout 函数
xhr. ontimeout = function (event) {
alert('请求超时! ')
xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks');
xhr.send();
xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && status === 200) {
        console.log(xhr.responseText)
    };
};
```



##  FormData对象管理表单数据

Ajax操作往往用来提交表单数据。为了方便表单处理，HTML5新增了一个FormData对象

### 模拟表单操作:

```javascript
//1.创建 FormData 实例
let fd = nre FromData();
//调用append函数向fd中追加函数
fd.append('uname','wz');
fd.append('upwd','123');

let xhr = new XMLHttpRequest();
xhr.open('POST', 'http://www.liulongbin.top:3006/api/formdata');
//设置Content-Type 属性 (固定写法)  不需写    fd数据已经默认处理过
//xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
xhr.send(fd);
xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && xhr.status === 200) {
        let result = JSON.parse(xhr.responseText)
        console.log(result);
    };
};    
```



###  FormData对象获取网页表单的值·

```javascript
//获取表单元素
let form = document.querySelector('#form');
//监听表单元素的 submit 事件
form.addEventListener('submit',function(e){
    e.preventDefault(); //阻止默认提交跳转行为
    //创建FormData 获取form 表单元素
    let fd = nre FromData(form);
    let xhr = new XMLHttpRequest();
    xhr.open('POST', 'http://www.liulongbin.top:3006/api/formdata');
    xhr.send(fd);
    xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && xhr.status === 200) {
        let result = JSON.parse(xhr.responseText)
        console.log(result);
     };
    };
        
})
```



### 上传文件

实现步骤:
①定义UI结构
②验证是否选择了文件
③向FormData中追加文件
④使用xhr发起上传文件的请求
⑤监听onreadystatechange事件 

```html
     <!-- 文件选择框 -->
    <input type="file" id="file">
    <button id="btnUpload">上传文件</button>
    <br />
    <!-- img标签  来显示上传成功后的图片 -->
    <img src="" alt="" id="img" width="800">

    <script>
        //1.获取按钮
        let btnUpload = document.querySelector('#btnUpload');
        //2. 为按钮添加点击事件
        btnUpload.addEventListener('click', function () {
            //获取到选择文件列表
            //let files = document.querySelector('#file')获取的是文件选择框
            //他有个属性 files 数组   就是用户选择的文件
            let files = document.querySelector('#file').files;
            if (files.length <= 0) {
                return alert('请选择上传的文件');
            }
            let fd = new FormData();
            //将用户选择的文件添加到FormData中
            fd.append('avatar', files[0]);
            let xhr = new XMLHttpRequest();
            xhr.open('POST', 'http://www.liulongbin.top:3006/api/upload/avatar');
            xhr.send(fd);

            xhr.onreadystatechange = function () {
                if (xhr.readyState === 4 && xhr.status === 200) {
                    let data = JSON.parse(xhr.responseText);
                    if (data.status === 200) {
                        //文件上传成功
                        //将服器返回的图片地址设置给img 的src
                        document.querySelector('#img').src = 'http://www.liulongbin.top:3006' + data.url
                    } else {
                        //上传文件失败
                        console.log(data.message);
                    }
                }

            };

        })
    </script>
```



### 显示上传文件进度

新版本的XMLHttpRequest对象中，可以通过监听xhr.upload.onprogress事件,来获取到文件的上传进度。

写在     let xhr = new XMLHttpRequest();    创建之后。

```javascript
let xhr = new XMLHttpRequest();
xhr.upload.onprogress = function (e) {
                //e.lengthComputable是一个布尔值,表示当前上传的资源是否具有柯计算的长度
                if (e.lengthComputable) {  
                    //计算除上传的进度  
                    // e.loaded  以传输的字节
                    // e.total   需要传输的总字节
                    let procentComplete = Math.ceil((e.loaded / e.total) * 100); //Math.ceil向上取整
                    console.log(procentComplete);
                };
            };
```

# axios发起Ajax请求

## axios GET请求

```javascript
axios.get('url',{params: {/*参数*/}}).then(callback);
```

```javascript
//调用axios.js
        //请求的URL地址
        let url = 'http://www.liulongbin.top:3006/api/get';
        //请求的参数对象
        let paramsObj = {
            name: 'wuwu',
            age: 18,
        };
        //调用axios.get() 发起GET请求
        axios.get(url, { params:paramsObj}).then(function (res) {
            //data 是服务器返回的数据
            let result = res.data;
            console.log(res);
        });
```

## axios POST请求

```javascript
axios.post('url',{params: {/*参数*/}}).then(callback);
```

同上 更改请求就可以了



## axios 直接发起请求

```javascript
axios({
    method: '请求类型'，
    url：'请求地址'，
    data:{/*POST数据*/}，
    params:{/*GET参数*/}
})then(callback)
```



------

# 同源策略和跨域

**两个页面的协议、域名、和端口都相同，则两个页面具有相同的源。** 

http://www.test.com:80/index.html

http://  协议

www.test.com/   域名

:80  端口     默认是  ：8 0。



<font style='color:#DA924A'>**同源策略**</font>**(英文全称Same origin policy) :**是浏览器提供的一个安全功能。
MDN官方给定的概念:同源策略限制了从同-一个源加载的文档或脚本如何与来自另一个源的资源进行交互。这
是一个用于隔离潜在恶意文件的重要安全机制。

**通俗的理解**:浏览器规定，A网站的JavaScript,不允许和非同源的网站C之间，进行资源的交互,例如:

1. 无法读取非同源网页的Cookie、LocalStorage 和IndexedDB
2. 无法接触非同源网页的DOM
3. 无法向非同源地址发送Ajax请求
   

<font style='color:#DA924A'>出现跨域的根本原因</font>同源指的是两个URL的协议、域名、端口-致，反之，则是**<u><font style='color:#DA924A'>跨域</font></u>**。
:浏览器的同源策略不允许非同源的URL之间进行资源的交互。

## JSONP

如何实现跨域数据请求
现如今,实现跨域数据请求，最主要的两种解决方案,分别是<font style='color:#DA924A'>JSONP和CORS</font>。
<font style='color:#DA924A'>JSONP</font>:出现的早，兼容性好(兼容低版本IE)。是前端程序员为了解决跨域问题,被迫想出来的一种临时解决方
案。缺点是只支持GET请求,不支持POST请求。
<font style='color:#DA924A'>CORS</font>出现的较晚，它是W3C标准，属于跨域Ajax请求的根本解决方案。支持GET和POST请求。缺点是不兼
容某些低版本的浏览器。



由于浏览器同源策略的限制，网页中无法通过Ajax请求非同源的接口数据。但是<script> 标签不受浏览器同
源策略的影响，可以通过src属性,请求非同源的js脚本。

因此，JSONP的实现原理，就是通过<script> 标签的src属性,请求跨域的数据接口，并通过函数调用的形式,
接收跨域接口响应回来的数据。

----

# 输入框防抖

<font style='color:#DA924A'>防抖celue</font>是当事件触发后，<font style='color:#DA924A'>延迟N秒后在执行回调</font>，如果在这N秒内事件又被触发，则重新计时。

<font style='color:#DA924A'>防抖应用场景</font>

用户在输入框中连续输入- -串字符时,可以通过防抖策略,只在输入完后,才执行查询的请求,这样可以有效减
少请求次数，**节约请求资源**。

```javascript
let timer = null;
// 1.防抖动的timer
function debounceSearch(keywords) { // 2.定义防抖的函数
timer = setTimeout (function() {
//发起JSONP请求
getSugge stList (keywords)
}，500);
};
$('#ipt') .on('keyup', function() { // 3.在触发keyup 事件时，立即清空timer
clearTimeout (timer);
// ...省略其他代码
debounceSearch (keywords );
});
```

----

# 搜索缓存

当用户输入后又删除  会重新发起 已经发起过的请求 

采取缓存的方式节约资源

```javascript
//再发起请求在先判断缓存中有没有当前请求
//监听文本框的keyup 事件
$('#ipt') .on('keyup', function() {
// ... 省略其他代码
//优先从缓存中获取搜索建议
if (cache0bj [keywords]) {
return renderSugge stList (cache0bj [keywords] )
}
//获取搜索建议列表
debounceSearch (keywords)
})

```



```javascript
//将搜索结果保存到缓存对象中
let cacheObj = {};
//写道渲染建议列表下
function renderSuggestList(res) {
// ...省略其他代码
//将搜索的结果，添加到缓存对象中
let k = $('#ipt') .val() . trim()
cacheObj[k] = res
};
```

----

# 节流

节流策略(throttle) ，顾名思义，可以减少段时间内事件的触发频率。

1. 鼠标连续不断地触发某事件(如点击)，只在单位时间内只触发-次。
2. 懒加载时要监听计算滚动条的位置，但不必每次滑动都触发,可以降低计算的频率,而不必去浪费CPU资源。

节流阀为空，表示可以执行下次操作;不为空，表示不能执行下次操作。

当前操作执行完，必须将节流阀重置为空，表示可以执行下次操作了。

每次执行操作前，必须先判断节流阀是否为空。



```javascript
$ (function() {
let angel = $('#angel')
let timer = null      // 1.预定义一个timer节流阀
$ (document) . on ( 'mousemove', function(e) {
if (timer) { 
    return           // 3.判断节流阀是否为空，如果不为空，则证明距离上次执行间隔不足16毫秒
           };       
timer = setTimeout (function() {
$ (angel) .css('left', e.pagex + 'px') .ass('top', e.pageY + 'px');
timer = null         // 2.当设置了鼠标跟随效果后，清空timer节流阀，方便下次开启延时器
}，16);
}); 
});

```

----



# HTTP协议

通信：信息的传递和交换

三要素

1. 通讯的主题。
2. 通讯的内容
3. 通信的方式



**通信协议**(Communication Protocol)：是指通信的双方完成通信所必须遵守的规则和约定。
通俗的理解:通信双方采用约定好的格式来发送和接收消息，这种事先约定好的通信格式，就叫做通信协议。

网页内容又叫做超文本，因此网页内容的传输协议又叫做<font style = 'color: #D26B6B'>超文本传输协议</font>.(HyperText Transfer Protocol) ,
<font style = 'color: #D26B6B'>简称HTTP协议</font>。

<font style = 'color: #D26B6B'>HTTP协议</font>即超文本传送协议(HyperText Transfer Protocol)，它规定了客户端与服务器之间进行网页内容传输时,
所必须遵守的传输格式。

●客户端要以HTTP协议要求的格式把数据提交到服务器
●服务器要以HTTP协议要求的格式把内容响应给客户端



## HTTP协议的交互模型

HTTP协议采用了<font style = 'color: #D26B6B'>请求 / 响应</font>的交互模型。



## 请求消息

由于HTTP协议属于客户端浏览器和服务器之间的通信协议。因此，客户端发起的请求叫做HTTP请求,客户
端发送到服务器的消息，叫做HTTP请求消息。

HTTP 请求消息又叫做HTTP请求报文。



<font style='color:#DA924A'>HTTP请求消息组成</font>：

**请求行(request line)**

**请求头部( header)**

**空行** 

**请求体**



**网页中的组参考  ↓** 



Request Headers   View Source **（请求消息头）（点击View Source）**

GET /api/getbooks HTTP/1.1 

Accept:* */* *

Accept-Encoding: gzip, deflate 

Accept-Language: zh-CN,zh;q=0.9

 Connection: keep-alive 

Host: www.liulongbin.top:3006 

Origin: http://127.0.0.1:5500

 Referer: http://127.0.0.1:5500/ 

User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.0.0 Safari/537.36







### 请求行(request line)

Request Headers    **（请求消息头）**

POST/api/post HTTP/1.1       **请求行**

<font style='color:#DA924A'>请求行</font>由请求 **方式、  URL 和      HTTP协议版本**3个部分组成,他们之间使用空格隔开。

​                        ↓                ↓                       ↓  

​                     POST     /api/post       HTTP/1.1





### 请求头部( header)

**请求头部**用来描述**客户端的基本信息**，从而把**客户端相关的信息告知服务器**。比如: User-Agent 用来说明当前是什
么类型的浏览器; Content- Type用来描述发送到服务器的数据格式; Accept 用来描述客户端能够接收什么类型的返
回内容; Accept-Language 用来描述客户端期望接收哪种人类语言的文本内容。



请求头部是由多行 <font style='color:#DA924A'>键 / 值对</font>组成，每行的键和值之间用  **：** 隔开。

| 头部字段                                              | 说明                                       |
| ----------------------------------------------------- | ------------------------------------------ |
| Host                                                  | 要请求的服务器域名                         |
| Connection                                            | 客户端与服务器的连接方式(close或keepalive) |
| Content-Length                                        | 用来描述请求体的大小                       |
| <font style = 'color: #D26B6B'>Accept</font>          | 客户端可识别的响应内容类型列表             |
| <font style = 'color: #D26B6B'>User-Agent</font>      | 产生请求的浏览器类型                       |
| <font style = 'color: #D26B6B'>Content Type</font>    | 客户端告诉服务器实际发送的数据类型         |
| Accept-Encoding                                       | 客户端可接收的内容压缩编码形式             |
| <font style = 'color: #D26B6B'>Accept-Language</font> | 用户期望获得的自然语言的优先顺序           |

 <font style = 'color: #D26B6B'>**请求头部**    **↓**</font>

请求行以下

~~GET /api/getbooks HTTP/1.1~~    （请求行剩下的都是请求头部）

Accept:* */* *

Accept-Encoding: gzip, deflate 

Accept-Language: zh-CN,zh;q=0.9

 Connection: keep-alive 

Host: www.liulongbin.top:3006 

Origin: http://127.0.0.1:5500

 Referer: http://127.0.0.1:5500/ 

User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.0.0 Safari/537.36





### 空行

最后一一个请求头字段的后面是一个空行，通知服务器请求头部至此结束。
请求消息中的空行，用来分隔请求头部与请求体。



### 请求体

请求体中存放的，是要通过<font style = 'color: #D26B6B'>POST</font>方式提交到服务器的数据。

在Request Headers   View Source **（请求消息头）**下面



Form Data   View Source  （  点击View Source  请求体    ）

只有POST请求有请求体





## 响应消息

<font style = 'color: #D26B6B'>响应消息</font>就是服务器给客户端的消息内容，也叫做响应报文。

**组成：**

1. **状态行**
2. **响应头**
3. **空行**
4. **响应体**



**示例↓**



▼Response Headers       view parsed    （响应消息头）
HTTP/1.1 200 OK
X- Powered-By: Express
Access-Control-Allow-Origin: *
Content-Type: application/json; charset=utf-8
Content-Length: 68
ETag: W/*44-nT/y6y0Fj7H40EVW1DWBIMG+PqO"
Date: Wed, 27 Nov 2019 01:48:57 GMT
Connection: keep-alive





### 状态行

<font style = 'color: #D26B6B'>**状态行**</font>由**HTTP协议版本、状态码和状态码的描述文本**3个部分组成，他们之间使用空格隔开;

​                             ↓                  ↓                     ↓  

​                       HTTP/1.1           200              OK



### 响应头部

响应头部是用来描述<font style = 'color: #D26B6B'>服务器的基本信息 </font>/ 由多行 <font style='color:#DA924A'>键 / 值对</font>组成，每行的键和值之间用  **：** 隔开。



X- Powered-By: Express
Access-Control-Allow-Origin: *
Content-Type: application/json; charset=utf-8
Content-Length: 68
ETag: W/*44-nT/y6y0Fj7H40EVW1DWBIMG+PqO"
Date: Wed, 27 Nov 2019 01:48:57 GMT
Connection: keep-alive

 [<font color='cornflowerblue'>响应头字段  点击查阅文档</font>](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers)





### 空行

在最后一一个响应头部字段结束之后，会紧跟一个空行，用来通知客户端响应头部至此结束。



### 响应体	

响应体中存放的，是服务器给客户端的资源内容

之前都赞  Headers中   响应体在	Response中

即可查看响应体内容



## 请求方法

HTTP请求方法，属于HTTP协议中的一部分,请求方法的作用是:用来表明要**对服务器上的资源执行的操作**。
最常用的请求方法是**GET**和**POST**。

| 方法                                         | 描述                                                         |
| -------------------------------------------- | ------------------------------------------------------------ |
| <font style = 'color: #D26B6B'>GET</font>    | (查询)发送请求来获得服务器上的资源，请求体中不会包含请求数据，请求数据放在协议头中。 |
| <font style = 'color: #D26B6B'>POST</font>   | (新增)向服务器提交资源(例如提交表单或上传文件)。数据被包含在请求体中提交给服务器。 |
| <font style = 'color: #D26B6B'>PUT</font>    | (修改)向服务器提交资源，并使用提交的新资源，替换掉服务器对应的旧资源。 |
| <font style = 'color: #D26B6B'>DELETE</font> | (删除)请求服务器删除指定的资源。                             |
| HEAD                                         | HEAD方法请求一个与GET请求的响应相同的响应，但没有响应体。    |
| OPTIONS                                      | 获取http服务器支持的http请求方法，允许客户端查看服务器的性能，比如ajax跨域时的预检等 |
| CONNECT                                      | 建立一个到由目标资源标识的服务器的隧道。                     |
| TRACE                                        | 沿着到目标资源的路径执行个消息环回测试， 主要用于测试或诊断。 |
| PATCH                                        | 是对PUT方法的补充，用来对已知资源进行局部更新。              |





## 响应状态码

<font style = 'color: #D26B6B'>HTTP响应状态码</font>(HTTP Status Code)，也属于HTTP协议的一部分，用来标识响应的状态。

响应状态码会随着响应消息一起被发送至客户端浏览器， 浏览器根据服务器返回的响应状态码，就能知道这次
HTTP请求的结果是成功还是失败了。

响应行HTTP/1.1 200 OK

200  就是响应状态码   代表成功



### 响应状态码组成和类型

**分类 以1-5开头**

| 分类 | 分类描述                                                     |
| ---- | ------------------------------------------------------------ |
| 1**  | <font style = 'color: #D26B6B'>信息</font>，服务器收到请求，需要请求者继续执行操作(实际开发中很少遇到1**类型的状态码) |
| 2**  | <font style = 'color: #D26B6B'>成功</font>，操作被成功接收并处理 |
| 3**  | <font style = 'color: #D26B6B'>重定向</font>，需要进一步的操作以完成请求 |
| 4**  | <font style = 'color: #D26B6B'>客户端错误</font>，请求包含语法错误或无法完成请求 |
| 5**  | <font style = 'color: #D26B6B'>服务器错误</font>，服务器在处理请求的过程中发生了错误 |





### 2**范围的状态码

表示服务器已成功接收到请求并进行处理。

**常见的2开头类型的状态码如下:**

| 状态码 | 状态码英文名称 | 中文描述                                                     |
| ------ | -------------- | ------------------------------------------------------------ |
| 200    | OK             | <font style = 'color: #D26B6B'>请求成功</font>。一般用于GET与POST请求 |
| 201    | Created        | <font style = 'color: #D26B6B'>已创建</font>。成功请求并创建了新的资源，通常用于POST或PUT请求 |





### 3**范围的状态码

表示表示服务器要求客户端重定向,需要客户端进一步的操作以完成资源的请求。 

**常见的3开头类型的状态码如下:**

| 状态码 | 状态码英文名称                            | 中文描述                                                     |
| ------ | ----------------------------------------- | ------------------------------------------------------------ |
| 301    | Moved                         Permanently | <font style = 'color: #D26B6B'>永久移动</font>。请求的资源已被永久的移动到新URI,返回信息会包括新的URI,浏览器会自动定向到新URI。今后任何新的请求都应使用新的URI代替 |
| 302    | Found                                     | <font style = 'color: #D26B6B'>临时移动</font>。与301类似。但资源只是临时被移动。客户端应继续使用原有<br/>URI |
| 304    | Not Modified                              | <font style = 'color: #D26B6B'>未修改</font>。所请求的资源未修改，服务器返回此状态码时，不会返回任何资<br/>源(响应消息中不包含响应体)。客户端通常会缓存访问过的资源。 |





### 4**范围的状态码

表示客户端的请求有非法内容,从而导致这次请求失败。

**常见的4开头类型的状态码如下:**

| 状态码                                    | 状态码英文名称                                  | 中文描述                                                     |
| ----------------------------------------- | ----------------------------------------------- | ------------------------------------------------------------ |
| 400                                       | Bad Request                                     | 1、语义有误，当前请求无法被服务器理解。<br>除非进行修改，否则客户端 不应该重复提交这个请求。<br>2、请求参数有误。 |
| 401                                       | Unauthorized                                    | 当前请求需要用户验证。                                       |
| 403                                       | Forbidden                                       | 服务器已经理解请求，但是拒绝执行它。                         |
| <font style = 'color: #D26B6B'>404</font> | <font style = 'color: #D26B6B'>Not Found</font> | <font style = 'color: #D26B6B'>服务器无法根据客户端的请求找到资源(网页)。</font> |
| 408                                       | Request   Timeout                               | 请求超时。服务器等待客户端发送的请求时间过长，超时。         |





### 5**范围的状态码

表示服务器末能正常处理客户端的请求而出现意外错误。

**常见的5开头类型的状态码如下:**

| 状态码 | 状态码英文名称         | 中文描述                                                     |
| ------ | ---------------------- | ------------------------------------------------------------ |
| 500    | Internal Server Errorr | 服务器内部错误，无法完成请求。                               |
| 501    | Not Implemented        | 服务器不支持该请求方法，无法完成请求。<br>只有GET和HEAD请求方法是要求每个服务器必须支持的，<br>其它请求方法在不支持的服务器上会返回501 |
| 503    | Service Unavailable    | 由于超载或系统维护，服务器暂时的无法处理客户端的请求。       |

