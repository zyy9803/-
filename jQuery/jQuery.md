# jQuery

## 入口函数

![image-20210328215802961](jQuery.assets/image-20210328215802961.png)

## 顶级对象

* $ 是 jquery的别称，在代码中可以使用 jquery代替$,但一般为了方便，通常都直接使用$
* $ 是jquery的顶级对象，相当于原生 Javascript中的 window。把元素利用$包装成 Query对象，就可以调用
  jquery的方法

### jQuery对象和DOM对象

1. 用原生JS获取的对象是DOM对象，用jQuery获取的对象是jQuery对象
2. jQuery对象本质是：利用$对DOM对象包装后产生的对象（伪数组形式存储）
3. jQuery对象只能用jQuery方法，DOM对象则使用原生的JavaScript属性和方法

```javascript
myDiv.style.display = 'none';
myDiv.hide(); //myDiv是一个dom对象不能使用 jquery里面的hide方法
$('div').style.display = 'none'; //这个$('div')是一个jQuery对象不能使用原生js 的属性和方法
```

#### 互相转换

![image-20210327220600512](jQuery.assets/image-20210327220600512.png)

```javascript
//jQuery转换成DOM对象
$('video')[0].play()
$('video').get(0).play()
```

## 常用API

### 选择器

![image-20210327220727641](jQuery.assets/image-20210327220727641.png)

#### 隐式迭代

<strong style="color:red;">遍历内部DOM元素（伪数组形式存储）的过程就叫做隐式迭代</strong>。
简单理解：给匹配到的所有元素进行循环遍历，执行相应的方法，而不用我们再进行循环，简化我们的操作，方便我们调用

#### 筛选选择器

<strong style="color:red;">注意选第n个孩子是用:eq(n-1)，不是用[n-1]，注意！</strong>![image-20210327221045011](jQuery.assets/image-20210327221045011.png)

#### 筛选方法

![image-20210327221436719](jQuery.assets/image-20210327221436719.png)

parents()可以返回指定的祖先元素

#### 链式编程

```js
$(this).css("color", "red").siblings().css("color", "");
```

### 样式操作

![image-20210327223738299](jQuery.assets/image-20210327223738299.png)

#### 类操作

![image-20210327223933967](jQuery.assets/image-20210327223933967.png)

### 效果

![image-20210327224905981](jQuery.assets/image-20210327224905981.png)

#### 显示隐藏

![image-20210327224937472](jQuery.assets/image-20210327224937472.png)

#### 滑动

![image-20210327225314187](jQuery.assets/image-20210327225314187.png)

#### 事件切换

![image-20210327225528991](jQuery.assets/image-20210327225528991.png)

如果只写一个，那么鼠标经过和离开都会触发

#### 停止动画排队

![image-20210327225809159](jQuery.assets/image-20210327225809159.png)

<strong style="color:red;">stop()必须写到动画的前面</strong>

#### 淡入淡出

![image-20210327225930995](jQuery.assets/image-20210327225930995.png)

![image-20210327230026110](jQuery.assets/image-20210327230026110.png)

#### 自定义动画

![image-20210327230108935](jQuery.assets/image-20210327230108935.png)

### 属性操作

#### 获取固有属性

![image-20210328212521462](jQuery.assets/image-20210328212521462.png)

#### 获取自定义属性

通过attr()

![image-20210328212756031](jQuery.assets/image-20210328212756031.png)

#### 数据缓存

不会修改DOM元素结构

![image-20210328212941832](jQuery.assets/image-20210328212941832.png)

### 内容文本值

#### ![image-20210328221936816](jQuery.assets/image-20210328221936816.png)

![image-20210328222003160](jQuery.assets/image-20210328222003160.png)

### 元素操作

#### 遍历元素

**遍历DOM**

![image-20210328224212376](jQuery.assets/image-20210328224212376.png)

<strong style="color:red;">一定注意domEle是DOM对象</strong>

**遍历数据**

![image-20210328224706150](jQuery.assets/image-20210328224706150.png)

#### 创建元素

![image-20210328225028177](jQuery.assets/image-20210328225028177.png)

##### 内部添加

父子关系

![image-20210328225207003](jQuery.assets/image-20210328225207003.png)

element.preappend(“内容”) //添加到内部前面

##### 外部添加

兄弟关系

![image-20210328225255294](jQuery.assets/image-20210328225255294.png)

#### 删除元素

![image-20210328225346177](jQuery.assets/image-20210328225346177.png)

### 尺寸位置操作

#### 尺寸方法

![image-20210328225542370](jQuery.assets/image-20210328225542370.png)

#### 位置方法

##### offset相对文档

![image-20210328225813041](jQuery.assets/image-20210328225813041.png)

##### position相对父级

![image-20210328225918440](jQuery.assets/image-20210328225918440.png)

<strong style="color:red;">此方法只能获取，不能设置偏移</strong>

##### scrollTop被卷去

![image-20210328230110241](jQuery.assets/image-20210328230110241.png)

scrollLeft()被卷去左边

## 事件

### 事件注册

![image-20210330125642307](jQuery.assets/image-20210330125642307.png)

### 事件处理

#### 事件绑定

![image-20210330125727654](jQuery.assets/image-20210330125727654.png)

```js
$("div").on({
                mouseenter: function() {
                    $(this).css("background", "skyblue");
                },
                click: function() {
                    $(this).css("background", "purple");
                },
                mouseleave: function() {
                    $(this).css("background", "blue");
                }
            });
```

#### 事件委派

把原来子元素身上的事件绑定在父元素身上

绑定在ul上，但触发对象是li

![image-20210330130036831](jQuery.assets/image-20210330130036831.png)

#### 动态创建元素绑定事件

<strong style="color:red;">动态创建的元素， click()没有办法绑定事件，on()可以给动态生成的元素邦定事件，通过事件委派</strong>

#### 事件解绑

![image-20210330132805422](jQuery.assets/image-20210330132805422.png)

<strong style="color:red;">one()事件可以只触发一次</strong>

#### 自动触发事件

![image-20210330133025930](jQuery.assets/image-20210330133025930.png)

![image-20210330133040893](jQuery.assets/image-20210330133040893.png)

<strong style="color:red;">第三种不会触发元素的默认行为</strong>

### 事件对象

![image-20210330141306525](jQuery.assets/image-20210330141306525.png)

## 其他方法

### 对象拷贝

![image-20210330141503454](jQuery.assets/image-20210330141503454.png)

### 多库共存

![image-20210330141903100](jQuery.assets/image-20210330141903100.png)

## 插件

![image-20210330141954971](jQuery.assets/image-20210330141954971.png)

[jQuery插件库](http://www.jq22.com/)

[jQuery之家](http://www.htmleaf.com/)





# 源码解析

















