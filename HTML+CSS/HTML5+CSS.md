HTML5+CSS



# HTML5+CSS3基础

## 元素显示方式

### 块级元素

`<h1>, <p>, <div>, <ul>, <ol>, <li> `

1. 独占一行。
2. 高度，宽度、外边距以及内边距都可以控制。
3. 宽度默认是容器（父级宽度）的100%。
4. 是一个容器及盒子，里面可以放行内或者块级元素

注意：文字类元素p,h1等里面不能放块级元素

### 行内元素

`<a>、<strong>、<b>、<em>、<del>、<s>、<ins>、<u>、<span>`

其中 <span>标签是最典型的行内元素。有的地方也将行内元素称为内联元素。

 行内元素的特点：

1. 相邻行内元素在一行上，一行可以显示多个。
2. 高、宽直接设置是无效的。
3. <strong style="color:red;">默认宽度就是它本身内容的宽度。</strong>
4. 行内元素只能容纳文本或其他行内元素。

注意：<a>里可以放块级元素，但是给它转换一下块级模式最安全

### 行内块元素

`<img>, <input>, <td>`

它们同时具有块元素和行内元素的特点。有些资料称它们为行内块元素。

行内块元素的特点：

1. 和相邻行内元素（行内块）在一行上，但是<strong style="color:red;">他们之间会有空白缝隙</strong>。
2. 一行可以显示多个（行内元素特点）。
3. <strong style="color:red;">默认宽度就是它本身内容的宽度度（行内元素特点）。</strong>
4. 高度，行高、外边距以及内边距都可以控制（块级元素特点）。



## CSS属性

### 字体属性

* font-family 设置字体
  * `font-family: 'Microsoft Yahei'`

* font-size 字号大小
  * `font-size: 16px`
* font-weight 字体粗细
  * `font-weight: bold` 可以选择 normal、bold、lighter 或者使用 100、700、800 等数字
* font-style 字体风格
  * `font-style: italic` italic 是斜体
* 复合写法：
  * `font: font-style font-weight font-size/line-height font-family`

### 文本属性

* color 颜色
* text-align 文本<strong style="color:red;">水平对齐</strong>
  * `text-align: center` 水平居中对齐，还有 left、right 参数
* text-decoration 装饰文本
  * `text-decoration: none` 没有装饰线
  * underline 下划线
  * line-through 删除线
  * overline 上划线
* text-indent 文本缩进
  * `text-indent: 10px` 首行缩进 10px
  * `text-indent: 2em` 首行缩进 2 字符
* line-height 行间距
  * `line-height: 26px` 上 + 文本高度 + 下 = 26px
  * ![image-20211015201839571](HTML5+CSS.assets/image-20211015201839571.png)

### 选择器

* 后代选择器：中间用空格隔开
  * `元素1 元素2 { 样式 }`

* 子元素选择器：只选择儿子元素
  * `元素1 > 元素2 { 样式 }`

* 并集选择器：用逗号分隔
  * `元素1, 元素2 { 样式 }`
* 伪类选择器
  * `a:link {}` 未被访问
  * `a:visited {}` 已访问
  * `a:hover {}` 悬停
  * `a:active {}` 活动链接
* focus 伪类选择器：选取获得光标的表单元素
  * `input:focus {}`

### 背景

* 背景颜色 background-color
* 背景图片 background-image
  * `background-image: url()`
* 背景平铺 backgroud-repeat
  * `backgroud-repeat: no-repeat`
  * `backgroud-repeat: repeat`
  * `backgroud-repeat: repeat-x`
  * `backgroud-repeat: repeat-y`
* 背景图片位置 background-position
  * 方位名词 `background-position:center top` 水平居中靠上
  * 精确单位 `background-position:20px 50px` X-20px Y-50px 
  * 混合写法 `background-position:center 50px` 水平居中 距离顶部50px
* 背景图像固定 background-attachment
  * `background-attachment: scroll` 滚动
  * `background-attachment: fixed` 固定
* 复合写法
  * `bakcground: 颜色 地址 平铺 滚动 位置`

### 圆角边框

* `border-radius: 10px` 圆角边框半径10px

### 阴影

盒子阴影

* `box-shadow: h-shadow v-shadow 模糊距离 阴影尺寸 颜色 内外阴影` 水平阴影的位置
* `box-shadow: 10px 10px 10px 10px black `  默认外阴影，内阴影为 inset 

文字阴影

* `text-shadow: h-shadow v-shadow blur color `



## CSS三大特性

### 层叠性

1. 样式冲突，遵循最后的样式
2. 不冲突不会重叠

### 继承性

1. 子标签会继承父标签的<strong style="color:red;">某些</strong>样式，比如text-, font-, line- 这些开头的，以及color属性

### 优先级

![image-20210310113033902](HTML5+CSS.assets\image-20210310113033902.png)



## 盒子模型

![image-20210310162821093](HTML5+CSS.assets\image-20210310162821093.png)

<strong style="color:red;">盒子指定的宽高是内容的宽高</strong>

### Border

* `border-width：边框粗细`

* `border-style：边框样式`（<strong style="color:red;">四个参数：上-右-下-左；三个参数：上、左-右、下；两个参数：上-下、左-右</strong>）

* `border-color：边框颜色`

* `复合写法：border: 1px solid red`

* `border-collapse: collapse`  用于合并表格中相邻单元格的边框

### Padding

padding是边框与内容之间的距离

* `padding: 5px` 上下左右
* `padding: 5px 10px` 上下   左右
* `padding: 5px 10px 20px` 上   左右  下
* `padding: 5px 10px 20px 30px` 上 下 左 右

<strong style="color:red;">padding会影响盒子的实际大小，比如盒子是200×200的，padding指定了20，那么盒子被撑大到240×240</strong>

解决方法：

* 计算盒子高度和宽度减去 padding 值
* 使用怪异盒子模型 `box-sizing: border-box`     

padding不会撑开盒子的情况：盒子本身没有指定宽度/高度，padding不会撑开盒子；

### Margin

用于<strong style="color:red;">块级盒子水平居中</strong>，但是必须满足两个条件：

1. 盒子必须指定了宽度；
2. `margin: 0 auto;`

<strong style="color:red;">行内元素或行内块元素水平居中</strong>给其父元素添加：text-align: center

<strong style="color:red;">塌陷问题</strong>：对于两个嵌套关系（父子关系）的块元素，父元素有上外边距同时子元素也有上外边距，此时父元素会塌陷较大的外边距值。<strong style="color:red;">注意浮动的盒子不会有外边距塌陷的问题！</strong>

解决方案：

1. 父元素定义上边框 `border: 1px solid transparent`
2. 父元素定义上内边距
3. 为父元素添加 `overflow: hidden`

<img src="HTML5+CSS.assets\image-20210310194233964.png" alt="image-20210310194233964" style="zoom:50%;" />

### 清除内外边距

```css
* {
    margin: 0;
    padding: 0;
}
CSS第一行代码
```











## 网页布局方式

网页布局分为三种：标准流（普通流、文档流）、 浮动、定位



### 浮动

浮动最典型的应用：可以让多个块级元素一行内排列显示。

网页布局第一准则：**多个块级元素纵向排列找标准流，多个块级元素横向排列找浮动**

float属性用于创建浮动框，将其移动到一边，直到左边缘或右边绿角触及包含块或另一个浮动框的边绿。

```css
选择器 { float: 属性值 } none 不浮动  left 左  right 右
```

#### 浮动特性

1. 浮动元素会脱离标准流（**脱标**）：脱离标准普通流的控制（浮）移动到指定位置（动）（俗称脱标），浮动的盒子**不再保留原先的位置**

2. 浮动的元素会一行内显示并且元素**顶部对齐**

3. 浮动的元素会具有**行内块元素**的特性

常规的做法是**用标准流嵌套浮动**

#### 常见网页布局

![image-20210305215310685](HTML5+CSS.assets\image-20210305215310685.png)

#### 浮动布局注意点

1. 浮动和标准流的父盒子搭配
2. 一个元素，其余兄弟元素也要浮动
3. 浮动的盒子只会影响后面的标准流，不会影响前面的标准流

![image-20210305220725755](HTML5+CSS.assets\image-20210305220725755.png)

#### 清除浮动

父盒子不方便给高度，但是子盒子又不占有位置，导致父盒子高度变为0，影响下面标准流，因此需要清除浮动

![image-20210306160647968](HTML5+CSS.assets\image-20210306160647968.png)

```css
clear:both 清除左右浮动
```

![image-20210306160618417](HTML5+CSS.assets\image-20210306160618417.png)

清除浮动的策略：<strong style="color:red;">闭合浮动</strong>

目前有四种方法：

1. 额外标签法也称为隔墙去，是W3C推荐的做法，在子盒子后面添加一个空标签，必须是块级元素clear:both
2. 父级添加 overflow属性
3. 父级添加 after伪元素

```css
        .clearfix:after {
            content: "";
            display: block;
            height: 0;
            clear: both;
            visibility: hidden;
        }

        .clearfix {
            /* IE6、7 专有 */
            *zoom: 1;
        }
```

4. 父级添加双伪元素

```css
 		.clearfix:before,
        .clearfix:after {
            content: "";
            display: table;
        }

        .clearfix:after {
            clear: both;
        }

        .clearfix {
            *zoom: 1;
        }
```







### 案例

CSS书写顺序：

1. 布局定位属性：display/ position/foat/ clear/ visibility/ overflow(建议display第一个写，毕竟关系到模式)

2. 自身属性：width/ height/ margin/ padding/ border/ background

3. 文本属性：color/ font/ text-decoration/ text-align/ vertical-align/ white-space/ break-word
4. 其他属性：content/cursor/border-radius/shadow/text-shadow/background



页面布局整体思路：

1. 必须确定页面的版心（可视区），我们测量可得知
2. 分析页面中的行模块，以及每个行模块中的列模块，页面布局第一准则
3. 一行中的列模块经常浮动布局先确定每个列的大小之后确定列的位置，页面布局第二准则
4. 制作HTML结构。遵循先有结构，后有样式的原则，结构永远最重要！



导航栏：

1. 导航栏实际制作中，不用链接a而是用li包含链接(li+a)的做法，一是因为语义清晰，二是用a搜索引擎会辨别为有堆砌关键字嫌疑，影响网站排名
2. 导航栏nav可以不给宽度，行内块元素由内容自动撑大盒子
3. 因为导航栏里面文字不一样多所以最好给链接a左右padding撑开盒子，而不是指定宽度

搜索框：

1. 注意padding会撑大盒子
2. 搜索框和button都是行内块元素，之间会有间隙，因此二者都要加浮动
3. button默认边框需要手动去掉

注意行内元素a要指定高度，需要进行block转换

links部分用dl和dd标签来做



### 定位

1. 浮动可以让多个块级盒子一行没有层叠排列显示，经常用于横向排列盒子
2. 定位则是可以让盒子自由的在某个盒子内移动位置或者固定屏幕中某个位置，并且可以压住其他盒子。

定位：将盒子定在某个位置，所以定位也是在撰放盒子，按照定位的方式移动盒子

定位=定位模式+边偏移

<strong style="color:red;">定位模式</strong>用于指定一个元素在文档中的定位方式。<strong style="color:red;">边偏移</strong>则決定了该元素的最终位置

#### 定位模式

![image-20210312214727156](HTML5+CSS.assets\image-20210312214727156.png)

##### 静态定位

静态定位是元素的默认定位方式，无定位的意思

##### 相对定位

相对定位是元素在移动位置的时候，相对于它原来的位置来说的

<strong style="color:red;">相对定位的特点</strong>：

- 它是相对于自己原来的位置来移动的（移动位置的时候参照点是自己原来的位置）。

- <strong style="color:red;">原来在标准流的位置继续占有，后面的盒子仍然以标准流的方式对待它。(不脱标，继续保留原来位置)</strong>

##### 绝对定位

绝对定位是元素在移动位置的时候，相对于它父元素来说的

<strong style="color:red;">绝对定位的特点</strong>：

1. 如果没有祖先元素或者祖先元素没有定位，则以浏览器为准定位( Document文档)。
2. 如果祖先元素有定位(相对、绝对、固定定位)，则<strong style="color:red;">以最近一级的有定位祖先元素</strong>为参考点移动位置
3. <strong style="color:red;">绝对定位不再占有原先的位置（脱标）</strong>

###### 子绝父相

弄清楚这个口诀，就明白了绝对定位和相对定位的使用场景

这个“子绝父相”太重要了，是我们学习定位的口诀，是定位中最常用的一种方式这句话的意思是：子级是绝对定位的话，父级要用相对定位。

1. 子级绝对定位，不会占有位置，可以放到父盒子里面的任何一个地方，不会影响其他的兄弟盒子
2. 父盒子需要加定位限制子盒子在父盒子内显示
3. 父盒子布局时，需要占有位置，因此父亲只能是相对定位

这就是子绝父相的由来，所以相对定位经常用来作为绝对定位的父级

总结：因为父级需要占有位置，因此是相对定位，子盒子不需要占有位置，则是绝对定位

##### 固定定位

固定定位是元素<strong style="color:red;">固定于浏览器可视区的位置</strong>。主要使用场景：可以在浏览器页面滚动时元素的<strong style="color:red;">位置不会改变</strong>。

固定定位的特点：（务必记住）

1. 以浏览器的可视窗口为参照点移动元素， 跟父元素没有任何关系
2. <strong style="color:red;">不随滚动条滚动</strong>
3. 固定定位不在占有原先的位置
4. 固定定位也是脱标的，其实固定定位也可以看做是一种特殊的绝对定位。

##### 粘性定位

粘性定位可以被认为是相对定位和固定定位的混合

```css
选择器{ position: sticky;top:10px;}
```

 粘性定位的特点

1. 以浏测览器的可视窗口为参照点移动元素（固定定位特点）
2. 粘性定位占有原先的位置（相对定位特点）
3. 必须添加top、left、 right、 bottom其中一个才有效

#### 定位叠放次序 z-index

在使用定位布局时，可能会出现盒子重叠的情况。此时，可以使用z- index来控制盒子的前后次序(z轴)

```css
选择器 {z-index:1;}
```

* 数值可以是正整数、负整数或0,默认是auto,数值越大，盒子越靠上

* 如果属性值相同，则按照书写顺字，后来居上

* 数字后面不能加单位

* <strong style="color:red;">只有定位的盒子才有z- index属性</strong>

#### 定位的拓展

##### 绝对定位水平垂直居中

使用绝对定位不能通过margin: 0 auto 水平居中，因此

```css
{
    left: 50%;
    margin-left: -50%;
    top: 50%;
    margin-top: -50%;
}
```

##### 定位的特殊性

1. 行内元素添加绝对或者固定定位，可以直接设置高度和宽度
2. 块级元素添加绝对或者固定定位，如果不给宽度或者高度，默认大小是内容的大小
3. 脱标的盒子不会触发外边距合并问题
4. 浮动元素不同，只会压住它下面标准流的盒子，但是不会压住下面标准流盒子里面的文字（图片）；绝对定位（固定定位）会压住下面标准流所有的内容。

#### 案例

* 对于相同的的样式，用并集选择器简化代码

#### 元素的显示与隐藏

```css
{display: none} //隐藏
{display: block} //显示
```

<strong style="color:red;">使用display: none以后，元素不再占据标准流</strong>

```css
{visibility: visible} //隐藏
{visibility: hidden} //显示
```

<strong style="color:red;">使用visibility: visible以后，元素仍然占据标准流</strong>

```css
{overflow: visible|auto|hidden|scroll}
```

visible：默认

auto：溢出时显示滚动条，不溢出不显示

scroll：溢出的部分显示滚动条，不溢出也显示

## CSS高级技巧

### 精灵图

为了有效地減少服务器收和发送请求的次数，提高页面的加载速度

使用精灵图核心：

1. 精灵技术主要针对于背景图片使用。就是把多个小肖景图片整合到一张大图片中
2. 这个大图片也称为 sprites精灵图或者雪碧图
3. 移动背景图片位置，此时可以使用 background- position
4. 移动的距离就是这个目标图片的x和y坐标。注意网页中的标有所不同
5. 因为一般情況下都是往上往左移动，所以数值是负值
6. 使用精灵图的时候需要精确则量，每个小背景图片的大小和位置

```css
    .box1 {
      width: 60px;
      height: 60px;
      background: url(images/sprites.png);
      margin: 100px auto;
      background-position: -182px 0;
    }
```

### 字体图标

字体图标使用场景：主要用于显示网页中通用、常用的一些小图标。精灵图是有诸多优点的，但是缺点很明显。

此时，有一种技术的出现很好的解決了以上问题，就是字体图标 confront

字体图标可以为前端工程师提供一种方便高效的图标使用方式，展示的是图标，本质属于字体

[下载字体图标](http://icomoon.io)

引入：

1. 把下载包里面的 fonts文件夹放入页面根目录下

2. 在CSS样式中全局声明字体：简单理解把这些字体文件通过css引入到我们页面中。
    一定注意字体文件路径的问题

![image-20210316213603061](HTML5+CSS.assets\image-20210316213603061.png)

3. html标签内添加小图标

![image-20210316213704148](HTML5+CSS.assets\image-20210316213704148.png)

4. ```css
   span {
       font-family: "icomoon";
   }
   ```

### CSS三角

原理：无宽高的盒子，一个border有颜色，其余透明

![image-20210316214115713](HTML5+CSS.assets\image-20210316214115713.png)

### CSS用户界面样式

#### 鼠标样式

![image-20210316214426586](HTML5+CSS.assets\image-20210316214426586.png)

#### 表单轮廓线

鼠标定位在某输入框时出现的轮廓线

![image-20210316214624647](HTML5+CSS.assets\image-20210316214624647.png)

#### 防止拖拽文本域

![image-20210316214732287](HTML5+CSS.assets\image-20210316214732287.png)

#### vertical-align属性应用(图片文字垂直居中对齐)

图片居中对齐

图片垂直居中

![image-20210316215218156](HTML5+CSS.assets\image-20210316215218156.png)

![image-20210316215257579](HTML5+CSS.assets\image-20210316215257579.png)

![image-20210316215647882](HTML5+CSS.assets\image-20210316215647882.png)

<img src="HTML5+CSS.assets\image-20210316215625072.png" alt="image-20210316215625072" style="zoom:50%;" />

#### 文字溢出省略号显示

<img src="HTML5+CSS.assets\image-20210316215810756.png" alt="image-20210316215810756" style="zoom:50%;" />

![image-20210316215851113](HTML5+CSS.assets\image-20210316215851113.png)

nowrap强制一行显示

![image-20210316220038667](HTML5+CSS.assets\image-20210316220038667.png)

### 常见布局技巧

#### margin负值运用

让边框避免重合变粗

![image-20210317215350244](HTML5+CSS.assets/image-20210317215350244.png)

![image-20210317215402581](HTML5+CSS.assets/image-20210317215402581.png)

#### 文字围绕浮动元素

利用浮动的特性，给图片添加浮动

![image-20210317220506713](HTML5+CSS.assets/image-20210317220506713.png)

#### 行内块元素写换页栏

给行内块元素的父元素添加text-align: center，子元素都会水平居中对齐

![image-20210317220856909](HTML5+CSS.assets/image-20210317220856909.png)

### CSS初始化

[CSS初始化](https://www.bilibili.com/video/BV14J4114768?p=273)







# HTML5+CSS3提高

## HTML5新特性

### 新增语义化标签

<img src="HTML5+CSS.assets/image-20210318202341491.png" alt="image-20210318202341491" style="zoom:50%;" />

* 在IE9需要转换成block
* 可以使用多次
* 主要是针对搜索引擎，更多的用于移动端

### 新增多媒体标签

1. 视频：`<video>`

![image-20210318202847631](HTML5+CSS.assets/image-20210318202847631.png)

常见属性

![image-20210318203001805](HTML5+CSS.assets/image-20210318203001805.png)

2. 音频：`<audio>`

![image-20210318203248705](HTML5+CSS.assets/image-20210318203248705.png)

常见属性

![image-20210318203320286](HTML5+CSS.assets/image-20210318203320286.png)

### 新增input类型

![image-20210318203539734](HTML5+CSS.assets/image-20210318203539734.png)

### 新增表单属性

![image-20210318203802679](HTML5+CSS.assets/image-20210318203802679.png)

## CSS3新特性

### CSS3新增选择器

#### 属性选择器

![image-20210318204553232](HTML5+CSS.assets/image-20210318204553232.png)

#### 结构伪类选择器

结构伪类选择器主要根据文档结构来选择元素，常用于根据父级选择器里面的子元素

![image-20210318204711778](HTML5+CSS.assets/image-20210318204711778.png)

<strong style="color:red;">n可以是数字，关键字和公式</strong>

关键字：even偶数，odd奇数

#### 伪元素选择器

伪元素选择器可以帮助我们利用CSS创建新标签元素，而不需要HTML标签，从而简化HTML结构![image-20210318205624566](HTML5+CSS.assets/image-20210318205624566.png)

* before和after创建一个元素，该元素为行内元素

* 新创建的这个元素<strong style="color:red;">在文档树中是找不到的</strong>，所以我们称为伪元素

* 语法： element::before

* before和 after <strong style="color:red;">必须有 content属性</strong>

* 伪元素选择器和标签选择器一样，权重为1

### CSS3盒子模型

CSS3中可以通过box- sizing来指定盒模型，有2个值：即可指定为 content-box、 border-box，这样我们计算盒子大小的方式就发生了改变。

可以分成两种情况：

1. box- sizing: content-box   盒子大小为 width+ padding+ border（以前默认的）
2. box-sizing: border-box  盒子大小为 width

如果盒子模型我们改为了box- sizing: border-box，那 padding和 border就不会撑大盒子了（前提 padding和 border不会超过 width宽度）

### CSS3过渡

经常和hover配合使用

![image-20210318213242487](HTML5+CSS.assets/image-20210318213242487.png)

<strong style="color:red;">谁做过渡给谁加，如果写多个属性，用逗号分隔，所有属性就写all</strong>

![image-20210318213258905](HTML5+CSS.assets/image-20210318213258905.png)

### CSS3 2D转换

区别于定位偏移和外边距偏移的优点：<strong style="color:red;">不会影响其他盒子的位置</strong>

<strong style="color:red;">过渡效果：</strong>

```css
div img {
    transition: all 0.4s;
}
```

#### 平移

translate

2D移动是2D转换里面的一种功能，可以改变元素在页面中的位置，类似定位。

语法：

![image-20210324201030925](HTML5+CSS.assets/image-20210324201030925.png)

重点：

![image-20210324202251557](HTML5+CSS.assets/image-20210324202251557.png)

#### 旋转

rotate

![image-20210324202616882](HTML5+CSS.assets/image-20210324202616882.png)

#### 中心点

transform-origin

![image-20210324202825260](HTML5+CSS.assets/image-20210324202825260.png)

#### 缩放

scale

![image-20210324203041604](HTML5+CSS.assets/image-20210324203041604.png)

### CSS3动画

1. 先定义动画
2. 再调用动画

![image-20210324204821317](HTML5+CSS.assets/image-20210324204821317.png)

![image-20210324205031926](HTML5+CSS.assets/image-20210324205031926.png)

![image-20210324205301441](HTML5+CSS.assets/image-20210324205301441.png)

常用属性：

![image-20210324205443878](HTML5+CSS.assets/image-20210324205443878.png)

![image-20210324211000556](HTML5+CSS.assets/image-20210324211000556.png)

### CSS3 3D转换

![image-20210325202314678](HTML5+CSS.assets/image-20210325202314678.png)

![image-20210325202710822](HTML5+CSS.assets/image-20210325202710822.png)

<img src="HTML5+CSS.assets/image-20210325204645126.png" alt="image-20210325204645126" style="zoom: 50%;" />







### CSS3其他特性

* 滤镜filter属性

![image-20210318212956821](HTML5+CSS.assets/image-20210318212956821.png)

* calc函数

可以在声明CSS属性时执行一些计算

![image-20210318213102826](HTML5+CSS.assets/image-20210318213102826.png)



## 品优购项目

### 网站TDK三大标签SEO优化

![image-20210320140648087](HTML5+CSS.assets/image-20210320140648087.png)

![image-20210320140714226](HTML5+CSS.assets/image-20210320140714226.png)

![image-20210320140748400](HTML5+CSS.assets/image-20210320140748400.png)



### LOGO SEO优化

<img src="HTML5+CSS.assets/image-20210321120820673.png" alt="image-20210321120820673" style="zoom: 70%;" />



# 移动端WEB开发

## 移动端基础

### 视口

视口( viewport)就是浏览器显示页面内容的屏幕区域。<strong style="color:red;">视口可以分为布局视口、视觉视口和理想视口</strong>

![image-20210402161913692](HTML5+CSS.assets/image-20210402161913692.png)

![image-20210402161950300](HTML5+CSS.assets/image-20210402161950300.png)

![image-20210402162014026](HTML5+CSS.assets/image-20210402162014026.png)

#### meta视口标签

![image-20210402162515352](HTML5+CSS.assets/image-20210402162515352.png)

标准的viewport设置

* 视口宽度和设备保持一致

* 视口的默认缩放比例1.0

* 不允许用户自行缩放

* 最大允许的缩放比例1.0

* 最小允许的缩放比例1.0

### 二倍图

#### 物理像素&物理像素比

* 物理像素点指的是屏幕显示的最小颗粒，是物理真实存在的。这是厂商在出厂时就设置好了比如苹果678是750*1334
* <strong style="color:red;">我们开发时候的1px不是一定等于1个物理像素的</strong>
* PC端页面，1个px等于1个物理像素的，但是移动端就不尽相同
* 1px能显示的物理像素点的个数，称为物理像素比或屏幕像素比

#### 多倍图

* 对于一张50px*50px的图片，在手机 Retina屏中打开，按照刚才的物理像素比会放大倍数，这样会造成图片模糊
* 在标准的 viewport设置中，使用倍图来提高图片质量，解决在高清设备中的模糊问题
* 通常使用二倍图，因为 iphone678的影响，但是现在还存在3倍图4倍图的情兄，这个看实际开发公司需求
* 背景图片注意缩放问题

假设需要50*50的图片，放到iphone8里会放大两倍，因此我们直接放一个100×100的图片，手动把它缩小为50×50，<strong style="color:red;">我们准备的图片比我们实际需要的大小大2倍，这就方式就是2倍图</strong>

##### 背景缩放 background-size

![image-20210402164958434](HTML5+CSS.assets/image-20210402164958434.png)

### 常见布局

![image-20210402183732777](HTML5+CSS.assets/image-20210402183732777.png)

## 流式布局（百分比布局）

采用百分比来进行布局，不写死



## Flex 布局

### 原理

弹性布局

* 当为父盒子设置为 flex 布局以后，子元素的 float、clear、vertical-align 失效
* 伸缩布局 = 弹性布局 = flex 布局

采用 Flex 布局的元素，称为“容器”，它的所有**子元素**都会自动成为容器成员，称为“项目”

### 父项常见属性

* **flex-direction:设置主轴的方向**
  * row 默认从左到右
  * row-reverse 从右到左
  * column 从上到下
  * column-reverse 从下到上
* **justify-content:设置主轴上的子元素排列方式**
  * flex-start 默认值从头部开始，如果主轴是x轴，就从左到右
  * flex-end 从尾部开始
  * center 在主轴居中对齐，如果主轴是x轴，就水平居中
  * space-around 平分剩余空间
  * space-between 先两边贴边，再平分剩余空间
* **flex-wrap:设置子元素是否换行**
  * nowrap 默认不换行
  * wrap 换行
* **align-content:设置侧轴上的子元素的排列方式（多行）**
  * flex-start 默认值，在侧轴的头部开始排列
  * flex-end 在侧轴的尾部开始排列
  * center 在侧轴中间显示
  * space-around 子项在侧轴平分剩余空间
  * space-between 子项在侧轴先分布在两头，再平分剩余空间
  * stretch 设置子项元素高度平分父元素
* **align-items:设置侧轴上的子元素排列方式（单行）**
  * flex-start 从上到下
  * flex-end 从下到上
  * center （聚在一起居中）垂直居中
  * stretch 拉伸（默认值）
* **flex-flow:复合属性，相当于同时设置了flex-direction和flex-wrap**



### 子项常见属性

* **flex** 子项目占的份数
* **align-self** 控制子项目自己在侧轴的排列方式
  * 可以允许某个单个盒子按照自己的方式在侧轴排列
* **order** 属性定义子项的排列顺序（前后顺序）
  * 数值越小越靠前



# 积累

## clientWidth scrollWidth offsetWidth区别

* scrollWidth：对象的实际内容的宽度，不包边线宽度，会随对象中内容超过可视区后而变大。
* clientWidth：对象内容的可视区的宽度，不包滚动条等边线，会随对象显示大小的变化而改变。
* offsetWidth：对象整体的实际宽度，包滚动条等边线，会随对象显示大小的变化而改变。



**情况1：元素内无内容或者内容不超过可视区，滚动不出现或不可用的情况**

scrollWidth=clientWidth，两者皆为内容可视区的宽度。

offsetWidth为元素的实际宽度。

![](HTML5+CSS.assets/291654504031651.png) 

**情况2：元素的内容超过可视区，滚动条出现和可用的情况**

scrollWidth>clientWidth。

scrollWidth为实际内容的宽度。

clientWidth是内容可视区的宽度。

offsetWidth是元素的实际宽度。

![](https://images0.cnblogs.com/blog/166781/201412/291655026226285.png) 

