---
 学习目标:
  - 理解面向对象开发思想
  - 掌握 JavaScript 面向对象开发相关模式
  
typora-copy-images-to media
---

# JavaScript 高级

<img src="./media/Unofficial_JavaScript_logo_2.svg.png" width="400" alt="">

### 目标

- 理解面向对象开发思想
- 掌握 JavaScript 面向对象开发相关模式

  

### 案例演示

- [贪吃蛇](snake/index.html)

---

## 回顾

> 由于 JavaScript 高级还是针对 JavaScript 语言本身的一个进阶学习，所以在开始之前我们先对以前所学过的 JavaScript 相关知识点做一个快速复习总结。

### 重新介绍 JavaScript

#### JavaScript 是什么

#### 	解析执行：轻量级解释型的 

- 语言特点：动态，头等函数 (First-class Function)
  
  + 又称函数是 JavaScript 中的一等公民
- 执行环境：在宿主环境（host environment）下运行，浏览器是最常见的 JavaScript 宿主环境
  + 但是在很多非浏览器环境中也使用 JavaScript ，例如 node.js

  [MDN-JavaScript](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript)

#### JavaScript 的组成

- ECMAScript  - 语法规范
  - 变量、数据类型、类型转换、操作符
  - 流程控制语句：判断、循环语句
  - 数组、函数、作用域、预解析
  - 对象、属性、方法、简单类型和复杂类型的区别
  - 内置对象：Math、Date、Array，基本包装类型String、Number、Boolean
- Web APIs
  - BOM
    - onload页面加载事件，window顶级对象
    - 定时器
    - location、history
  - DOM
    - 获取页面元素，注册事件
    - 属性操作，样式操作
    - 节点属性，节点层级
    - 动态创建元素
    - 事件：注册事件的方式、事件的三个阶段、事件对象 

#### JavaScript 可以做什么

> 阿特伍德定律：
>
> Any application that can be written in JavaScript, will eventually be written in JavaScript.  
>
> 任何可以用*JavaScript*来写的应用，最终都将用*JavaScript*来写
>
> 阿特伍德 stackoverflow的创始人之一

- [知乎 - JavaScript 能做什么，该做什么？](https://www.zhihu.com/question/20796866)
- [最流行的编程语言 JavaScript 能做什么？](https://github.com/phodal/articles/issues/1)

### 浏览器是如何工作的

 ![img](media/jszxgc.png)

 [参考链接](http://www.2cto.com/kf/201202/118111.html)

```
User Interface  用户界面，我们所看到的浏览器
Browser engine  浏览器引擎，用来查询和操作渲染引擎
*Rendering engine 用来显示请求的内容，负责解析HTML、CSS，并把解析的内容显示出来
Networking   网络，负责发送网络请求
*JavaScript Interpreter(解析者)   JavaScript解析器，负责执行JavaScript的代码
UI Backend   UI后端，用来绘制类似组合框和弹出窗口
Data Persistence(持久化)  数据持久化，数据存储  cookie、HTML5中的sessionStorage
```



### JavaScript 执行过程

JavaScript 运行分为两个阶段：

- 预解析
  + 全局预解析（<strong style="color:red;">所有变量和函数声明都会提前；同名的函数和变量函数的优先级高</strong>）
  + 函数内部预解析（所有的变量、函数和形参都会参与预解析）
    * 函数
    * 形参
    * 普通变量
- 执行

先预解析全局作用域，然后执行全局作用域中的代码，
在执行全局代码的过程中遇到函数调用就会先进行函数预解析，然后再执行函数内代码。

---

## JavaScript 面向对象编程

<img src="./media/mxdxkf.png" width="400" alt="">

### 面向对象介绍

#### 什么是对象

> Everything is object （万物皆对象）

<img src="./media/20160823024542444.jpg" alt="">

对象到底是什么，我们可以从两次层次来理解。

**(1) 对象是单个事物的抽象。**

一本书、一辆汽车、一个人都可以是对象，一个数据库、一张网页、一个与远程服务器的连接也可以是对象。当实物被抽象成对象，实物之间的关系就变成了对象之间的关系，从而就可以模拟现实情况，针对对象进行编程。

**(2) 对象是一个容器，封装了属性（property）和方法（method）。**

属性是对象的状态，方法是对象的行为（完成某种任务）。比如，我们可以把动物抽象为animal对象，使用“属性”记录具体是那一种动物，使用“方法”表示动物的某种行为（奔跑、捕猎、休息等等）。

在实际开发中，对象是一个抽象的概念，可以将其简单理解为：**数据集或功能集**。

ECMAScript-262 把对象定义为：**无序属性的集合，其属性可以包含基本值、对象或者函数**。
严格来讲，这就相当于说对象是一组没有特定顺序的值。对象的每个属性或方法都有一个名字，而每个名字都映射到一个值。


  提示：每个对象都是基于一个引用类型创建的，这些类型可以是系统内置的原生类型，也可以是开发人员自定义的类型。


#### 什么是面向对象

> 面向对象不是新的东西，它只是过程式代码的一种高度封装，目的在于提高代码的开发效率和可维 护性。

<img src="./media/664ba37eeee9f4623c06c066867f1d38_r.jpg" width="400" alt="">

面向对象编程 —— Object Oriented Programming，简称 OOP ，是一种编程开发思想。
它将真实世界各种复杂的关系，抽象为一个个对象，然后由对象之间的分工与合作，完成对真实世界的模拟。

在面向对象程序开发思想中，每一个对象都是功能中心，具有明确分工，可以完成接受信息、处理数据、发出信息等任务。
因此，面向对象编程具有灵活、代码可复用、高度模块化等特点，容易维护和开发，比起由一系列函数或指令组成的传统的过程式编程（procedural programming），更适合多人合作的大型软件项目。

面向对象与面向过程： 

- 面向过程就是亲力亲为，事无巨细，面面俱到，步步紧跟，有条不紊
- 面向对象就是找一个对象，指挥得结果
- 面向对象将执行者转变成指挥者
- 面向对象不是面向过程的替代，而是面向过程的封装

面向对象的特性：

- 封装性 
- 继承性
- [多态性]抽象
  - 多态 ：让父类的引用指向子类的实例
  - Animal animal = new Dog();
  - var array = [dog, cat, pig, tigger];
  - for (var i = 0; i < array.length; i++) {
    - Animal animal = array[i];
    - animal.eat();
  - }

扩展阅读：

- [维基百科 - 面向对象程序设计](https://zh.wikipedia.org/wiki/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1)
- [知乎：如何用一句话说明什么是面向对象思想？](https://www.zhihu.com/question/19854505)
- [知乎：什么是面向对象编程思想？](https://www.zhihu.com/question/31021366)

#### 程序中面向对象的基本体现

在 JavaScript 中，所有数据类型都可以视为对象，当然也可以自定义对象。
自定义的对象数据类型就是面向对象中的类（ Class ）的概念。

我们以一个例子来说明面向过程和面向对象在程序流程上的不同之处。

假设我们要处理学生的成绩表，为了表示一个学生的成绩，面向过程的程序可以用一个对象表示：

```javascript
var std1 = { name: 'Michael', score: 98 }
var std2 = { name: 'Bob', score: 81 }
```

而处理学生成绩可以通过函数实现，比如打印学生的成绩：

```javascript
function printScore (student) {
  console.log('姓名：' + student.name + '  ' + '成绩：' + student.score)
}
```

如果采用面向对象的程序设计思想，我们首选思考的不是程序的执行流程，
而是 `Student` 这种数据类型应该被视为一个对象，这个对象拥有 `name` 和 `score` 这两个属性（Property）。
如果要打印一个学生的成绩，首先必须创建出这个学生对应的对象，然后，给对象发一个 `printScore` 消息，让对象自己把自己的数据打印出来。

抽象数据行为模板（Class）：

```javascript
function Student(name, score) {
  this.name = name;
  this.score = score;
  this.printScore = function() {
    console.log('姓名：' + this.name + '  ' + '成绩：' + this.score);
  }
}
```

根据模板创建具体实例对象（Instance）：

```javascript
var std1 = new Student('Michael', 98)
var std2 = new Student('Bob', 81)
```

实例对象具有自己的具体行为（给对象发消息）：

```javascript
std1.printScore() // => 姓名：Michael  成绩：98
std2.printScore() // => 姓名：Bob  成绩 81
```

面向对象的设计思想是从自然界中来的，因为在自然界中，类（Class）和实例（Instance）的概念是很自然的。
Class 是一种抽象概念，比如我们定义的 Class——Student ，是指学生这个概念，
而实例（Instance）则是一个个具体的 Student ，比如， Michael 和 Bob 是两个具体的 Student 。

所以，面向对象的设计思想是：

- 抽象出 Class(构造函数)
- 根据 Class(构造函数) 创建 Instance
- 指挥 Instance 得结果

面向对象的抽象程度又比函数要高，因为一个 Class 既包含数据，又包含操作数据的方法。

### 创建对象

#### 简单方式new

我们可以直接通过 `new Object()` 创建：

```javascript
var person = new Object()
person.name = 'Jack'
person.age = 18

person.sayName = function () {
  console.log(this.name)
}
```

每次创建通过 `new Object()` 比较麻烦，所以可以通过它的简写形式对象字面量来创建：

```javascript
var person = {
  name: 'Jack',
  age: 18,
  sayName: function () {
    console.log(this.name)
  }
}
```

对于上面的写法固然没有问题，但是假如我们要生成两个 `person` 实例对象呢？

```javascript
var person1 = {
  name: 'Jack',
  age: 18,
  sayName: function () {
    console.log(this.name)
  }
}

var person2 = {
  name: 'Mike',
  age: 16,
  sayName: function () {
    console.log(this.name)
  }
}
```

通过上面的代码我们不难看出，这样写的代码太过冗余，重复性太高。

#### 简单方式的改进：工厂函数

我们可以写一个函数，解决代码重复问题：

```javascript
function createPerson (name, age) {
  return {
    name: name,
    age: age,
    sayName: function () {
      console.log(this.name)
    }
  }
}
```

然后生成实例对象：

```javascript
var p1 = createPerson('Jack', 18)
var p2 = createPerson('Mike', 18)
```

这样封装确实爽多了，通过工厂模式我们解决了创建多个相似对象代码冗余的问题，
<strong style="color:red;">但却没有解决对象识别的问题（即怎样知道一个对象的类型）。</strong>

### 构造函数

构造函数第一个字母要大写

内容引导：

- 构造函数语法
- 分析构造函数
- 构造函数和实例对象的关系
  + 实例的 constructor 属性
  + instanceof 操作符
- 普通函数调用和构造函数调用的区别
- 构造函数的返回值
- 构造函数的问题

#### 更优雅的工厂函数：构造函数

一种更优雅的工厂函数就是下面这样，构造函数：

```javascript
function Person (name, age) {
  this.name = name
  this.age = age
  this.sayName = function () {
    console.log(this.name)
  }
}

var p1 = new Person('Jack', 18)
p1.sayName() // => Jack

var p2 = new Person('Mike', 23)
p2.sayName() // => Mike
```

new的作用：

1. 在内存中创建一个空对象
2. <strong style="color:red;">让构造数中的this，指向刚创建的利象</strong>
3. 执行构造函数(一般情況下，过this设置对象的成员)
4. 返回对象

```javascript
var s1 = new Person('Jack', 99);//this指向s1
var s2 = Person('Jack', 99);//this指向window，因为Person是window下的函数
```



#### 解析构造函数代码的执行

在上面的示例中，`Person()` 函数取代了 `createPerson()` 函数，但是实现效果是一样的。
这是为什么呢？

我们注意到，`Person()` 中的代码与 `createPerson()` 有以下几点不同之处：

- 没有显示的创建对象
- 直接将属性和方法赋给了 `this` 对象
- 没有 `return` 语句
- 函数名使用的是大写的 `Person`

而要创建 `Person` 实例，则必须使用 `new` 操作符。
以这种方式调用构造函数会经历以下 4 个步骤：

1. 创建一个新对象
2. 将构造函数的作用域赋给新对象（因此 this 就指向了这个新对象）
3. 执行构造函数中的代码
4. 返回新对象

下面是具体的伪代码：

```javascript
function Person (name, age) {
  // 当使用 new 操作符调用 Person() 的时候，实际上这里会先创建一个对象
  // var instance = {}
  // 然后让内部的 this 指向 instance 对象
  // this = instance
  // 接下来所有针对 this 的操作实际上操作的就是 instance

  this.name = name
  this.age = age
  this.sayName = function () {
    console.log(this.name)
  }

  // 在函数的结尾处会将 this 返回，也就是 instance
  // return this
}
```

#### 构造函数和实例对象的关系

使用构造函数的好处不仅仅在于代码的简洁性，更重要的是我们可以识别对象的具体类型了。
在每一个实例对象中同时有一个 <strong style="color:red;">`constructor`</strong> 属性，该属性指向创建该实例的构造函数：

```javascript
console.log(p1.constructor === Person) // => true
console.log(p2.constructor === Person) // => true
console.log(p1.constructor === p2.constructor) // => true
```

对象的 `constructor` 属性最初是用来标识对象类型的，
但是，如果要检测对象的类型，还是使用 <strong style="color:red;">`instanceof`</strong> 操作符更可靠一些：

```javascript
console.log(p1 instanceof Person) // => true
console.log(p2 instanceof Person) // => true
```

总结：

- 构造函数是根据具体的事物抽象出来的抽象模板
- 实例对象是根据抽象的构造函数模板得到的具体实例对象
- 每一个实例对象都具有一个 `constructor` 属性，指向创建该实例的构造函数
  + 注意： `constructor` 是实例的属性的说法不严谨，具体后面的原型会讲到
- 可以通过实例的 `constructor` 属性判断实例和构造函数之间的关系
  + 注意：这种方式不严谨，推荐使用 `instanceof` 操作符，后面学原型会解释为什么

#### 构造函数的问题

使用构造函数带来的最大的好处就是创建对象更方便了，但是其本身也存在一个浪费内存的问题：

```javascript
function Person (name, age) {
  this.name = name
  this.age = age
  this.type = 'human'
  this.sayHello = function () {
    console.log('hello ' + this.name)
  }
}

var p1 = new Person('Tom', 18)
var p2 = new Person('Jack', 16)
```

在该示例中，从表面上好像没什么问题，但是实际上这样做，有一个很大的弊端。
那就是对于每一个实例对象，`type` 和 `sayHello` 都是一模一样的内容，
每一次生成一个实例，都必须为重复的内容，多占用一些内存，如果实例对象很多，会造成极大的内存浪费。

```javascript
console.log(p1.sayHello === p2.sayHello) // => false
```

对于这种问题我们可以把需要共享的函数定义到构造函数外部：

```javascript
function sayHello = function () {
  console.log('hello ' + this.name)
}

function Person (name, age) {
  this.name = name
  this.age = age
  this.type = 'human'
  this.sayHello = sayHello
}

var p1 = new Person('Top', 18)
var p2 = new Person('Jack', 16)

console.log(p1.sayHello === p2.sayHello) // => true
```

这样确实可以了，但是如果有多个需要共享的函数的话就会造成全局命名空间冲突的问题。

你肯定想到了可以把多个函数放到一个对象中用来避免全局命名空间冲突的问题：

```javascript
var fns = {
  sayHello: function () {
    console.log('hello ' + this.name)
  },
  sayAge: function () {
    console.log(this.age)
  }
}

function Person (name, age) {
  this.name = name
  this.age = age
  this.type = 'human'
  this.sayHello = fns.sayHello
  this.sayAge = fns.sayAge
}

var p1 = new Person('lpz', 18)
var p2 = new Person('Jack', 16)

console.log(p1.sayHello === p2.sayHello) // => true
console.log(p1.sayAge === p2.sayAge) // => true
```

至此，我们利用自己的方式基本上解决了构造函数的内存浪费问题。
但是代码看起来还是那么的格格不入，那有没有更好的方式呢？

#### 小结

- 构造函数语法
- 分析构造函数
- 构造函数和实例对象的关系
  + 实例的 constructor 属性
  + instanceof 操作符
- 构造函数的问题

### 原型

内容引导：

- 使用 prototype 原型对象解决构造函数的问题
- 分析 构造函数、prototype 原型对象、实例对象 三者之间的关系
- 属性成员搜索原则：原型链
- 实例对象读写原型对象中的成员
- 原型对象的简写形式
- 原生对象的原型
  + Object
  + Array
  + String
  + ...
- 原型对象的问题
- 构造的函数和原型对象使用建议

#### 更好的解决方案： `prototype`

JavaScript 规定，<strong style="color:red;">每一个构造函数都有一个 `prototype` 属性</strong>，指向另一个对象。
这个对象的所有属性和方法，都会被构造函数的所拥有。

这也就意味着，我们可以把所有对象实例需要共享的属性和方法直接定义在 `prototype` 对象上。

```javascript
function Person (name, age) {
  this.name = name
  this.age = age
}

console.log(Person.prototype)

Person.prototype.type = 'human'

Person.prototype.sayName = function () {
  console.log(this.name)
}

var p1 = new Person(...)
var p2 = new Person(...)

console.log(p1.sayName === p2.sayName) // => true
```

这时所有实例的 `type` 属性和 `sayName()` 方法，
其实都是同一个内存地址，指向 `prototype` 对象，因此就提高了运行效率。

#### 构造函数、实例、原型三者之间的关系

<img src="./media/构造函数-实例-原型之间的关系.png" alt="">

任何函数都具有一个 `prototype` 属性，该属性是一个对象。

```javascript
function F () {}
console.log(F.prototype) // => object

F.prototype.sayHi = function () {
  console.log('hi!')
}
```

构造函数的 `prototype` 对象默认都有一个 `constructor` 属性，指向 `prototype` 对象所在函数。

```javascript
console.log(F.prototype.constructor === F) // => true
```

通过构造函数得到的实例对象内部会包含一个指向构造函数的 `prototype` 对象的指针 `__proto__`。

```javascript
var instance = new F()
console.log(instance.__proto__ === F.prototype) // => true
```

<p class="tip">
  `__proto__` 是非标准属性。
</p>

实例对象可以直接访问原型对象成员。

```javascript
instance.sayHi() // => hi!
```

<strong style="color:red;">总结</strong>：

- <strong style="color:red;">任何函数都具有一个 `prototype` 属性，该属性是一个对象，如果是构造函数，可以通过`prototype`向构造函数中添加属性或者函数</strong>
- <strong style="color:red;">构造函数的 `prototype` 对象默认都有一个 `constructor` 属性，指向 `prototype` 对象所在函数（指回到构造函数）</strong>
- <strong style="color:red;">通过构造函数得到的实例对象内部会包含一个指向构造函数的 `prototype` 对象的指针 `__proto__`（实例的proto指向构造函数的prototype）</strong>
- <strong style="color:red;">所有实例都直接或间接继承了原型对象的成员</strong>

#### 属性成员的搜索原则：原型链

<img src="D:\Markdown笔记\前端笔记\HTML+CSS\HTML5+CSS.assets\image-20210318161351474.png" alt="image-20210318161351474" style="zoom: 50%;" />

了解了 **构造函数-实例-原型对象** 三者之间的关系后，接下来我们来解释一下为什么实例对象可以访问原型对象中的成员。

每当代码读取某个对象的某个属性时，都会执行一次搜索，目标是具有给定名字的属性

- 搜索首先从对象实例本身开始
- 如果在实例中找到了具有给定名字的属性，则返回该属性的值
- 如果没有找到，则继续搜索指针指向的原型对象，在原型对象中查找具有给定名字的属性
- 如果在原型对象中找到了这个属性，则返回该属性的值

也就是说，在我们调用 `person1.sayName()` 的时候，会先后执行两次搜索：

- 首先，解析器会问：“实例 person1 有 sayName 属性吗？”答：“没有。
- ”然后，它继续搜索，再问：“ person1 的原型有 sayName 属性吗？”答：“有。
- ”于是，它就读取那个保存在原型对象中的函数。
- 当我们调用 person2.sayName() 时，将会重现相同的搜索过程，得到相同的结果。

而这正是多个对象实例共享原型所保存的属性和方法的基本原理。

总结：

- 先在自己身上找，找到即返回
- 自己身上找不到，则沿着原型链向上查找，找到即返回
- 如果一直到原型链的末端还没有找到，则返回 `undefined`

#### 实例对象读写原型对象成员

读取：

- 先在自己身上找，找到即返回
- 自己身上找不到，则沿着原型链向上查找，找到即返回
- 如果一直到原型链的末端还没有找到，则返回 `undefined`

值类型成员写入（`实例对象.值类型成员 = xx`）：

- 当实例期望重写原型对象中的某个普通数据成员时实际上会把该成员添加到自己身上
- 也就是说该行为实际上会屏蔽掉对原型对象成员的访问

引用类型成员写入（`实例对象.引用类型成员 = xx`）：

- 同上

复杂类型修改（`实例对象.成员.xx = xx`）：

- 同样会先在自己身上找该成员，如果自己身上找到则直接修改
- 如果自己身上找不到，则沿着原型链继续查找，如果找到则修改
- 如果一直到原型链的末端还没有找到该成员，则报错（`实例对象.undefined.xx = xx`）

#### 更简单的原型语法

我们注意到，前面例子中每添加一个属性和方法就要敲一遍 `Person.prototype` 。
为减少不必要的输入，更常见的做法是用一个包含所有属性和方法的对象字面量来重写整个原型对象：

```javascript
function Person (name, age) {
  this.name = name
  this.age = age
}

Person.prototype = {
  type: 'human',
  sayHello: function () {
    console.log('我叫' + this.name + '，我今年' + this.age + '岁了')
  }
}
```

在该示例中，我们将 `Person.prototype` 重置到了一个新的对象。
这样做的好处就是为 `Person.prototype` 添加成员简单了，但是也会带来一个问题，那就是原型对象丢失了 `constructor` 成员。

所以，我们为了保持 `constructor` 的指向正确，建议的写法是：

```javascript
function Person (name, age) {
  this.name = name
  this.age = age
}

Person.prototype = {
  constructor: Person, // => 手动将 constructor 指向正确的构造函数
  type: 'human',
  sayHello: function () {
    console.log('我叫' + this.name + '，我今年' + this.age + '岁了')
  }
}
```

#### 原生对象的原型

<p class="tip">
  所有函数都有 prototype 属性对象。
</p>

- Object.prototype
- Function.prototype
- Array.prototype
- String.prototype
- Number.prototype
- Date.prototype
- ...

练习：为数组对象和字符串对象扩展原型方法。

#### 原型对象使用建议

- <strong style="color:red;">私有成员（一般就是非函数成员）放到构造函数中</strong>
- <strong style="color:red;">共享成员（一般就是函数）放到原型对象中</strong>
- <strong style="color:red;">如果重置了 `prototype` 记得修正 `constructor` 的指向</strong>

### 案例：随机方块

---

## 面向对象游戏案例：贪吃蛇

### 案例介绍

#### 游戏演示

演示：[贪吃蛇](snake/index.html)

#### 案例目标

游戏的目的是用来体会JavaScript高级语法的使用 不需要具备抽象对象的能力，使用面向对象的方式分析问题，需要一个漫长的过程。

### 功能实现

#### 搭建页面

放一个容器盛放游戏场景 div#map，设置样式

```css
#map {
  width: 800px;
  height: 600px;
  background-color: #ccc;
  position: relative;
}
```

#### 分析对象

- 游戏对象
- 蛇对象
- 食物对象

#### 创建食物对象

- Food

  - 属性

    - x       
    - y
    - width
    - height
    - color       

  - 方法

    - render       随机创建一个食物对象，并输出到map上

- 创建Food的构造函数，并设置属性

```js
var position = 'absolute';
var elements = [];
function Food(x, y, width, height, color) {
  this.x = x || 0;
  this.y = y || 0;
  // 食物的宽度和高度(像素)
  this.width = width || 20;
  this.height = height || 20;
  // 食物的颜色
  this.color = color || 'green';
}
```

- 通过原型设置render方法，实现随机产生食物对象，并渲染到map上

```js
Food.prototype.render = function (map) {
  // 随机食物的位置，map.宽度/food.宽度，总共有多少分food的宽度，随机一下。然后再乘以food的宽度
  this.x = parseInt(Math.random() * map.offsetWidth / this.width) * this.width;
  this.y = parseInt(Math.random() * map.offsetHeight / this.height) * this.height;

  // 动态创建食物对应的div
  var div = document.createElement('div');
  map.appendChild(div);
  div.style.position = position;
  div.style.left = this.x + 'px';
  div.style.top = this.y + 'px';
  div.style.width = this.width + 'px';
  div.style.height = this.height + 'px';
  div.style.backgroundColor = this.color;
  elements.push(div);
}
```

- 通过自调用函数，进行封装，通过window暴露Food对象

```js
window.Food = Food;
```

#### 创建蛇对象


- Snake

- 属性

  - width    蛇节的宽度 默认20
  - height   蛇节的高度 默认20
  - body     数组，蛇的头部和身体，第一个位置是蛇头
  - direction    蛇运动的方向  默认right  可以是 left  top bottom

- 方法

  - render  把蛇渲染到map上

- Snake构造函数

```js
var position = 'absolute';
var elements = [];
function Snake(width, height, direction) {
  // 设置每一个蛇节的宽度
  this.width = width || 20;
  this.height = height || 20;
  // 蛇的每一部分, 第一部分是蛇头
  this.body = [
    {x: 3, y: 2, color: 'red'},
    {x: 2, y: 2, color: 'blue'},
    {x: 1, y: 2, color: 'blue'}
  ];
  this.direction = direction || 'right';
}
```

- render方法

```js
Snake.prototype.render = function(map) {
  for(var i = 0; i < this.body.length; i++) {
    var obj = this.body[i];
    var div = document.createElement('div');
    map.appendChild(div);
    div.style.left = obj.x * this.width + 'px';
    div.style.top = obj.y * this.height + 'px';
    div.style.position = position;
    div.style.backgroundColor = obj.color;
    div.style.width = this.width + 'px';
    div.style.height = this.height + 'px';
  }
}
```

- 在自调用函数中暴露Snake对象

```js
window.Snake = Snake;
```

#### 创建游戏对象

游戏对象，用来管理游戏中的所有对象和开始游戏

- Game

  - 属性

    - food

    - snake

    - map

  - 方法

    - start            开始游戏（绘制所有游戏对象）



- 构造函数

```js
function Game(map) {
  this.food = new Food();
  this.snake = new Snake();
  this.map = map;
}
```

- 开始游戏，渲染食物对象和蛇对象

```js
Game.prototype.start = function () {
  this.food.render(this.map);
  this.snake.render(this.map);
}
```

### 游戏的逻辑

#### 写蛇的move方法

- 在蛇对象(snake.js)中，在Snake的原型上新增move方法

1. 让蛇移动起来，把蛇身体的每一部分往前移动一下
2. 蛇头部分根据不同的方向决定 往哪里移动

```js
Snake.prototype.move = function (food, map) {
  // 让蛇身体的每一部分往前移动一下
  var i = this.body.length - 1;
  for(; i > 0; i--) {
    this.body[i].x = this.body[i - 1].x;
    this.body[i].y = this.body[i - 1].y;
  }
  // 根据移动的方向，决定蛇头如何处理
  switch(this.direction) {
    case 'left': 
      this.body[0].x -= 1;
      break;
    case 'right':
      this.body[0].x += 1;
      break;
    case 'top':
      this.body[0].y -= 1;
      break;
    case 'bottom':
      this.body[0].y += 1;
      break;
  }
}
```

- 在game中测试

```js
this.snake.move(this.food, this.map);
this.snake.render(this.map);
```

#### 让蛇自己动起来

- 私有方法

    ```
    什么是私有方法？
      不能被外部访问的方法
    如何创建私有方法？
      使用自调用函数包裹
    ```
- 在snake中添加删除蛇的私有方法，在render中调用

```js
function remove() {
  // 删除渲染的蛇
  var i = elements.length - 1;
  for(; i >= 0; i--) {
    // 删除页面上渲染的蛇
    elements[i].parentNode.removeChild(elements[i]);
    // 删除elements数组中的元素
    elements.splice(i, 1);
  }
}
```

- 在game.js中 添加runSnake的私有方法，开启定时器调用蛇的move和render方法，让蛇动起来
- 判断蛇是否撞墙

```js
function runSnake() {
  var timerId = setInterval(function() {
    this.snake.move(this.food, this.map);
    // 在渲染前，删除之前的蛇
    this.snake.render(this.map);

    // 判断蛇是否撞墙
    var maxX = this.map.offsetWidth / this.snake.width;
    var maxY = this.map.offsetHeight / this.snake.height;
    var headX = this.snake.body[0].x;
    var headY = this.snake.body[0].y;
    if (headX < 0 || headX >= maxX) {
      clearInterval(timerId);
      alert('Game Over');
    }

    if (headY < 0 || headY >= maxY) {
      clearInterval(timerId);
      alert('Game Over');
    }

  }.bind(that), 150);
}
```

- 在game中通过键盘控制蛇的移动方向

```js
function bindKey() {
  document.addEventListener('keydown', function(e) {
    switch (e.keyCode) {
      case 37:
        // left
        this.snake.direction = 'left';
        break;
      case 38:
        // top
        this.snake.direction = 'top';
        break;
      case 39:
        // right
        this.snake.direction = 'right';
        break;
      case 40:
        // bottom
        this.snake.direction = 'bottom';
        break;
    }
  }.bind(that), false);
}
```

- 在start方法中调用

```js
bindKey();
```

#### 判断蛇是否吃到食物

```js
// 在Snake的move方法中

// 在移动的过程中判断蛇是否吃到食物
// 如果蛇头和食物的位置重合代表吃到食物
// 食物的坐标是像素，蛇的坐标是几个宽度，进行转换
var headX = this.body[0].x * this.width;
var headY = this.body[0].y * this.height;
if (headX === food.x && headY === food.y) {
  // 吃到食物，往蛇节的最后加一节
  var last = this.body[this.body.length - 1];
  this.body.push({
    x: last.x,
    y: last.y,
    color: last.color
  })
  // 把现在的食物对象删除，并重新随机渲染一个食物对象
  food.render(map);
}
```

### 其它处理

#### 把html中的js代码放到index.js中

避免html中出现js代码

#### 自调用函数的参数

```js
(function (window, undefined) {
  var document = window.document;

}(window, undefined))
```

- 传入window对象

将来代码压缩的时候，可以吧 function (window)  压缩成 function (w)

- 传入undefined

在将来会看到别人写的代码中会把undefined作为函数的参数(当前案例没有使用)
因为在有的老版本的浏览器中 undefined可以被重新赋值，防止undefined 被重新赋值

#### 整理代码

现在的代码结构清晰，谁出问题就找到对应的js文件即可。
通过自调用函数，已经防止了变量命名污染的问题

但是，由于js文件数较多，需要在页面上引用，会产生文件依赖的问题(先引入那个js，再引入哪个js)
将来通过工具把js文件合并并压缩。现在手工合并js文件演示

- 问题1

```js
// 如果存在多个自调用函数要用分号分割，否则语法错误
// 下面代码会报错
(function () {
}())

(function () {
}())
// 所以代码规范中会建议在自调用函数之前加上分号
// 下面代码没有问题
;(function () {
}())

;(function () {
}())
```

- 问题2 

```js
// 当自调用函数 前面有函数声明时，会把自调用函数作为参数
// 所以建议自调用函数前，加上;
var a = function () {
  alert('11');
}
    
(function () {
  alert('22');
}())
```

---

## 继承

### 什么是继承

- 现实生活中的继承
- 程序中的继承

### 对象的继承

```javascript
// 继承演示（对象的继承）
function extend(child, parent) {
  for (var key in parent) {
    if (child[key]) continue;  // 如果child中有该成员，不替换成parent对象中的成员
    child[key] = parent[key];
  }
}

var parent = {
  name: '王健林',
  age: 60,
  house: '别墅',
  money: 1000000,
  car: '玛莎拉蒂',
  play: function () {
    console.log('弹吉他');
  }
};

var child = {
  name: '王思聪',
  age: 18
};
// 把parent对象的所有成员 拷贝到 child对象上 （实现继承）
extend(child, parent);
```

### 原型继承

```javascript
// 1 原型继承
function Super() {
  this.color = 'red';
}
function Sub() {
}

Sub.prototype = new Super();
Sub.prototype.constructor = Super;//修改了原型属性一定要修改constructor

var sub = new Sub();
console.log(sub.color);
```

原型继承的问题：无法给构造函数传参

如上例：Sub继承自Super，Super具有属性color，无法在创建Sub对象的时候传递color参数，Sub(color)错误

### 借构造函数继承

```javascript
function Person(name, age, sex) {
  this.name = name;
  this.age = age;
  this.sex = sex;
}
function Student(name, age, sex, score) {
  Person.call(this, name, age, sex);
  this.score = score;
}
var stu = new Student('zs', 18, '男', 100);
console.log(stu);
```

借用构造函数继承问题：无法重用方法

### 组合式继承

```javascript
// 结合原型继承和组合式继承
function Person(name, age, sex) {
  this.name = name;
  this.age = age;
  this.sex = sex;
}
Person.prototype.sayHi = function () {
  console.log(this.name);
}
function Student(name, age, sex, score) {
  Person.call(this, name, age, sex);
  this.score = score;
}
Student.prototype = new Person();
Student.prototype.constructor = Student;

var stu = new Student('zs', 18, '男', 100);
console.log(stu);
```

---

## 函数进阶

### 函数的定义方式

- 函数声明
- 函数表达式
- `new Function`

#### 函数声明 

```javascript
function foo () {

}
```

#### 函数表达式

```javascript
var foo = function () {

}
```

#### 实例化方式 new Function()

```javascript
// 不推荐使用这种方式，但是通过这种方式更容易理解函数是对象
var fn = new Function('a', 'b', 'console.log(a + b)');
fn(5, 6);
console.log(fn.constructor);
```



#### 函数声明与函数表达式的区别

- 函数声明必须有名字
- 函数声明会函数提升，在预解析阶段就已创建，声明前后都可以调用
- 函数表达式类似于变量赋值
- 函数表达式可以没有名字，例如匿名函数
- 函数表达式没有变量提升，在执行阶段创建，必须在表达式执行之后才可以调用



```javascript
console.log(foo1); // [Function: foo1]
foo1(); // foo1
console.log(foo2); // undefined
foo2(); // TypeError: foo2 is not a function
function foo1 () {
	console.log("foo1");
};
var foo2 = function () {
	console.log("foo2");
};
```





下面是一个根据条件定义函数的例子：

```javascript
// if语句中的函数声明，不进行提升
// 老版本的IE会函数提升，新版本的浏览器不会提升
if (true) {
  function f () {
    console.log(1)
  }
} else {
  function f () {
    console.log(2)
  }
}
```

以上代码执行结果在不同浏览器中结果不一致。

不过我们可以使用函数表达式解决上面的问题：

```javascript
var f;

if (true) {
  f = function () {
    console.log(1);
  }
} else {
  f = function () {
    console.log(2);
  }
}
```

### 函数的调用方式

- 普通函数
- 构造函数
- 对象方法

### 函数内 `this` 指向的不同场景

函数的调用方式决定了 `this` 指向的不同：

| 调用方式   | 非严格模式   | 备注                |
| ------ | ------- | ----------------- |
| 普通函数调用 | window  | 严格模式下是 undefined  |
| 构造函数调用 | 实例对象    | 原型方法中 this 也是实例对象 |
| 对象方法调用 | 该方法所属对象 | 紧挨着的对象            |
| 事件绑定方法 | 绑定事件对象  |                   |
| 定时器函数  | window  |                   |

这就是对函数内部 this 指向的基本整理，写代码写多了自然而然就熟悉了。

### 函数也是对象

- 所有函数都是 `Function` 的实例

### call、apply、bind

那了解了函数 this 指向的不同场景之后，我们知道有些情况下我们为了使用某种特定环境的 this 引用，
这时候时候我们就需要采用一些特殊手段来处理了，例如我们经常在定时器外部备份 this 引用，然后在定时器函数内部使用外部 this 的引用。
然而实际上对于这种做法我们的 JavaScript 为我们专门提供了一些函数方法用来帮我们更优雅的处理函数内部 this 指向问题。
这就是接下来我们要学习的 call、apply、bind 三个函数方法。

#### call

`call()` 方法调用一个函数, 其具有一个指定的 `this` 值和分别地提供的参数(参数的列表)。

注意：该方法的作用和 `apply()` 方法类似，只有一个区别，就是 `call()` 方法接受的是若干个参数的列表，而 `apply()` 方法接受的是一个包含多个参数的数组。


语法：

```javascript
fun.call(this,Arg[, arg1[, arg2[, ...]]])
```

参数：

- `thisArg`
  + 在 fun 函数运行时指定的 this 值
  + 如果指定了 null 或者 undefined 则内部 this 指向 window

- `arg1, arg2, ...`
  + 指定的参数列表

#### apply

`apply()` 方法调用一个函数, 其具有一个指定的 `this` 值，以及作为一个数组（或类似数组的对象）提供的参数。

<p class="danger">
  注意：该方法的作用和 `call()` 方法类似，只有一个区别，就是 `call()` 方法接受的是若干个参数的列表，而 `apply()` 方法接受的是一个包含多个参数的数组。
</p>

语法：

```javascript
fun.apply(thisArg, [argsArray])
```

参数：

- `thisArg`
- `argsArray`

`apply()` 与 `call()` 非常相似，不同之处在于提供参数的方式。
`apply()` 使用参数数组而不是一组参数列表。例如：

```javascript
fun.apply(this, ['eat', 'bananas'])
```

#### bind

bind() 函数会创建一个新函数（称为绑定函数），新函数与被调函数（绑定函数的目标函数）具有相同的函数体（在 ECMAScript 5 规范中内置的call属性）。
当目标函数被调用时 this 值绑定到 bind() 的第一个参数，该参数不能被重写。绑定函数被调用时，bind() 也接受预设的参数提供给原函数。
一个绑定函数也能使用new操作符创建对象：这种行为就像把原函数当成构造器。提供的 this 值被忽略，同时调用时的参数被提供给模拟函数。

语法：

```javascript
fun.bind(thisArg[, arg1[, arg2[, ...]]])
```

参数：

- thisArg
  + 当绑定函数被调用时，该参数会作为原函数运行时的 this 指向。当使用new 操作符调用绑定函数时，该参数无效。

- arg1, arg2, ...
  + 当绑定函数被调用时，这些参数将置于实参之前传递给被绑定的方法。

返回值：

返回由指定的this值和初始化参数改造的原函数拷贝。

示例1：

```javascript
this.x = 9; 
var module = {
  x: 81,
  getX: function() { return this.x; }
};

module.getX(); // 返回 81

var retrieveX = module.getX;
retrieveX(); // 返回 9, 在这种情况下，"this"指向全局作用域

// 创建一个新函数，将"this"绑定到module对象
// 新手可能会被全局的x变量和module里的属性x所迷惑
var boundGetX = retrieveX.bind(module);
boundGetX(); // 返回 81
```

示例2：

```javascript
function LateBloomer() {
  this.petalCount = Math.ceil(Math.random() * 12) + 1;
}

// Declare bloom after a delay of 1 second
LateBloomer.prototype.bloom = function() {
  window.setTimeout(this.declare.bind(this), 1000);
};

LateBloomer.prototype.declare = function() {
  console.log('I am a beautiful flower with ' +
    this.petalCount + ' petals!');
};

var flower = new LateBloomer();
flower.bloom();  // 一秒钟后, 调用'declare'方法
```

#### 应用

- 让伪数组使用数组的方法

  ```javascript
  var obj = {
    0: 1,
    1: 8,
    2: 10,
    3: 3,
    4: 2,
    length: 5
  }; 
  Array.prototype.splice.call(obj, 0, 1);
  Array.prototype.push.call(obj, 100);
  console.log(obj);
  ```

- 对象内部使用使用定时器

  ```javascript
  var o = {
    name: 'hanmeimei',
    func1: function () {
      console.log(this.name);
    },
    func2: function () {
      setInterval(function () {
        console.log(this);
      }.bind(this), 2000);
    }
  };
  o.func2();
  ```

- 让数组的每一项作为方法的参数

  ```javascript
  var arr = [2, 1, 8, 9, 10, 3];
  console.log(Math.max.apply(Math, arr));
  console.log.apply(console, arr);
  ```

#### 小结

- call 和 apply 特性一样
  + 都是用来调用函数，而且是立即调用
  + 但是可以在调用函数的同时，通过第一个参数指定函数内部 `this` 的指向
  + call 调用的时候，参数必须以参数列表的形式进行传递，也就是以逗号分隔的方式依次传递即可
  + apply 调用的时候，参数必须是一个数组，然后在执行的时候，会将数组内部的元素一个一个拿出来，与形参一一对应进行传递
  + 如果第一个参数指定了 `null` 或者 `undefined` 则内部 this 指向 window

- bind
  + 可以用来指定内部 this 的指向，然后生成一个改变了 this 指向的新的函数
  + 它和 call、apply 最大的区别是：bind 不会调用
  + bind 支持传递参数，它的传参方式比较特殊，一共有两个位置可以传递
    * 1. 在 bind 的同时，以参数列表的形式进行传递
    * 2. 在调用的时候，以参数列表的形式进行传递
    * 那到底以谁 bind 的时候传递的参数为准呢还是以调用的时候传递的参数为准
    * 两者合并：bind 的时候传递的参数和调用的时候传递的参数会合并到一起，传递到函数内部

### 函数的其它成员

- arguments
  + 实参集合
- caller
  + 函数的调用者
- length
  + 形参的个数
- name
  + 函数的名称

```javascript
function fn(x, y, z) {
  console.log(fn.length) // => 形参的个数
  console.log(arguments) // 伪数组实参参数集合
  console.log(arguments.callee === fn) // 函数本身
  console.log(fn.caller) // 函数的调用者
  console.log(fn.name) // => 函数的名字
}

function f() {
  fn(10, 20, 30)
}

f()
```

### 高阶函数

- 函数可以作为参数
- 函数可以作为返回值

#### 作为参数

```javascript
function eat (callback) {
  setTimeout(function () {
    console.log('吃完了')
    callback()
  }, 1000)
}

eat(function () {
  console.log('去唱歌')
})
```

#### 作为返回值

```javascript
function makeAdder(x) {
  return function(y) {
    return x + y;
  };
}

var add5 = makeAdder(5);
var add10 = makeAdder(10);

console.log(add5(2));  // 7
console.log(add10(2)); // 12
```



```javascript
function genFun (type) {
  return function (obj) {
    return Object.prototype.toString.call(obj) === type
  }
}

var isArray = genFun('[object Array]')
var isObject = genFun('[object Object]')

console.log(isArray([])) // => true
console.log(isArray({})) // => true
```

### 函数闭包

```javascript
function fn () {
  var count = 0
  return {
    getCount: function () {
      console.log(count)
    },
    setCount: function () {
      count++
    }
  }
}

var fns = fn()

fns.getCount() // => 0
fns.setCount()
fns.getCount() // => 1
```

#### 作用域、作用域链、预解析

- 全局作用域
- 函数作用域
- **没有块级作用域，但是ES6中let 和 const可以实现块级作用域**



```javascript
    {
        var a = 1;
        console.log(a); // 1
    }
    console.log(a); // 1
    // 可见，通过var定义的变量可以跨块作用域访问到。

    (function A() {
        var b = 2;
        console.log(b); // 2
    })();
    // console.log(b); // 报错，
    // 可见，通过var定义的变量不能跨函数作用域访问到

    if(true) {
        var c = 3;
    }
    console.log(c); // 3
    for(var i = 0; i < 4; i++) {
        var d = 5;
    };
    console.log(i);    // 4   (循环结束i已经是4，所以此处i为4)
    console.log(d); // 5
    // if语句和for语句中用var定义的变量可以在外面访问到，
    // 可见，if语句和for语句属于块作用域，不属于函数作用域。
```

  var定义的变量，没有块的概念，可以跨块访问, 不能跨函数访问。
  let定义的变量，只能在块作用域里访问，不能跨块访问，也不能跨函数访问。
  const用来定义常量，使用时必须初始化(即必须赋值)，只能在块作用域里访问，而且不能修改

**let 定义变量也会提升，但是不会自动赋值一个undefined，而var定义变量的同时会自动赋值undefined。**

```javascript
	// 块作用域
    {
        var a = 1;
        let b = 2;
        const c = 3;
        // c = 4; // 报错
        var aa;
        let bb;
        // const cc; // 报错
        console.log(a); // 1
        console.log(b); // 2
        console.log(c); // 3
        console.log(aa); // undefined
        console.log(bb); // undefined
    }
    console.log(a); // 1
    // console.log(b); // 报错
    // console.log(c); // 报错

    // 函数作用域
    (function A() {
        var d = 5;
        let e = 6;
        const f = 7;
        console.log(d); // 5
        console.log(e); // 6  (在同一个{ }中,也属于同一个块，可以正常访问到)
        console.log(f); // 7  (在同一个{ }中,也属于同一个块，可以正常访问到)

    })();
    // console.log(d); // 报错
    // console.log(e); // 报错
    // console.log(f); // 报错
```







```javascript
{
  var foo = 'bar'
}

console.log(foo)

if (true) {
  var a = 123
}
console.log(a)
```

作用域链示例代码：

```javascript
var a = 10

function fn () {
  var b = 20

  function fn1 () {
    var c = 30
    console.log(a + b + c)
  }

  function fn2 () {
    var d = 40
    console.log(c + d)
  }

  fn1()
  fn2()
}
```

- 内层作用域可以访问外层作用域，反之不行

#### 什么是闭包

闭包就是在另一个作用域能够读取其他函数内部变量的函数，
由于在 Javascript 语言中，只有函数内部的子函数才能读取局部变量，
因此可以把闭包简单理解成 “定义在一个函数内部的函数”。
所以，在本质上，闭包就是将函数内部和函数外部连接起来的一座桥梁。

闭包的用途：

- 可以在函数外部读取函数内部成员
- 让函数内成员始终存活在内存中

#### 一些关于闭包的例子

示例1：

```javascript
var ul = document.getElementById('mv');
var i = 0, len = ul.children.length;
for (; i < len; i++) {
  var li = ul.children[i];
  (function (i) {
    li.onclick = function () {
      console.log(i);
    };
  })(i);
}
```

示例2：

```javascript
console.log(111)

for(var i = 0; i < 3; i++) {
  setTimeout(function () {
    console.log(i)
  }, 0)
}
console.log(222)
```

#### 闭包的思考题

思考题 1：

```javascript
var name = "The Window";
var object = {
  name: "My Object",
  getNameFunc: function () {
    return function () {
      return this.name;
    };
  }
};

console.log(object.getNameFunc()())
```

思考题 2：

```javascript
var name = "The Window";　　
var object = {　　　　
  name: "My Object",
  getNameFunc: function () {
    var that = this;
    return function () {
      return that.name;
    };
  }
};
console.log(object.getNameFunc()())
```

---

## 附录

### A 代码规范

#### 代码风格

- [JavaScript Standard Style ](https://github.com/feross/standard)
- [Airbnb JavaScript Style Guide() {](https://github.com/airbnb/javascript)

#### 校验工具

- [JSLint](https://github.com/douglascrockford/JSLint)
- [JSHint](https://github.com/jshint/jshint)
- [ESLint](https://github.com/eslint/eslint)

### B Chrome 开发者工具

### C 文档相关工具

- 电子文档制作工具: [docute](https://github.com/egoist/docute)
- 流程图工具：[DiagramDesigner](http://logicnet.dk/DiagramDesigner/)



# 积累

## 深拷贝与浅拷贝

正常情况下都是浅拷贝，即引用传递，不会开辟新的内存空间

```javascript
let a = {
    age: 20
};

let b = a;

b.age = 30;

console.log(a.age); // 30
```

实现深拷贝的方法：

**利用JSON类**

```javascript
let a = {
    age: 20
};

let b = JSON.parse(JSON.stringify(a));

b.age = 30;

console.log(a.age); // 20
```

优点：优点是方便快捷，性能相对比较好

缺点：但是复杂的对象进行JSON转换有可能会丢失属性，如下代码

```javascript
let a = {
    age: 20,
    local: function() {
        return 5;
    }
};

let b = JSON.parse(JSON.stringify(a));

console.log(b); // { age : 20 }
console.log(b.local()); //  b.loacl is not a function
```

**利用递归的方式**



## JavaScript 参数传递方式

- **基本类型值** primitive type，比如Undefined,Null,Boolean,Number,String。
- **引用类型值** 也就是对象类型 Object type,比如Object,Array,Function,Date等。 

基本类型按值传递，引用类型按共享传递

* 按值传递

```javascript
let a = 1;
function add(val) {
  val += 1;
  console.log(`val=${val}`); // 2
}

add(a);
console.log(`a=${a}`); // 1
```

* 按共享传递

```javascript
let obj = {
    a: 1
}
function change(obj) {
    obj.a = 2;
    console.log(obj); // {a: 2}
    obj = {
        a: 3
    }
    console.log(obj); // {a: 3}
}

change(obj);
console.log(obj); // {a: 2}
```

从上面的代码可以看出，在函数中对参数所指向的对象进行修改时会影响到外面的实参，但对函数参数重新赋值时，不会影响到实参，故js引用类型的传值方式为**call by sharing**



## Async 和 Await

* async 是声明异步函数，返回值是promise对象，如果async关键字函数返回的不是promise，会自动用Promise.resolve()包装。

```js
async function async1() {
    console.log('1')
    return 'test'
}

//等价于

new Promise(function(resolve) {
    console.log('1')
    resolve('test')
})

//等价于
console.log('1')
Promise.resolve('test')

```

* await 等待右侧表达式的结果，这个结果是promise对象或者其他值
  * 如果它等到的不是一个 promise 对象，那 await 表达式的运算结果就是它等到的东西
  * 如果它等到的是一个 promise 对象，它会阻塞后面的代码，等着 promise 对象 resolve，然后得到 resolve 的值，作为 await 表达式的运算结果。

```js
function test() {
    return new Promise(resolve => {
        setTimeout(() => resolve("test"), 2000);
    });
}

const result = await test();
console.log(result);
console.log('end')
```

由于test()造成的阻塞，console.log('end')会等到两秒后执行

所以为了避免造成阻塞，await 必须用在 async 函数中，async 函数调用不会造成阻塞

```js
function test() {
    return new Promise(resolve => {
        setTimeout(() => resolve("test"), 2000);
    });
}

async function test2() {
    const result = await test();
    console.log(result);
}
test2();
console.log('end');
```



## 接收Promise抛出值

平时我们在 Promise 中是无法接收抛出值的，都是将值通过 resolve 传递到下一层 then 中，如果要从外部接收抛出值，则需要通过 async 和 await

```js
fetchPromiseValue = () => {
    return new Promise(function(resolve, reject) {
        resolve({value: 'PromiseReturnValue'});   // Promise 抛出状态值
    })
};

handlePromise = async () =>{
    let  getValue  = await this.fetchPromiseValue();  // 异步获取 Promise  抛出的状态值
    console.log('Promise 的状态值： ',getValue.value);
};
```



## 事件循环机制

[前端干货：JS的执行顺序 - 简书](https://www.jianshu.com/p/62c7d633a879)

[8张图帮你一步步看清 async/await 和 promise 的执行顺序 - SegmentFault 思否](https://segmentfault.com/a/1190000017224799)

这两篇文章对于 await 的阐述不一样，因为 chrome版本不一样，导致解析过程不同，下面是我个人的理解

文章1 认为遇到 await 就要把后面的代码放入微队列，文章2 认为要进行阻塞，跳出 async，最后回来处理，这样就会得到不同的结果

因此 1 和 2 的描述都是不准确的

[js async/await - 码农1213 - 博客园](https://www.cnblogs.com/bear-blogs/p/10423759.html)

文章3 的描述应该是最为准确的

> await等待右侧表达式的结果，这个结果是promise对象或者其他值。
> 如果它等到的不是一个 promise 对象，那 await 表达式的运算结果就是它等到的东西。
> 如果它等到的是一个 promise 对象，await 就忙起来了，它会阻塞后面的代码，等着 promise 对象 resolve，然后得到 resolve 的值，作为 await 表达式的运算结果。

具体解析在下述**Promise和async中的立即执行**

### 例子

有一个地方很容易产生歧义，到底是先打印 async1 end 还是先打印 promise2，我们这样分析

```js
await async2();
console.log('async1 end');
```

等价于

```js
new Promise(() => {
    console.log('async2')
}).then((null) => {
    console.log('async1 end')
})
```

这里会把 then 后面的放入微任务队列

但是如果讲 async2 函数改成

```js
async function async2() {
    console.log('async2');
    return await 'candy'
}
```

等价于

```js
new Promise(() => {
    console.log('async2')
}).then((null) => {
    console.log('async1 end')
}).then(('candy') => {
    console.log('async1 end')
})
```

第一个 then 会先放入微任务队列，执行完成后，发现还有 then ，再将任务放到队尾，所以这种情况下 async1 end 会后打印，就像下面那道题一样

```js
async function async1() {
    console.log('async1 start');
    await async2();
    console.log('async1 end');
}
async function async2() {
    console.log('async2');
}

console.log('script start');

setTimeout(function() {
    console.log('setTimeout');
}, 0)

async1();

new Promise(function(resolve) {
    console.log('promise1');
    resolve();
}).then(function() {
    console.log('promise2');
});
console.log('script end');


/*
script start
async1 start
async2
promise1
script end
async1 end
promise2
setTimeout
*/
```

### 流程图

* JS 是单线程的，代码自上而下运行，所有代码被放到`执行栈`中运行
* 遇到异步函数将回调函数添加到一个`任务队列`里面；
* 当`执行栈`中的代码执行完以后，会去循环`任务队列`里的函数;
* 将`任务队列`里的函数放到`执行栈`中执行;
* 如此往复，称为`事件循环`;

![image-20211105204127764](JavaScript高级.assets/image-20211105204127764.png)

再来看下面一段代码：

```js
function fn() {
    setTimeout(()=>{
        console.log('a');
    },0);
    new Promise((resolve)=>{
        console.log('b');
        resolve();
    }).then(()=>{
        console.log('c')
    });
}
fn() // b c a
```

我们知道Promise中的异步体现在then和catch中，所以写在Promise中的代码是被当做同步任务立即执行的。而在async/await中，**在出现await出现之前，其中**

**的代码也是立即执行的**。那么出现了await时候发生了什么呢？

### Promise和async中的立即执行

很多人以为await会一直等待之后的表达式执行完之后才会继续执行后面的代码，实际上await是一个让出线程的标志。

* await 首先会执行右侧的函数
* 情况1：如果右侧没有返回 Promise 对象，则会把 await 下面的同步代码全部放到微队列中（上述例题情况，文章1）
* 情况2：如果返回 Promise 对象， await 则会中断，先跳出 async 函数，后面的全部执行完毕/放入任务队列后，再回来处理（文章2）

下面举例说明情况2：

* 遇到了 `await test2()`，首先执行打印 test2，并且有返回值，async 会默认将返回值包装成 `Promise.resolve(await 'return test2 value')`，而 await 可以将 resolve 中的值解析出来，因此最终返回 `await ‘return test2 value’`，则后面的代码不放入微任务队列
* 继续在外部执行，最后回到`await ‘return test2 value’`，执行右边，打印`return test2 value`，将`console.log('end test1')`放入微任务队列，再从队列按顺序中取出打印

```js
  async function test1() {
    console.log('start test1');
    console.log(await test2());
    console.log('end test1');
  }
  async function test2() {
    console.log('test2');
    return await 'return test2 value'
  }
  test1();
  console.log('start async');
  setTimeout(() => {
    console.log('setTimeout');
  }, 0);
  new Promise((resolve, reject) => {
    console.log('promise1');
    resolve();
  }).then(() => {
    console.log('promise2');
  });
  console.log('end async');
```

打印结果为：

![image-20211105221350403](JavaScript高级.assets/image-20211105221350403.png)

### 宏任务与微任务

任务分为**宏任务**和**微任务**，二者的区别决定了上述代码执行顺序

宏任务包括：

- setTimeout
- setInterval
- setImmediate (Node独有)
- requestAnimationFrame (浏览器独有)
- I/O
- UI rendering (浏览器独有)

微任务包括：

- process.nextTick (Node独有)
- Promise
- Object.observe
- MutationObserver

![image-20211105205559947](JavaScript高级.assets/image-20211105205559947.png)

* 执行全局Script同步代码，这些同步代码有一些是同步语句，有一些是异步语句（比如setTimeout等）
* 全局Script代码执行完毕后，`执行栈`Stack会清空
* 从`微队列`中取出位于队首的回调任务，放入`执行栈`Stack中执行，执行完后`微队列`长度减1
* 继续循环取出位于`微队列`的任务，放入`执行栈`Stack中执行，以此类推，直到直到把`微任务`执行完毕。注意，如果在执行`微任务`的过程中，又产生了`微任务`那么会加入到`微队列`的末尾，也会在这个周期被调用执行
* `微队列`中的所有`微任务`都执行完毕，此时`微队列`为空队列，`执行栈`Stack也为空
* 取出`宏队列`中的任务，放入`执行栈`Stack中执行
* 执行完毕后，`执行栈`Stack为空
* 重复第3-7个步骤

### 几个关键点

* Promise中的代码是被当做同步任务立即执行
* 出现 await 之前，async 中代码是同步的
* 遇到 await，如果接收的不是 Promise，则先立即执行 await 右边，并把 await 下面（仍在async中）的代码放到微任务队列中
* 遇到 await，如果接收的是 Promise，则先立即执行 await 右边，并跳出该 async，直到把外部的代码都运行完后，再把 await 下面（在async中）的代码放到微任务队列中

## 模板字符串(反引号)

https://blog.csdn.net/ksx2333/article/details/115523597

常用到的是在模板字符串中使用变量和表达式，使用`${}`包裹
