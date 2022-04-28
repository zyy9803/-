---
学习目标:
  - 掌握API和Web API的概念
  - 掌握常见浏览器提供的API的调用方式
  - 能通过Web API开发常见的页面交互功能
  - 能够利用搜索引擎解决问题
typora-copy-images-to: media
---

# Web API

## Web API介绍

### API的概念

API（Application Programming Interface,应用程序编程接口）是一些预先定义的函数，目的是提供应用程序与开发人员基于某软件或硬件得以访问一组例程的能力，而又无需访问源码，或理解内部工作机制的细节。

- 任何开发语言都有自己的API
- API的特征输入和输出(I/O)
  - var max =  Math.max(1, 2, 3);
- API的使用方法(console.log('adf'))

### Web  API的概念

浏览器提供的一套操作浏览器功能和页面元素的API(BOM和DOM)

此处的Web API特指浏览器提供的API(一组方法)，Web API在后面的课程中有其它含义


### 掌握常见浏览器提供的API的调用方式
[MDN-Web API](https://developer.mozilla.org/zh-CN/docs/Web/API)

### JavaScript的组成



#### ECMAScript - JavaScript的核心 

定义了JavaScript 的语法规范

JavaScript的核心，描述了语言的基本语法和数据类型，ECMAScript是一套标准，定义了一种语言的标准与具体实现无关

#### BOM - 浏览器对象模型

一套操作浏览器功能的API

通过BOM可以操作浏览器窗口，比如：弹出框、控制浏览器跳转、获取分辨率等 

#### DOM - 文档对象模型

一套操作页面元素的API

DOM可以把HTML看做是文档树，通过DOM提供的API可以对树上的节点进行操作

## DOM

### DOM的概念 

文档对象模型（Document Object Model，简称DOM），是[W3C](https://baike.baidu.com/item/W3C)组织推荐的处理[可扩展标记语言](https://baike.baidu.com/item/%E5%8F%AF%E6%89%A9%E5%B1%95%E7%BD%AE%E6%A0%87%E8%AF%AD%E8%A8%80)的标准[编程接口](https://baike.baidu.com/item/%E7%BC%96%E7%A8%8B%E6%8E%A5%E5%8F%A3)。它是一种与平台和语言无关的[应用程序接口](https://baike.baidu.com/item/%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F%E6%8E%A5%E5%8F%A3)(API),它可以动态地访问程序和脚本，更新其内容、结构和[www](https://baike.baidu.com/item/www/109924)文档的风格(目前，HTML和XML文档是通过说明部分定义的)。文档可以进一步被处理，处理的结果可以加入到当前的页面。[DOM](https://baike.baidu.com/item/DOM/50288)是一种基于树的[API](https://baike.baidu.com/item/API/10154)文档，它要求在处理过程中整个文档都表示在[存储器](https://baike.baidu.com/item/%E5%AD%98%E5%82%A8%E5%99%A8)中。

DOM又称为文档树模型

![image-20210510193634646](JavaScript.assets/image-20210510193634646.png)

![1497154623955](JavaScript.assets/1497154623955.png)





- 文档：一个网页可以称为文档
- 节点：网页中的所有内容都是节点（标签、属性、文本、注释等）
- 元素：网页中的标签
- 属性：标签的属性

### DOM经常进行的操作

- 获取元素
- 对元素进行操作(设置其属性或调用其方法)
- 动态创建元素
- 事件(什么时机做相应的操作)

## 获取页面元素

### 为什么要获取页面元素

例如：我们想要操作页面上的某部分(显示/隐藏，动画)，需要先获取到该部分对应的元素，才进行后续操作

### 根据id获取元素

```javascript
var div = document.getElementById('main');
console.log(div);

// 获取到的数据类型 HTMLDivElement，对象都是有类型的
```

注意：由于id名具有唯一性，部分浏览器支持直接使用id名访问元素，但不是标准方式，不推荐使用。

### 根据标签名获取元素

```javascript
var divs = document.getElementsByTagName('div');
for (var i = 0; i < divs.length; i++) {
  var div = divs[i];
  console.log(div);
} 
```

### 根据name获取元素

```javascript
var inputs = document.getElementsByName('hobby');
for (var i = 0; i < inputs.length; i++) {
  var input = inputs[i];
  console.log(input);
}
```

### 根据类名获取元素

```javascript
var mains = document.getElementsByClassName('main');
for (var i = 0; i < mains.length; i++) {
  var main = mains[i];
  console.log(main);
}
```

### 根据选择器获取元素

```javascript
var text = document.querySelector('#text');
console.log(text);

var boxes = document.querySelectorAll('.box');
for (var i = 0; i < boxes.length; i++) {
  var box = boxes[i];
  console.log(box);
}
```

- 总结

```
掌握
	getElementById()
	getElementsByTagName()
了解
	getElementsByName()
	getElementsByClassName()
	querySelector()
	querySelectorAll()
```

## 事件

事件：触发-响应机制

### 事件三要素

- 事件源:触发(被)事件的元素
- 事件名称: click 点击事件
- 事件处理程序:事件触发后要执行的代码(函数形式)

### 事件的基本使用

```javascript
var box = document.getElementById('box');
box.onclick = function() {
  console.log('代码会在box被点击后执行');  
};
```

### 案例
- 点击按钮弹出提示框
- 点击按钮切换图片

## 属性操作

### 非表单元素的属性

href、title、id、src、className

```javascript
var link = document.getElementById('link');
console.log(link.href);
console.log(link.title);

var pic = document.getElementById('pic');
console.log(pic.src)
```



案例：

​	点击按钮显示隐藏div

​	美女相册

- innerHTML和innerText

```javascript
var box = document.getElementById('box');
box.innerHTML = '我是文本<p>我会生成为标签</p>';
console.log(box.innerHTML);
box.innerText = '我是文本<p>我不会生成为标签</p>';
console.log(box.innerText);
```
- HTML转义符

```
"		&quot;
'		&apos;
&		&amp;
<		&lt;   // less than  小于
>		&gt;   // greater than  大于
空格	   &nbsp;
©		&copy;
```

- innerHTML和innerText的区别

- innerText的兼容性处理


### 表单元素属性

- value 用于大部分表单元素的内容获取(option除外)
- type 可以获取input标签的类型(输入框或复选框等)
- disabled 禁用属性
- checked 复选框选中属性
- selected 下拉菜单选中属性

### 案例

- 给文本框赋值，获取文本框的值
- 点击按钮禁用文本框
- 检测用户名是否是3-6位，密码是否是6-8位，如果不满足要求高亮显示文本框
- 设置下拉框中的选中项
- 搜索文本框
- 全选反选

### 自定义属性操作

- getAttribute() 获取标签行内属性
- setAttribute() 设置标签行内属性
- 使用.直接添加属性，不会在html标签内形成属性，但是可以在js中使用
- removeAttribute() 移除标签行内属性
- 与element.属性的区别: 上述三个方法用于获取任意的行内属性。

### 样式操作

- 使用style方式设置的样式显示在标签行内
```javascript
var box = document.getElementById('box');
box.style.width = '100px';
box.style.height = '100px';
box.style.backgroundColor = 'red';
```

- 注意

  <strong style="color:red;">通过样式属性设置宽高、位置的属性类型是字符串，需要加上px</strong>

### 类名操作

- 修改标签的className属性相当于直接修改标签的类名
```javascript
var box = document.getElementById('box');
box.className = 'show';
```

### 案例

- 开关灯
- 点击按钮改变div的背景颜色
- 图片切换二维码案例
- 当前输入的文本框高亮显示
- 点击按钮改变div的大小和位置
- 列表隔行变色、高亮显示
- tab选项卡切换

## 创建元素的三种方式

### 区分节点和元素

<strong style="color:red;">节点有许多种：元素节点、属性节点、文本节点等等，用nodeType不同的值来区分。元素指的是元素节点，是节点中的一种</strong>

```html
<body>
  <ul id="ul">
    <li>first</li>
    <li>1111</li>
    <li>1111</li>
    <li>1111</li>
    <li>1111</li>
    <li>last</li>
  </ul>


  <script src="js/common.js"></script>
  <script>
    var ul = document.getElementById('ul');

    // 获取第一个子节点
    console.dir(ul.firstChild);
    // 获取第一个子元素
    console.dir(ul.firstElementChild);


    // 获取最后一个子节点
    console.dir(ul.lastChild);
    // 获取最后一个子元素
    console.dir(ul.lastElementChild);

    var firstElement = getFirstElementChild(ul);
    console.log(firstElement);
  </script>
</body>
```

<strong style="color:red;">注意获取第一个元素（ul）和第一个节点（文本）的内容是不一样的，带element的是元素</strong>

### document.write()

```javascript
document.write('新设置的内容<p>标签也可以生成</p>');
```

### innerHTML

```javascript
var box = document.getElementById('box');
box.innerHTML = '新内容<p>新标签</p>';
```

### document.createElement()

```javascript
var div = document.createElement('div');
document.body.appendChild(div);
```

### 性能问题

- innerHTML方法由于会对字符串进行解析，需要避免在循环内多次使用。
- 可以借助字符串或数组的方式进行替换，再设置给innerHTML
- 优化后与document.createElement性能相近


### 案例

- 动态创建列表，高亮显示
- 根据数据动态创建表格

## 节点操作

### 元素节点操作

```javascript
var body = document.body;
var div = document.createElement('div');
body.appendChild(div);

var firstEle = body.children[0];
body.insertBefore(div, firstEle);

body.removeChild(firstEle);

var text = document.createElement('p');
body.replaceChild(text, div);
```

案例：

​	选择水果

### 节点属性

- nodeType  节点的类型
  - 1 元素节点
  - 2 属性节点
  - 3 文本节点 
- nodeName  节点的名称(标签名称)
- nodeValue  节点值
  - 元素节点的nodeValue始终是null


### 模拟文档树结构

![1497165666684](media/1497165666684.png)

```javascript
function Node(option) {
  this.id = option.id || '';
  this.nodeName = option.nodeName || '';
  this.nodeValue = option.nodeValue || '';
  this.nodeType = 1;
  this.children = option.children || [];
}

var doc = new Node({
  nodeName: 'html'
});
var head = new Node({
  nodeName: 'head'
});
var body = new Node({
  nodeName: 'body'
})
doc.children.push(head);
doc.children.push(body);

var div = new Node({
  nodeName: 'div',
  nodeValue: 'haha',
});

var p = new Node({
  nodeName: 'p',
  nodeValue: '段落'
})
body.children.push(div);
body.children.push(p);

function getChildren(ele) {
  for(var i = 0; i < ele.children.length; i++) {
    var child = ele.children[i];
    console.log(child.nodeName);
    getChildren(child);
  }
}
getChildren(doc);
```

### 节点层级

```javascript
var box = document.getElementById('box');
console.log(box.parentNode);
console.log(box.childNodes);
console.log(box.children);
console.log(box.nextSibling);
console.log(box.previousSibling);
console.log(box.firstChild);
console.log(box.lastChild);
```

- 注意

  childNodes和children的区别，<strong style="color:red;">childNodes获取的是子节点，children获取的是子元素</strong>

  nextSibling和previousSibling获取的是节点，<strong style="color:red;">获取元素对应的属性是nextElementSibling和previousElementSibling获取的是元素</strong>

  ​	nextElementSibling和previousElementSibling有兼容性问题，IE9以后才支持

- 总结

```
节点操作，方法
	appendChild()
	insertBefore()
	removeChild()
	replaceChild()
节点层次，属性
	parentNode
	childNodes
	children
	nextSibling/previousSibling
	firstChild/lastChild
```

## 事件详解

### 注册/移除事件的三种方式

<strong style="color:red;">add 添加 Event 事件 Listener 监听者（事件处理函数） IE9以后才支持</strong>

第一个参数 事件名称 不带on

第二个参数 事件处理函数

第三个参数 事件冒泡/事件捕获

  ```javascript
btn.addEventListener('click', function () {
   // alert('abc');
   alert(this); // 触发事件的对象
  }, false);

btn.addEventListener('click', function () {
   // alert('hello');
   alert(this);
  }, false);
  ```



```javascript
var box = document.getElementById('box');
box.onclick = function () {
  console.log('点击后执行');
};
box.onclick = null;

box.addEventListener('click', eventCode, false);
box.removeEventListener('click', eventCode, false);

box.attachEvent('onclick', eventCode);
box.detachEvent('onclick', eventCode);

function eventCode() {
  console.log('点击后执行');
}
```

### 兼容代码

```javascript
function addEventListener(element, type, fn) {
  if (element.addEventListener) {
    element.addEventListener(type, fn, false);
  } else if (element.attachEvent){
    element.attachEvent('on' + type,fn);
  } else {
    element['on' + type] = fn;
  }
}

function removeEventListener(element, type, fn) {
  if (element.removeEventListener) {
    element.removeEventListener(type, fn, false);
  } else if (element.detachEvent) {
    element.detachEvent('on' + type, fn);
  } else {
    element['on'+type] = null;
  }
}
```

### 事件的三个阶段

1. 捕获阶段

2. 当前目标阶段

3. <strong style="color:red;">冒泡阶段：如果父元素和子元素都有相同的事件，触发子元素事件时，会同时触发父元素事件</strong>

   事件对象.eventPhase属性可以查看事件触发时所处的阶段

### 事件委托

把子元素要做的事情，转交给父元素来做（事件冒泡）

### 事件对象的属性和方法

- event.type 获取事件类型
- clientX/clientY     所有浏览器都支持，窗口位置
- pageX/pageY       IE8以前不支持，页面位置
- event.target || event.srcElement 用于获取触发事件的元素
- <strong style="color:red;">event.preventDefault() 取消默认行为</strong>

#### 案例

- 跟着鼠标飞的天使

```js
    var img = document.getElementById('img');
    document.onmousemove = function (e) {
      console.log('abc');
      e = e || window.event;

      img.style.position = 'absolute';

      // clientX / clientY  获取的是鼠标在可视区域中的位置
      img.style.left = e.clientX + 'px';
      img.style.top = e.clientY + 'px';

      // 获取鼠标在页面中的位置
      // img.style.left = e.pageX + 'px';
      // img.style.top = e.pageY + 'px';
    }
```



- 鼠标点哪图片飞到哪里
- 获取鼠标在div内的坐标

### 阻止事件传播的方式

- <strong style="color:red;">标准方式 event.stopPropagation();</strong>

```javascript
    array.forEach(function (item) {

      item.addEventListener('click', function (e) {
        // eventPhase 事件的阶段   
        // 1 捕获阶段  2 目标阶段  3 冒泡阶段
        // console.log(e.eventPhase);

        // target 始终是点击的那个元素
        console.log('target  ' + e.target.id);
        // currentTarget 调用事件处理函数的元素
        console.log('currentTarget  ' + e.currentTarget.id);
        // this跟currentTarget一样 是调用事件处理函数的元素
        console.log('this ' + this.id);

        // 阻止事件冒泡
        e.stopPropagation();
      }, false);

    });
```

- IE低版本 event.cancelBubble = true; 标准中已废弃

### 常用的鼠标和键盘事件

- onmouseup 鼠标按键放开时触发
- onmousedown 鼠标按键按下触发
- onmousemove 鼠标移动触发
- onmouseover/onmouseout 鼠标进入/离开 会触发事件冒泡
- onmouseenter/onmouseleave 鼠标进入/离开 不会触发事件冒泡
- onkeyup 键盘按键按下触发
- onkeydown 键盘按键抬起触发


## BOM

### BOM的概念

BOM(Browser Object Model) 是指浏览器对象模型，浏览器对象模型提供了独立于内容的、可以与浏览器窗口进行互动的对象结构。BOM由多个对象组成，其中代表浏览器窗口的Window对象是BOM的顶层对象，其他对象都是该对象的子对象。

我们在浏览器中的一些操作都可以使用BOM的方式进行编程处理，

比如：刷新浏览器、后退、前进、在浏览器中输入URL等

### BOM的顶级对象window

window是浏览器的顶级对象，当调用window下的属性和方法时，可以省略window
注意：window下一个特殊的属性 window.name

### 对话框

- alert()
- prompt()
- confirm()

### 页面加载事件

- onload：页面加载完毕执行 （DOM元素加载完毕，当外部文件加载完毕）

```javascript
window.onload = function () {
  // 当页面加载完成执行
  // 当页面完全加载所有内容（包括图像、脚本文件、CSS 文件等）执行
$('qwer').load(function () {
　　var x = document.getElementsByTagName('iframe')[0];
　　var y = (x.contentWindow || x.contentDocument);
   var z = y.getElementByTagName('video')[0];
　　console.log(z);
});
}
```

- onunload：当关闭网页的时候执行

```javascript
window.onunload = function () {
  // 当用户退出页面时执行
}
```

### 定时器

#### setTimeout()和clearTimeout()

在指定的毫秒数到达之后执行指定的函数，只执行一次

```javascript
// 创建一个定时器，1000毫秒后执行，返回定时器的标示
var timerId = setTimeout(function () {
  console.log('Hello World');
}, 1000);

// 取消定时器的执行
clearTimeout(timerId);
```

#### setInterval()和clearInterval()

定时调用的函数，可以按照给定的时间(单位毫秒)周期调用函数

```javascript
// 创建一个定时器，每隔1秒调用一次
var timerId = setInterval(function () {
  var date = new Date();
  console.log(date.toLocaleTimeString());
}, 1000);

// 取消定时器的执行
clearInterval(timerId);
```

案例：

```
定时器
简单动画
```

### location对象

location对象是window对象下的一个属性，使用的时候可以省略window对象

location可以获取或者设置浏览器地址栏的URL

#### location有哪些成员？

- 使用chrome的控制台查看

- 查MDN

  [MDN](https://developer.mozilla.org/zh-CN/)

- 成员

  - assign()/reload()/replace()
  - hash/host/hostname/search/href……

#### URL

统一资源定位符 (Uniform Resource Locator, URL)

- URL的组成

```
scheme://host:port/path?query#fragment
http://www.itheima.com:80/a/b/index.html?name=zs&age=18#bottom
scheme:通信协议
	常用的http,ftp,maito等
host:主机
	服务器(计算机)域名系统 (DNS) 主机名或 IP 地址。
port:端口号
	整数，可选，省略时使用方案的默认端口，如http的默认端口为80。
path:路径
	由零或多个'/'符号隔开的字符串，一般用来表示主机上的一个目录或文件地址。
query:查询
	可选，用于给动态网页传递参数，可有多个参数，用'&'符号隔开，每个参数的名和值用'='符号隔开。例如：name=zs
fragment:信息片断
	字符串，锚点.
```

#### 作业

解析URL中的query，并返回对象的形式

```javascript
function getQuery(queryStr) {
  var query = {};
  if (queryStr.indexOf('?') > -1) {
    var index = queryStr.indexOf('?');
    queryStr = queryStr.substr(index + 1);
    var array = queryStr.split('&');
    for (var i = 0; i < array.length; i++) {
      var tmpArr = array[i].split('=');
      if (tmpArr.length === 2) {
        query[tmpArr[0]] = tmpArr[1];
      }
    }
  }
  return query;
}
console.log(getQuery(location.search));
console.log(getQuery(location.href));
```

### history对象

- back()
- forward()
- go()

### navigator对象

- userAgent



## 特效

<strong style="color:red;">this.style 获取的仅仅是标签的style中设置的样式属性，如果标签没有设置style属性，此时获取到的都是空字符串</strong>

### 偏移量

<img src="E:\前端\前端笔记\JavaScript\media\image-20210313125034652.png" alt="image-20210313125034652" style="zoom: 33%;" />

- offsetParent用于获取定位的父级元素
- offsetParent和parentNode的区别
- offsetLeft是元素距离页面左边的偏移量，offsetTop是元素距离页面上部的偏移量

```javascript
var box = document.getElementById('box');
console.log(box.offsetParent);//最近的具有定位父元素
console.log(box.offsetLeft);//获取当前元素到 具有定位父节点 的left方向的距离
console.log(box.offsetTop);//获取当前元素到 具有定位父节点 的top方向的距离
console.log(box.offsetWidth);//水平方向 width + 左右padding + 左右border-width
console.log(box.offsetHeight);//垂直方向 height + 上下padding + 上下border-width
```

### 客户区大小

<img src="E:\前端\前端笔记\JavaScript\media\image-20210313133310273.png" alt="image-20210313133310273" style="zoom:50%;" />

```javascript
var box = document.getElementById('box');
console.log(box.clientLeft);//左border的宽度
console.log(box.clientTop);//上border的宽度
console.log(box.clientWidth);//水平方向 width + 左右padding
console.log(box.clientHeight);//垂直方向 height + 上下padding
```

### 滚动偏移

<img src="E:\前端\前端笔记\JavaScript\media\image-20210313132927398.png" alt="image-20210313132927398" style="zoom:50%;" />

```javascript
var box = document.getElementById('box');
console.log(box.scrollLeft)
console.log(box.scrollTop)
console.log(box.scrollWidth)//元素内容真实的宽度，内容不超出盒子高度时为盒子的clientWidth
console.log(box.scrollHeight)//元素内容真实的高度，内容不超出盒子高度时为盒子的clientHeight
```

### 案例 

- 拖拽案例
- 弹出登录窗口
- 放大镜案例

- 模拟滚动条
- 匀速动画函数
- 变速动画函数
- 无缝轮播图
- 回到顶部  


## 附录

### 元素的类型

![1497169919418](media/1497169919418.png)





# 浏览器：文档，事件，接口

现代 JavaScript 教程 https://zh.javascript.info/

## Document

### DOM节点

```html
<!DOCTYPE HTML>
<html>
<head>
  <title>About elk</title>
</head>
<body>
  The truth about elk.
</body>
</html>
```

标签被称为 **元素节点**（或者仅仅是元素），并形成了树状结构：`<html>` 在根节点，`<head>` 和 `<body>` 是其子项，等。

元素内的文本形成 **文本节点**，被标记为 `＃text`。一个文本节点只包含一个字符串。它没有子项，并且总是树的叶子。

例如，`<title>` 标签里面有文本 `"About elk"`。

请注意文本节点中的特殊字符：

- 换行符：`↵`（在 JavaScript 中为 `\n`）
- 空格：`␣`

空格和换行符都是完全有效的字符，就像字母和数字。它们形成文本节点并成为 DOM 的一部分。所以，例如，在上面的示例中，`<head>` 标签中的 `<title>` 标签前面包含了一些空格，并且该文本变成了一个 `#text` 节点（它只包含一个换行符和一些空格）。

只有两个顶级排除项：

1. 由于历史原因，`<head>` 之前的空格和换行符均被忽略。
2. 如果我们在 `</body>` 之后放置一些东西，那么它会被自动移动到 `body` 内，并处于 `body` 中的最下方，因为 HTML 规范要求所有内容必须位于 `<body>` 内。所以 `</body>` 之后不能有空格。

在其他情况下，一切都很简单 — 如果文档中有空格（就像任何字符一样），那么它们将成为 DOM 中的文本节点，而如果我们删除它们，则不会有任何空格。

除了元素节点和文本节点，还有其他的节点类型，比如注释

```html
<!DOCTYPE HTML>
<html>
<body>
  The truth about elk.
  <ol>
    <li>An elk is a smart</li>
    <!-- comment -->
    <li>...and cunning animal!</li>
  </ol>
</body>
</html>
```

在这里我们可以看到一个新的树节点类型 — *comment node*，被标记为 `#comment`，它在两个文本节点之间。

我们可能会想 — 为什么要将注释添加到 DOM 中？它不会对视觉展现产生任何影响吗。但是有一条规则 — 如果一些内容存在于 HTML 中，那么它也必须在 DOM 树中。

**HTML 中的所有内容，甚至注释，都会成为 DOM 的一部分。**

甚至 HTML 开头的 `<!DOCTYPE...>` 指令也是一个 DOM 节点。它在 DOM 树中位于 `<html>` 之前。我们不会触及那个节点，出于这个原因，我们甚至不会在图表中绘制它，但它确实就在那里。

表示整个文档的 `document` 对象，在形式上也是一个 DOM 节点。

一共有 [12 种节点类型](https://dom.spec.whatwg.org/#node)。实际上，我们通常用到的是其中的 4 种：

1. `document` — DOM 的“入口点”。
2. 元素节点 — HTML 标签，树构建块。
3. 文本节点 — 包含文本。
4. 注释 — 有时我们可以将一些信息放入其中，它不会显示，但 JS 可以从 DOM 中读取它。



### DOM兄弟儿子

#### 节点

![image-20211124194637222](JavaScript.assets/image-20211124194637222.png) 

**子节点：childNodes，firstChild，lastChild**

* `childNodes` 集合列出了所有子节点，包括文本节点
* `firstChild` 和 `lastChild` 属性是访问第一个和最后一个子元素的快捷方式。

childNodes 是一个看起来像数组的 **集合** ，是一个可迭代对象，因此它不能使用数组的方法，但是：

* 可以用 for of 来对其迭代
* `alert( Array.from(document.body.childNodes).filter ); // function` 转化成数组

**兄弟节点和父节点**

parentNode、previousSibling、nextSibling

#### 元素

对于很多任务来说，我们并不想要文本节点或注释节点。我们希望操纵的是代表标签的和形成页面结构的元素节点。

![image-20211124200014386](JavaScript.assets/image-20211124200014386.png) 

这些链接和我们在上面提到过的类似，只是在词中间加了 `Element`：

- `children` — 仅那些作为元素节点的子代的节点。
- `firstElementChild`，`lastElementChild` — 第一个和最后一个子元素。
- `previousElementSibling`，`nextElementSibling` — 兄弟元素。
- `parentElement` — 父元素。



### 元素导航

* **getElementById** 或者 只使用 id

```html
<div id="elem">
  <div id="elem-content">Element</div>
</div>

<script>
  // elem 是对带有 id="elem" 的 DOM 元素的引用
  elem.style.background = 'red';

  // id="elem-content" 内有连字符，所以它不能成为一个变量
  // ...但是我们可以通过使用方括号 window['elem-content'] 来访问它
</script>
```

* **querySelectorAll** 最常用，功能最强大

* **querySelector** 调用会返回给定 CSS 选择器的**第一个**元素

* **matches** ` elem.matches(css)` 不会查找任何内容，它只会检查 `elem` 是否与给定的 CSS 选择器匹配。它返回 `true` 或 `false`。

  当我们遍历元素（例如数组或其他内容）并试图过滤那些我们感兴趣的元素时，这个方法会很有用。

* **closest** `elem.closest(css)` 方法会查找与 CSS 选择器匹配的最近的祖先。`elem` 自己也会被搜索。

* **getElementsBy*** 可以是TagName、ClassName、Name等，但是不如 querySelectorAll 常用



### 节点类

![image-20211124200928869](JavaScript.assets/image-20211124200928869.png) 

- [EventTarget](https://dom.spec.whatwg.org/#eventtarget) — 是根的“抽象（abstract）”类。该类的对象从未被创建。它作为一个基础，以便让所有 DOM 节点都支持所谓的“事件（event）”，我们会在之后学习它。
- [Node](http://dom.spec.whatwg.org/#interface-node) — 也是一个“抽象”类，充当 DOM 节点的基础。它提供了树的核心功能：`parentNode`，`nextSibling`，`childNodes` 等（它们都是 getter）。`Node` 类的对象从未被创建。但是有一些继承自它的具体的节点类，例如：文本节点的 `Text`，元素节点的 `Element`，以及更多异域（exotic）类，例如注释节点的 `Comment`。
- [Element](http://dom.spec.whatwg.org/#interface-element) — 是 DOM 元素的基本类。它提供了元素级的导航（navigation），例如 `nextElementSibling`，`children`，以及像 `getElementsByTagName` 和 `querySelector` 这样的搜索方法。浏览器中不仅有 HTML，还会有 XML 和 SVG。`Element` 类充当更多特定类的基本类：`SVGElement`，`XMLElement` 和 `HTMLElement`。
- HTMLElement — 最终是所有 HTML 元素的基本类。各种 HTML 元素均继承自它：
  - [HTMLInputElement](https://html.spec.whatwg.org/multipage/forms.html#htmlinputelement) — `<input>` 元素的类，
  - [HTMLBodyElement](https://html.spec.whatwg.org/multipage/semantics.html#htmlbodyelement) — `<body>` 元素的类，
  - [HTMLAnchorElement](https://html.spec.whatwg.org/multipage/semantics.html#htmlanchorelement) — `<a>` 元素的类，
  - ……等，每个标签都有自己的类，这些类可以提供特定的属性和方法。

#### nodeType

`nodeType` 属性提供了另一种“过时的”用来获取 DOM 节点类型的方法。

它有一个数值型值（numeric value）：

- 对于元素节点 `elem.nodeType == 1`，
- 对于文本节点 `elem.nodeType == 3`，
- 对于 document 对象 `elem.nodeType == 9`，
- 在 [规范](https://dom.spec.whatwg.org/#node) 中还有一些其他值。

在现代脚本中，我们可以使用 `instanceof` 和其他基于类的检查方法来查看节点类型

#### nodeName 和 tagName

tagName 和 nodeName 之间有什么不同吗？

当然，差异就体现在它们的名字上，但确实有些微妙。

- `tagName` 属性仅适用于 `Element` 节点。
- nodeName 是为任意 Node 定义的：
  - 对于元素，它的意义与 `tagName` 相同。
  - 对于其他节点类型（text，comment 等），它拥有一个对应节点类型的字符串。

```html
<body><!-- comment -->

  <script>
    // for comment
    alert( document.body.firstChild.tagName ); // undefined（不是一个元素）
    alert( document.body.firstChild.nodeName ); // #comment

    // for document
    alert( document.tagName ); // undefined（不是一个元素）
    alert( document.nodeName ); // #document
  </script>
</body>
```

如果我们只处理元素，那么 `tagName` 和 `nodeName` 这两种方法，我们都可以使用，没有区别。

#### innerHTML 和 outerHTML

* innerHtml 属性允许将元素中的 HTML 获取为字符串形式。我们也可以修改它。因此，它是更改页面最有效的方法之一。

```html
<body>
  <p>A paragraph</p>
  <div>A div</div>
  <script>
    alert( document.body.innerHTML ); // 读取当前内容
    document.body.innerHTML = 'The new BODY!'; // 替换它
  </script>
</body>
```

* `outerHTML` 属性包含了元素的完整 HTML。就像 `innerHTML` **加上元素本身**一样。

```html
<div id="elem">Hello <b>World</b></div>
<script>
  alert(elem.outerHTML); // <div id="elem">Hello <b>World</b></div>
</script>
```

**注意：与 `innerHTML` 不同，写入 `outerHTML` 不会改变元素。而是在 DOM 中替换它。**

```html
<div>Hello, world!</div>

<script>
  let div = document.querySelector('div');

  // 使用 <p>...</p> 替换 div.outerHTML
  div.outerHTML = '<p>A new element</p>'; // (*)

  // 蛤！'div' 还是原来那样！
  alert(div.outerHTML); // <div>Hello, world!</div> (**)
</script>
```

原来的元素被替换了，但是div仍然存在，只是不存在于页面中了

所以，在 `div.outerHTML=...` 中发生的事情是：

- `div` 被从文档（document）中移除。
- 另一个 HTML 片段 `<p>A new element</p>` 被插入到其位置上。
- `div` 仍拥有其旧的值。新的 HTML 没有被赋值给任何变量。

#### textContent 纯文本

使用方法和 innerHTML 一样，只是插入的是纯文本，不会被解析



### 特性和属性

在 HTML 中，标签可能拥有特性（attributes）。当浏览器解析 HTML 文本，并根据标签创建 DOM 对象时，浏览器会辨别 **标准的** 特性并以此创建 DOM 属性。

所以，当一个元素有 `id` 或其他 **标准的** 特性，那么就会生成对应的 DOM 属性。但是非 **标准的** 特性则不会。

例如：

```html
<body id="test" something="non-standard">
  <script>
    alert(document.body.id); // test
    // 非标准的特性没有获得对应的属性
    alert(document.body.something); // undefined
  </script>
</body>
```

所以，如果一个特性不是标准的，那么就没有相对应的 DOM 属性。那我们有什么方法来访问这些特性吗？

当然。所有特性都可以通过使用以下方法进行访问：

- `elem.hasAttribute(name)` — 检查特性是否存在。
- `elem.getAttribute(name)` — 获取这个特性值。
- `elem.setAttribute(name, value)` — 设置这个特性值。
- `elem.removeAttribute(name)` — 移除这个特性。

#### 特性属性同步

当一个标准的特性被改变，对应的属性也会自动更新，（除了几个特例）反之亦然。但这里也有些例外，例如 `input.value` 只能从特性同步到属性，反过来则不行

#### 非标准特性

当编写 HTML 时，我们会用到很多标准的特性。但是非标准的，自定义的呢？首先，让我们看看它们是否有用？用来做什么？

有时，非标准的特性常常用于将自定义的数据从 HTML 传递到 JavaScript，或者用于为 JavaScript “标记” HTML 元素。

像这样：

```html
<!-- 标记这个 div 以在这显示 "name" -->
<div show-info="name"></div>
<!-- 标记这个 div 以在这显示 "age" -->
<div show-info="age"></div>

<script>
  // 这段代码找到带有标记的元素，并显示需要的内容
  let user = {
    name: "Pete",
    age: 25
  };

  for(let div of document.querySelectorAll('[show-info]')) {
    // 在字段中插入相应的信息
    let field = div.getAttribute('show-info');
    div.innerHTML = user[field]; // 首先 "name" 变为 Pete，然后 "age" 变为 25
  }
</script>
```

但是自定义的特性也存在问题。如果我们出于我们的目的使用了非标准的特性，之后它被引入到了标准中并有了其自己的用途，该怎么办？

为了避免冲突，存在 [data-*](https://html.spec.whatwg.org/#embedding-custom-non-visible-data-with-the-data-*-attributes) 特性。

**所有以 “data-” 开头的特性均被保留供程序员使用。它们可在 `dataset` 属性中使用。**

例如，如果一个 `elem` 有一个名为 `"data-about"` 的特性，那么可以通过 `elem.dataset.about` 取到它。

像这样：

```html
<body data-about="Elephants">
<script>
  alert(document.body.dataset.about); // Elephants
</script>
```

像 `data-order-state` 这样的多词特性可以以驼峰式进行调用：`dataset.orderState`。



### 修改文档

#### 创建

要创建 DOM 节点，这里有两种方法：

- `document.createElement(tag)`

  用给定的标签创建一个新 **元素节点（element node）**：`let div = document.createElement('div');`

- `document.createTextNode(text)`

  用给定的文本创建一个 **文本节点**：`let textNode = document.createTextNode('Here I am');`

大多数情况下，我们需要为此消息创建像 `div` 这样的元素节点。

#### 插入

元素插入方法，指明了不同的插入位置：

- `node.append(...nodes or strings)` —— 在 `node` **内部末尾** 插入节点或字符串，
- `node.prepend(...nodes or strings)` —— 在 `node` **内部开头** 插入节点或字符串，
- `node.before(...nodes or strings)` —— 在 `node` **前面** 插入节点或字符串，
- `node.after(...nodes or strings)` —— 在 `node` **后面** 插入节点或字符串，
- `node.replaceWith(...nodes or strings)` —— 将 `node` 替换为给定的节点或字符串。

![image-20211124203124542](JavaScript.assets/image-20211124203124542.png) 

但是如果插入的是文本，则会被当作文字像 `<`、`>` 这样的符号都会被作转义处理来保证正确显示。

例如，在这里插入了一个字符串和一个元素：

```html
<div id="div"></div>
<script>
  div.before('<p>Hello</p>', document.createElement('hr'));
</script>
```

所以，最终的 HTML 为：

```html
&lt;p&gt;Hello&lt;/p&gt;
<hr>
<div id="div"></div>
```

如果我们想要将内容“作为 HTML 代码插入”，让内容中的所有标签和其他东西都像使用 `elem.innerHTML` 所表现的效果一样，就要使用使用另一个非常通用的方法：`elem.insertAdjacentHTML(where, html)`。

该方法的第一个参数是代码字（code word），指定相对于 `elem` 的插入位置。必须为以下之一：

- `"beforebegin"` — 将 `html` 插入到 `elem` 前插入，
- `"afterbegin"` — 将 `html` 插入到 `elem` 开头，
- `"beforeend"` — 将 `html` 插入到 `elem` 末尾，
- `"afterend"` — 将 `html` 插入到 `elem` 后。

第二个参数是 HTML 字符串，该字符串会被“作为 HTML” 插入。

![image-20211124203430244](JavaScript.assets/image-20211124203430244.png) 

这个方法有两个兄弟：

- `elem.insertAdjacentText(where, text)` — 语法一样，但是将 `text` 字符串“作为文本”插入而不是作为 HTML，
- `elem.insertAdjacentElement(where, elem)` — 语法一样，但是插入的是一个元素。

它们的存在主要是为了使语法“统一”。实际上，大多数时候只使用 `insertAdjacentHTML`。因为对于元素和文本，我们有 `append/prepend/before/after` 方法 — 它们也可以用于插入节点/文本片段，但写起来更短。

#### 移除

可以使用`node.remove()`

请注意：如果我们要将一个元素 **移动** 到另一个地方，则无需将其从原来的位置中删除。

**所有插入方法都会自动从旧位置删除该节点。**

例如，让我们进行元素交换：

```html
<div id="first">First</div>
<div id="second">Second</div>
<script>
  // 无需调用 remove
  second.after(first); // 获取 #second，并在其后面插入 #first
</script>
```

#### 克隆

调用 `elem.cloneNode(true)` 来创建元素的一个“深”克隆 — 具有所有特性（attribute）和子元素。如果我们调用 `elem.cloneNode(false)`，那克隆就不包括子元素。

#### DocumentFragment

`DocumentFragment` 是一个特殊的 DOM 节点，用作来传递节点列表的包装器（wrapper）。

我们可以向其附加其他节点，但是当我们将其插入某个位置时，则会插入其内容。

```html
<ul id="ul"></ul>

<script>
function getListContent() {
  let fragment = new DocumentFragment();

  for(let i=1; i<=3; i++) {
    let li = document.createElement('li');
    li.append(i);
    fragment.append(li);
  }

  return fragment;
}

ul.append(getListContent()); // (*)
</script>
```



### 样式和类

#### className 和 classList

在很久以前，JavaScript 中有一个限制：像 `"class"` 这样的保留字不能用作对象的属性。这一限制现在已经不存在了，但当时就不能存在像 `elem.class` 这样的 `"class"` 属性。

因此，对于类，引入了看起来类似的属性 `"className"`：`elem.className` 对应于 `"class"` 特性（attribute）。

如果我们对 `elem.className` 进行赋值，它将替换类中的整个字符串。有时，这正是我们所需要的，但通常我们希望添加/删除单个类。

这里还有另一个属性：`elem.classList`。

`elem.classList` 是一个特殊的对象，它具有 `add/remove/toggle` 单个类的方法。

`classList` 的方法：

- `elem.classList.add/remove(class)` — 添加/移除类。
- `elem.classList.toggle(class)` — 如果类不存在就添加类，存在就移除它。
- `elem.classList.contains(class)` — 检查给定类，返回 `true/false`。

#### 元素样式

`elem.style` 属性是一个对象，它对应于 `"style"` 特性（attribute）中所写的内容。

对于多词（multi-word）属性，使用驼峰式 camelCase：

```javascript
background-color  => elem.style.backgroundColor
z-index           => elem.style.zIndex
border-left-width => elem.style.borderLeftWidth
```

#### getComputedStyle

**`style` 属性仅对 `"style"` 特性（attribute）值起作用，而没有任何 CSS 级联（cascade）。**

**因此我们无法使用 `elem.style` 读取来自 CSS 类的任何内容。**

例如，这里的 `style` 看不到 margin：

```html
<head>
  <style> body { color: red; margin: 5px } </style>
</head>
<body>

  The red text
  <script>
    alert(document.body.style.color); // 空的
    alert(document.body.style.marginTop); // 空的
  </script>
</body>
```

……但如果我们需要，例如，将 margin 增加 20px 呢？那么我们需要 margin 的当前值。

对于这个需求，这里有另一种方法：`getComputedStyle`。

语法如下：

```javascript
getComputedStyle(element, [pseudo])
```



### 元素大小和滚动

![image-20211124232300038](JavaScript.assets/image-20211124232300038.png) 



### Window大小和滚动

为了获取窗口（window）的宽度和高度，我们可以使用 `document.documentElement` 的`clientWidth/clientHeight`：

<img src="JavaScript.assets/image-20211124232907122.png" alt="image-20211124232907122" style="zoom:50%;" />  

**文档的 width/height**

为了可靠地获得完整的文档高度，我们应该采用以下这些属性的最大值：

```javascript
let scrollHeight = Math.max(
  document.body.scrollHeight, document.documentElement.scrollHeight,
  document.body.offsetHeight, document.documentElement.offsetHeight,
  document.body.clientHeight, document.documentElement.clientHeight
);

alert('Full document height, with scrolled out part: ' + scrollHeight);
```

**滚动**

滚动在 `window.pageXOffset/pageYOffset` 中可用：

```javascript
alert('Current scroll from the top: ' + window.pageYOffset);
alert('Current scroll from the left: ' + window.pageXOffset);
```

这些属性是只读的。

可以通过更改 `scrollTop/scrollLeft` 来滚动常规元素。

我们可以使用 `document.documentElement.scrollTop/scrollLeft` 对页面进行相同的操作（Safari 除外，而应该使用 `document.body.scrollTop/Left` 代替）。

或者，有一个更简单的通用解决方案：使用特殊方法 [window.scrollBy(x,y)](https://developer.mozilla.org/zh/docs/Web/API/Window/scrollBy) 和 [window.scrollTo(pageX,pageY)](https://developer.mozilla.org/zh/docs/Web/API/Window/scrollTo)。

- 方法 `scrollBy(x,y)` 将页面滚动至 **相对于当前位置的 `(x, y)` 位置**。例如，`scrollBy(0,10)` 会将页面向下滚动 `10px`。

- 方法 `scrollTo(pageX,pageY)` 将页面滚动至 **绝对坐标**，使得可见部分的左上角具有相对于文档左上角的坐标 `(pageX, pageY)`。就像设置了 `scrollLeft/scrollTop` 一样。

  要滚动到最开始，我们可以使用 `scrollTo(0,0)`。

这些方法适用于所有浏览器。



### 坐标

大多数 JavaScript 方法处理的是以下两种坐标系中的一个：

1. 相对于窗口：类似于 position:fixed，从窗口的顶部/左侧边缘计算得出。
   - 我们将这些坐标表示为 `clientX/clientY`，当我们研究事件属性时，就会明白为什么使用这种名称来表示坐标。
2. 相对于文档：与文档根（document root）中的 position:absolute类似，从文档的顶部/左侧边缘计算得出。
   - 我们将它们表示为 `pageX/pageY`。

当页面滚动到最开始时，此时窗口的左上角恰好是文档的左上角，它们的坐标彼此相等。但是，在文档移动之后，元素的窗口相对坐标会发生变化，因为元素在窗口中移动，而元素在文档中的相对坐标保持不变。

在下图中，我们在文档中取一点，并演示了它滚动之前（左）和之后（右）的坐标：

![image-20211124233635414](JavaScript.assets/image-20211124233635414.png) 

#### 元素坐标

方法 `elem.getBoundingClientRect()` 返回最小矩形的窗口坐标，该矩形将 `elem` 作为内建 [DOMRect](https://www.w3.org/TR/geometry-1/#domrect) 类的对象。

主要的 `DOMRect` 属性：

- `x/y` — 矩形原点相对于窗口的 X/Y 坐标，
- `width/height` — 矩形的 width/height（可以为负）。

此外，还有派生（derived）属性：

- `top/bottom` — 顶部/底部矩形边缘的 Y 坐标，
- `left/right` — 左/右矩形边缘的 X 坐标。

<img src="JavaScript.assets/image-20211124234503461.png" alt="image-20211124234503461" style="zoom:50%;" /> 



## 事件简介

### 浏览器事件简介

常用的 DOM 事件的列表如下：

**鼠标事件：**

- `click` —— 当鼠标点击一个元素时（触摸屏设备会在点击时生成）。
- `contextmenu` —— 当鼠标右键点击一个元素时。
- `mouseover` / `mouseout` —— 当鼠标指针移入/离开一个元素时。
- `mousedown` / `mouseup` —— 当在元素上按下/释放鼠标按钮时。
- `mousemove` —— 当鼠标移动时。

**键盘事件**：

- `keydown` 和 `keyup` —— 当按下和松开一个按键时。

**表单（form）元素事件**：

- `submit` —— 当访问者提交了一个 `<form>` 时。
- `focus` —— 当访问者聚焦于一个元素时，例如聚焦于一个 `<input>`。

**Document 事件**：

- `DOMContentLoaded` —— 当 HTML 的加载和处理均完成，DOM 被完全构建完成时。

**CSS 事件**：

- `transitionend` —— 当一个 CSS 动画完成时。

#### 特性和属性

例如，要为一个 `input` 分配一个 `click` 处理程序，我们可以使用 `onclick`，像这样；

```html
<input value="Click me" onclick="alert('Click!')" type="button">
```

我们可以使用 DOM 属性（property）<strong style="color:red;">on<event></strong> 来分配处理程序。

例如 `elem.onclick`：

```markup
<input id="elem" type="button" value="Click me">
<script>
  elem.onclick = function() {
    alert('Thank you');
  };
</script>
```

**这里注意一点：特性中是`onclick=func()`，属性中是`onclick=func`**

这是因为当浏览器读取 HTML 特性（attribute）时，浏览器将会使用 **特性中的内容** 创建一个处理程序。

所以，标记（markup）会生成下面这个属性：

```javascript
button.onclick = function() {
  sayThanks(); // <-- 特性（attribute）中的内容变到了这里
};
```

#### addEventListener

上述的on<event>的方法不能为一个事件分配多个处理程序，因此要使用 addEventListener 添加处理程序，就可以分配多个处理程序

添加处理程序的语法：

```javascript
element.addEventListener(event, handler[, options]);
```

- `event`

  事件名，例如：`"click"`。

- `handler`

  处理程序。

- `options`

  具有以下属性的附加可选对象：`once`：如果为 `true`，那么会在被触发后自动删除监听器。`capture`：事件处理的阶段，我们稍后将在 [冒泡和捕获](https://zh.javascript.info/bubbling-and-capturing) 一章中介绍。由于历史原因，`options` 也可以是 `false/true`，它与 `{capture: false/true}` 相同。`passive`：如果为 `true`，那么处理程序将不会调用 `preventDefault()`，我们稍后将在 [浏览器默认行为](https://zh.javascript.info/default-browser-action) 一章中介绍。

要移除处理程序，可以使用 `removeEventListener`：

```javascript
element.removeEventListener(event, handler[, options]);
```

注意：只有具名的函数才能被移除

例子：

多次调用 `addEventListener` 允许添加多个处理程序，如下所示：

```html
<input id="elem" type="button" value="Click me"/>

<script>
  function handler1() {
    alert('Thanks!');
  };

  function handler2() {
    alert('Thanks again!');
  }

  elem.onclick = () => alert("Hello");
  elem.addEventListener("click", handler1); // Thanks!
  elem.addEventListener("click", handler2); // Thanks again!
</script>
```

#### 事件对象

当事件发生时，浏览器会创建一个 **`event` 对象**，将详细信息放入其中，并将其作为参数传递给处理程序。

`event` 对象的一些属性：

- `event.type`

  事件类型，这里是 `"click"`。

- `event.currentTarget`

  处理事件的元素。这与 `this` 相同，除非处理程序是一个箭头函数，或者它的 `this` 被绑定到了其他东西上，之后我们就可以从 `event.currentTarget` 获取元素了。

- `event.clientX / event.clientY`

  指针事件（pointer event）的指针的窗口相对坐标。

还有很多属性。其中很多都取决于事件类型

#### 对象处理程序 handleEvent

我们不仅可以分配函数，还可以使用 `addEventListener` 将一个对象分配为事件处理程序。当事件发生时，就会调用该对象的 `handleEvent` 方法。

例如：

```html
<button id="elem">Click me</button>

<script>
  let obj = {
    handleEvent(event) {
      alert(event.type + " at " + event.currentTarget);
    }
  };

  elem.addEventListener('click', obj);
</script>
```

正如我们所看到的，当 `addEventListener` 接收一个对象作为处理程序时，在事件发生时，它就会调用 `obj.handleEvent(event)` 来处理事件。

`handleEvent` 方法不必通过自身完成所有的工作。它可以调用其他特定于事件的方法，例如：

```html
<button id="elem">Click me</button>

<script>
  class Menu {
    handleEvent(event) {
      // mousedown -> onMousedown
      let method = 'on' + event.type[0].toUpperCase() + event.type.slice(1);
      this[method](event);
    }

    onMousedown() {
      elem.innerHTML = "Mouse button pressed";
    }

    onMouseup() {
      elem.innerHTML += "...and released.";
    }
  }

  let menu = new Menu();
  elem.addEventListener('mousedown', menu);
  elem.addEventListener('mouseup', menu);
</script>
```

现在事件处理程序已经明确地分离了出来，这样更容易进行代码编写和后续维护。



### 冒泡和捕获

#### 冒泡

![image-20211125193721792](JavaScript.assets/image-20211125193721792.png) 

**引发事件的那个嵌套层级最深的元素被称为目标元素,可以通过 `event.target` 访问。**

注意与 `this`（=`event.currentTarget`）之间的区别：

- `event.target` —— 是引发事件的“目标”元素，它在冒泡过程中不会发生变化。
- `this` —— 是“当前”元素，其中有一个当前正在运行的处理程序。

例如，如果我们有一个处理程序 `form.onclick`，那么它可以“捕获”表单内的所有点击。无论点击发生在哪里，它都会冒泡到 `<form>` 并运行处理程序。

在 `form.onclick` 处理程序中：

- `this`（=`event.currentTarget`）是 `<form>` 元素，因为处理程序在它上面运行。
- `event.target` 是表单中实际被点击的元素。

**停止冒泡**的方法是 `event.stopPropagation()`

如果一个元素在一个事件上有多个处理程序，即使其中一个停止冒泡，其他处理程序仍会执行。

换句话说，`event.stopPropagation()` 停止向上移动，但是当前元素上的其他处理程序都会继续运行。

有一个 `event.stopImmediatePropagation()` 方法，可以用于停止冒泡，并阻止当前元素上的处理程序运行。使用该方法之后，其他处理程序就不会被执行。

#### 捕获

[DOM 事件](http://www.w3.org/TR/DOM-Level-3-Events/)标准描述了事件传播的 3 个阶段：

1. 捕获阶段（Capturing phase）—— 事件（从 Window）向下走近元素。
2. 目标阶段（Target phase）—— 事件到达目标元素。
3. 冒泡阶段（Bubbling phase）—— 事件从元素上开始冒泡。

![image-20211125193826219](JavaScript.assets/image-20211125193826219.png) 

为了在捕获阶段捕获事件，我们需要将处理程序的 `capture` 选项设置为 `true`：

```javascript
elem.addEventListener(..., {capture: true})
// 或者，用 {capture: true} 的别名 "true"
elem.addEventListener(..., true)
```



### 事件委托

例如，我们想要编写一个有“保存”、“加载”和“搜索”等按钮的菜单。并且，这里有一个具有 `save`、`load` 和 `search` 等方法的对象。如何匹配它们？

第一个想法可能是为每个按钮分配一个单独的处理程序。但是有一个更优雅的解决方案。我们可以为整个菜单添加一个处理程序，并为具有方法调用的按钮添加 `data-action` 特性（attribute）：

```html
<button data-action="save">Click to Save</button>
```

处理程序读取特性（attribute）并执行该方法。工作示例如下：

```html
<div id="menu">
  <button data-action="save">Save</button>
  <button data-action="load">Load</button>
  <button data-action="search">Search</button>
</div>

<script>
  class Menu {
    constructor(elem) {
      this._elem = elem;
      elem.onclick = this.onClick.bind(this); // (*)
    }

    save() {
      alert('saving');
    }

    load() {
      alert('loading');
    }

    search() {
      alert('searching');
    }

    onClick(event) {
      let action = event.target.dataset.action;
      if (action) {
        this[action]();
      }
    };
  }

  new Menu(menu);
</script>
```

对父元素进行事件委托，根据子元素的 attribute 分配不同的任务

#### 行为模式

我们还可以使用事件委托将“行为（behavior）”以 **声明方式** 添加到具有特殊特性（attribute）和类的元素中。

行为模式分为两个部分：

1. 我们将自定义特性添加到描述其行为的元素。
2. 用文档范围级的处理程序追踪事件，如果事件发生在具有特定特性的元素上 —— 则执行行为（action）。

点击一个具有 `data-toggle-id` 特性的元素将显示/隐藏具有给定 `id` 的元素：

```html
<button data-toggle-id="subscribe-mail">
  Show the subscription form
</button>

<form id="subscribe-mail" hidden>
  Your mail: <input type="email">
</form>

<script>
  document.addEventListener('click', function(event) {
    let id = event.target.dataset.toggleId;
    if (!id) return;

    let elem = document.getElementById(id);

    elem.hidden = !elem.hidden;
  });
</script>
```

要向元素添加切换功能 —— 无需了解 JavaScript，只需要使用特性 `data-toggle-id` 即可。



### 浏览器默认行为

#### 阻止浏览器默认行为

有两种方式来告诉浏览器我们不希望它执行默认行为：

- 主流的方式是使用 `event` 对象。有一个 `event.preventDefault()` 方法。
- 如果处理程序是使用 `on<event>`（而不是 `addEventListener`）分配的，那返回 `false` 也同样有效。

在下面这个示例中，点击链接不会触发导航（navigation），浏览器不会执行任何操作：

```html
<a href="/" onclick="return false">Click here</a>
or
<a href="/" onclick="event.preventDefault()">here</a>
```

#### 处理程序选项“passive”

`addEventListener` 的可选项 `passive: true` 向浏览器发出信号，表明处理程序将不会调用 `preventDefault()`

移动设备上会发生一些事件，例如 `touchmove`（当用户在屏幕上移动手指时），默认情况下会导致滚动，但是可以使用处理程序的 `preventDefault()` 来阻止滚动。

因此，当浏览器检测到此类事件时，它必须首先处理所有处理程序，然后如果没有任何地方调用 `preventDefault`，则页面可以继续滚动。但这可能会导致 UI 中不必要的延迟和“抖动”。

`passive: true` 选项告诉浏览器，处理程序不会取消滚动。然后浏览器立即滚动页面以提供最大程度的流畅体验，并通过某种方式处理事件。

#### event.defaultPrevented

可以用于检查处理程序是否阻止了浏览器的默认行为？如果阻止了，那么该事件已经得到了处理，我们无需再对此事件做出反应。



### 自定义事件

#### 事件构造器

我们可以像这样创建 `Event` 对象：

```javascript
let event = new Event(type[, options]);
```

参数：

- **type** —— 事件类型，可以是像这样 `"click"` 的字符串，或者我们自己的像这样 `"my-event"` 的参数。

- **options** —— 具有两个可选属性的对象：

  - `bubbles: true/false` —— 如果为 `true`，那么事件会冒泡。
  - `cancelable: true/false` —— 如果为 `true`，那么“默认行为”就会被阻止。稍后我们会看到对于自定义事件，它意味着什么。

  默认情况下，以上两者都为 false：`{bubbles: false, cancelable: false}`。

#### dispachEvent

事件对象被创建后，我们应该使用 `elem.dispatchEvent(event)` 调用在元素上“运行”它。

然后，处理程序会对它做出反应，就好像它是一个常规的浏览器事件一样。如果事件是用 `bubbles` 标志创建的，那么它会冒泡。

```html
<h1 id="elem">Hello from the script!</h1>

<script>
  // 在 document 上捕获...
  document.addEventListener("hello", function(event) { // (1)
    alert("Hello from " + event.target.tagName); // Hello from H1
  });

  // ...在 elem 上 dispatch！
  let event = new Event("hello", {bubbles: true}); // (2)
  elem.dispatchEvent(event);

  // 在 document 上的处理程序将被激活，并显示消息。

</script>
```

#### MouseEvent, keyboardEvent 等

这是一个摘自于 [UI 事件规范](https://www.w3.org/TR/uievents) 的一个简短的 UI 事件类列表：

- `UIEvent`
- `FocusEvent`
- `MouseEvent`
- `WheelEvent`
- `KeyboardEvent`
- …

如果我们想要创建这样的事件，我们应该使用它们而不是 `new Event`。例如，`new MouseEvent("click")`。

正确的构造器允许为该类型的事件指定标准属性。

#### 自定义事件

对于我们自己的全新事件类型，例如 `"hello"`，我们应该使用 `new CustomEvent`。从技术上讲，[CustomEvent](https://dom.spec.whatwg.org/#customevent) 和 `Event` 一样。除了一点不同。

在第二个参数（对象）中，我们可以为我们想要与事件一起传递的任何自定义信息添加一个附加的属性 `detail`。

例如：

```html
<h1 id="elem">Hello for John!</h1>

<script>
  // 事件附带给处理程序的其他详细信息
  elem.addEventListener("hello", function(event) {
    alert(event.detail.name);
  });

  elem.dispatchEvent(new CustomEvent("hello", {
    detail: { name: "John" }
  }));
</script>
```

`detail` 属性可以有任何数据。从技术上讲，我们可以不用，因为我们可以在创建后将任何属性分配给常规的 `new Event` 对象中。但是 `CustomEvent` 提供了特殊的 `detail` 字段，以避免与其他事件属性的冲突。



#### event.preventDefault()

对于新的，自定义的事件，绝对没有默认的浏览器行为，但是分派（dispatch）此类事件的代码可能有自己的计划，触发该事件之后应该做什么。

通过调用 `event.preventDefault()`，事件处理程序可以发出一个信号，指出这些行为应该被取消。

在这种情况下，`elem.dispatchEvent(event)` 的调用会返回 `false`。那么分派（dispatch）该事件的代码就会知道不应该再继续。

```html
<pre id="rabbit">
  |\   /|
   \|_|/
   /. .\
  =\_Y_/=
   {>o<}
</pre>
<button onclick="hide()">Hide()</button>

<script>
  function hide() {
    let event = new CustomEvent("hideMe", {
      cancelable: true // 没有这个标志，preventDefault 将不起作用
    });
    if (!rabbit.dispatchEvent(event)) {
      alert('The action was prevented by a handler');
    } else {
      rabbit.hidden = true;
    }
  }

  rabbit.addEventListener('hideMe', function(event) {
    if (confirm("Call preventDefault?")) {
      event.preventDefault();
    }
  });
</script>
```



## UI事件

### 鼠标事件

其中的一些事件：

- `mousedown/mouseup`

  在元素上点击/释放鼠标按钮。

- `mouseover/mouseout`

  鼠标指针从一个元素上移入/移出。

- `mousemove`

  鼠标在元素上的每个移动都会触发此事件。

- `click`

  如果使用的是鼠标左键，则在同一个元素上的 `mousedown` 及 `mouseup` 相继触发后，触发该事件。

- `dblclick`

  在短时间内双击同一元素后触发。如今已经很少使用了。

- `contextmenu`

  在鼠标右键被按下时触发。还有其他打开上下文菜单的方式，例如使用特殊的键盘按键，在这种情况下它也会被触发，因此它并不完全是鼠标事件。

#### 事件顺序

从上面的列表中我们可以看到，一个用户操作可能会触发多个事件。

例如，点击鼠标左键，在鼠标左键被按下时，会首先触发 `mousedown`，然后当鼠标左键被释放时，会触发 `mouseup` 和 `click`。

在单个动作触发多个事件时，事件的顺序是固定的。也就是说，会遵循 `mousedown` → `mouseup` → `click` 的顺序调用处理程序。

#### 鼠标按钮

与点击相关的事件始终具有 `button` 属性，该属性允许获取确切的鼠标按钮。

通常我们不在 `click` 和 `contextmenu` 事件中使用这一属性，因为前者只在单击鼠标左键时触发，后者只在单击鼠标右键时触发。

不过，在 `mousedown` 和 `mouseup` 事件中则可能需要用到 `event.button`，因为这两个事件在任何按键上都会触发，所以我们可以使用 `button` 属性来区分是左键单击还是右键单击。

`event.button` 的所有可能值如下：

| 鼠标按键状态     | `event.button` |
| :--------------- | :------------- |
| 左键 (主要按键)  | 0              |
| 中键 (辅助按键)  | 1              |
| 右键 (次要按键)  | 2              |
| X1 键 (后退按键) | 3              |
| X2 键 (前进按键) | 4              |

#### 组合键：shift, alt, ctrl, meta

所有的鼠标事件都包含有关按下的组合键的信息。

事件属性：

- `shiftKey`：Shift
- `altKey`：Alt（或对于 Mac 是 Opt）
- `ctrlKey`：Ctrl
- `metaKey`：对于 Mac 是 Cmd

如果在事件期间按下了相应的键，则它们为 `true`。

比如，下面这个按钮仅在 Alt+Shift+click 时才有效：

```html
<button id="button">Alt+Shift+Click on me!</button>

<script>
  button.onclick = function(event) {
    if (event.altKey && event.shiftKey) {
      alert('Hooray!');
    }
  };
</script>
```

#### 防止在鼠标按下时的选择

双击鼠标会有副作用，在某些界面中可能会出现干扰：它会选择文本。

比如，双击下面的文本，除了我们的处理程序外，还会选择文本：

```html
<span ondblclick="alert('dblclick')">Double-click me</span>
```

如果按下鼠标左键，并在不松开的情况下移动鼠标，这也常常会造成不必要的选择。

有多种防止选择的方法，你可以在 [选择（Selection）和范围（Range）](https://zh.javascript.info/selection-range) 一章中详细阅读。

在这种情况下，最合理的方式是防止浏览器对 `mousedown` 进行操作。这样能够阻止刚刚提到的两种选择：

```html
Before...
<b ondblclick="alert('Click!')" onmousedown="return false">
  Double-click me
</b>
...After
```

现在，在双击时，粗体元素不会被选中，并且在粗体元素上按下鼠标左键也不会开始选择。

**防止复制** 可以对 oncopy 事件进行默认行为阻塞



### 移动鼠标

#### mouseover / out, relatedTarget

![image-20211127163717974](media/image-20211127163717974.png) 

它们具有 `relatedTarget` 属性。此属性是对 `target` 的补充。当鼠标从一个元素离开并去往另一个元素时，其中一个元素就变成了 `target`，另一个就变成了 `relatedTarget`。

对于 `mouseover`：

- `event.target` —— 是鼠标移过的那个元素。
- `event.relatedTarget` —— 是鼠标来自的那个元素（`relatedTarget` → `target`）。

`mouseout` 则与之相反：

- `event.target` —— 是鼠标离开的元素。
- `event.relatedTarget` —— 是鼠标移动到的，当前指针位置下的元素（`target` → `relatedTarget`）。

#### 当移动到子元素时 mouseout

`mouseout` 的一个重要功能 —— 当鼠标指针从元素移动到其后代时触发，例如在下面的这个 HTML 中，从 `#parent` 到 `#child`：

```html
<div id="parent">
  <div id="child">...</div>
</div>
```

如果我们在 `#parent` 上，然后将鼠标指针更深入地移入 `#child`，但是在 `#parent` 上会得到 `mouseout`

![image-20211127165304319](media/image-20211127165304319.png) 

**根据浏览器的逻辑，鼠标指针随时可能位于单个元素上 —— 嵌套最多的那个元素（z-index 最大的那个）。**

因此，如果它转到另一个元素（甚至是一个后代），那么它将离开前一个元素。

**后代的 `mouseover` 事件会冒泡。因此，如果 `#parent` 具有 `mouseover` 处理程序，它将被触发。**

#### mouseenter / mouseleave

事件 `mouseenter/mouseleave` 类似于 `mouseover/mouseout`。它们在鼠标指针进入/离开元素时触发。

但是有两个重要的**区别**：

1. 元素内部与后代之间的转换不会产生影响。
2. 事件 `mouseenter/mouseleave` 不会冒泡。

这些事件非常简单。

当鼠标指针进入一个元素时 —— 会触发 `mouseenter`。而鼠标指针在元素或其后代中的确切位置无关紧要。

当鼠标指针离开该元素时，事件 `mouseleave` 才会触发。

这个例子和上面的例子相似，但是现在最顶部的元素有 `mouseenter/mouseleave` 而不是 `mouseover/mouseout`。

正如你所看到的，唯一生成的事件是与将鼠标指针移入或移出顶部元素有关的事件。当鼠标指针进入 child 并返回时，什么也没发生。在后代之间的移动会被忽略。

#### 事件委托

可以利用 mouseover 和 mouseout 事件冒泡特性进行事件委托



### 鼠标拖放事件

基础的拖放算法如下所示：

1. 在 `mousedown` 上 —— 根据需要准备要移动的元素（也许创建一个它的副本，向其中添加一个类或其他任何东西）。
2. 然后在 `mousemove` 上，通过更改 `position:absolute` 情况下的 `left/top` 来移动它。
3. 在 `mouseup` 上 —— 执行与完成的拖放相关的所有行为。

这些都是基础内容。稍后，我们将看到如何实现其他功能，例如当我们将一个东西拖动到一个元素上方时，高亮显示该元素。

下面是拖放一个球的实现代码：

```javascript
ball.onmousedown = function(event) {
  // (1) 准备移动：确保 absolute，并通过设置 z-index 以确保球在顶部
  ball.style.position = 'absolute';
  ball.style.zIndex = 1000;

  // 将其从当前父元素中直接移动到 body 中
  // 以使其定位是相对于 body 的
  document.body.append(ball);

  // 现在球的中心在 (pageX, pageY) 坐标上
  function moveAt(pageX, pageY) {
    ball.style.left = pageX - ball.offsetWidth / 2 + 'px';
    ball.style.top = pageY - ball.offsetHeight / 2 + 'px';
  }

  // 将我们绝对定位的球移到指针下方
  moveAt(event.pageX, event.pageY);

  function onMouseMove(event) {
    moveAt(event.pageX, event.pageY);
  }

  // (2) 在 mousemove 事件上移动球
  document.addEventListener('mousemove', onMouseMove);

  // (3) 放下球，并移除不需要的处理程序
  ball.onmouseup = function() {
    document.removeEventListener('mousemove', onMouseMove);
    ball.onmouseup = null;
  };

};
```

如果我们运行这段代码，我们会发现一些奇怪的事情。在拖放的一开始，球“分叉”了：我们开始拖动它的“克隆”。

这是因为浏览器有自己的对图片和一些其他元素的拖放处理。它会在我们进行拖放操作时自动运行，并与我们的拖放处理产生了冲突。

禁用它：

```javascript
ball.ondragstart = function() {
  return false;
};
```

一个重要的方面是 —— 我们在 `document` 上跟踪 `mousemove`，而不是在 `ball` 上。乍一看，鼠标似乎总是在球的上方，我们可以将 `mousemove` 放在球上。但正如我们所记得的那样，`mousemove` 会经常被触发，但不会针对每个像素都如此。因此，在快速移动鼠标后，鼠标指针可能会从球上跳转至文档中间的某个位置（甚至跳转至窗口外）。因此，我们应该监听 `document` 以捕获它。

#### 修正定位

用 `ball.getBoundingClientRect() `来修正球的定位



### 指针事件

由于移动端的事件更加复杂，因此引入了指针事件来提供了一套统一的事件

指针事件的命名方式和鼠标事件类似：

| 指针事件             | 类似的鼠标事件 |
| :------------------- | :------------- |
| `pointerdown`        | `mousedown`    |
| `pointerup`          | `mouseup`      |
| `pointermove`        | `mousemove`    |
| `pointerover`        | `mouseover`    |
| `pointerout`         | `mouseout`     |
| `pointerenter`       | `mouseenter`   |
| `pointerleave`       | `mouseleave`   |
| `pointercancel`      | -              |
| `gotpointercapture`  | -              |
| `lostpointercapture` | -              |

不难发现，每一个 `mouse<event>` 都有与之相对应的 `pointer<event>`。同时还有 3 个额外的事件没有相应的 `mouse...`，我们会在稍后详细解释它们。

#### 指针事件属性

指针事件具备和鼠标事件完全相同的属性，包括 `clientX/Y` 和 `target` 等，以及一些其他属性：

- `pointerId` —— 触发当前事件的指针唯一标识符。

  浏览器生成的。使我们能够处理多指针的情况，例如带有触控笔和多点触控功能的触摸屏（下文会有相关示例）。

- `pointerType` —— 指针的设备类型。必须为字符串，可以是：“mouse”、“pen” 或 “touch”。

  我们可以使用这个属性来针对不同类型的指针输入做出不同响应。

- `isPrimary` —— 当指针为首要指针（多点触控时按下的第一根手指）时为 `true`。

有些指针设备会测量接触面积和点按压力（例如一根手指压在触屏上），对于这种情况可以使用以下属性：

- `width` —— 指针（例如手指）接触设备的区域的宽度。对于不支持的设备（如鼠标），这个值总是 `1`。
- `height` —— 指针（例如手指）接触设备的区域的长度。对于不支持的设备，这个值总是 `1`。
- `pressure` —— 触摸压力，是一个介于 0 到 1 之间的浮点数。对于不支持压力检测的设备，这个值总是 `0.5`（按下时）或 `0`。
- `tangentialPressure` —— 归一化后的切向压力（tangential pressure）。
- `tiltX`, `tiltY`, `twist` —— 针对触摸笔的几个属性，用于描述笔和屏幕表面的相对位置。

大多数设备都不支持这些属性，因此它们很少被使用。如果你需要使用它们，可以在 [规范文档](https://w3c.github.io/pointerevents/#pointerevent-interface) 中查看更多有关它们的详细信息。

#### 多点触控

多点触控（用户在手机或平板上同时点击若干个位置，或执行特殊手势）是鼠标事件完全不支持的功能之一。

指针事件使我们能够通过 `pointerId` 和 `isPrimary` 属性的帮助，能够处理多点触控。

当用户用一根手指触摸触摸屏的某个位置，然后将另一根手指放在该触摸屏的其他位置时，会发生以下情况：

1. 第一个手指触摸：
   - `pointerdown` 事件触发，`isPrimary=true`，并且被指派了一个 `pointerId`。
2. 第二个和后续的更多个手指触摸（假设第一个手指仍在触摸）：
   - `pointerdown` 事件触发，`isPrimary=false`，并且每一个触摸都被指派了不同的 `pointerId`。

请注意：`pointerId` 不是分配给整个设备的，而是分配给每一个触摸的。如果 5 根手指同时触摸屏幕，我们会得到 5 个 `pointerdown` 事件和相应的坐标以及 5 个不同的 `pointerId`。

和第一个触摸相关联的事件总有 `isPrimary=true`。

利用 `pointerId`，我们可以追踪多根正在触摸屏幕的手指。当用户移动或抬起某根手指时，我们会得到和 `pointerdown` 事件具有相同 `pointerId` 的 `pointermove` 或 `pointerup` 事件。

#### 指针捕获

主要的方法是：

- `elem.setPointerCapture(pointerId)` —— 将给定的 `pointerId` 绑定到 `elem`。在调用之后，所有具有相同 `pointerId` 的指针事件都将 `elem` 作为目标（就像事件发生在 `elem` 上一样），无论这些 `elem` 在文档中的实际位置是什么。

换句话说，`elem.setPointerCapture(pointerId)` 将所有具有给定 `pointerId` 的后续事件重新定位到 `elem`。

绑定会在以下情况下被移除：

- 当 `pointerup` 或 `pointercancel` 事件出现时，绑定会被自动地移除。
- 当 `elem` 被从文档中移除后，绑定会被自动地移除。
- 当 `elem.releasePointerCapture(pointerId)` 被调用，绑定会被移除。

比如上一节移动滑块需要给document绑定移动事件，但是通过 `setPointerCapture` 对 elem 进行绑定

```javascript
thumb.onpointerdown = function(event) {
  // 把所有指针事件（pointerup 之前发生的）重定向到 thumb
  thumb.setPointerCapture(event.pointerId);
};

thumb.onpointermove = function(event) {
  // 移动滑动条：在 thumb 上监听即可，因为所有指针事件都被重定向到了 thumb
  let newLeft = event.clientX - slider.getBoundingClientRect().left;
  thumb.style.left = newLeft + 'px';
};

// 注意：无需调用 thumb.releasePointerCapture，
// 它会在 pointerup 时自动调用
```



### 键盘事件

#### keydown 和 keyup

当一个按键被按下时，会触发 `keydown` 事件，而当按键被释放时，会触发 `keyup` 事件。

#### event.code 和 event.key

事件对象的 `key` 属性允许获取字符，而事件对象的 `code` 属性则允许获取“物理按键代码”。

例如，同一个按键 Z，可以与或不与 `Shift` 一起按下。我们会得到两个不同的字符：小写的 `z` 和大写的 `Z`。

`event.key` 正是这个字符，并且它将是不同的。但是，`event.code` 是相同的：

| Key     | `event.key` | `event.code` |
| :------ | :---------- | :----------- |
| Z       | `z`（小写） | `KeyZ`       |
| Shift+Z | `Z`（大写） | `KeyZ`       |

如果按键没有给出任何字符呢？例如，Shift 或 F1 或其他。对于这些按键，它们的 `event.key` 与 `event.code` 大致相同：

| Key       | `event.key` | `event.code`                |
| :-------- | :---------- | :-------------------------- |
| F1        | `F1`        | `F1`                        |
| Backspace | `Backspace` | `Backspace`                 |
| Shift     | `Shift`     | `ShiftRight` 或 `ShiftLeft` |

#### 自动重复

如果按下一个键足够长的时间，它就会开始“自动重复”：`keydown` 会被一次又一次地触发，然后当按键被释放时，我们最终会得到 `keyup`。因此，有很多 `keydown` 却只有一个 `keyup` 是很正常的。对于由自动重复触发的事件，`event` 对象的 `event.repeat` 属性被设置为 `true`。

#### 默认行为

默认行为各不相同，因为键盘可能会触发很多可能的东西。

例如：

- 出现在屏幕上的一个字符（最明显的结果）。
- 一个字符被删除（Delete 键）。
- 滚动页面（PageDown 键）。
- 浏览器打开“保存页面”对话框（Ctrl+S）
- ……等。

阻止对 `keydown` 的默认行为可以取消大多数的行为，但基于 OS 的特殊按键除外。例如，在 Windows 中，Alt+F4 会关闭当前浏览器窗口。并且无法通过在 JavaScript 中阻止默认行为来阻止它。

例如，下面的这个 `<input>` 期望输入的内容为一个电话号码，因此它不会接受除数字，`+`，`()` 和 `-` 以外的按键：

```html
<script>
function checkPhoneKey(key) {
  return (key >= '0' && key <= '9') || ['+','(',')','-'].includes(key);
}
</script>
<input onkeydown="return checkPhoneKey(event.key)" placeholder="请输入手机号" type="tel">
```



### 滚动

`scroll` 事件允许对页面或元素滚动作出反应。我们可以在这里做一些有用的事情。

例如：

- 根据用户在文档中的位置显示/隐藏其他控件或信息。
- 当用户向下滚动到页面末端时加载更多数据。

这是一个显示当前滚动的小函数：

```javascript
window.addEventListener('scroll', function() {
  document.getElementById('showScroll').innerHTML = window.pageYOffset + 'px';
});
```

#### 防止滚动

我们不能通过在 `onscroll` 监听器中使用 `event.preventDefault()` 来阻止滚动，因为它会在滚动发生 **之后** 才触发。

但是我们可以在导致滚动的事件上，例如在 pageUp 和 pageDown 的 `keydown` 事件上，使用 `event.preventDefault()` 来阻止滚动。

如果我们向这些事件中添加事件处理程序，并向其中添加 `event.preventDefault()`，那么滚动就不会开始。



## 表单和控件

### 表单属性和方法

表单（form）以及例如 `<input>` 的控件（control）元素有许多特殊的属性和事件。

#### 表单和元素导航

文档中的表单是特殊集合 `document.forms` 的成员。

这就是所谓的“命名的集合”：既是被命名了的，也是有序的。我们既可以使用名字，也可以使用在文档中的编号来获取表单。

当我们有了一个表单时，其中的任何元素都可以通过命名的集合 `form.elements` 来获取到。

例如：

```html
<form name="my">
  <input name="one" value="1">
  <input name="two" value="2">
</form>

<script>
  // 获取表单
  let form = document.forms.my; // <form name="my"> 元素

  // 获取表单中的元素
  let elem = form.elements.one; // <input name="one"> 元素

  alert(elem.value); // 1
</script>
```

可能会有多个名字相同的元素，这种情况经常在处理单选按钮中出现。

在这种情况下，`form.elements[name]` 将会是一个集合，例如：

```html
<form>
  <input type="radio" name="age" value="10">
  <input type="radio" name="age" value="20">
</form>

<script>
let form = document.forms[0];

let ageElems = form.elements.age;

alert(ageElems[0]); // [object HTMLInputElement]
</script>
```

#### 表单元素

* **input 和 textarea**

我们可以通过 `input.value`（字符串）或 `input.checked`（布尔值）来访问复选框（checkbox）中的它们的 `value`。

像这样：

```javascript
input.value = "New value";
textarea.value = "New text";

input.checked = true; // 对于复选框（checkbox）或单选按钮（radio button）
```

* **select**

一个 `<select>` 元素有 3 个重要的属性：

1. `select.options` —— `<option>` 的子元素的集合，
2. `select.value` —— 当前所选择的 `<option>` 的 `value`，
3. `select.selectedIndex` —— 当前所选择的 `<option>` 的编号。

它们提供了三种为 `<select>` 设置 `value` 的不同方式：

1. 找到对应的 `<option>` 元素，并将 `option.selected` 设置为 `true`。
2. 将 `select.value` 设置为对应的 `value`。
3. 将 `select.selectedIndex` 设置为对应 `<option>` 的编号。



### 聚焦

#### focus / blur 事件

当元素聚焦时，会触发 `focus` 事件，当元素失去焦点时，会触发 `blur` 事件。

让我们使用它们来校验一个 `input` 字段。

在下面这个示例中：

- `blur` 事件处理程序检查这个字段是否输入了电子邮箱，如果没有输入，则显示一个 error。
- `focus` 事件处理程序隐藏 error 信息（在 `blur` 事件处理程序上会被再检查一遍）：

```html
<style>
  .invalid { border-color: red; }
  #error { color: red }
</style>

Your email please: <input type="email" id="input">

<div id="error"></div>

<script>
input.onblur = function() {
  if (!input.value.includes('@')) { // not email
    input.classList.add('invalid');
    error.innerHTML = 'Please enter a correct email.'
  }
};

input.onfocus = function() {
  if (this.classList.contains('invalid')) {
    // 移除 "error" 指示，因为用户想要重新输入一些内容
    this.classList.remove('invalid');
    error.innerHTML = "";
  }
};
</script>
```

#### focus / blur 方法

`elem.focus()` 和 `elem.blur()` 方法可以设置和移除元素上的焦点。

例如，如果输入值无效，我们可以让焦点无法离开这个 `input` 字段

#### tabindex 聚焦顺序

可以指定 tabindex 特性，使 tab 键按照规定的顺序移动

举个例子，这里有一个列表。点击第一项，然后按 Tab 键：

```html
<ul>
  <li tabindex="1">One</li>
  <li tabindex="0">Zero</li>
  <li tabindex="2">Two</li>
  <li tabindex="-1">Minus one</li>
</ul>

<style>
  li { cursor: pointer; }
  :focus { outline: 1px dashed green; }
</style>
```

**事件委托**

* focus / blur 事件不会冒泡，因此无法通过其进行事件委托
* focusin / focusout 事件效果和 focus / blur 一样，但是其会进行事件冒泡，可以用于事件委托



### 数据更新事件

#### change

当元素更改完成时，将触发 `change` 事件。

对于文本输入框，当其失去焦点时，就会触发 `change` 事件。

例如，当我们在下面的文本字段中键入内容时 —— 不会触发 `change` 事件。但是，当我们将焦点移到其他位置时，例如，点击按钮 —— 就会触发 `change` 事件：

```html
<input type="text" onchange="alert(this.value)">
<input type="button" value="Button">
```

对于其它元素：`select`，`input type=checkbox/radio`，会在选项更改后立即触发 `change` 事件。

#### input

每当用户对输入值进行修改后，就会触发 `input` 事件。

与键盘事件不同，只要值改变了，`input` 事件就会触发，即使那些不涉及键盘行为（action）的值的更改也是如此：使用鼠标粘贴，或者使用语音识别来输入文本。

#### cut / copy / paste

这些事件发生于剪切/拷贝/粘贴一个值的时候。

它们属于 [ClipboardEvent](https://www.w3.org/TR/clipboard-apis/#clipboard-event-interfaces) 类，并提供了对拷贝/粘贴的数据的访问方法。

我们也可以使用 `event.preventDefault()` 来中止行为，然后什么都不会被复制/粘贴。

例如，下面的代码阻止了所有的这样的事件，并显示出了我们所尝试剪切/拷贝/粘贴的内容：

```html
<input type="text" id="input">
<script>
  input.oncut = input.oncopy = input.onpaste = function(event) {
    alert(event.type + ' - ' + event.clipboardData.getData('text/plain'));
    return false;
  };
</script>
```

### 表单事件

#### submit 事件

提交表单主要有两种方式：

1. 第一种 —— 点击 `<input type="submit">` 或 `<input type="image">`。
2. 第二种 —— 在 `input` 字段中按下 Enter 键。

这两个行为都会触发表单的 `submit` 事件。处理程序可以检查数据，如果有错误，就显示出来，并调用 `event.preventDefault()`，这样表单就不会被发送到服务器了。

#### submit() 方法

如果要手动将表单提交到服务器，我们可以调用 `form.submit()`。

这样就不会产生 `submit` 事件。这里假设如果开发人员调用 `form.submit()`，就意味着此脚本已经进行了所有相关处理。



## 加载文档和其他资源

### 页面生命周期

HTML 页面的生命周期包含三个重要事件：

- `DOMContentLoaded` —— 浏览器已完全加载 HTML，并构建了 DOM 树，但像 `<img>` 和样式表之类的外部资源可能尚未加载完成。
- `load` —— 浏览器不仅加载完成了 HTML，还加载完成了所有外部资源：图片，样式等。
- `beforeunload/unload` —— 当用户正在离开页面时。

每个事件都是有用的：

- `DOMContentLoaded` 事件 —— DOM 已经就绪，因此处理程序可以查找 DOM 节点，并初始化接口。
- `load` 事件 —— 外部资源已加载完成，样式已被应用，图片大小也已知了。
- `beforeunload` 事件 —— 用户正在离开：我们可以检查用户是否保存了更改，并询问他是否真的要离开。
- `unload` 事件 —— 用户几乎已经离开了，但是我们仍然可以启动一些操作，例如发送统计数据。

#### readyState

在某些情况下，我们不确定文档是否已经准备就绪。我们希望我们的函数在 DOM 加载完成时执行，无论现在还是以后。

`document.readyState` 属性可以为我们提供当前加载状态的信息。

它有 3 个可能值：

- `loading` —— 文档正在被加载。
- `interactive` —— 文档被全部读取。
- `complete` —— 文档被全部读取，并且所有资源（例如图片等）都已加载完成。



### 脚本：async, defer

当浏览器加载 HTML 时遇到 `<script>...</script>` 标签，浏览器就不能继续构建 DOM。它必须立刻执行此脚本。对于外部脚本 `<script src="..."></script>` 也是一样的：浏览器必须等脚本下载完，并执行结束，之后才能继续处理剩余的页面。

这会导致两个重要的问题：

1. 脚本不能访问到位于它们下面的 DOM 元素，因此，脚本无法给它们添加处理程序等。
2. 如果页面顶部有一个笨重的脚本，它会“阻塞页面”。在该脚本下载并执行结束前，用户都不能看到页面内容：

这里有一些解决办法。例如，我们可以把脚本放在页面底部。此时，它可以访问到它上面的元素，并且不会阻塞页面显示内容。但是浏览器只有在下载了完整的 HTML 文档之后才会注意到该脚本（并且可以开始下载它）。对于长的 HTML 文档来说，这样可能会造成明显的延迟。

#### defer

`defer` 特性告诉浏览器不要等待脚本。相反，浏览器将继续处理 HTML，构建 DOM。脚本会“在后台”下载，然后等 DOM 构建完成后，脚本才会执行。

```html
<p>...content before script...</p>

<script defer src="https://javascript.info/article/script-async-defer/long.js?speed=1"></script>

<!-- 立即可见 -->
<p>...content after script...</p>
```

换句话说：

- 具有 `defer` 特性的脚本不会阻塞页面。
- 具有 `defer` 特性的脚本总是要等到 DOM 解析完毕，但在 `DOMContentLoaded` 事件之前执行。

**具有 `defer` 特性的脚本保持其相对顺序，就像常规脚本一样。**

#### async

`async` 特性与 `defer` 有些类似。它也能够让脚本不阻塞页面。但是，在行为上二者有着重要的区别。

`async` 特性意味着脚本是完全独立的：

- 浏览器不会因 `async` 脚本而阻塞（与 `defer` 类似）。
- 其他脚本不会等待 `async` 脚本加载完成，同样，`async` 脚本也不会等待其他脚本。
- `DOMContentLoaded` 和异步脚本不会彼此等待：
  - `DOMContentLoaded` 可能会发生在异步脚本之前（如果异步脚本在页面完成后才加载完成）
  - `DOMContentLoaded` 也可能发生在异步脚本之后（如果异步脚本很短，或者是从 HTTP 缓存中加载的）

#### 动态脚本

此外，还有一种向页面添加脚本的重要的方式。

我们可以使用 JavaScript 动态地创建一个脚本，并将其附加（append）到文档（document）中：

```javascript
let script = document.createElement('script');
script.src = "/article/script-async-defer/long.js";
document.body.append(script); // (*)
```

当脚本被附加到文档 `(*)` 时，脚本就会立即开始加载。

**默认情况下，动态脚本的行为是“异步”的。**

也就是说：

- 它们不会等待任何东西，也没有什么东西会等它们。
- 先加载完成的脚本先执行（“加载优先”顺序）。

如果我们显式地设置了 `script.async=false`，则可以改变这个规则。然后脚本将按照脚本在文档中的顺序执行，就像 `defer` 那样。



### 资源加载

浏览器允许我们跟踪外部资源的加载 —— 脚本，iframe，图片等。

这里有两个事件：

- `onload` —— 成功加载，
- `onerror` —— 出现 error。

#### script.onload

它会在脚本加载并执行完成时触发。

例如：

```javascript
let script = document.createElement('script');

// 可以从任意域（domain），加载任意脚本
script.src = "https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.3.0/lodash.js"
document.head.append(script);

script.onload = function() {
  // 该脚本创建了一个变量 "_"
  alert( _.VERSION ); // 显示库的版本
};
```

因此，在 `onload` 中我们可以使用脚本中的变量，运行函数等。

#### script.onerror

发生在脚本加载期间的 error 会被 `error` 事件跟踪到。

#### 其他资源

`load` 和 `error` 事件也适用于其他资源，基本上（basically）适用于具有外部 `src` 的任何资源。

#### 跨源策略

暂时用不上





# JavaScript进阶

## 数据类型

### 数字

* `num.toString(进制)` 将数字转换成规定进制字符串的形式，如果要直接对数字使用，则在数字后跟两个点，`123456..toString(8)`
* `num.toFixed(小数位)` 返回一个字符串，配合 Numer 或者 + 使用，`+num.toFixed(5)`
* `parseInt(字符串[，进制])` 和 `parseFloat(字符串[，进制])` 可以对取出字符串中的数字，`alert( parseFloat('12.5em') ); // 12.5`

### 字符串

* `str[pos]` 或 `strcharAt(pos)` 访问字符串，也可以使用 `for...of` 进行遍历
* 字符串检索：
  * `str.indexOf(字符串[，位置])` 检索字符串，如果有，则返回位置，没有返回-1，可以指定位置开始检索
  * `str.includes(字符串)` 检索字符串，有true，无false
* 获取字符串：
  * `str.slice(start[, end])` 返回从 start 到 end (不包括) 之间的部分，支持负数 **（推荐）**
  * `str.substring(start[, end])` 与 slice 相同，不支持负数，但是允许 end 大于 start
  * `str.substr(start [, length])` 按长度取，支持负数

### 数组

* `push/pop` 尾部进、出，`shift/unshift` 头部出、进
* `length` 是可以改写的属性，因此清空数组最好的方法就是 `arr.length = 0`
* `[1,2,3].toString()` 会变成 `'1,2,3'`
* 改动数组：
  * 添加、删除和插入 `arr.splice(start[, deleteCount, elem1, ..., elemN])` 
  * 截取数组 `arr.slice([start], [end])` **返回新数组，原数组不变**
  * 拼接数组 `arr.concat(arg1, arg2)` **返回新数组，原数组不变**，用于拼接多个数组或其他项

* 遍历数组 `arr.forEach(function(item, index, array) {});`
* 数组检索：
  * `arr.indexOf(item, from)` 从索引 `from` 开始搜索 `item`，如果找到则返回索引，否则返回 `-1`
  * `arr.includes(item)` 检索数组，有true，无false，它可以检索到 NaN
  * 详细查找 `arr.find(function(item, index, array) {  // 如果返回 true，则返回 item 并停止迭代  // 对于假值（falsy）的情况，则返回 undefined });` **只返回匹配的第一个元素**
  * `arr.finxIndex`方法（与 `arr.find` 方法）基本上是一样的，但它返回找到元素的索引，而不是元素本身。并且在未找到任何内容时返回 `-1`
  * `arr.filter` 方法与 **find** 方法用法相同，**但是返回匹配所有元素的数组**
* 转换数组：
  - `map(func)` —— 根据对每个元素调用 `func` 的结果创建一个新数组
  - `sort(func)` —— 对数组进行原位（in-place）排序，然后返回它
  - `reverse()` —— 原位（in-place）反转数组，然后返回它
  - `split/join` —— 将字符串转换为数组并返回
  - `reduce/reduceRight(func, initial)` —— 通过对每个元素调用 `func` 计算数组上的单个值，并在调用之间传递中间结果

### Map和Set

`Map` 是一个带键的数据项的集合，就像一个 `Object` 一样。 但是它们最大的差别是 `Map` 允许任何类型的键

* Map 基础方法：
  * `new Map()` —— 创建 map
  * `map.set(key, value)` —— 根据键存储值
  * `map.get(key)` —— 根据键来返回值，如果 `map` 中不存在对应的 `key`，则返回 `undefined`
  * `map.has(key)` —— 如果 `key` 存在则返回 `true`，否则返回 `false`
  * `map.delete(key)` —— 删除指定键的值
  * `map.clear()` —— 清空 map
  * `map.size` —— 返回当前元素个数
* Map 迭代：
  * `map.keys()` —— 遍历并返回所有的键（returns an iterable for keys )
  * `map.values()` —— 遍历并返回所有的值（returns an iterable for values）
  * `map.entries()` —— 遍历并返回所有的实体（returns an iterable for entries）`[key, value]`，`for..of` 在默认情况下使用的就是这个



`Set` 是一个特殊的类型集合 —— “值的集合”（没有键），它的每一个值只能出现一次

* Set 基础方法：
  * `new Set(iterable)` —— 创建一个 `set`，如果提供了一个 `iterable` 对象（通常是数组），将会从数组里面复制值到 `set` 中。
  * `set.add(value)` —— 添加一个值，返回 set 本身
  * `set.delete(value)` —— 删除值，如果 `value` 在这个方法调用的时候存在则返回 `true` ，否则返回 `false`。
  * `set.has(value)` —— 如果 `value` 在 set 中，返回 `true`，否则返回 `false`。
  * `set.clear()` —— 清空 set。
  * `set.size` —— 返回元素个数。

### 对象

* 可以使用计算属性，即属性名 fruit 从用户输入中获取，也可以直接使用变量作为属性名

```js
let fruit = prompt("Which fruit to buy?", "apple");
let bag = {[fruit]: 5}
```

* 使用 `for...in` 循环可以遍历所有的 `key`

* 使用 `Object.assign()` 进行浅拷贝

```js
let user = {
  name: "John",
  age: 30
};
let clone = Object.assign({}, user);
```

* `Object.keys()` `Object.values()` `Object.entries()` 返回键、值、键值对，如果处理的是对象，则返回数组，如果是 Map，则返回一个可迭代对象

## 装饰器

装饰器可以用于缓存函数返回的固定结果

假设我们有一个 CPU 重负载的函数 `slow(x)`，但它的结果是稳定的。换句话说，对于相同的 `x`，它总是返回相同的结果。

如果经常调用该函数，我们可能希望将结果缓存（记住）下来，以避免在重新计算上花费额外的时间。

```js
function slow(x) {
  alert(`Called with ${x}`);
  return x;
}

function cachingDecorator(func) {
  let cache = new Map();

  return function(x) {
    if (cache.has(x)) {    // 如果缓存中有对应的结果
      return cache.get(x); // 从缓存中读取结果
    }

    let result = func(x);  // 否则就调用 func

    cache.set(x, result);  // 然后将结果缓存（记住）下来
    return result;
  };
}

slow = cachingDecorator(slow);

alert( slow(1) ); // slow(1) 被缓存下来了
alert( "Again: " + slow(1) ); // 一样的

alert( slow(2) ); // slow(2) 被缓存下来了
alert( "Again: " + slow(2) ); // 和前面一行结果相同
```

`cachingDecorator` 就是一个装饰器

如果想要将装饰器用于**对象方法**，那么就要通过 `call` 设定上下文 

```js
let worker = {
  slow(min, max) {
    alert(`Called with ${min},${max}`);
    return min + max;
  }
};

function cachingDecorator(func, hash) {
  let cache = new Map();
  return function() {
    let key = hash(arguments); // (*)
    if (cache.has(key)) {
      return cache.get(key);
    }

    let result = func.call(this, ...arguments); // (**)

    cache.set(key, result);
    return result;
  };
}

function hash(args) {
  return args[0] + ',' + args[1];
}

worker.slow = cachingDecorator(worker.slow, hash);

alert( worker.slow(3, 5) ); // works
alert( "Again " + worker.slow(3, 5) ); // same (cached)
```



## 对象属性配置

### 属性标志

平时设置对象属性的时候都是一个个键值对，我们可以把 value 看作对象属性，除 **`value`** 外，还有三个特殊的特性（attributes），也就是所谓的“标志”：

- **`writable`** — 如果为 `true`，则值可以被修改，否则它是只可读的。
- **`enumerable`** — 如果为 `true`，则会被在循环中列出，否则不会被列出。
- **`configurable`** — 如果为 `true`，则此特性可以被删除，这些属性也可以被修改，否则不可以。

通过 `Object.getOwnPropertyDescriptor` 来查询属性完整信息。

```js
let user = {
  name: "John"
};

let descriptor = Object.getOwnPropertyDescriptor(user, 'name');

alert( JSON.stringify(descriptor, null, 2 ) );
/* 属性描述符：
{
  "value": "John",
  "writable": true, // 控制是否只读
  "enumerable": true, // 控制是否可枚举
  "configurable": true // 控制是否可配置
}
*/
```

通过 `Object.defineProperties` 来定义多个属性：

```js
Object.defineProperties(user, {
  name: { value: "John", writable: false },
  surname: { value: "Smith", writable: false },
  // ...
});
```

### getter 和 setter

对象属性分两种，一种是 **数据属性**，上述的所有属性都属于数据属性，另一种是 **访问器属性**，是用于获取和设置值的函数。

通过 `get` 和 `set` 来决定访问和修改属性时的动作

```js
let user = {
  name: "John",
  surname: "Smith",

  get fullName() {
    return `${this.name} ${this.surname}`;
  },

  set fullName(value) {
    [this.name, this.surname] = value.split(" ");
  }
};

// set fullName 将以给定值执行
user.fullName = "Alice Cooper";

alert(user.name); // Alice
alert(user.surname); // Cooper
```

对于访问器属性，没有 `value` 和 `writable`，但是有 `get` 和 `set` 函数。

所以访问器描述符可能有：

- **`get`** —— 一个没有参数的函数，在读取属性时工作，
- **`set`** —— 带有一个参数的函数，当属性被设置时调用，
- **`enumerable`** —— 与数据属性的相同，
- **`configurable`** —— 与数据属性的相同。

```js
let user = {
  name: "John",
  surname: "Smith"
};

Object.defineProperty(user, 'fullName', {
  get() {
    return `${this.name} ${this.surname}`;
  },

  set(value) {
    [this.name, this.surname] = value.split(" ");
  }
});

alert(user.fullName); // John Smith

for(let key in user) alert(key); // name, surname
```

## 原型和继承

参考文章 https://zhuanlan.zhihu.com/p/23090041

### 原型继承

<strong style="color:red;">注意：`__proto__`是对于对象来说的，`prototype` 是对于（构造）函数来说的，他们都指向了构造函数的prototype对象</strong>

对象有一个隐藏属性 `[[Prototype]]`，它指向了该对象的原型，当我们从 `object` 中读取一个缺失的属性时，JavaScript 会自动从原型中获取该属性。

通过 `__Proto__` 来设定原型

```js
let animal = {
  eats: true,
  walk() {
    alert("Animal walk");
  }
};

let rabbit = {
  jumps: true,
  __proto__: animal
};

let longEar = {
  earLength: 10,
  __proto__: rabbit
};

// walk 是通过原型链获得的
longEar.walk(); // Animal walk
alert(longEar.jumps); // true（从 rabbit）
```

**注意：**

* `__Proto__` 是 `[[Prototype]]` 的 getter 和 setter
* `for..in` 循环在其自身和继承的属性上进行迭代。所有其他的键/值获取方法仅对对象本身起作用。

### 新的继承方法

传统的 `__proto__` 只能在浏览器环境运行，现代的方法有：

- [Object.create(proto, [descriptors])](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/create) —— 利用给定的 `proto` 作为 `[[Prototype]]` 和可选的属性描述来创建一个空对象。
- [Object.getPrototypeOf(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/getPrototypeOf) —— 返回对象 `obj` 的 `[[Prototype]]`。
- [Object.setPrototypeOf(obj, proto)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/setPrototypeOf) —— 将对象 `obj` 的 `[[Prototype]]` 设置为 `proto`。

create 第二个参数属性描述器，可以为新对象提供额外的属性

```js
let animal = {
  eats: true
};

let rabbit = Object.create(animal, {
  jumps: {
    value: true
  }
});

alert(rabbit.jumps); // true
```

### F.prototype

如果需要通过构造函数来创建新对象，那么 new 操作符会使用它为新对象设置 `[[prototype]]`

我们可以通过对构造函数设置其 `prototype` 属性

```js
let animal = {
  eats: true
};

function Rabbit(name) {
  this.name = name;
}

Rabbit.prototype = animal;

let rabbit = new Rabbit("White Rabbit"); //  rabbit.__proto__ == animal

alert( rabbit.eats ); // true
```

设置 `Rabbit.prototype = animal` 的字面意思是：当创建了一个 `new Rabbit` 时，把它的 `[[Prototype]]` 赋值为 `animal`

![image-20220113103911559](media/image-20220113103911559.png) 

每个函数都有 `prototype` 属性，默认的 `prototype` 是一个只有属性 `constructor` 的对象，并且 `constructor` 属性可以通过 `[[Prototype]]` 给所有 rabbits 使用，还可以使用 `constructor` 属性来创建一个新对象，该对象使用与现有对象相同的构造器：

```js
function Rabbit(name) {
  this.name = name;
  alert(name);
}

let rabbit = new Rabbit("White Rabbit");

let rabbit2 = new rabbit.constructor("Black Rabbit");
```

![image-20220113104245868](JavaScript.assets/image-20220113104245868.png) 

## 类

最基本的 class 跳过

### 类继承

创建一个继承自 `Animal` 的 `class Rabbit`：

```js
class Rabbit extends Animal {
  hide() {
    alert(`${this.name} hides!`);
  }
}

let rabbit = new Rabbit("White Rabbit");

rabbit.run(5); // White Rabbit runs with speed 5.
rabbit.hide(); // White Rabbit hides!
```

在内部，关键字 `extends` 使用了很好的旧的原型机制进行工作。它将 `Rabbit.prototype.[[Prototype]]` 设置为 `Animal.prototype`。所以，如果在 `Rabbit.prototype` 中找不到一个方法，JavaScript 就会从 `Animal.prototype` 中获取该方法。

![image-20220113153120309](JavaScript.assets/image-20220113153120309.png) 

#### 重写方法

假如在父类中已经有一个方法，我们想要在子类中进行扩展，笨办法是对该方法进行重写，但是Class 为此提供了 `"super"` 关键字：

- 执行 `super.method(...)` 来调用一个父类方法。
- 执行 `super(...)` 来调用一个父类 constructor（只能在我们的 constructor 中）。

```js
class Animal {
  constructor(name) {
    this.speed = 0;
    this.name = name;
  }

  run(speed) {
    this.speed = speed;
    alert(`${this.name} runs with speed ${this.speed}.`);
  }

  stop() {
    this.speed = 0;
    alert(`${this.name} stands still.`);
  }

}

class Rabbit extends Animal {
  hide() {
    alert(`${this.name} hides!`);
  }

  stop() {
    super.stop(); // 调用父类的 stop
    this.hide(); // 然后 hide
  }
}

let rabbit = new Rabbit("White Rabbit");

rabbit.run(5); // White Rabbit 以速度 5 奔跑
rabbit.stop(); // White Rabbit 停止了。White rabbit hide 了！
```

#### 重写 constructor

一个子类想要写自己的 constructor，必须要使用 super

**继承类的 constructor 必须调用 `super(...)`，并且一定要在使用 `this` 之前调用。**

```js
class Animal {

  constructor(name) {
    this.speed = 0;
    this.name = name;
  }

  // ...
}

class Rabbit extends Animal {

  constructor(name, earLength) {
    super(name);
    this.earLength = earLength;
  }

  // ...
}

// 现在可以了
let rabbit = new Rabbit("White Rabbit", 10);
alert(rabbit.name); // White Rabbit
alert(rabbit.earLength); // 10
```





### 静态属性和静态方法

可以把一个方法赋值给类的函数本身，而不是赋给它的 `"prototype"`

```js
class User {
  static staticMethod() {
    alert(this === User);
  }
}

User.staticMethod(); // true
```

且静态属性和静态方法可以通过原型链继承
