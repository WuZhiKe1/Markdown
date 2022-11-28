# 标题标签

HTML提供了6个等级的网页标题

//<h1>-<h6>

单词head缩写,意思为头部,标题

- h1为一级标题

- 加了标题的字号会依次变大

- 一个标题独占一行  </h>再写字后面会另起一行

# 段落标签和换行标签

//<p>我是一个段落</p>



可以吧HTML文档分割为若干段落

- 1. 文本在一个段落中会根据浏览器窗口的大小自动换换行
  2. 段落和段落之间保有空隙.





### 换行标签

//     <br />

- 是单个标签.
- 只是简单的开始新的一行,跟段落不一样,段落之间会插入一些间距.



# 文本格式化标签

是文字以特殊的方式显示

- 加粗              //  <strong></strong> 或者<b></b>  推荐使用strong
- 斜体              em /em或者i /i                                     推荐使用em /em
- 删除线          del /del      or      s /s                              推荐 del /del
- 下划线           ins /ins   or           u /u                              与i见ins

# (div)(span)

div   这是头部 /div

span 今日的价格 /span

- div 用来布局的 ,但是一行只能放一个div,大盒子

- span 用来布局的,一行可以有多个span,小盒子

# 图像标签

  src = 属性

  <img src ="图像URL"/    >

src 图片路径  必须属性

alt 文本  替换文本.图像不能显示显示文字 

title  文本   提示文本,鼠标放到图像上显示文字

width 像素  设置图像的宽度

height 像素 设置图像高度

border 像素  设置图像边框粗细

- 属性之间没有顺序
- 格式   key = "value"    属性 = "属性值"



![image-20220417145358230](C:\Users\小柯\AppData\Roaming\Typora\typora-user-images\image-20220417145358230.png)

- 同一根目录下相对路径只需写名字/下一级要写文件路径   /  上一级加..
- 绝对路径:是指目录下的绝对位置,从盘符到文件
- 可以使用网络上的绝对地址

![image-20220417155011427](C:\Users\小柯\AppData\Roaming\Typora\typora-user-images\image-20220417155011427.png)

# 超链接标签

- a 标签定义超链接,从一个页面到另一个页面
- 语法格式:   //<a href="跳转目标" target = "目标窗口的弹出方式" 文本图像</a>
- href 用于指定链接目标的url地址,(必须属性)当为标签应用href属性时,他就具有了超链接的功能.
- target 用于链接页面的打开方式,其中_self为默认值 ,__blank为在新窗口的打开方式.

链接分类:

1.  外部链接:<//a href = "http//www.baidu.com">百度</a>

2. 内部链接:网站内部之间的互相链接,直接链接内部页面名称,例如:<//a href = "index.html">首页</a>.

3. 空链接:  <//a href ="#">首页</a>

4. 下载链接: 如果href里面地址是一个文件或者压缩包,会下载这个文件.

5. 网页元素链接:文本 图像 表格 音频 视频等都可以加链接.

6. 锚点链接:点我们的链接可以定位到页面的某个位置.

7. - 在链接文本的herf属性中,设置属性的值为  #名字  的形式<//a herf = "#tow">第二集</a>
   -  找到目标位置标签,里面添加一个id属性=刚才的名字     <//h3 id = "tow">第二集介绍</h3>

   ​                        ![image-20220417172157866](C:\Users\小柯\AppData\Roaming\Typora\typora-user-images\image-20220417172157866.png)                                                         

# 注释标签和特殊字符

<!-- 我 -->

ctrl+/  注释

1. - &nbsp一个代表一次空格*
2. - &lt小于号   &gt  大于号*
3. &amp  和号
4. &yen  人民币
5. &copy  版权
6. &reg  注册商标
7. &deg 摄氏度
8. &plusmn  正负号
9. &times  乘号
10. &divide 除号
11. &sup2 平方2
12. &sup3 平方3

![image-20220417191227884](C:\Users\小柯\AppData\Roaming\Typora\typora-user-images\image-20220417191227884.png)

# 表格标签

## 表格的作用:

用于显示,展示数据,它可以让数据非常规整.

1. table  用于定义表格的标签.
2. <tr 用于定义表格中的行,必须嵌套在table中.
3. <td 用于定义表格中的单元格,必须嵌套在tr中.
4. 字母 td 指表格中的数据,即单元格的内容,

![image-20220418062410473](C:\Users\小柯\AppData\Roaming\Typora\typora-user-images\image-20220418062410473.png)

## 表头单元格标签

把想要坐表头哪一行的td换成th  就会加粗居中

![image-20220418063935767](C:\Users\小柯\AppData\Roaming\Typora\typora-user-images\image-20220418063935767.png)

## 表格属性:

| 属性名      | 属性值            | 描述                                         |
| :---------- | :---------------- | :------------------------------------------- |
| align       | left,center,right | 居左居中居右对其.                            |
| border      | 1 或 " "          | 规定单元格是否拥有边框,默认为"",表示没有边框 |
| cellpadding | 像素值            | 规定单元边沿与其内容之间的空白,默认像素1.    |
| cellspacing | 像素值            | 规定单元格之间的空白,默认2像素.              |
| width       | 像素或百分比      | 规定表格的宽度.                              |

​                          

<img src="D:\小柯\Pictures\Saved Pictures\IMG_20220418_100756.jpg" alt="IMG_20220418_100756" style="zoom:12%;" />

td不是tb

![image-20220418104817636](C:\Users\小柯\AppData\Roaming\Typora\typora-user-images\image-20220418104817636.png)

# 合并单元格

<img src="D:\小柯\Pictures\Saved Pictures\IMG_20220418_101059.jpg" alt="IMG_20220418_101059" style="zoom:13%;" />



![image-20220418110004357](C:\Users\小柯\AppData\Roaming\Typora\typora-user-images\image-20220418110004357.png)



# 列表标签

<img src="D:\小柯\Pictures\Saved Pictures\IMG_20220418_101108.jpg" alt="IMG_20220418_101108" style="zoom:13%;" />

<img src="D:\小柯\Pictures\Saved Pictures\IMG_20220418_100822_1.jpg" alt="IMG_20220418_100822_1" style="zoom:13%;" />

![image-20220418110256923](C:\Users\小柯\AppData\Roaming\Typora\typora-user-images\image-20220418110256923.png)

# 表单标签

### 是form不是from

![image-20220418132859400](C:\Users\小柯\AppData\Roaming\Typora\typora-user-images\image-20220418132859400.png)

<img src="D:\小柯\Pictures\Saved Pictures\IMG_20220418_101026.jpg" alt="IMG_20220418_101026" style="zoom:13%;" />

<input为单标签

type设置不同的属性来指定不通的控件类型.

type属性类型如下:

1. button                   定义可点击按钮.
2. checkbox             复选框
3. file                        输入字段和浏览按钮 供文件上传
4. hidden                  隐藏输入路段
5. image                   图形形式的提交按钮
6. password             密码字段,给字段被字符掩盖
7. radio                    定义单选按钮
8. reset                    重置按钮,重置按钮会清除列表中的所有数据
9. submit                 定义提交按钮  会把表单数据发送到服务器
10. text                      定义单行的输入字段,用户可在其输入文本,默认宽度为20个字符.

- 出type外input还有其他属性

  | 属性      | 属性值       | 描述                                      |
  | --------- | ------------ | ----------------------------------------- |
  | name      | 用户自由定义 | 定义input 元素名称.                       |
  | value     | 用户自由定义 | 规定input 元素值.  可以显示元素    返回值 |
  | checked   | checked      | 规定此input 元素首次加载时应当被选中.     |
  | maxlength | 正整数       | 规定输入字段中的字符最大长度长度.         |

  1. name 和value 是每个表单元素都有的属性值,主要给后台人员使用.
  2. name 表单元素的名字,要求单选按钮和复选框要有相同的name值.
  3. maxlength 限制输入最大字符使用较少.

  ![](C:\Users\小柯\AppData\Roaming\Typora\typora-user-images\image-20220418144128425.png)

![image-20220418151351411](C:\Users\小柯\AppData\Roaming\Typora\typora-user-images\image-20220418151351411.png)

### lable标签

lable 标签为input元素定义标注(标签)

绑定一个表单元素,点击文本时浏览器会自动将焦点转到或者选择对应的元素表单上,增加用户体验.

![image-20220418153639789](C:\Users\小柯\AppData\Roaming\Typora\typora-user-images\image-20220418153639789.png)

### select下拉表单元素

如 选择省份时下拉表单

- 至少包含一对<option
- 在<option中定义selected="selected"时,当前项目为默认选项.

![image-20220418155354197](C:\Users\小柯\AppData\Roaming\Typora\typora-user-images\image-20220418155354197.png)

## textarea文本域

- 使用场景:当用户输入内容较多的情况下,使用
- 定义多行文本输入的控件
- 常见 : 留言板 评论.

![image-20220418160110597](C:\Users\小柯\AppData\Roaming\Typora\typora-user-images\image-20220418160110597.png)







