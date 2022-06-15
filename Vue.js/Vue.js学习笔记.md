# 基础

## 安装

对于制作原型或学习，你可以这样使用最新版本：

```
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

对于生产环境，我们推荐链接到一个明确的版本号和构建文件，以避免新版本造成的不可预期的破坏：

```
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.12"></script>
```

如果你使用原生 ES Modules，这里也有一个兼容 ES Module 的构建文件：

```
<script type="module">
  import Vue from 'https://cdn.jsdelivr.net/npm/vue@2.6.12/dist/vue.esm.browser.js'
</script>
```

你可以在 [cdn.jsdelivr.net/npm/vue](https://cdn.jsdelivr.net/npm/vue/) 浏览 NPM 包的源代码。

Vue 也可以在 [unpkg](https://unpkg.com/vue@2.6.12/dist/vue.js) 和 [cdnjs](https://cdnjs.cloudflare.com/ajax/libs/vue/2.6.12/vue.js) 上获取 (cdnjs 的版本更新可能略滞后)。

请确认了解[不同构建版本](https://cn.vuejs.org/v2/guide/installation.html#对不同构建版本的解释)并在你发布的站点中使用**生产环境版本**，把 `vue.js` 换成 `vue.min.js`。这是一个更小的构建，可以带来比开发环境下更快的速度体验。

**NPM**

在用 Vue 构建大型应用时推荐使用 NPM 安装[[1\]](https://cn.vuejs.org/v2/guide/installation.html#footnote-1)。NPM 能很好地和诸如 [webpack](https://webpack.js.org/) 或 [Browserify](http://browserify.org/) 模块打包器配合使用。同时 Vue 也提供配套工具来开发[单文件组件](https://cn.vuejs.org/v2/guide/single-file-components.html)。

```
# 最新稳定版
$ npm install vue
```



## 简介

Vue.js 的核心是一个允许采用简洁的模板语法来声明式地将数据渲染进 DOM 的系统：

```html
<div id="app">
  {{ message }}
</div>
var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
})
```

显示：Hello Vue!

我们已经成功创建了第一个 Vue 应用！看起来这跟渲染一个字符串模板非常类似，但是 Vue 在背后做了大量工作。现在数据和 DOM 已经被建立了关联，所有东西都是**响应式的**。我们要怎么确认呢？打开你的浏览器的 JavaScript 控制台 (就在这个页面打开)，并修改 `app.message` 的值，你将看到上例相应地更新。

**条件与循环**

条件：v-if

```html
<div id="app-3">
  <p v-if="seen">现在你看到我了</p>
</div>
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
```

循环：v-for

```html
<div id="app-4">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
```

```javascript
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: '学习 JavaScript' },
      { text: '学习 Vue' },
      { text: '整个牛项目' }
    ]
  }
})
```

  **事件绑定**

```html
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">反转消息</button>
</div>
```

```javascript
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Hello Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
```



## Vue实例

每个 Vue 应用都是通过用 `Vue` 函数创建一个新的 **Vue 实例**开始的：

```javascript
var vm = new Vue () {
    el: "", //定位dom元素
    data: { //需要传入的数据
        
    }, 
    methods: { //方法的定义
        
    }
}
```

### 生命周期

每个 Vue 实例在被创建时都要经过一系列的初始化过程——例如，需要设置数据监听、编译模板、将实例挂载到 DOM 并在数据变化时更新 DOM 等。同时在这个过程中也会运行一些叫做**生命周期钩子**的函数，这给了用户在不同阶段添加自己的代码的机会。

也就是说，用户可以通过不同的生命周期函数，在不同的生命周期完成自己的需求

```js
new Vue({
  data: {
    a: 1
  },
  created: function () {
    // `this` 指向 vm 实例
    console.log('a is: ' + this.a)
  }
})
// => "a is: 1"
```

<img src="https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/19/16ca74f183827f46~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp" style="zoom: 300%;" />



## 模板语法

Vue.js 使用了基于 HTML 的模板语法，允许开发者声明式地将 DOM 绑定至底层 Vue 实例的数据。所有 Vue.js 的模板都是合法的 HTML，所以能被遵循规范的浏览器和 HTML 解析器解析。

### 插值

**文本**

```html
<span v-once>这个将不会改变: {{ msg }}</span>
```

**HTML**

双大括号会将数据解释为普通文本，而非 HTML 代码。为了输出真正的 HTML，你需要使用 [`v-html` 指令](https://cn.vuejs.org/v2/api/#v-html)：

```html
<p>Using mustaches: {{ rawHtml }}</p>
<p>Using v-html directive: <span v-html="rawHtml"></span></p>
```

```
Using mustaches: <span style="color: red">This should be red.</span>
Using v-html directive: This should be red.
```

**属性**

Mustache 语法不能作用在 HTML attribute 上，遇到这种情况应该使用 [`v-bind` 指令](https://cn.vuejs.org/v2/api/#v-bind)：

```html
<div v-bind:id="dynamicId"></div>
```

对于布尔 attribute (它们只要存在就意味着值为 `true`)，`v-bind` 工作起来略有不同，在这个例子中：

```html
<button v-bind:disabled="isButtonDisabled">Button</button>
```

如果 `isButtonDisabled` 的值是 `null`、`undefined` 或 `false`，则 `disabled` attribute 甚至不会被包含在渲染出来的 `<button>` 元素中。

语法糖：

```html
<button :disabled="isButtonDisabled">Button</button>
```

**表达式支持**

对于所有的数据绑定，Vue.js 都提供了完全的 JavaScript 表达式支持。

```html
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}

<div v-bind:id="'list-' + id"></div>
```

这些表达式会在所属 Vue 实例的数据作用域下作为 JavaScript 被解析。有个限制就是，每个绑定都只能包含**单个表达式**，所以下面的例子都**不会**生效。

```html
<!-- 这是语句，不是表达式 -->
{{ var a = 1 }}

<!-- 流控制也不会生效，请使用三元表达式 -->
{{ if (ok) { return message } }}
```

### 指令

**参数**

一些指令能够接收一个“参数”，在指令名称之后以冒号表示。例如，`v-bind` 指令可以用于响应式地更新 HTML attribute：

```html
<a v-bind:href="url">...</a>
```

在这里 `href` 是参数，告知 `v-bind` 指令将该元素的 `href` attribute 与表达式 `url` 的值绑定。

另一个例子是 `v-on` 指令，它用于监听 DOM 事件：

```html
<a v-on:click="doSomething">...</a>
```

在这里参数是监听的事件名。我们也会更详细地讨论事件处理。

v-bind 可以通过{}、[]等绑定诸如style、class等内容

对象语法

```html
用法一：直接通过{}绑定一个类
<h2 :class="{'active': isActive}">Hello World</h2>

用法二：也可以通过判断，传入多个值
<h2 :class="{'active': isActive, 'line': isLine}">Hello World</h2>

用法三：和普通的类同时存在，并不冲突
注：如果isActive和isLine都为true，那么会有title/active/line三个类
<h2 class="title" :class="{'active': isActive, 'line': isLine}">Hello World</h2>

用法四：如果过于复杂，可以放在一个methods或者computed中
注：classes是一个计算属性
<h2 class="title" :class="classes">Hello World</h2>
```

数组语法

```html
用法一：直接通过{}绑定一个类
<h2 :class="['active']">Hello World</h2>

用法二：也可以传入多个值
<h2 :class="['active', 'line']">Hello World</h2>

用法三：和普通的类同时存在，并不冲突
注：会有title/active/line三个类
<h2 class="title" :class="['active', 'line']">Hello World</h2>

用法四：如果过于复杂，可以放在一个methods或者computed中
注：classes是一个计算属性
<h2 class="title" :class="classes">Hello World</h2>
```



## 计算属性 computed

通过computed引入计算属性

```html
<body>
  <div id='app'>
    <h2>{{fullname}}</h2>
  </div>

  <script src="../vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        firstName: 'Kobe',
        lastName: 'Brant'
      },
      computed: {
        fullname: {
          set: function (newValue) {
            const names = newValue.split(' ');
            this.firstName = names[0];
            this.lastName = names[1];
          },
          get: function () {
            return this.firstName + ' ' + this.lastName;
          }
        }
      }
    })
  </script>
```

默认情况下set属性可以不要，即

```html
<body>
  <div id='app'>
    <h2>总价：{{totalPrice}}</h2>
  </div>

  <script src="../vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        firstName: 'Lebron',
        lastName: 'James',
        books: [{
            price: 111
          },
          {
            price: 222
          },
          {
            price: 333
          }
        ]
      },
      computed: {
        fullName: function () {
          return this.firstName + '' + this.lastName;
        },
        totalPrice: function () {
          let total = 0;
          for (i = 0; i < this.books.length; i++) {
            total += this.books[i].price;
          }
          return total;
        }
      }
    })
  </script>
</body>
```

**计算属性的效率比方法要高**



## 事件监听 v-on

### v-on

可以给标签**绑定事件**

```html
<body>
  <div id='app'>
    <h2>{{counter}}</h2>
    <button v-on:click='increment()'>+</button>
    <button v-on:click='decrement()'>-</button>
  </div>

  <script src="../vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: 'Hello',
        counter: 0
      },
      methods: {
        increment() {
          this.counter++;
        },
        decrement() {
          this.counter--;
        }
      }
    })
  </script>
</body>
```

语法糖：使用@

```html
<button @click> + </button>
```

### v-on 参数传递问题



```html
<body>

<div id="app">
  <!--1.事件调用的方法没有参数-->
  <button @click="btn1Click()">按钮1</button>
  <button @click="btn1Click">按钮1</button>

  <!--2.在事件定义时, 写方法时省略了小括号, 但是方法本身是需要一个参数的, 这个时候, Vue会默认将浏览器生产的event事件对象作为参数传入到方法-->
  <!--<button @click="btn2Click(123)">按钮2</button>-->
  <!--<button @click="btn2Click()">按钮2</button>-->
  <button @click="btn2Click">按钮2</button>

  <!--3.方法定义时, 我们需要event对象, 同时又需要其他参数-->
  <!-- 在调用方式, 如何手动的获取到浏览器参数的event对象: $event-->
  <button @click="btn3Click(abc, $event)">按钮3</button>
</div>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      abc: 123
    },
    methods: {
      btn1Click() {
        console.log("btn1Click");
      },
      btn2Click(event) {
        console.log('--------', event);
      },
      btn3Click(abc, event) {
        console.log('++++++++', abc, event);
      }
    }
  })

  // 如果函数需要参数,但是没有传入, 那么函数的形参为undefined
  // function abc(name) {
  //   console.log(name);
  // }
  //
  // abc()
</script>

</body>
```

### v-on 修饰符



```html
<body>

<div id="app">
  <!--1. .stop修饰符的使用 阻止事件冒泡-->
  <div @click="divClick">
    aaaaaaa
    <button @click.stop="btnClick">按钮</button>
  </div>

  <!--2. .prevent修饰符的使用 阻止默认行为-->
  <br>
  <form action="baidu">
    <input type="submit" value="提交" @click.prevent="submitClick">
  </form>

  <!--3. .监听某个键盘的键帽-->
  <input type="text" @keyup.enter="keyUp">

  <!--4. .once修饰符的使用 只触发一次-->
  <button @click.once="btn2Click">按钮2</button>
    
  <!--5. .native修饰符的使用 当需要监听组件的原生方法时需要用该修饰符-->
  <back-top @click.native="backClick"></back-top>
</div>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    },
    methods: {
      btnClick() {
        console.log("btnClick");
      },
      divClick() {
        console.log("divClick");
      },
      submitClick() {
        console.log('submitClick');
      },
      keyUp() {
        console.log('keyUp');
      },
      btn2Click() {
        console.log('btn2Click');
      }
    }
  })
</script>

</body>
```



## 条件判断 v-if

if-else

```html
<body>

  <div id="app">
    <h2 v-if="isShow">
      <div>abc</div>
      <div>abc</div>
      <div>abc</div>
      <div>abc</div>
      <div>abc</div>
      {{message}}
    </h2>
    <h2 v-else>isShow 为 false 时显示我</h2>
  </div>

  <script src="../vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: '你好啊',
        isShow: true
      }
    })
  </script>

</body>
```

else-if

```html
<body>

  <div id="app">
    <h2 v-if='score>=90'>优秀</h2>
    <h2 v-else-if='score>=80'>良好</h2>
    <h2 v-else-if='score>=60'>及格</h2>
    <h2 v-else>不及格</h2>
  </div>

  <script src="../vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: '你好啊',
        score: 59
      }
    })
  </script>

</body>
```

v-if 和 v-show的区别

```html
<body>

<div id="app">
  <!--v-if: 当条件为false时, 包含v-if指令的元素, 根本就不会存在dom中-->
  <h2 v-if="isShow" id="aaa">{{message}}</h2>

  <!--v-show: 当条件为false时, v-show只是给我们的元素添加一个行内样式: display: none-->
  <h2 v-show="isShow" id="bbb">{{message}}</h2>
</div>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      isShow: true
    }
  })
</script>

</body>
```



## 循环遍历 v-for

### 遍历数组

```html
<body>

<div id="app">
  <!--1.在遍历的过程中,没有使用索引值(下标值)-->
  <ul>
    <li v-for="item in names">{{item}}</li>
  </ul>

  <!--2.在遍历的过程中, 获取索引值-->
  <ul>
    <li v-for="(item, index) in names">
      {{index+1}}.{{item}}
    </li>
  </ul>
</div>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      names: ['why', 'kobe', 'james', 'curry']
    }
  })
</script>

</body>
```

### 遍历对象

```html
<body>

<div id="app">
  <!--1.在遍历对象的过程中, 如果只是获取一个值, 那么获取到的是value-->
  <ul>
    <li v-for="item in info">{{item}}</li>
  </ul>


  <!--2.获取key和value 格式: (value, key) -->
  <ul>
    <li v-for="(value, key) in info">{{value}}-{{key}}</li>
  </ul>


  <!--3.获取key和value和index 格式: (value, key, index) -->
  <ul>
    <li v-for="(value, key, index) in info">{{value}}-{{key}}-{{index}}</li>
  </ul>
</div>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      info: {
        name: 'why',
        age: 18,
        height: 1.88
      }
    }
  })
</script>

</body>
```

### 状态维护

官方推荐我们在使用v-for时，给对应的元素或组件添加上一个:key属性。

为什么需要这个key属性呢？

这个其实和Vue的虚拟DOM的Diff算法有关系。

这里我们借用[React’s](https://link.zhihu.com/?target=https://calendar.perfplanet.com/2013/diff/)[ diff algorithm](https://link.zhihu.com/?target=https://calendar.perfplanet.com/2013/diff/)中的一张图来简单说明一下：

当某一层有很多相同的节点时，也就是列表节点时，我们希望插入一个新的节点

我们希望可以在B和C之间加一个F，Diff算法默认执行起来是这样的。

即把C更新成F，D更新成C，E更新成D，最后再插入E，是不是很没有效率？

所以我们需要使用key来给每个节点做一个**唯一标识**（因此key必须是一个一一对应的值）

Diff算法就可以正确的识别此节点

找到正确的位置区插入新的节点。

所以一句话，**key**的作用主要是为了**高效的**更新虚拟DOM

![](https://calendar.perfplanet.com/wp-content/uploads/2013/12/vjeux/1.png)

![](https://calendar.perfplanet.com/wp-content/uploads/2013/12/vjeux/2.png)

```html
<div id="app">
  <ul>
    <li v-for="item in letters" :key="item">{{item}}</li> //或者使用item.id
  </ul>
</div>
```

### 数组更新

有些操作数组方法不支持响应式

支持响应式的方法：push，pop，shift，unshift， splice，sort，reverse

注意：不要通过索引的方式修改数组，不支持响应式，用`array.splice(2, 1, 'aaa')`方式修改数组，或者用Vue自带的set方法修改

```html
<body>

<div id="app">
  <ul>
    <li v-for="item in letters">{{item}}</li>
  </ul>
  <button @click="btnClick">按钮</button>
</div>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      letters: ['a', 'b', 'c', 'd']
    },
    methods: {
      btnClick() {
        // 1.push方法
        // this.letters.push('aaa')
        // this.letters.push('aaaa', 'bbbb', 'cccc')

        // 2.pop(): 删除数组中的最后一个元素
        // this.letters.pop();

        // 3.shift(): 删除数组中的第一个元素
        // this.letters.shift();

        // 4.unshift(): 在数组最前面添加元素
        // this.letters.unshift()
        // this.letters.unshift('aaa', 'bbb', 'ccc')

        // 5.splice作用: 删除元素/插入元素/替换元素
        // 删除元素: 第二个参数传入你要删除几个元素(如果没有传,就删除后面所有的元素)
        // 替换元素: 第二个参数, 表示我们要替换几个元素, 后面是用于替换前面的元素
        // 插入元素: 第二个参数, 传入0, 并且后面跟上要插入的元素
        // splice(start)
        // splice(start):
        this.letters.splice(1, 3, 'm', 'n', 'l', 'x')
        // this.letters.splice(1, 0, 'x', 'y', 'z')

        // 5.sort()
        // this.letters.sort()

        // 6.reverse()
        // this.letters.reverse()

        // 注意: 通过索引值修改数组中的元素
        // this.letters[0] = 'bbbbbb';
        // this.letters.splice(0, 1, 'bbbbbb')
        // set(要修改的对象, 索引值, 修改后的值)
        Vue.set(this.letters, 0, 'bbbbbb')
      }
    }
  })


  // function sum(num1, num2) {
  //   return num1 + num2
  // }
  //
  // function sum(num1, num2, num3) {
  //   return num1 + num2 + num3
  // }
  // function sum(...num) {
  //   console.log(num);
  // }
  //
  // sum(20, 30, 40, 50, 601, 111, 122, 33)

</script>

</body>
```



## 表单输入绑定 v-model

### 双向数据绑定原理

v- model其实是一个语法糖，它的背后本质上是包含两个操作：

* v-bind 绑定一个 value 属性
* v-on 指令给当前元素绑定 input  事件，通过 methods 的方法修改参数

```html
<input type="text" v-model="message">
```

等同于

```html
<input type="text" :value="message" @input="$event.target.value">
```

### 基本用法

**v-model 结合 radio 使用**

```html
<body>
  <div id='app'>
    <label for="male">
      <input type="radio" id='male' name='sex' value='男' v-model='sex'>男
    </label>
    <label for="female">
      <input type="radio" id='female' name='sex' value='女' v-model='sex'>女
    </label>
    <h2>性别：{{sex}}</h2>
  </div>

  <script src="../vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: 'Hello',
        sex: ''
      }
    })
  </script>
</body>
```

**v-model 结合 checkbox 使用**

单选

```html
<body>
  <div id='app'>
    <label for="">
      <input type="checkbox" id="liscence" v-model='isAgree'>同意协议
    </label>
    <button :disabled="!isAgree">下一步</button>
    {{isAgree}}
  </div>

  <script src="../vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: 'Hello',
        isAgree: false
      }
    })
  </script>
</body>
```

多选

```html
<body>
  <div id='app'>
    <label for="">
      <input type="checkbox" value="篮球" v-model="hobbies">篮球
      <input type="checkbox" value="足球" v-model="hobbies">足球
      <input type="checkbox" value="羽毛球" v-model="hobbies">羽毛球
      <input type="checkbox" value="乒乓球" v-model="hobbies">乒乓球
    </label>
    {{hobbies}}
  </div>

  <script src="../vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: 'Hello',
        isAgree: false,
        hobbies: []
      }
    })
  </script>
</body>
```

**v-model 结合 select 使用**

```html
<body>
  <div id='app'>
    //单选
    <select name="abc" id="" v-model="fruit">
      <option value="苹果">苹果</option>
      <option value="香蕉">香蕉</option>
      <option value="榴莲">榴莲</option>
      <option value="葡萄">葡萄</option>
    </select>
    {{fruit}}
	//多选
    <select name="abc" id="" v-model="fruits" multiple>
      <option value="苹果">苹果</option>
      <option value="香蕉">香蕉</option>
      <option value="榴莲">榴莲</option>
      <option value="葡萄">葡萄</option>
    </select>
    {{fruits}}
  </div>

  <script src="../vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        fruit: '苹果',
        fruits: []
      }
    })
  </script>
</body>
```

### 值绑定

需要用 v-for 从服务器动态获取值进行显示与绑定

```html
<body>
  <div id='app'>
    <label v-for="item in hobbies" :for="item">
      <input type="checkbox" :value="item" v-model="hobbiesOut">{{item}}
    </label>
    {{hobbiesOut}}
  </div>

  <script src="../vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        hobbies: ['篮球', '足球', '羽毛球'],
        hobbiesOut: []
      }
    })
  </script>
</body>
```

### 修饰符

* lazy: 默认情况下，v-model默认是在input事件中同步输入框的数据的。也就是说，一旦有数据发生改变对应的data中的数据就会自动发生改变。lazy修饰符可以让数据在失去焦点或者回车时才会更新
* number: 默认情况下，在输入框中无论我们输入的是字母还是数字，都会被当做字符串类型进行处理。但是如果我们希望处理的是数字类型，那么最好直接将内容当做数字处理。number修饰符可以让在输入框中输入的内容自动转成数字类型
* trim: 如果输入的内容首尾有很多空格，通常我们希望将其去除；trim修饰符可以过滤内容左右两边的空格

```html
<body>
  <div id='app'>
    <input type="text" v-model.lazy="message">
    <h2>{{message}}</h2>

    <input type="text" v-model.number="age">
    <h2>{{age}} - {{typeof age}}</h2>

    <input type="text" v-model.trim='name'>
    <h2>{{name}}</h2>
  </div>

  <script src="../vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: 'Hello',
        age: 18,
        name: 'zyy'
      }
    })
  </script>
</body>
```



# 组件

## 注册组件基本步骤

分为三步：创建组件构造器、注册组件、使用组件

```html
<body>

<div id="app">
  <!--3.使用组件-->
  <my-cpn></my-cpn>
  <my-cpn></my-cpn>
  <my-cpn></my-cpn>
  <my-cpn></my-cpn>

  <div>
    <div>
      <my-cpn></my-cpn>
    </div>
  </div>
</div>

<my-cpn></my-cpn>

<script src="../js/vue.js"></script>
<script>
  // 1.创建组件构造器对象
  const cpnC = Vue.extend({
    template: `
      <div>
        <h2>我是标题</h2>
        <p>我是内容, 哈哈哈哈</p>
        <p>我是内容, 呵呵呵呵</p>
      </div>
	`
  })

  // 2.注册组件
  Vue.component('my-cpn', cpnC)

  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    }
  })
</script>

</body>
```

步骤解析：

1. Vue.extend():

	* 调用Vue.extend()创建的是一个组件构造器
	* 通常在创建组件构造器时，传入template代表我们自定义组件的模板
	* 该模板就是在使用到组件的地方，要显示的HTML代码
	* 事实上，这种写法在Vue2.x的文档中几乎已经看不到了，它会直接使用下面我们会讲到的语法糖，但是在很多资料还是会提到这种方式，而且这种方式是学习后面方式的基础
2. Vue.component()：

   * 调用Vue.component()是将刚才的组件构造器注册为一个组件，并且给它起一个组件的标签名称
   * p所以需要传递两个参数：1、注册组件的标签名 2、组件构造器
3. 组件必须挂载在某个Vue实例下，否则它不会生效

### 全局组件与局部组件

上述创建方式为全局组件，可以在多个Vue实例中使用，但局部组件只能在一个Vue实例中使用

局部组件的创建方法为：

```html
<body>

  <div id='app'>
    <cpn></cpn>
  </div>

  <div id='app2'>
    <cpn></cpn>
  </div>

  <script src="../vue.js"></script>
  <script>
    const cpnC = Vue.extend({
      template: `
      <div>
        <h2>我是标题</h2>
        <p>我是内容</p>
      </div>
      `
    })
    // 局部组件在创建Vue实例时通过components引入
    const app = new Vue({
      el: '#app',
      data: {
        message: 'Hello',
      },
      components: {
        cpn: cpnC //cpn为使用组件时的标签名
      }
    })

    const app2 = new Vue({
      el: '#app2'
    })
  </script>

</body>
```

### 组件中数据存放

组件中不可以直接使用 Vue 实例中的数据，需要在注册组件时，通过`data(){}`函数，return一个对象来进行数据传递

```html
<template id="cpn">
    <div>
      <h2>{{message}}</h2>
      <p>我是内容,呵呵呵</p>
    </div>
</template>
<script>
Vue.component('cpn', {
      template: '#cpn',
      data() {
        return {
          message: '这里存放组件的数据'
        }
      }
    })
</script>
```



## 父子组件

### 基本使用

示例：

cpn2 为父组件， cpn1 为子组件

* 首先创建两个组件实例

* 在父组件cpn2中通过components注册子组件cpn1
* 在Vue实例中注册父组件cpn2

```html
<body>

  <div id='app'>
    <cpn2></cpn2>
  </div>

  <script src="../vue.js"></script>
  <script>
    const cpnC1 = Vue.extend({
      template: `
      <div>
        <h2>我是标题1</h2>
        <p>我是内容1111111111</p>
      </div>
      `
    })

    const cpnC2 = Vue.extend({
      template: `
      <div>
        <h2>我是标题2</h2>
        <p>我是内容22222222</p>
        <cpn1></cpn1>  
      `,
      components: {
        cpn1: cpnC1
      }
    })

    const app = new Vue({
      el: '#app',
      data: {
        message: 'Hello',
      },
      components: {
        cpn2: cpnC2,
      }

    })
  </script>

</body>
```

**语法糖：**

省去了调用Vue.extend()的步骤，而是可以直接使用一个对象来代替

```html
<body>

<div id="app">
  <cpn1></cpn1>
  <cpn2></cpn2>
</div>

<script src="../js/vue.js"></script>
<script>
  // 1.全局组件注册的语法糖
  // 1.创建组件构造器
  // const cpn1 = Vue.extend()

  // 2.注册组件
  Vue.component('cpn1', {
    template: `
      <div>
        <h2>我是标题1</h2>
        <p>我是内容, 哈哈哈哈</p>
      </div>
    `
  })

  // 2.注册局部组件的语法糖
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    },
    components: {
      'cpn2': {
        template: `
          <div>
            <h2>我是标题2</h2>
            <p>我是内容, 呵呵呵</p>
          </div>
    `
      }
    }
  })
</script>

</body>
```

**模板抽离写法**

```html
<body>

<div id="app">
  <cpn></cpn>
  <cpn></cpn>
  <cpn></cpn>
</div>

<!--1.script标签, 注意:类型必须是text/x-template-->
<!--<script type="text/x-template" id="cpn">-->
<!--<div>-->
  <!--<h2>我是标题</h2>-->
  <!--<p>我是内容,哈哈哈</p>-->
<!--</div>-->
<!--</script>-->

<!--2.template标签-->
<template id="cpn">
  <div>
    <h2>我是标题</h2>
    <p>我是内容,呵呵呵</p>
  </div>
</template>

<script src="../js/vue.js"></script>
<script>

  // 1.注册一个全局组件
  Vue.component('cpn', {
    template: '#cpn'
  })

  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    }
  })
</script>

</body>
```

### 父子组件通信

由于每一个组件相当于一个封闭的空间，因此需要参数传递功能，才能将参数在各个组件之间传递

#### 父=>子 Props

父组件通过 Props 属性向子组件传递参数，下面以 Vue 实例为父组件 cpn 为子组件演示参数传递过程

* 在子组件中通过 props 属性创建数据
  * 可以通过数组`props: ['cmovies', 'cmessage']`
  * 可以通过对象，提供默认值
* 在使用组件时通过属性将子组件中的数据和父组件中数据关联`<cpn :cmessage="message" :cmovies="movies"></cpn>`

```html
<body>

<div id="app">
  <!--<cpn v-bind:cmovies="movies"></cpn>-->
  <!--<cpn cmovies="movies" cmessage="message"></cpn>-->

  <cpn :cmessage="message" :cmovies="movies"></cpn>
</div>

<template id="cpn">
  <div>
    <ul>
      <li v-for="item in cmovies">{{item}}</li>
    </ul>
    <h2>{{cmessage}}</h2>
  </div>
</template>

<script src="../js/vue.js"></script>
<script>
  // 父传子: props
  const cpn = {
    template: '#cpn',
    // props: ['cmovies', 'cmessage'],
    props: {
      // 1.类型限制
      // cmovies: Array,
      // cmessage: String,

      // 2.提供一些默认值, 以及必传值
      cmessage: {
        type: String,
        default: 'aaaaaaaa',
        required: true
      },
      // 类型是对象或者数组时, 默认值必须是一个函数
      cmovies: {
        type: Array,
        default() {
          return []
        }
      }
    },
    data() {
      return {}
    },
    methods: {

    }
  }

  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      movies: ['海王', '海贼王', '海尔兄弟']
    },
    components: {
      cpn
    }
  })
</script>

</body>
```

<strong style="color:red;">注意 props 的驼峰命名</strong>

如果在 props 里使用了驼峰命名

```js
const cpn = {
   template: '#cpn',
   props: {
     childMyMessage: {
       type: String,
       default () {
         return 'a'
       }
     }
   }
}
```

那么在使用组件时，属性要使用`-`连接 `<cpn :child-my-message="message1"></cpn>`

#### 子=>父 自定义事件

通过自定义事件实现子组件向父组件传递数据

* 首先在子组件中定义btnClick事件，获取item数据
* 在btnClick事件中通过`this.$emit('item-click', item)`通过自定义`item-click`事件传递 item 数据
* 在父组件中使用子组件时，监听`item-click`事件，并在父组件中注册`cpnClick`事件进行数据接收，往常未传入实参时，会默认接收到点击事件，但是此处默认接收到 emit 的参数，即 item

```html
<body>

  <div id="app">
    <cpn @item-click="cpnClick"></cpn>
  </div>

  <template id="cpn">
    <div>
      <button v-for="item in categories" @click="btnClick(item)">{{item.name}}</button>
    </div>
  </template>

  <script src="../vue.js"></script>
  <script>
    const cpn = {
      template: "#cpn",
      data() {
        return {
          categories: [{
              id: 'aaa',
              name: '热门推荐'
            },
            {
              id: 'bbb',
              name: '手机数码'
            },
          ]
        }
      },
      methods: {
        btnClick(item) {
          this.$emit('item-click', item);
        }
      },
    }

    const app = new Vue({
      el: '#app',
      data: {
        message: 'hello'
      },
      components: {
        cpn
      },
      methods: {
        cpnClick(item) {
          console.log(item)
        }
      },
    })
  </script>

</body>
```

### 父子组件访问

父子组件互相访问对方

<strong style="color:#ff0000;">ref如果绑定在组件中，那么通过`this.$ref.refname`获取到的是一个组件对象
</strong>
<strong style="color:#ff0000;">
</strong>
<strong style="color:#ff0000;">ref如果绑定在元素中，那么通过`this.$ref.refname`获取到的是一个元素对象</strong>

#### 父访问子 $children $refs

方法一：使用 $children

如果一个子组件使用了 n 次，就会产生 n 个children， 因此在使用`this.$children[0].name`时要指定具体访问哪个，但是一旦后续增加、减少了子组件，就会影响下标，因此不常用

```html
<body>

  <div id="app">
    <cpn></cpn>
    <cpn></cpn>
    <cpn></cpn>
    <button @click="showChildren">点击</button>
  </div>

  <template id="cpn">
    <div>
      {{message}}
    </div>
  </template>

  <script src="../vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {

      },
      components: {
        cpn: {
          template: '#cpn',
          data() {
            return {
              message: '我是子组件',
              name: 'zyy'
            }
          },
          methods: {
            showName() {
              console.log(this.name)
            }
          },
        }
      },
      methods: {
        showChildren() {
          console.log(this.$children[0]);
        }
      },
    })
  </script>

</body>
```

方法二：使用 $refs

需要提前在使用子组件时，添加 ref 属性，只有有了 ref 属性，才可以被`this.$refs`接收到

```html
<div id="app">
    <cpn ref='aaa'></cpn>
    <cpn ref="bbb"></cpn>
    <cpn></cpn>
    <button @click="showChildren">点击</button>
</div>
```

```js
showChildren() {
  console.log(this.$refs.aaa.name);
}
```

#### 子访问父 $parent $root

```html
<body>

  <div id="app">
    <cpn></cpn>
  </div>

  <template id="cpn">
    <div>
      <h2>我是cpn组件</h2>
      <ccpn></ccpn>
    </div>
  </template>

  <template id="ccpn">
    <div>
      <h2>我是子组件</h2>
      <button @click="btnClick">按钮</button>
    </div>
  </template>

  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: '你好啊'
      },
      components: {
        cpn: {
          template: '#cpn',
          data() {
            return {
              name: '我是cpn组件的name'
            }
          },
          components: {
            ccpn: {
              template: '#ccpn',
              methods: {
                btnClick() {
                  // 1.访问父组件$parent
                  console.log(this.$parent);
                  console.log(this.$parent.name);

                  // 2.访问根组件$root
                  // console.log(this.$root);
                  // console.log(this.$root.message);
                }
              }
            }
          }
        }
      }
    })
  </script>

</body>
```



## 插槽

可以对组件的功能进行扩展

### 基本使用

`<slot></slot>`即为插槽，里面可以放默认值

* 如果有默认值，使用组件时显示默认值
* 如果使用组件时传入了其他值，则默认值会被覆盖
* 可以传入多个值

```html
<body>

  <div id="app">
    <cpn></cpn>
    <cpn><span>123</span></cpn>
    <cpn>
      <span>123</span>
      <button>按钮</button>
    </cpn>
  </div>

  <template id="cpn">
    <div>
      <h2>我是组件</h2>
      <slot><button>按钮</button></slot>
    </div>
  </template>

  <script src="../vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        message: '你好啊'
      },
      components: {
        cpn: {
          template: '#cpn'
        }
      }
    })
  </script>

</body>
```

### 具名插槽

```html
 <template id="cpn">
    <div>
      <slot name="left"><span>左边</span></slot>
      <slot name="middle"><span>中间</span></slot>
      <slot name="right"><span>右边</span></slot>
    </div>
 </template>
```

使用

```html
  <div id="app">
    <cpn>
      <span slot="left">修改左边</span>
    </cpn>
    <cpn>
      <button slot="middle">中间</button>
    </cpn>
  </div>
```

### 作用域插槽

父组件想要替换插槽里的标签，但是内容、数据由子组件提供

由于作用域的限制，父组件无法直接访问子组件的数据，需要借助作用域插槽

* 首先在插槽 slot 中添加属性 `:data='pLanguages'`data名字可以随意指定，暴露出pLanguages数据
* 在使用子组件时，添加 template 属性 `slot-scope='slot'`即可在子组件中使用 `slot.data`数据

```html
<body>

  <div id="app">
    <cpn>
      <template slot-scope="slot">
        <span v-for="item in slot.data">{{item}} - </span>
      </template>
    </cpn>
  </div>

  <template id="cpn">
    <div>
      <slot :data="pLanguages">
        <ul>
          <li v-for="item in pLanguages">{{item}}</li>
        </ul>
      </slot>
    </div>
  </template>

  <script src="../vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        message: '你好啊'
      },
      components: {
        cpn: {
          template: '#cpn',
          data() {
            return {
              pLanguages: ['JavaScript', 'Python', 'Swift', 'C++', 'C#', 'JAVA']
            }
          }
        }
      }
    })
  </script>

</body>
```



# 模块化导入导出

**导出**

```js
// 1.导出方式一:
export {
  flag, sum
}

// 2.导出方式二:
export var num1 = 1000;
export var height = 1.88


// 3.导出函数/类
export function mul(num1, num2) {
  return num1 * num2
}

export class Person {
  run() {
    console.log('在奔跑');
  }
}
```

**导入**

```js
// 1.导入的{}中定义的变量
import {flag, sum} from "./aaa.js";

if (flag) {
  console.log('小明是天才, 哈哈哈');
  console.log(sum(20, 30));
}

// 2.直接导入export定义的变量
import {num1, height} from "./aaa.js";

console.log(num1);
console.log(height);

// 3.导入 export的function/class
import {mul, Person} from "./aaa.js";
```

**default导出**

每个文件只能使用一次default导出，导出的对象可以被导入者**自定义名字**

```js
//导出
export default function (argument) {
  console.log(argument);
}
// 导入 export default中的内容
import addr from "./aaa.js";
```

**全部导入**

```js
// 统一全部导入
// import {flag, num, num1, height, Person, mul, sum} from "./aaa.js";
import * as aaa from './aaa.js'

console.log(aaa.flag);
console.log(aaa.height);
```



# webpack

现在的js文件中使用了模块化的方式进行开发，他们可以直接使用吗？不可以

因为如果直接在`index.html`引入这两个js文件，浏览器并不识别其中的模块化代码

另外，在真实项目中当有许多这样的js文件时，我们一个个引用非常麻烦，并且后期非常不方便对它们进行管理

因此，需要使用webpack工具，对多个js文件进行打包

**安装** `npm install webpack@3.6.0 -g`

**打包** `webpack src/main.js dist/bundle.js` 前一部分是需要打包的js文件（入口），后一部分是打包后的js文件（出口），html文件引用打包后的js文件即可

## 配置

如果每次使用webpack的命令都需要写上入口和出口作为参数，就非常麻烦，有没有一种方法可以将这两个参数写到配置中，在运行时，直接读取呢？

创建一个`webpack.config.js`文件

![image-20210616212256933](Vue.js学习笔记.assets/image-20210616212256933.png)

这样一来在终端里直接输入`webpack`即可进行打包

### 局部安装webpack

一个项目往往依赖特定的webpack版本，全局的版本可能很这个项目的webpack版本不一致，导出打包出现问题，所以需要局部安装webpack

* 在文件夹路径下，执行`npm install webpack@3.6.0 --save-dev`
* 通过`node_modules/.bin/webpack`启动 webpack 打包

### package.json中定义启动

每次执行都敲这么一长串有没有觉得不方便呢？我们可以在`package.json`的scripts中定义自己的执行脚本

```js
{
  "name": "meetwebpack",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack"
  },
  "author": "",
  "license": "ISC"
}
```

之后，即可使用`npm run build`执行 webpack 命令

* 首先，会寻找本地的node_modules/.bin路径中对应的命令
* 如果没有找到，会去全局的环境变量中寻找

## Loader

在开发中我们不仅仅有基本的js代码处理，我们也需要加载css、图片，也包括一些高级的将ES6转成ES5代码，将TypeScript转成ES5代码，将scss、less转成css，将.jsx、.vue文件转成js文件等等，对于webpack本身的能力来说，对于这些转化是不支持的，给webpack扩展对应的loader就可以了

使用过程：

* 通过npm安装需要使用的loader
* 在webpack.config.js中的modules关键字下进行配置

### CSS文件处理

首先在 src 文件夹下创建 css 文件。之后在入口文件 main.js 中通过 require 引用

![image-20210616215619514](Vue.js学习笔记.assets/image-20210616215619514.png)

通过 npm 命令安装 loader

```bash
npm install --save-dev css-loader
npm install --save-dev style-loader
```

在webpack.config.js文件中进行配置

```js
const path = require('path')

module.exports = {
  entry: './src/main.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        // css-loader只负责将css文件进行加载
        // style-loader负责将样式添加到DOM中
        // 使用多个loader时, 是从右向左
        use: [ 'style-loader', 'css-loader' ]
      }
    ]
  }
}
```

### less文件处理

* 安装loader  `npm install --save-dev less-loader less`
* 配置

```js
const path = require('path')

module.exports = {
  entry: './src/main.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [ 'style-loader', 'css-loader' ]
      },
      {
        test: /\.less$/,
        use: [{
            loader: "style-loader" // creates style nodes from JS strings
        }, {
            loader: "css-loader" // translates CSS into CommonJS
        }, {
            loader: "less-loader" // compiles Less to CSS
            }]
      }
    ]
  }
}
```

### 图片文件处理

#### url-loader

![image-20210617203457655](Vue.js学习笔记.assets/image-20210617203457655.png)

* 使用 url 引用图片
* `npm install --save-dev url-loader` 安装
* 配置 webpack.config.js 文件

```js
{
        test: /\.(png|jpg|gif)$/,
        use: [
          {
            loader: 'url-loader',
            options: {
              limit: 8192
            }
          }
        ]
}
```

注意此处的 limit 意为大小小于8192的图片可以用 url-loader 转化成 base64 字符串进行显示，大于 limit 的图片将通过 file-loader 进行打包

#### file-loader

* `npm install --save-dev file-loader` 安装，无需配置

* 打包后 dist 文件夹下多以一个图片文件

![image-20210617203950086](Vue.js学习笔记.assets/image-20210617203950086.png)

* 我们可以在options中添加上如下选项：

  * img：文件要打包到的文件夹
  * name：获取图片原来的名字，放在该位置
  * hash:8：为了防止图片名称冲突，依然使用hash，但是我们只保留8位
  * ext：使用图片原来的扩展名

  ![image-20210617204213020](Vue.js学习笔记.assets/image-20210617204213020.png)

* 我们发现图片并没有显示出来，这是因为图片使用的路径不正确.默认情况下，webpack会将生成的路径直接返回给使用者。但是，我们整个程序是打包在dist文件夹下的，所以这里我们需要在路径下再添加一个dist/

![image-20210617204143316](Vue.js学习笔记.assets/image-20210617204143316.png)

### ES6转ES5

使用babel对应的loader即可将ES6转成ES5

* `npm install --save-dev babel-loader@7 babel-core babel-preset-es2015`
* 配置webpack.config.js文件

```js
rules: [
    {
      test: /\.js$/,
      exclude: /(node_modules|bower_components)/,
      use: {
        loader: 'babel-loader',
        options: {
          presets: ['@babel/preset-env']
        }
      }
    }
  ]
```

* 重新打包，查看bundle.js文件



## 配置Vue

我们希望在项目中使用Vuejs，那么必然需要对其有依赖，所以需要先进行安装

* `npm install vue --save`，之后就可以按照之前学习的方式来使用Vue了
* 重新打包，运行程序，但是浏览器中会报错，这个错误说的是我们使用的是runtime-only版本的Vue
* 修改webpack的配置，添加如下内容，即可正常使用

```js
resole: {
    alias: {
        'vue$': 'vue/dist/vue.esm.js'
    }
}
```

##  组件抽离

首先要搞明白el和template的区别

![image-20210703140218379](Vue.js学习笔记.assets/image-20210703140218379.png)

如果Vue实例中同时指定了el和template，那么template模板的内容会替换掉挂载的对应el的模板，这样做之后我们就不需要在以后的开发中再次操作index.html，只需要在template中写入对应的标签即可

但是书写template模板非常麻烦，因此我们需要将template进行抽离

* 首先想到的，是将整个组件抽离到app.js中，之后在main.js中通过`import App from './vue/app.js'`使用App组件，但是在这种文件结构不太好，且没法编写样式

```js
export default {
  template:  `
  <div>
    <h2>{{message}}</h2>
    <button @click="btnClick">按钮</button>
    <h2>{{name}}</h2>
  </div>
  `,
  data() {
    return {
      message: 'Hello Webpack',
      name: 'coderwhy'
    }
  },
  methods: {
    btnClick() {

    }
  }
}
```

* 更好的方法是用.vue文件进行抽离，但是不能直接使用，需要`npm install vue-loader vue-template-compiler --save-dev`安装依赖，并修改webpack.config.js的配置文件，之后就可以使用了

![image-20210703140900757](Vue.js学习笔记.assets/image-20210703140900757.png)

```js
<template>
  <div>
    <h2 class="title">{{message}}</h2>
    <button @click="btnClick">按钮</button>
    <h2>{{name}}</h2>
    <Cpn/>
  </div>
</template>

<script>
  import Cpn from './Cpn.vue'

  export default {
    name: "App",
    components: {
      Cpn
    },
    data() {
      return {
        message: 'Hello Webpack',
        name: 'coderwhy'
      }
    },
    methods: {
      btnClick() {

      }
    }
  }
</script>

<style scoped>
  .title {
    color: green;
  }
</style>
```

通过import导入即可使用该组件，且文件结构和逻辑都很清晰

## Plugin

作用相当于插件

### 横幅BannerPlugin

```js
const webpack = require('webpack')

module.exports = {
    plugins: [
        new webpack.BannerPlugin('最终版权由candy所有')
    ]
}
```

重新打包程序，查看bundle.js文件头部，可以看到版权信息

### 打包html的plugin

在真实发布项目时，发布的是dist文件夹中的内容，但是dist文件夹中如果没有index.html文件，那么打包的js等文件也就没有意义了。所以，我们需要将index.html文件打包到dist文件夹中，这个时候就可以使用HtmlWebpackPlugin插件

HtmlWebpackPlugin插件可以为我们做这些事情：自动生成一个index.html文件(可以指定模板来生成)；将打包的js文件，自动通过script标签插入到body中

* `npm install html-webpack-plugin --save-dev`安装HtmlWebpackPlugin插件

* 使用插件，修改webpack.config.js文件中plugins部分的内容如下：

  ![image-20210629100610167](Vue.js学习笔记.assets/image-20210629100610167.png)

  * 这里的template表示根据什么模板来生成index.html
  * 另外，我们需要删除之前在output中添加的publicPath属性
  * 否则插入的script标签中的src可能会有问题

### js压缩的plugin

项目发布前，要对js等文件进行压缩处理

* `npm install uglifyjs-webpack-plugin@1.1.1 --save-dev`
* 修改webpack.config.js文件，使用插件：

```js
const path = require('path')
const webpack = require('webpack')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const UglifyjsWebpackPlugin = require('uglifyjs-webpack-plugin')

module.exports = {
  ...
  module: {
  	plugins: [
    	new webpack.BannerPlugin('最终版权归candy所有'),
    	new HtmlWebpackPlugin({
      	template: 'index.html'
    	}),
    	new UglifyjsWebpackPlugin()
  	],
}
```



## 搭建本地服务器

webpack提供了一个可选的本地开发服务器，这个本地服务器基于node.js搭建，内部使用express框架，可以实现我们想要的让浏览器自动刷新显示我们修改后的结果。

* 安装`npm install --save-dev webpack-dev-server@2.9.1`
* devserver也是作为webpack中的一个选项，选项本身可以设置如下属性：
  * contentBase：为哪一个文件夹提供本地服务，默认是根文件夹，我们这里要填写./dist
  * port：端口号
  * inline：页面实时刷新
  * historyApiFallback：在SPA页面中，依赖HTML5的history模式

```js
module.exports = {
  ...
  devServer: {
    contentBase: './dist',
    inline: true
  }
}
```

* 在package.json文件中配置scripts，加一个dev，之后就可以用`npm run dev`使用，`--open`表示自动打开

```js
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack",
    "dev": "webpack-dev-server --open"
  },
```



# 脚手架

安装`npm install -g @vue/cli`

上面安装的是Vue CLI3的版本，如果需要想按照Vue CLI2的方式初始化项目时不可以的。

有时需要用CLI2，因此也需要拉取CLI2模板`npm install -g @vue/cli-init`

Vue CLI2初始化项目`vue init webpack my-project`

Vue CLI3初始化项目`vue create my-project`

## CLI2

<img src="Vue.js学习笔记.assets/image-20210701210532371.png" alt="image-20210701210532371" style="zoom:150%;" />

### 目录结构

![image-20210701214813522](Vue.js学习笔记.assets/image-20210701214813522.png)

### Runtime-compiler 和 Runtime-only 的区别

![image-20210703131331034](Vue.js学习笔记.assets/image-20210703131331034.png)![image-20210703131351691](Vue.js学习笔记.assets/image-20210703131351691.png)

Vue程序运行过程：

![image-20210703133059630](Vue.js学习笔记.assets/image-20210703133059630.png)

runtime-compiler编译过程：template -> ast -> render -> vdom -> UI

runtime-only编译过程：render -> vdom -> UI

对于每一个.vue文件（即组件）,Vue在编译的时候都会将template编译好，直接输出一个对象，对象里包含render方法，因此我们没有必要每次都通过template -> ast -> render步骤，所以使用runtime-only可以节省空间

render函数的使用方法：

![image-20210703141907592](Vue.js学习笔记.assets/image-20210703141907592.png)

![image-20210703141915893](Vue.js学习笔记.assets/image-20210703141915893.png)

## CLI3

![image-20210703160351246](Vue.js学习笔记.assets/image-20210703160351246.png)

### 目录结构

![image-20210703160358414](Vue.js学习笔记.assets/image-20210703160358414.png)

### 配置文件查看与修改

* 可以通过执行`vue ui`命令，通过ui的方式进行查看与修改

* CLI2的webpack配置被隐藏在了node_modules文件夹里

  ![image-20210703171413263](Vue.js学习笔记.assets/image-20210703171413263.png)

* 如果有配置文件需要自己修改，需要创建一个`vue.config.js`文件，名字必须是这个，在其中自定义配置





# Vue-router

前端路由是通过一次请求资源，返回所有数据，通过js代码决定显示什么，由前端配置url，核心是改变URL，但是页面不进行整体的刷新

## 前端路由的规则

### URL的hash 

* URL的hash也就是锚点(#), 本质上是改变window.location的href属性.
* 我们可以通过直接赋值location.hash来改变href, 但是页面不发生刷新

![image-20210706171010402](Vue.js学习笔记.assets/image-20210706171010402.png)

### history

* history接口是HTML5新增的, 它有五种模式改变URL而不刷新页面
* history.pushState()

![image-20210706171052907](Vue.js学习笔记.assets/image-20210706171052907.png)

* history.replaceState()

![image-20210706171123806](Vue.js学习笔记.assets/image-20210706171123806.png)

* history.go()

![image-20210706171141174](Vue.js学习笔记.assets/image-20210706171141174.png)

## 基础

### 安装和配置

* `npm install vue-router --save`

* 创建router文件夹，在其中创建index.js文件，编写如下内容，在routers里配置路由映射关系

```js
import Vue from 'vue'
import VueRouter from 'vue-router'

// 1.通过Vue.use(插件)，安装插件
Vue.use(VueRouter);

// 2.创建VueRouter对象
const routes = [

]

const router = new VueRouter({
  routes
})

// 3.将Router对象传入到Vue实例中
export default router

```

* 在main.js中进行挂载

```js
import Vue from 'vue'
import App from './App'
import router from './router'

Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  render: h => h(App)
})
```

### 使用

* 在components文件夹中创建路由组件

![image-20210706212722053](Vue.js学习笔记.assets/image-20210706212722053.png)

* 配置组件和路径的映射关系

![image-20210706212744994](Vue.js学习笔记.assets/image-20210706212744994.png)

* 使用路由

![image-20210706212800431](Vue.js学习笔记.assets/image-20210706212800431.png)

Vue默认使用hash规则，如果想要使用history，则需要修改

```js
const router = new VueRouter({
  routes,
  mode: 'history'
})
```

#### router-link

* <router-link>: 该标签是一个vue-router中已经内置的组件, 它会被渲染成一个<a>标签，如果不想渲染成<a>标签，可以添加tag属性`<router-link to="/about" tag="button">关于</router-link>`

* 如果不希望返回，使用replace模式，则`<router-link to="/home" replace>首页</router-link>`

* <router-view>: 该标签会根据当前的路径, 动态渲染出不同的组件.

* 网页的其他内容, 比如顶部的标题/导航, 或者底部的一些版权信息等会和<router-view>处于同一个等级.

* 在路由切换时, 切换的是<router-view>挂载的组件, 其他内容不会发生改变
* 通过router-link选中的标签会有一个router-active-class属性，如果想改变class的名字，可以通过`<router-link to="/about" tag="button" active-class="active">关于</router-link>`改变，或者通过

![image-20210706215519304](Vue.js学习笔记.assets/image-20210706215519304.png)

#### 通过代码跳转

通过this指针自带的方法$router.push进行跳转，同样，也可以使用replace方法

```js
<template>
  <div id="app">
    <router-view></router-view>
    <button @click="homeClick">首页</button>
    <button @click="aboutClick">关于</button>
  </div>
</template>

<script>
export default {
  name: "App",
  methods: {
    homeClick() {
      this.$router.push("/home");
      console.log("homeclick");
    },
    aboutClick() {
      this.$router.push("/about");
      console.log("aboutClick");
    },
  },
};
</script>

<style>
</style>
```

### 动态路由

在某些情况下，一个页面的path路径可能是不确定的，比如我们进入用户界面时，希望是如下的路径：

* /user/aaaa或/user/bbbb
* 除了有前面的/user之外，后面还跟上了用户的ID
* 这种path和Component的匹配关系，我们称之为动态路由(也是路由传递数据的一种方式)

步骤如下：

* 首先我们创建一个User.vue文件，并在index.js中配置动态路由映射关系，冒号表示这是一个变量

```js
const routes = [{
    path: '/',
    redirect: '/home'
  },
  {
    path: '/home',
    component: Home
  },
  {
    path: '/about',
    component: About
  },
  {
    path: '/user/:userId',
    component: User
  }
]
```

* 之后在App.vue文件中指定data中userId的值，并在router-link中进行拼接，即可跳转到动态的url地址

```html
<template>
  <div id="app">
    <router-link to="/home">首页</router-link>
    <router-link to="/about">关于</router-link>
    <router-link :to="'/user/' + userId">用户</router-link>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      userId: "zhangsan",
    };
  },
};
</script>

<style>
</style>
```

* 下面需要考虑的问题是，对于不同的动态url，如何显示相应的userId呢？具体的做法是，在User.vue文件中，通过`this.$route`对象，这个`$route`对象是当前活跃的路由，获取动态的userId，这样就可以将userId显示在页面上。

```html
<template>
  <div>
    <h2>我是用户</h2>
    <p>我是用户内容</p>
    <h2>{{ userId }}</h2>
  </div>
</template>

<script>
export default {
  name: "User",
  computed: {
    userId() {
      return this.$route.params.userId;
    },
  },
};
</script>

<style>
</style>
```



## 进阶

### 路由懒加载

当打包构建应用时，Javascript 包会变得非常大，影响页面加载。

如果我们能把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应组件，这样就更加高效了

路由懒加载的主要作用就是将路由对应的组件打包成一个个的js代码块，只有在这个路由被访问到的时候, 才加载对应的组件

路由懒加载只需要在index.js中，将各个组件引用的格式进行改变即可：

```js
import Home from '../components/Home'
import About from '../components/About'
import User from '../components/User'
//改为如下的形式
const Home = () => import('../components/Home')
const About = () => import('../components/About')
const User = () => import('../components/User')
```

![image-20210707225239581](Vue.js学习笔记.assets/image-20210707225239581.png)

webpack打包后，会将不同的组件打包成不同的js文件

### 路由嵌套使用

比如在home页面中, 我们希望通过/home/news和/home/message访问一些内容

路由和组件的关系如下：

![image-20210707233231431](Vue.js学习笔记.assets/image-20210707233231431.png)

实现嵌套路由有两个步骤:

* 创建对应的子组件, 并且在路由映射中配置对应的子路由，在home路径下，通过添加children数组

![image-20210707234100618](Vue.js学习笔记.assets/image-20210707234100618.png)

![image-20210707234114610](Vue.js学习笔记.assets/image-20210707234114610.png)

* 在组件内部使用<router-view>标签

![image-20210707234136560](Vue.js学习笔记.assets/image-20210707234136560.png)

![image-20210707234141064](Vue.js学习笔记.assets/image-20210707234141064.png)

```js
const routes = [{
    path: '/',
    redirect: '/home',

  },
  {
    path: '/home',
    component: Home,
    children: [{
        path: '',
        redirect: 'news'
      },
      {
        path: 'news',
        component: HomeNews
      },
      {
        path: 'message',
        component: HomeMessage
      }
    ]
  },
]
```

```html
<template>
  <div>
    <h2>我是首页</h2>
    <p>我是首页内容</p>
    <router-link to="/home/message">消息</router-link>
    <router-link to="/home/news">新闻</router-link>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: "Home",
};
</script>

<style>
</style>
```

### 参数传递

有时候url需要携带一些query数据，如何将query数据传递过去呢？

* 创建新的组件Profile.vue
* 配置路由映射
* 添加跳转的router-link，注意此时要通过对象的方式，指定path和query数据

```js
<router-link :to="{ path: '/profile', query: { name: 'zhangsan' } }">档案</router-link>
```

* 之后可以在组件中通过`$route.query`来获取query

```js
<template>
  <div>
    <h2>我是profile</h2>
    <h2>{{ $route.query }}</h2>
  </div>
</template>

<script>
export default {
  name: "Profile",
};
</script>

<style>
</style>
```

还可以通过`this.$router.push()`进行路由跳转和参数传递

```html
<template>
  <div id="app">
    <button @click="profileClick">档案</button>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: "App",
  methods: {
    profileClick() {
      this.$router.push({
        path: "/profile",
        query: { name: "zhangsan" },
      });
    },
  },
};
</script>

<style>
</style>
```

### 导航守卫

导航守卫主要用来监听监听路由的进入和离开的

考虑一个需求：在一个SPA应用中, 如何改变网页的标题呢?

可以使用导航守卫，在每一次路由改变时，执行钩子函数，vue-router提供了beforeEach和afterEach的钩子函数, 它们会在路由即将改变前和改变后触发

```js
router.beforeEach((to, from, next) => {
  window.document.title = to.meta.title
  next()
})
```

每个守卫方法接收三个参数：

- `to: Route`: 即将要进入的目标 [路由对象](https://router.vuejs.org/zh/api/#路由对象)
- `from: Route`: 当前导航正要离开的路由
- `next: Function`: 一定要调用该方法来 **resolve** 这个钩子。执行效果依赖 `next` 方法的调用参数。
  - `next()`: 进行管道中的下一个钩子。如果全部钩子执行完了，则导航的状态就是 **confirmed** (确认的)。
  - `next(false)`: 中断当前的导航。如果浏览器的 URL 改变了 (可能是用户手动或者浏览器后退按钮)，那么 URL 地址会重置到 `from` 路由对应的地址。
  - `next('/')` 或者 `next({ path: '/' })`: 跳转到一个不同的地址。当前的导航被中断，然后进行一个新的导航。你可以向 `next` 传递任意位置对象，且允许设置诸如 `replace: true`、`name: 'home'` 之类的选项以及任何用在 [`router-link` 的 `to` prop](https://router.vuejs.org/zh/api/#to) 或 [`router.push`](https://router.vuejs.org/zh/api/#router-push) 中的选项。
  - `next(error)`: (2.4.0+) 如果传入 `next` 的参数是一个 `Error` 实例，则导航会被终止且该错误会被传递给 [`router.onError()`](https://router.vuejs.org/zh/api/#router-onerror) 注册过的回调。

**确保 `next` 函数在任何给定的导航守卫中都被严格调用一次。它可以出现多于一次，但是只能在所有的逻辑路径都不重叠的情况下，否则钩子永远都不会被解析或报错**

同样的，还有**全局后置钩子、全局解析守卫**

如果想单独对某一路由配置守卫，有**路由独享守卫**

你可以在路由配置上直接定义 `beforeEnter` 守卫：

```js
const router = new VueRouter({
  routes: [
    {
      path: '/foo',
      component: Foo,
      beforeEnter: (to, from, next) => {
        // ...
      }
    }
  ]
})
```

这些守卫与全局前置守卫的方法参数是一样的

### keep-alive

keep-alive 是 Vue 内置的一个组件，可以使被包含的组件保留状态，或避免重新渲染

一般我们从一个路由跳转到另一个路由，组件都会被销毁，但是keep-alive可以避免销毁，保留状态，使用方法为：

```html
<keep-alive>
   <router-view></router-view>
</keep-alive>
```

将`router-view`标签包含在`keep-alive`标签内即可

有了keep-alive，我们多了两个生命周期函数`activated`和`deactivated`，可以用于判断当前组件处于活跃/非活跃状态，可以通过生命周期函数`created`和`destroyed`在创建和销毁时执行操作

现在有一个问题，如果想指定一个组件不被keep-alive约束，离开即销毁，该怎么操作呢？

* exclude：字符串或正则表达式，任何匹配的组件都不会被缓存

```html
<keep-alive exclude="Profile,User">
   <router-view></router-view>
</keep-alive>
```

* include：字符串或正则表达，只有匹配的组件会被缓存

```html
<keep-alive include="Profile,User">
   <router-view></router-view>
</keep-alive>
```

<strong style="color:#ff0000;">**注意Profile和User之间的逗号，不能有空格**</strong>



# Vuex

Vuex 是一个专为 Vue.js 应用程序开发的**状态管理模式**

**状态管理模式、集中式存储管理**可以简单的将其看成把需要多个组件共享的变量全部存储在一个对象里面。然后，将这个对象放在顶层的Vue实例中，让其他组件可以使用。则多个组件就可以共享这个对象中的所有变量属性。

<img src="https://vuex.vuejs.org/flow.png" style="zoom:33%;" />

* State：是我们的状态。（姑且可以当做就是data中的属性）

* View：视图层，可以针对State的变化，显示不同的信息

* Actions：主要是用户的各种操作：点击、输入等等，会导致状态的改变

![](https://vuex.vuejs.org/vuex.png)

## State

需求是定义一个counter变量，在父组件和子组件中都可以对其进行修改

* 首先`npm install vuex --save`安装插件

* 在src文件夹中建立一个store文件夹，建立index.js文件，大致和vue-router相同

```js
import Vuex from 'vuex'
import Vue from 'vue'


//1.安装插件
Vue.use(Vuex)

//2.创建对象
const store = new Vuex.Store({
  state: {
    counter: 1000
  },
  mutations: {

  },
  actions: {

  },
  getters: {

  },
  modules: {

  }
})

//3.导出store对象
export default store
```

* 在main.js中进行挂载

```js
import Vue from 'vue'
import App from './App'
import router from './router'
import store from './store'

Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  store,
  render: h => h(App)
})
```

* 随后在任何组件中都和通过`$store.state.counter`对此状态进行访问

```html
<template>
  <div>
    <h2>{{ $store.state.counter }}</h2>
  </div>
</template>

<script>
export default {
  name: "HelloVuex",
};
</script>

<style>
</style>
```

## Getters

有时候，我们需要从store中获取一些state处理后的状态，则需要通过getters（类似于计算属性）

在state中定义一个students数组，存放一些学生信息

* 需求为获取年龄大于20的学生，在getters中定义方法，return通过filter过滤后的数组
* 需求为获取年龄大于20的学生的人数，此时我们传入state和getters两个参数，调用第一个定义的getters，再获取它的length属性
* 需求为获取年龄大于age的学生，return一个函数，传入age参数

```js
  getters: {
    morethan20(state) {
      return state.students.filter(s => s.age > 20)
    },
    morethan20Length(state, getters) {
      return getters.morethan20.length
    },
    morethanAge(state, getters) {
      return function (age) {
        return state.students.filter(s => s.age > age)
      }
    },

  },
```

```html
    <h2>{{ $store.getters.morethan20 }}</h2>
    <h2>{{ $store.getters.morethan20Length }}</h2>
    <h2>{{ $store.getters.morethanAge(23) }}</h2>
```

## Mutations

如果需要定义一些方法进行状态的改变，则需要在mutations中进行定义，下面以改变counter为例

* 在mutaions中定义增加和减少，需要**传入state变量**

```js
const store = new Vuex.Store({
  state: {
    counter: 1000
  },
  mutations: {
    increment(state) {
      state.counter++;
    },
    decrement(state) {
      state.counter--;
    }
  },
})
```

* 在组件方法中定义两个点击事件，在点击事件中通过`this.$store.commit("increment")`进行提交，完成增加或减少动作

```html
<template>
  <div id="app">
    <h2>{{ message }}</h2>
    <h2>{{ $store.state.counter }}</h2>
    <button @click="addition">+</button>
    <button @click="substraction">-</button>
    <hello-vuex></hello-vuex>
  </div>
</template>

<script>
import HelloVuex from "./components/HelloVuex.vue";

export default {
  name: "App",
  components: {
    HelloVuex,
  },
  data() {
    return {
      message: "App组件",
    };
  },
  methods: {
    addition() {
      this.$store.commit("increment");
    },
    substraction() {
      this.$store.commit("decrement");
    },
  },
};
</script>

<style>
</style>

```

### 参数传递

在通过mutation更新数据的时候, 有可能我们希望携带一些额外的参数，参数被称为是mutation的载荷(Payload)

mutations中代码：

* 同时传入state和需要的参数
* 如果参数不唯一，可以以对象的形式传递参数，再从对象中取出相关的信息

```js
mutations: {
    addCount(state, num) {
      state.counter = state.counter + num
    },
    addStu(state, obj) {
      state.students.push(obj)
    }
  },
```

App中代码：

```js
methods: {
    addCount(num) {
      this.$store.commit("addCount", num);
    },
    addStu() {
      const obj = { id: 123, name: "alex", age: 23 };
      this.$store.commit("addStu", obj);
    },
  },
```

```html
<template>
  <div id="app">
    <h2>{{ $store.state.students }}</h2>
    <button @click="addCount(5)">+5</button>
    <button @click="addStu">addStu</button>
  </div>
</template>
```

还有另外一种提交方式：

```js
methods: {
    addCount(num) {
      this.$store.commit({
          type: 'addCount',
          num,
      });
    },
  },
```

```js
mutations: {
    addCount(state, payload) {
      state.counter = state.counter + payload.num
    },
  },
```

此时传入到mutations中的是一个对象，要从这个对象把num取出来

### 响应规则

Vuex的store中的state是响应式的, 当state中的数据发生改变时, Vue组件会自动更新，这就要求我们必须遵守一些Vuex对应的规则：

* 提前在store中初始化好所需的属性
* 当给state中的对象添加新属性时, 使用下面的方式：
  * 使用`Vue.set(obj, 'newProp', 123)`
  * 用新对象给旧对象重新赋值

否则，数据更新后不会被加入到响应式系统

举例，在state中添加一个info对象，想要给它添加一个address属性

```js
  state: {
    info: {
      name: 'Kobe',
      age: '23',
      skill: 'basketball'
    }
  }
```

```js
  methods: {
    addProperty() {
      this.$store.commit("addPro");
    },
  },
```

```js
  mutations: {
    addPro(state) {
      Vue.set(state.info, 'address', '洛杉矶')//必须用这种方式添加
      Vue.delete(state.info, 'skill')//通过这种方式删除
      //通过普通的对象添加、删除属性的方式无法保证响应式
    }
  },
```

### 常量类型

在mutation中, 我们定义了很多事件类型(也就是其中的方法名称)，当我们的项目增大时, Vuex管理的状态越来越多, 需要更新状态的情况越来越多, 那么意味着Mutation中的方法越来越多，方法过多, 使用者需要花费大量的经历去记住这些方法, 甚至是多个文件间来回切换, 查看方法名称, 甚至如果不是复制的时候, 可能还会出现写错的情况，因此可以创建一个文件: mutation-types.js, 并且在其中定义我们的常量

![image-20210806163317291](Vue.js学习笔记.assets/image-20210806163317291.png)

![image-20210806163321959](Vue.js学习笔记.assets/image-20210806163321959.png)

![image-20210806163330965](Vue.js学习笔记.assets/image-20210806163330965.png)

## Actions

Mutation中不能进行异步操作，如果要在Vuex中进行一些异步操作, 比如网络请求，则需要用到actions，基本使用代码如下：

* 首先在mutations中定义事件
* 在actions中定义事件，传入context参数，并且把异步代码放到actions中，进行提交

```js
const store = new Vuex.Store({
  state: {
    info: {
      name: 'Kobe',
      age: '23',
      skill: 'basketball'
    }
  },
  mutations: {
    updateInfo(state) {
      Vue.set(state.info, 'address', '洛杉矶')
    }
  },
  actions: {
    aupdateInfo(context) {
      setTimeout(() => {
        context.commit('updateInfo')
      }, 2000)
    }
  },
})
```

* 在App中对actions中的方法进行提交

```js
  methods: {
    updateInfo() {
      this.$store.dispatch("aupdateInfo");
    },
  }
```

相当于绕了一个弯，先提交actions，再在action中提交mutations，完成异步操作

在Action中, 我们可以将异步操作放在一个Promise中, 并且在成功或者失败后, 调用对应的resolve或reject

```js
  actions: {
    aupdateInfo(context, payload) {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          context.commit('updateInfo')
          console.log(payload)
          resolve('111111111111')
        }, 2000)
      })
    }
  },
```

```js
  methods: {
    updateInfo() {
      this.$store.dispatch("aupdateInfo", "i'm the message").then((res) => {
        console.log("里面完成了提交");
        console.log(res);
      });
    },
  },
```

## Modules

Module是模块的意思，Vue使用单一状态树,那么也意味着很多状态都会交给Vuex来管理，当应用变得非常复杂时,store对象就有可能变得相当臃肿，为了解决这个问题，Vuex允许我们将store分割成模块(Module)，而每个模块拥有自己的state、mutation、action、getters等

* 首先定义module对象，并在store中注册
* 访问state里对象的时候要先通过模块a，再进行访问
* 同样可以定义mutations和getters，并且依然通过`this.$store`进行直接调用
* 使用getters时，可以携带第三个参数`rootState`，用以访问根store中的state对象

```js
const moduleA = {
  state: {
    name: 'zhangsan'
  },
  mutations: {
    updateName(state, payload) {
      state.name = payload
    }
  },
  getters: {
    fullname1(state) {
      return state.name + '11111'
    },
    fullname2(state, getters) {
      return getters.fullname1 + '2222'
    },
    fullname3(state, getters, rootState) {
      return getters.fullname2 + rootState.counter
    }
  },
  actions: {

  }

}


const store = new Vuex.Store({
  state: {
    counter: 1000,
  },
  mutations: {

  },
  actions: {

  },
  getters: {

  },
  modules: {
    a: moduleA
  }
})
```

```html
<h2>{{ $store.state.a.name }}</h2>
<button @click="updateName('lisi')">修改名字</button>
<h2>{{ $store.getters.fullname1 }}</h2>
<h2>{{ $store.getters.fullname2 }}</h2>
<h2>{{ $store.getters.fullname3 }}</h2>


<script>
import HelloVuex from "./components/HelloVuex.vue";

export default {
  name: "App",
  components: {
    HelloVuex,
  },
  data() {
    return {
      message: "App组件",
      counter: 0,
    };
  },
  methods: {
    updateName(name) {
      this.$store.commit("updateName", name);
    },
  },
};
</script>
```



# Axios

Axios是用于发送异步的网络请求，主要有以下几种API

* axios(config)
* axios.request(config)
* axios.get(url[, config])
* axios.delete(url[, config])
* axios.head(url[, config])
* axios.post(url[, data[, config]])
* axios.put(url[, data[, config]])
* axios.patch(url[, data[, config]])



## 基本使用

首先要先通过`npm install axios --save`安装axios

```js
import Vue from 'vue'
import App from './App'
import axios from 'axios'

Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  render: h => h(App)
})

//设定默认配置信息
//axios.defaults.baseURL = 'http://123.207.32.32:8000'
//axios.defaults.timeout = 5000


//get请求
axios.get('http://123.207.32.32:8000/home/multidata')
.then({
    console.log(res)
})

//axios支持promise，可以直接调用then
axios({
  url: 'http://123.207.32.32:8000/home/multidata',
}).then(res => {
  console.log(res);
})

//axios携带参数，可以用params，也可以直接放到url里
axios({
  url: 'http://123.207.32.32:8000/home/data',
  params: {
    type: 'pop',
    page: 1
  }
}).then(res => {
  console.log(res);
})

//发送并发请求
axios.all([axios({
  url: 'http://123.207.32.32:8000/home/multidata'
}), axios({
  url: 'http://123.207.32.32:8000/home/data',
  params: {
    type: 'sell',
    page: 3
  }
})]).then(results => {
  console.log(results);
})
//也可以写成
axios.all([axios({
  url: 'http://123.207.32.32:8000/home/multidata'
}), axios({
  url: 'http://123.207.32.32:8000/home/data',
  params: {
    type: 'sell',
    page: 3
  }
})]).then(axios.spread((res1, res2) => {
  console.log(res1);
  console.log(res2);
}))

```

## 封装

有时候不同的请求需要不同的baseUrl，所以我们可以创建多个axios实例

```js
const instance1 = axios.create()
instance1.defaults.baseURL = 'http://152.136.185.210:7878/api/m5'
instance1({
  url: '/home/multidata'
}).then(res => {
  console.log(res);
})
```

首先可以通过回调函数进行封装，创建一个networks文件夹，里面创建一个requests.js文件

```js
import axios from 'axios'

export function requests(config) {
  const instance1 = axios.create({
      baseURL: 'http://152.136.185.210:7878/api/m5',
      timeout: 5000
  })

  instance1(config.url).then(res => {
    config.success(res)
  }, err => {
    config.failure(err)
  })
}
```

使用：

```js
import {
  requests
} from "./networks/requests";

requests({
  url: "/home/multidata",
  success(res) {
    console.log(res);
    this.message = res;
  },
  failure(err) {
    console.log(err);
  },
});
```

此时，requests.js文件还可以进一步封装，因为axios对象本身就支持promise，所以可以直接将其返回

```js
export function requests(config) {
  const instance1 = axios.create({
    baseURL: 'http://152.136.185.210:7878/api/m5',
    timeout: 5000
  })

  return instance1(config)
}
```

使用：

```js
requests({
  url: "/home/multidata",
}).then(res => {
  console.log(res);
}, err => {
  console.log(err);
})
```

## 拦截器

有时候需要对网络请求和响应进行拦截，则需要用到拦截器

```js
//请求拦截
  instance1.interceptors.request.use(config => {
    console.log(config);

    //拦截过后需要再把config重新return回去，请求才能继续
    return config
  }, err => {
    console.log(err);
  })

  //响应拦截
  instance1.interceptors.response.use(res => {
    console.log(res);
    return res.data
  }, err => {
    console.log(err);
  })
```



# 项目积累

## 事件总线

当涉及到非父子组件之间的通信时，需要用到事件总线

* 在main.js文件中`Vue.prototype.$bus = new Vue()`
* `this.$bus.$emit('事件名称',参数)`
* `this.$bus.$on('事件名称',回调函数(参数))`

## 防抖函数

对于refresh非常频繁的问题，进行防抖操作

* 防抖debounce/节流throttle
* 防抖函数起作用过程：
  * 如果直接执行refresh，那么会进行很多次
  * 可以将refresh传入到debounce函数中，生成一个新的函数，通过定时器判断

```js
//防抖函数定义
debounce(func, delay) {
        let timer = null

        return function (...args) {
          if (timer) clearTimeout(timer)
          timer = setTimeout(() => {
            func.apply(this, args)
          }, delay);
        }
      }

//使用
mounted() {
      const refresh = this.debounce(this.$refs.scroll.refresh, 500)
      this.$bus.$on('itemImageLoad', () => {
        refresh()
      })
    },
```

## 对话框组件 CDialog

对话框组件，用于弹出对话框，主要由以下**三部分构成**：

* 头部，传入左上角头部显示文字
* 内容，内置一个 slot ，可以放入 input 组件，也可以放入文字
* 按钮
  * 取消按钮
  * slot 自定义按钮
  * 确认按钮

**运行逻辑：**

* 定义 dialogShow 变量，用于控制组件是否显示
* 通过 watch 功能监视 dialogShow 变量的改变，可以添加 / 删除该对话框元素
* 定义 show hide 方法改变 dialogShow 变量值
* 定义 cancel confirm 方法用于按钮 click



## Vue.extend 和 $mount

* Vue.extend 用于创建一个组件构造器

```js
// 创建构造器
var Profile = Vue.extend({
  template: '<p>{{firstName}} {{lastName}} aka {{alias}}</p>',
  data: function () {
    return {
      firstName: 'Walter',
      lastName: 'White',
      alias: 'Heisenberg'
    }
  }
})
```

* 创建好构造器后，实例化组件，并通过 $mount 挂载到页面中，如果 $mount 没有传参，模板将被渲染为文档之外的的元素，必须使用原生 DOM API 把它插入文档中

```js
// 创建 Profile 实例，并挂载到一个元素上。
new Profile().$mount('#mount-point')
```



## 插件

### 插件与组件的区别

组件 (Component) 是用来构成你的 App 的**业务模块**，它的目标是 `App.vue`

插件 (Plugin) 是用来增强你的技术栈的**功能模块**，它的目标是 Vue 本身

插件可以实现的功能有以下几种：

1. 添加全局方法或者 property。如：[vue-custom-element](https://github.com/karol-f/vue-custom-element)
2. 添加全局资源：指令/过滤器/过渡等。如 [vue-touch](https://github.com/vuejs/vue-touch)
3. 通过全局混入来添加一些组件选项。如 [vue-router](https://github.com/vuejs/vue-router)
4. 添加 Vue 实例方法，通过把它们添加到 `Vue.prototype` 上实现。
5. 一个库，提供自己的 API，同时提供上面提到的一个或多个功能。如 [vue-router](https://github.com/vuejs/vue-router)

自定义插件需要以下几个步骤：

* 暴露一个 install 方法，第一个参数是 vue 构造器，第二个参数 options 可选

```js
MyPlugin.install = function (Vue, options) {
    
}
```

* 在 install 函数中可以自定义需要实现的功能（下面的 CToast 插件添加了 Vue 实例方法）
* 在 main.js 中引入插件，并 Vue.use(MyPlugin)

### CToast插件

弹窗工具，用于弹出提示并在一定时间后自动消失

* 首先创建 CToast.vue 文件，内置一个可以显示文字的 div, 并通过 visible 变量控制其显示与否
* 创建 index.js 文件，将其插件化，挂载到 Vue 原型链上，以便于调用，具体方法如下
  * 创建一个 cToast 对象，并添加 install 方法，当use插件时，会自动调用该方法
  * 向 Vue 原型链中添加新的实例方法 $cToast，<strong style="color:red;">此时 cToast 没有注册组件，没有实例化的，也没有挂载，所以要完成上述任务</strong>
    * 使用 Vue.extend(TempToast) 创建一个组件构造器
    * 将其实例化，并传入新的 data 数据
    * 将实例挂载在到 body 上，如果 $mount 没有传参，模板将被渲染为文档之外的的元素，必须使用原生 DOM API 把它插入文档中
* 最后在 main.js 中通过 Vue.use(cToast) 使用插件

参考资料：https://blog.csdn.net/wucan111/article/details/107687047/

```js
import TempToast from './CToast'

let showToast = false
let time

const cToast = {
  install(Vue, options) {
    let opt = TempToast.data()

    Vue.prototype.$cToast = (message, position) => {
      // 清除之前的定时器
      if (showToast) {
        clearTimeout(time)
        instance.vm.visible = showToast = false
        document.body.removeChild(instance.vm.$el)
      }

      // 根据传入的值修改 message 和 position
      if (message) {
        opt.message = message
      }
      if (position) {
        opt.position = position
      }

      // 创建一个子类
      const TempToastConstructor = Vue.extend(TempToast)
      // 将子类实例化，并传入新的 data 数据
      let instance = new TempToastConstructor({
        data: opt
      })
      // 将实例挂载在到 body 上，如果 $mount 没有传参，模板将被渲染为文档之外的的元素，必须使用原生 DOM API 把它插入文档中
      instance.vm = instance.$mount()
      document.body.appendChild(instance.vm.$el)
      console.log(1);

      // 设定定时器
      time = setTimeout(function () {
        instance.vm.visible = showToast = false
        document.body.removeChild(instance.vm.$el)
        console.log(2);
      }, opt.duration)
    }
  }
}

export default cToast
```



## 渲染函数 render

### 基本原理

有时候我们不想通过 template 模板字符串生成HTML，那么可以使用渲染函数 render 来生成，如果 render 存在，则 template 会失效

一个浅显的例子，如果我们希望根据传入的 level 值，生成对应标题的级别，常规的模板字符串需要这么写：

```html
<script type="text/x-template" id="anchored-heading-template">
  <h1 v-if="level === 1">
    <slot></slot>
  </h1>
  <h2 v-else-if="level === 2">
    <slot></slot>
  </h2>
  <h3 v-else-if="level === 3">
    <slot></slot>
  </h3>
  <h4 v-else-if="level === 4">
    <slot></slot>
  </h4>
  <h5 v-else-if="level === 5">
    <slot></slot>
  </h5>
  <h6 v-else-if="level === 6">
    <slot></slot>
  </h6>
</script>
```

```js
Vue.component('anchored-heading', {
  template: '#anchored-heading-template',
  props: {
    level: {
      type: Number,
      required: true
    }
  }
})
```

代码冗长，但是使用 render 函数就可以变得非常灵活：

```js
Vue.component('anchored-heading', {
  render: function (createElement) {
    return createElement(
      'h' + this.level,   // 标签名称
      this.$slots.default // 子节点数组
    )
  },
  props: {
    level: {
      type: Number,
      required: true
    }
  }
})
```

render 函数通过 return createElement 函数来生成 VNode

还可以通过 **JSX语法** 使其可读性提升，例如：

```js
createElement(
  'anchored-heading', {
    props: {
      level: 1
    }
  }, [
    createElement('span', 'Hello'),
    ' world!'
  ]
)
```

可以写成：

```js
import AnchoredHeading from './AnchoredHeading.vue'

new Vue({
  el: '#demo',
  render: function (h) {
    return (
      <AnchoredHeading level={1}>
        <span>Hello</span> world!
      </AnchoredHeading>
    )
  }
})
```

### CIcon 图标全局组件

根据传入的字符串，动态生成 class，适配各种图标，此处的 render 使用了 JSX 语法

```js
  render() {
    const Icon = (
      <i
        style={this.getIconStyle()}
        class={`iconfont ${this.getIconCls()}`}
        onClick={this.onClick}
      />
    );
    return Icon;
  }
```



## export import require 

### export 和 import

用于导出和导入常量、函数、文件、模块等

import 只能放在开头，所有逻辑代码之前

* export

```js
// demo1.js
export const str = 'hello world'
export function test1() {}
const test2 = () => {}
export {test2 as aaa}

// demo2.js
import {test1, str, aaa} from './demo1'
```

* export default 一个文件中只能有一个 default，引入时不需要花括号，且可以自由命名

```js
// demo1.js
export const str = 'hello world'
export function test1() {}
const test2 = () => {}
export {test2 as aaa}
export default function (){}

// demo2.js
import {test1, str, aaa} from './demo1'
import test3 from './demo1'
```

### require

require 可以出现在任何地方

require 的使用非常简单，它相当于 module.exports 的传送门，module.exports 后面的内容是什么，require 的结果就是什么，对象、数字、字符串、函数……再把require的结果**赋值**给某个变量。

<strong style="color:red;">从理解上，require是赋值过程，import是解构过程</strong>

### 加载图片

在 Vue 中引入图片，需要用 require("路径") 来引入

```html
<dt>
    <img :src="musicPic" />
</dt>
```

```js
musicPic() {
   return this.currentMusic.image
   		  ? this.currentMusic.image
          : require("../../assets/img/player_cover.png");
},
```















# 思维导图

![01_map](Vue.js学习笔记.assets/01_map.jpg)

## 钩子函数和指令

![02_map](Vue.js学习笔记.assets/02_map.jpg)

## 动态绑定样式和列表循环

![03_map](Vue.js学习笔记.assets/03_map.jpg)

## 事件绑定和双向绑定

![04_map](Vue.js学习笔记.assets/04_map.jpg)

## 组件

![05_map](Vue.js学习笔记.assets/05_map.jpg)

## 父子组件数据传递

![06_map](Vue.js学习笔记.assets/06_map.jpg)

## 高级语法

![07_map](Vue.js学习笔记.assets/07_map.jpg)

## Composition API

![08_map](Vue.js学习笔记.assets/08_map.jpg)

![09_map](Vue.js学习笔记.assets/09_map.jpg)

![10_map](Vue.js学习笔记.assets/10_map.jpg)

# Vue源码解析

## 数据驱动

### 模板

首先考虑一个问题，Vue是如何将数据替换到模板中的？

* 首先通过 tmpNode 拿到DOM，获取模板
* 通过 compiler 函数
  * 先获取其子节点，判断节点类型，当为元素节点时递归调用
  * 当为文本节点时，利用正则表达式提取其中的内容，并进行替换
* 如果直接对 tmpNode 进行替换，那么我们就丢失了模板，因此将其拷贝一份 generateNode, 使用此进行替换

```html
<body>
  <div id="root">
    <p>{{name}}</p>
    <p>{{message}}</p>
  </div>


  <script>
    // 步骤拆解
    // 1. 拿到模板
    // 2. 拿到数据
    // 3. 将数据与模板结合，得到的是 HTML 元素
    // 4. 放到页面中

    let kuohao = /\{\{(.+?)\}\}/g

    let tmpNode = document.querySelector('#root')
    console.log(tmpNode);

    let data = {
      name: 'Candy.',
      message: 'Success!'
    }

    // 真正的源码中是 DOM -> 字符串模板 -> VNode -> 真正的DOM
    function compiler(template, data) {
      let childNodes = template.childNodes
      for (let i = 0; i < childNodes.length; i++) {
        let type = childNodes[i].nodeType // 1元素, 3节点
        if (type === 3) {
          let txt = childNodes[i].nodeValue
          txt = txt.replace(kuohao, function (_, g) { // replace 使用正则匹配一次，函数就会被调用一次
            // 函数的第 0 个参数，表示匹配到的内容，第 n 个参数，表示匹配到的第 n 组
            let key = g.trim()
            let value = data[key]
            return value
          })
          childNodes[i].nodeValue = txt
        } else if (type === 1) {
          compiler(childNodes[i], data)
        }
      }
    }

    // 我们此时没有生成新的 template, 所以这里看到的是直接在页面中更新的数据，因为DOM是引用类型
    // 这样做模板就没了,因此要复制一份

    let generateNode = tmpNode.cloneNode(true) // 这里是DOM元素，可以这么用

    compiler(generateNode, data)
    // 4.
    root.parentNode.replaceChild(generateNode, root)
  </script>

</body>
```

这种替换思路有很大问题：

* Vue 使用的是虚拟DOM
* 只考虑了单属性`{{name}}`，而 Vue 中有很多使用层级`{{child.name.firstName}}`
* 代码未整合



所以我们通过如下的方法进行优化:

* 首先用构造函数构造 Vue 类，通过 render, compiler, update 对模板进行解析并挂载
* 还需要一个对链式调用进行处理，先切分 path 之后对数组进行循环，获取到最后的路径
* 上述过程可以函数柯里化

```html
<body>
  <div id="root">
    <p>{{name.firstName}}</p>
    <p>{{message}}</p>
  </div>


  <script>
    let kuohao = /\{\{(.+?)\}\}/g
    // 要解决一个问题，使用'xxx.yyy.zzz'访问成员
    function getValueByPath(obj, path) {
      let paths = path.split('.'); //获得一个数组[xxx,yyy,zzz]
      let res = obj
      let prop
      while (prop = paths.shift()) {
        res = res[prop]
      }
      return res
    }
      
    // function createGetValueByPth(path) {
    //   let paths = path.split('.'); //获得一个数组[xxx,yyy,zzz]
    //   return function getValueByPth(obj) {
    //     let res = obj
    //     let prop
    //     while (prop = paths.shift()) {
    //       res = res[prop]
    //     }
    //     return res
    //   }
    // }

    function compiler(template, data) {
      let childNodes = template.childNodes
      for (let i = 0; i < childNodes.length; i++) {
        let type = childNodes[i].nodeType // 1元素, 3节点
        if (type === 3) {
          let txt = childNodes[i].nodeValue
          txt = txt.replace(kuohao, function (_, g) { // replace 使用正则匹配一次，函数就会被调用一次
            // 函数的第 0 个参数，表示匹配到的内容，第 n 个参数，表示匹配到的第 n 组
            let path = g.trim()
            let value = getValueByPath(data, path)
            return value
          })
          childNodes[i].nodeValue = txt
        } else if (type === 1) {
          compiler(childNodes[i], data)
        }
      }
    }

    function JGVue(options) {
      this._data = options.data
      this._el = options.el
      this._templateDOM = document.querySelector(this._el)
      this._parent = this._templateDOM.parentNode

      this.render()
    }

    JGVue.prototype.render = function () {
      this.compiler()
    }

    JGVue.prototype.compiler = function () {
      let realHTMLDOM = this._templateDOM.cloneNode(true)
      compiler(realHTMLDOM, this._data)
      this.update(realHTMLDOM)
    }

    JGVue.prototype.update = function (real) {
      this._parent.replaceChild(real, document.querySelector('#root'))
    }

    let app = new JGVue({
      el: '#root',
      data: {
        name: {
          firstName: 'candy',
          lastName: 'Z'
        },
        message: 'info'
      }
    })
  </script>

</body>
```



### 虚拟DOM

1. 将 DOM 转换成虚拟 DOM

* 创建 VNode 类，定义 tag data value type children 存储标签，属性节点数据，节点类型，子节点
* getVNode 方法，传入一个真实 DOM 节点
  * 如果为元素节点
    * 获取节点类型 nodeName
    * 获取属性节点 attributes
    * 获取属性节点的属性内容并存储
    * 生成 VNode
    * 获取子节点，递归调用添加到 children 中
  * 如果为文本节点，直接生成 VNode

2. 将虚拟 DOM 转换成真实 DOM

* 判断节点类型
  * 元素类型，创建元素节点，并添加属性，递归添加 child 节点
  * 文本类型，创建文本节点，并添加属性

```html
<body>
  <div id="root" name="ggg">
    <div class="c1">
      <div title="tt1" id="id">hello1</div>
      <div title="tt2">hello2</div>
      <div title="tt3">hello3</div>
      <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
      </ul>
    </div>
  </div>

  <script>
    // 为什么要使用虚拟 DOM? 性能
    // <div /> => { tag: 'div' }
    // 文本节点 => { tag: undefined, value: '文本节点' }
    // <div title="1" class="c" /> => { tag: 'div', data: { title: '1', class: 'c' } }
    // <div><div /></div> => { tag: 'div', children: [ { tag: 'div' } ] }

    class VNode {
      constructor(tag, data, value, type) {
        this._tag = tag
        this._data = data
        this._value = value
        this._type = type
        this._children = []
      }

      appendChild(vNode) {
        this._children.push(vNode)
      }
    }

    /** 
     * 使用递归 来遍历 DOM 元素, 生成 虚拟 DOM
     * Vue 中的源码使用的 栈结构 , 使用栈存储 父元素来实现递归生成
     */

    function transferVNode(node) {
      let nodeType = node.nodeType
      let _vNode = null
      if (nodeType === 1) {
        let nodeName = node.nodeName.toLowerCase()
        let data = {}
        let _attrs = node.attributes
        for (let i = 0; i < _attrs.length; i++) {
          data[_attrs[i].nodeName] = _attrs[i].value
        }
        _vNode = new VNode(nodeName, data, undefined, nodeType)

        let children = node.childNodes
        for (let i = 0; i < children.length; i++) {
          _vNode.appendChild(transferVNode(children[i]))
        }

      } else if (nodeType === 3) {
        _vNode = new VNode(undefined, undefined, node.nodeValue, nodeType)
      }
      return _vNode
    }

    let root = document.querySelector('#root')
    console.log(root.attributes[0]);
    let vNode = transferVNode(root)
    console.log(vNode);

    function parseVNode(vNode) {
      let node = null
      if (vNode._type === 1) {
        node = document.createElement(vNode._tag)
        let _attrs = vNode._data
        let keys = Object.keys(_attrs)
        for (let i = 0; i < keys.length; i++) {
          node.setAttribute(keys[i], _attrs[keys[i]])
        }
        for (let i = 0; i < vNode._children.length; i++) {
          node.appendChild(parseVNode(vNode._children[i]))
        }

      } else if (vNode._type === 3) {
        node = document.createTextNode(vNode._value)
      }
      return node
    }
    let node = parseVNode(vNode)
    document.body.appendChild(node)
  </script>
</body>
```



## 函数柯里化

参考资料:

- [函数式编程](https://llh911001.gitbooks.io/mostly-adequate-guide-chinese/content/)
- [维基百科](https://zh.wikipedia.org/wiki/%E6%9F%AF%E9%87%8C%E5%8C%96)

概念:

* 科里化: 一个函数原本有多个参数, 之传入**一个**参数, 生成一个新函数, 由新函数接收剩下的参数来运行得到结构
* 偏函数: 一个函数原本有多个参数, 之传入**一部分**参数, 生成一个新函数, 由新函数接收剩下的参数来运行得到结构
* 高阶函数: 一个函数**参数是一个函数**, 该函数对参数这个函数进行加工, 得到一个函数, 这个加工用的函数就是高阶函数

为什么要使用柯里化？为了提升性能，使用科里化可以缓存一部分能力

Vue 本质上是使用 HTML 的字符串作为模板的, 将字符串的模板 转换为 AST, 再转换为 VNode.

- 模板 -> AST
- AST -> VNode
- VNode -> DOM

那一个阶段最消耗性能？最消耗性能是字符串解析 ( 模板 -> AST )

例子: let s = "1 + 2 * ( 3 + 4 * ( 5 + 6 ) )"

写一个程序，解析这个表达式，得到结果 ( 一般化 )

我们一般会将这个表达式转换为 "波兰式" 表达式，然后使用栈结构来运算

在 Vue 中每一个标签可以是真正的 HTML 标签，也可以是自定义组件，该如何取分呢？

在 Vue 源码中其实将所有可以用的 HTML 标签已经存起来了

假设这里是考虑几个标签:

```js
let tags = 'div,p,a,img,ul,li'.split(',');
```

需要一个函数, 判断一个标签名是否为内置的标签

```js
function isHTMLTag( tagName ) {
  tagName = tagName.toLowerCase();
  if ( tags.indexOf( tagName ) > -1 ) return true;
  return false;
}
```

模板是任意编写的, 可以写的很简单, 也可以写到很复杂，indexOf 内部也是要循环的

如果有 6 种内置标签, 而模板中有 10 个标签需要判断, 那么就需要执行 60 次循环，这样很消耗性能，因此可以使用函数柯里化：

* 使用一个 set 来创建 map，并给每个标签赋值 true
* 返回一个函数，传入要判断的 tagName，这样只需要初始化 makeMap一次，就可以一直调用返回的函数进行判断

```js
let tags = 'div,p,a,img,ul,li'.split(',');

function makeMap( keys ) {
  let set = {}; // 集合
  tags.forEach( key => set[ key ] = true );
  return function ( tagName ) {
    return !!set[ tagName.toLowerCase() ]
  }
}
let isHTMLTag = makeMap( tags ); // 返回的函数
```

这就是函数柯里化的一个具体应用

下面再考虑一个问题：vue 项目模板 转换为 抽象语法树需要执行几次？

- 页面一开始加载需要渲染
- 每一个属性 ( 响应式 ) 数据在发生变化的时候 要渲染
- watch, computed 等等

上面实现的代码，每次需要渲染的时候，模板就会被解析一次 ( 注意, 这里我们简化了解析方法 )

render 的作用是将 虚拟 DOM 转换为 真正的 DOM 加到页面中

- 虚拟 DOM 可以降级理解为 AST
- 一个项目运行的时候 模板是不会变 的, 就表示 AST 是不会变的

我们可以将代码进行优化，将虚拟 DOM 缓存起来，生成一个函数，函数只需要传入数据就可以得到真正的 DOM



在真正的 Vue 中使用了二次提交的设计结构

* 在页面中 DOM 和 虚拟DOM 是一一对应的关系，因此当数据改变时我们不能直接替换 VNode， 这样太消耗性能
* 因此要先根据 AST 和 数据 生成新的 VNode（render）
* 再根据旧的 VNode 和新的 VNode 进行比较(diff算法)，进行更新（update）

![image-20210917160258693](Vue.js学习笔记.assets/image-20210917160258693.png)

下面的代码完成了三件事：

* 首先通过 getVNode 获取模板（AST），将模板缓存起来
* 利用 combine 将模板与数据结合，生成填充好数据的 VNode
* 挂载到页面上，但是没有使用 diff 算法，直接进行全部替换

<strong style="color:red;">这里第一步使用了函数柯里化，createRenderFn 函数中先将模板（AST）缓存起来，返回一个 render 函数，在 render 函数中进行数据替换处理，这样我们每次就直接调用 render 函数，无需再重新解析模板</strong>

```html
<body>
  <div id="root">
    <div>
      <div title="tt1" id="id">{{ name }}</div>
      <div title="tt2">{{ age }}</div>
      <div title="tt3">{{ gender }}</div>
      <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
      </ul>
    </div>
  </div>



  <script>
    // 虚拟 DOM 构造函数
    class VNode {
      constructor(tag, data, value, type) {
        this.tag = tag && tag.toLowerCase();
        this.data = data;
        this.value = value;
        this.type = type;
        this.children = [];
      }

      appendChild(vnode) {
        this.children.push(vnode);
      }
    }
    // 由HTML DOM 生成 虚拟 DOM，把它当作生成 AST 的 compiler 函数
    function getVNode(node) {
      let nodeType = node.nodeType;
      let _vnode = null;
      if (nodeType === 1) {
        // 元素
        let nodeName = node.nodeName;
        let attrs = node.attributes;
        let _attrObj = {};
        for (let i = 0; i < attrs.length; i++) { // attrs[ i ] 属性节点 ( nodeType == 2 )
          _attrObj[attrs[i].nodeName] = attrs[i].nodeValue;
        }
        _vnode = new VNode(nodeName, _attrObj, undefined, nodeType);

        // 考虑 node 的子元素
        let childNodes = node.childNodes;
        for (let i = 0; i < childNodes.length; i++) {
          _vnode.appendChild(getVNode(childNodes[i])); // 递归
        }

      } else if (nodeType === 3) {

        _vnode = new VNode(undefined, undefined, node.nodeValue, nodeType);
      }

      return _vnode;
    }
    // 将虚拟DOM 转换成 真正的DOM
    function parseVNode(vnode) {
      // 创建 真实的 DOM
      let type = vnode.type;
      let _node = null;
      if (type === 3) {
        return document.createTextNode(vnode.value); // 创建文本节点
      } else if (type === 1) {

        _node = document.createElement(vnode.tag);

        // 属性
        let data = vnode.data; // 现在这个 data 是键值对
        Object.keys(data).forEach((key) => {
          let attrName = key;
          let attrValue = data[key];
          _node.setAttribute(attrName, attrValue);
        });

        // 子元素
        let children = vnode.children;
        children.forEach(subvnode => {
          _node.appendChild(parseVNode(subvnode)); // 递归转换子元素 ( 虚拟 DOM )
        });

        return _node;
      }

    }


    // 将带有坑的 VNode 与数据结合，得到填充数据的 VNode，模拟 AST => VNode
    // 根据路径访问对象成员
    function getValueByPath(obj, path) {
      let paths = path.split('.'); // [ xxx, yyy, zzz ]
      let res = obj;
      let prop;
      while (prop = paths.shift()) {
        res = res[prop];
      }
      return res;
    }
    let rkuohao = /\{\{(.+?)\}\}/g

    function combine(vnode, data) {
      let _type = vnode.type
      let _data = vnode.data
      let _value = vnode.value
      let _tag = vnode.tag
      let _children = vnode.children


      let _vnode = null

      if (_type === 3) {
        // 对文本处理
        _value = _value.replace(rkuohao, function (_, g) {
          return getValueByPath(data, g.trim())
        })

        _vnode = new VNode(_tag, _data, _value, _type)

      } else if (_type === 1) {
        _vnode = new VNode(_tag, _data, _value, _type)
        _children.forEach(_subvnode => _vnode.appendChild(combine(_subvnode, data)))
      }
      return _vnode
    }


    function JGVue(options) {
      this._data = options.data
      let elm = document.querySelector(options.el)
      this._template = elm
      this._parent = elm.parentNode

      this.mount() // 挂载
    }

    JGVue.prototype.mount = function () {
      // 需要提供一个 render 方法：生成虚拟DOM
      this.render = this.createRenderFn()

      this.mountComponent()
    }

    JGVue.prototype.mountComponent = function () {

      // 执行 mountComponent() 函数
      let mount = () => {
        this.update(this.render())
      }

      mount.call(this) // 本质上应该交给 watcher 来调用
    }

    // 这里是生成 render 函数，目的是缓存 AST （我们使用虚拟DOM来模拟）
    JGVue.prototype.createRenderFn = function () {
      let ast = getVNode(this._template) // 获取模板
      // Vue 将 AST + data => VNode
      // 简化：将带有坑的 VNode + data => 含有数据的 VNode
      return function render() {
        // 将带坑的 VNode 转换为带数据的 VNode
        let _tmp = combine(ast, this._data)
        return _tmp
      }
    }

    // 将虚拟DOM渲染到页面中：diff 算法就在这里
    JGVue.prototype.update = function (vnode) {
      let realDOM = parseVNode(vnode)
      this._parent.replaceChild(realDOM, document.querySelector('#root'))
      // 这个算法是不负责任的，每次会将页面中的 DOM 全部替换，先不用 diff，太复杂
    }

    let app = new JGVue({
      el: '#root',
      data: {
        name: 'zyy',
        age: '19',
        gender: 'men'
      }
    })
  </script>
</body>
```



## 响应式原理

* 我们在使用 Vue 时候, 赋值属性获得属性都是直接使用的 Vue 实例，而不是 data

* 我们在设计属性值的时候, 页面的数据更新

### 对象的响应式化

对于普通的对象，我们无法监听到它值的改变，因此需要用到`Objective.defineProperty`的 get 和 set 方法对数据改变进行监听，这是响应式的基础

* 定义 `defineReactive` 函数，<strong style="color:red;">这个函数利用形参 value 来存储值，通过闭包实现了不开辟新空间的情况下对其值进行修改</strong>
* 定义 `reactify` 函数，遍历每个元素，将其响应式化

```html
<body>
  <script>
    let data = {
      price: {
        real: '999'
      },
      name: 'zyy',
      age: 19,
      course: [{
          name: '语文'
        },
        {
          name: '数学'
        },
        {
          name: '英语'
        },
      ]
    }

    function defineReactive(target, key, value, enumerable) {
      // 函数内部是个局部作用域，这个 value 是一个只在函数内部使用的变量（闭包）
      if (typeof value === 'object' && value !== null && !Array.isArray(value)) {
        reactify(value)
      }
      Object.defineProperty(target, key, {
        configurable: true,
        enumerable: !!enumerable,
        get() {
          return value
        },
        set(newVal) {
          value = newVal
        }
      })
    }

    // 将对象响应式化
    function reactify(o) {
      let keys = Object.keys(o)
      for (let i = 0; i < keys.length; i++) {
        let key = keys[i]
        let value = o[key]
        // 判断这个属性是不是引用类型，判断是不是数组
        // 如果是数组，循环数组，将数组里面的元素进行响应式化
        // 如果是引用类型，需要用 defineReactive 将其响应式化，如果不是，也要用 defineReactive 将其响应式化
        if (Array.isArray(value)) {
          for (let j = 0; j < value.length; j++) {
            reactify(value[j])
          }
        } else {
          // 对象或值类型
          defineReactive(o, key, value, true)
        }
      }
    }
    reactify(data)
  </script>
</body>
```

### 数组的响应式化

对数组进行 push, pop, shift, unshift 等操作元素时，新加入的元素是无法响应式的，对这种改变该如何监听呢？**需要对原生方法进行拦截**

首先，从一个最基础的功能开始，如何扩展一个函数的功能？

```html
  <script>
    // 如果一个函数已经定义了, 但是我们需要扩展其功能, 我们一般的处理办法:
    // 1. 使用一个临时的函数名存储函数
    // 2. 重新定义原来的函数
    // 3. 定义扩展的功能
    // 4. 调用临时的那个函数

    function func() {
      console.log('原始的功能');
    }

    let _tmpFn = func

    func = function () {
      _tmpFn()
      console.log('新的扩展的功能')
    }

    func()
  </script>
```

我们对数组的原生方法进行拦截：

* 首先通过 `let array_methods = Object.create(Array.prototype)` 获取 Array 的原型对象
* 遍历需要改变的方法，同时改变原型对象相应方法的函数
* 将数组的原型对象修改为 `array_methods` ，即完成了拦截

```html
<script>
    let ARRAY_METHOD = [
      'push',
      'pop',
      'shift',
      'unshift',
      'reverse',
      'sort',
      'splice',
    ];

    // 思路, 原型式继承: 修改原型链的结构
    let arr = [];
    // 继承关系: arr -> Array.prototype -> Object.prototype -> ...
    // 继承关系: arr -> 改写的方法 -> Array.prototype -> Object.prototype -> ...

    let array_methods = Object.create(Array.prototype);

    ARRAY_METHOD.forEach(method => {
      array_methods[method] = function () {
        console.log('调用的是拦截的' + method + '方法');
        let res = Array.prototype[method].apply(this, arguments)
        return res
      }
    })

    arr.__proto__ = array_methods;


    // Vue 的源码中也做了判断
    // 如果 浏览器支持 __proto__ 那么他就这么做
    // 如果不支持, vue 使用的是混入法

    // arr.length = 0
  </script>
```

通过上述代码，我们可以实现数组原生方法的拦截，那么就可以实现数组的响应式：

通过`reactify(arguments[i])`在每次修改数组元素时，对新加入的元素响应式化

```js
    ARRAY_METHOD.forEach(method => {
      array_methods[method] = function () {
        // 调用原来的方法
        console.log('调用的是拦截的 ' + method + ' 方法');
        // 将数据进行响应式化
        for (let i = 0; i < arguments.length; i++) {
          reactify(arguments[i]);
        }
        let res = Array.prototype[method].apply(this, arguments);
        // Array.prototype[ method ].call( this, ...arguments ); // 类比
        return res;
      }
    });
```

同时，在响应式化函数中，改变每个数组的原型对象：

```js
// 将对象响应式化
    function reactify(o, vm) {
      let keys = Object.keys(o)
      for (let i = 0; i < keys.length; i++) {
        let key = keys[i]
        let value = o[key]
        // 判断这个属性是不是引用类型，判断是不是数组
        // 如果是数组，循环数组，将数组里面的元素进行响应式化
        // 如果是引用类型，需要用 defineReactive 将其响应式化，如果不是，也要用 defineReactive 将其响应式化
        if (Array.isArray(value)) {
          for (let j = 0; j < value.length; j++) {
            value.__proto__ = array_methods
            reactify(value[j], vm)
          }
        } else {
          // 对象或值类型
          defineReactive.call(vm, o, key, value, true)
        }
      }
    }
```

最后，只需要在 set 方法中，调用 `this.mountComponent` 对修改后的 VNode 重新渲染，实现了响应式



### 代理方法

真正的 vue 直接通过 app.name 来访问数据，而我们目前只实现了 app._data.name 来访问，因此需要通过代理方法

**代理方法**，就是要将 app_data 中的成员给映射到 app 上

由于需要在更新数据的时候，更新页面的内容，所以 app._data 访问的成员与 app 访问的成员应该时同一个成员

由于 app._data 已经是响应式的对象了，所以只需要让 app 访问的成员去访问 app.__data 的对应成员就可以了

引入了一个函数 proxy(target, prop, key)，将 target 的操作映射到 target.prop 上，这是因为当时没有 proxy 语法（ES6）

* 首先在 initData 方法中先调用 reactify 编程响应式化
* 再创建 proxy 函数，通过 `return target[prop][key]`将 `this._data[keys[i]]` 映射到 `this[keys[i]]` 上

```js
JGVue.prototype.initData = function () {
      // 将 this._data 的成员转换成响应式，并将其属性代理到实例上
      let keys = Object.keys(this._data)
      for (let i = 0; i < keys.length; i++) {
        // 将对象 this._data[keys[i]] 变成响应式的
        reactify(this._data, this)
      }

      // 代理
      for (let i = 0; i < keys.length; i++) {
        // 将 this._data[keys[i]] 映射到 this[keys[i]] 上
        proxy(this, '_data', keys[i])
      }
    }

    // 将某一个对象的属性访问 映射到 对象的某一个属性成员上
    function proxy(target, prop, key) {
      Object.defineProperty(target, key, {
        enumerable: true,
        configurable: true,
        get() {
          return target[prop][key]
        },
        set(newVal) {
          target[prop][key] = newVal
        }
      })
    }
```





## 发布订阅模式

目标：解耦，让各个模块之间没有紧密联系

现在的处理办法是，属性在更新的时候，调用 mountComponents 方法

问题: mountComponent 更新的是 全部的页面 -> 当前虚拟 DOM 对应的页面 DOM

在 Vue 中, 整个的更新是按照组件为单位进行 **判断**, 以节点为单位进行更新

- 如果代码中没有自定义组件, 那么在比较算法的时候, 我们会将全部的模板对应的 虚拟 DOM 进行比较
- 如果代码中含有自定义组件, 那么在比较算法的时候, 就会判断更新的是哪一些组件中的属性，只会判断更新数据的组件，其他组件不会更新

复杂的页面是有很多组件构成，每一个属性要更新的都要调用更新的方法?

<strong style="color:red;">**目标：如果修改了什么属性，就尽可能只更新这些属性对应的页面 DOM**</strong>

这样就一定不能将更新的代码写死

例子：预售可能一个东西没有现货，告诉老板，如果东西到了就告诉我

老板就是发布者，订阅什么东西作为中间媒介,我就是订阅者

使用代码的结构来描述:

1. 老板提供一个账簿( 数组 )
2. 我可以根据需求订阅我的商品( 老板要记录下谁定了什么东西，在数组中存储某些东西 )
3. 等待，可以做其他的事情
4. 当货品来到的时候，老板就查看账簿，挨个的打电话 ( 遍历数组，取出数组的元素来使用 )

实际上就是事件模型

1. 有一个 event 对象
2. on, off, emit 方法

实现事件模型, 该怎么用?

1. event 是一个全局对象
2. event.on( '事件名', 处理函数 ), 订阅事件
   1. 事件可以连续订阅
   2. 可以移除: event.off()
      1. 移除所有
      2. 移除某一个类型的事件
      3. 移除某一个类型的某一个处理函数
3. 写别的代码
4. event.emit( '事件名', 参数 ), 先前注册的事件处理函数就会依次调用

![image-20210926153151401](Vue.js学习笔记.assets/image-20210926153151401.png)

### Watcher 与 Dep

<img src="Vue.js学习笔记.assets/image-20211013191513349.png" alt="image-20211013191513349" style="zoom: 50%;" />

<img src="Vue.js学习笔记.assets/image-20211013191526481.png" alt="image-20211013191526481" style="zoom:50%;" />

### Watcher 派发更新

构造一个 watcher 类，用于派发更新，传入的参数为：Vue实例、String||function

属性：

* this.deps 用于存储依赖项
* this.id 用于存储当前 watcher 的 id
* this.getter 存储 expOrfn
* 调用 this.get()

方法：

* get
  * 调用 Dep 中的 pushTarget 方法，将当前操作后的 watcher 存储到全局 watcher 中
  * 通过 call 方法调用 expOrfn 函数，把 vm 实例传入到函数中
  * 调用 Dep 中的 popTarget 方法，将当前 watcher 踢出
* run 调用get 方法
* update 对外暴露的接口，调用 run 方法
* addDep 将当前 dep 存入 this.deps 中，使得当前 dep 与当前 watcher 关联
* cleanupDep 清空 dep 队列

```js

let watcherid = 0;

/** Watcher 观察者, 用于 发射更新的行为 */
class Watcher {

  /**
   * 
   * @param {Object} vm JGVue 实例
   * @param {String|Function} expOrfn 如果是渲染 watcher, 传入的就是渲染函数, 如果是 计算 watcher 传入的就是路径表达式, 暂时只考虑 expOrFn 为函数的情况.
   */
  constructor( vm, expOrfn ) {
    this.vm = vm;
    this.getter = expOrfn;

    this.id = watcherid++;

    this.deps = []; // 依赖项
    this.depIds = {}; // 是一个 Set 类型, 用于保证 依赖项的唯一性 ( 简化的代码暂时不实现这一块 )

    // 一开始需要渲染: 真实 vue 中: this.lazy ? undefined : this.get()
    this.get();
  }

  /** 计算, 触发 getter */
  get() {
    pushTarget( this );

    this.getter.call( this.vm, this.vm ); // 上下文的问题就解决了

    popTarget();
  }

  /**
   * 执行, 并判断是懒加载, 还是同步执行, 还是异步执行: 
   * 我们现在只考虑 异步执行 ( 简化的是 同步执行 )
   */
  run() {
    this.get(); 
    // 在真正的 vue 中是调用 queueWatcher, 来触发 nextTick 进行异步的执行
  }

  /** 对外公开的函数, 用于在 属性发生变化时触发的接口 */
  update() {
    this.run(); 
  }

  /** 清空依赖队列 */
  cleanupDep() {

  }

  /** 将 当前的 dep 与 当前的 watcher 关联 */
  addDep( dep ) {
    this.deps.push( dep );
  }
}
```

### Dep 依赖收集

构造一个 Dep 类，用于收集依赖项

属性：

* this.id 用于存储当前 dep id
* this.subs 存储与 当前 Dep 关联的 watcher
* Dep.target = null 存储当前 watcher

方法：

* addSub 将当前 watcher 存入 this.subs 中，使得当前 watcher 与当前 dep 关联
* removeSub 移除 watcher
* depend
  * 如果 Dep.target 存在
    * 调用 this.addSub(Dep.target) 将当前 watcher 存入 this.subs 中
    * 调用 Dep.target.addDep(this)  将当前的 dep 存入当前 watcher 中
* notify
  * 依次取出 subs 中存储的 watcher，调用其 update 方法

全局方法：

* pushTarget
  * targetStack 存储当前 watcher
  * Dep.target  = target 指向当前 watcher
* popTarget 弹出当前 watcher

```js
let depId = 0

class Dep {

  constructor() {
    this.id = depId++
    this.subs = []; // 存储的是与 当前 Dep 关联的 watcher
  }

  /** 添加一个 watcher */
  addSub(sub) {
    this.subs.push(sub)
  }
  /** 移除 */
  removeSub(sub) {
    for (let i = this.subs.length - 1; i >= 0; i--) {
      if (sub === this.subs[i]) {
        this.subs.splice(i, 1)
      }
    }
  }

  /** 将当前 Dep 与当前的 watcher ( 暂时渲染 watcher ) 关联*/
  depend() {
    // 就是将当前 dep 与当前 watcher 互相关联
    if (Dep.target) {
      this.addSub(Dep.target) // 将当前的 watcher 关联到当前的 dep 上

      Dep.target.addDep(this) // 将当前的 dep 与当前渲染 watcher 关联起来
    }
  }
  /** 触发与之关联的 watcher 的 update 方法, 起到更新的作用 */
  notify() {
    // 在真实的 Vue 中是依次触发 this.subs 中的 watcher 的 update 方法

    let deps = this.subs.slice()

    deps.forEach(watcher => {
      watcher.update()
    })

  }

}

// 全局的容器存储渲染 Watcher
// let globalWatcher
// 学 Vue 的实现
Dep.target = null; // 这就是全局的 Watcher

let targetStack = []

// 将当前操作后的 watcher 存储到 全局watcher 中，参数 target 就是当前 watcher
function pushTarget(target) {
  targetStack.unshift(Dep.target)
  Dep.target = target
}

// 将当前 watcher 踢出
function popTarget() {
  Dep.target = targetStack.shift()
}
```



### 流程

* 在 mountComponent 函数中（渲染函数）
  * 创建一个全局 watcher，并传入 vm 实例 和 mount 函数，mount 函数开始会执行一次，后面当 watcher 监视到改变才执行
* 在 defineReactive 函数中（响应式化函数）
  * 对每一个属性创建属于它的 dep，当有模板使用该属性时，调用其 dep.depend() 进行依赖收集
  * 当重新设置 set 时，调用 dep.notify() 进行派发更新

```js
JGVue.prototype.mountComponent = function () {
  // 执行 mountComponent() 函数 
  let mount = () => { // 这里是一个函数, 函数的 this 默认是全局对象 "函数调用模式"
    this.update(this.render())
  }

  // 这个 Watcher 就是全局的 Watcher, 在任何一个位置都可以访问他了 ( 简化的写法 )
  new Watcher(this, mount); // 相当于这里调用了 mount
}
```

```js
function defineReactive(target, key, value, enumerable) {

  // 函数内部就是一个局部作用域, 这个 value 就只在函数内使用的变量 ( 闭包 )
  if (typeof value === 'object' && value != null) {
    // 是非数组的引用类型
    observe(value); // 递归
  }

  let dep = new Dep();

  dep.__propName__ = key

  Object.defineProperty(target, key, {
    configurable: true,
    enumerable: !!enumerable,

    get() {
      // console.log(`读取 ${key} 属性`); // 额外
      // 依赖收集 ( 暂时略 )
      dep.depend()
      return value;
    },
    set(newVal) {
      // console.log(`设置 ${key} 属性为: ${newVal}`); // 额外

      if (value === newVal) return;


      // 目的
      // 将重新赋值的数据变成响应式的, 因此如果传入的是对象类型, 那么就需要使用 observe 将其转换为响应式
      if (typeof newVal === 'object' && newVal != null) {
        observe(newVal);
      }

      value = newVal;

      // 派发更新, 找到全局的 watcher, 调用 update
      dep.notify();
    }
  });
}
```

最后举个例子，谈谈我的理解：

假设有组件 A 和 组件 B

A 有属性 a b c

B 有属性 d e f 且使用了 A 的属性 a

那么 A 和 B 会有两个 Watcher

b 和 c 属性中的 dep 存储 WatcherA

e 和 f 属性中的 dep 存储 WatcherB

而 a 属性中的 dep 则同时存储 WatcherA 和 WatcherB

bcef 变化只会重新渲染对应的组件，但 a 变化两个组件都会渲染

如果不适用发布订阅模式，任何属性的改变，都会引起全局重新渲染，这就是发布订阅模式的好处



