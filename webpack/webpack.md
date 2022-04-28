# 初体验

* `npm install webpack webpack-cli -D` 局部安装 webpack
* 创建 src 和 build 文件夹，存储源代码和打包代码
* 打包
  * 开发环境：`webpack ./src/index.js -o ./build/built.js --mode=development` webpack会以 ./src/ index.js 为入口文件开始打包，打包后输出到 ./build/built.js，整体打包环境，是开发环境
  * 生产环境：`webpack ./src/index.js -o ./build/built.js --mode=production` webpack会以 ./src/ index.js 为入口文件开始打包，打包后输出到 ./build/built.js，整体打包环境，是生产环境

webpack 可以打包 js, json 文件，不能打包 css 文件



# 开发环境配置

## 样式资源

* 创建 `webpack.config.js` 文件

```js
/*
  webpack.config.js  webpack的配置文件
    作用: 指示 webpack 干哪些活（当你运行 webpack 指令时，会加载里面的配置）

    所有构建工具都是基于nodejs平台运行的~模块化默认采用commonjs。
*/

// resolve用来拼接绝对路径的方法
const { resolve } = require('path');

module.exports = {
  // webpack配置
  // 入口起点
  entry: './src/index.js',
  // 输出
  output: {
    // 输出文件名
    filename: 'built.js',
    // 输出路径
    // __dirname nodejs的变量，代表当前文件的目录绝对路径
    path: resolve(__dirname, 'build')
  },
  // loader的配置
  module: {
    rules: [
      // 详细loader配置
      // 不同文件必须配置不同loader处理
      {
        // 匹配哪些文件
        test: /\.css$/,
        // 使用哪些loader进行处理
        use: [
          // use数组中loader执行顺序：从右到左，从下到上 依次执行
          // 创建style标签，将js中的样式资源插入进行，添加到head中生效
          'style-loader',
          // 将css文件变成commonjs模块加载js中，里面内容是样式字符串
          'css-loader'
        ]
      },
      {
        test: /\.less$/,
        use: [
          'style-loader',
          'css-loader',
          // 将less文件编译成css文件
          // 需要下载 less-loader和less
          'less-loader'
        ]
      }
    ]
  },
  // plugins的配置
  plugins: [
    // 详细plugins的配置
  ],
  // 模式
  mode: 'development', // 开发模式
  // mode: 'production'
}

```

* 运行 webpack



## HTML

打包 html 需要用到插件 plugin，它和 loader 的区别是需要引入

```js
/*
  loader: 1. 下载   2. 使用（配置loader）
  plugins: 1. 下载  2. 引入  3. 使用
*/
const { resolve } = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'built.js',
    path: resolve(__dirname, 'build')
  },
  module: {
    rules: [
      // loader的配置
    ]
  },
  plugins: [
    // plugins的配置
    // html-webpack-plugin
    // 功能：默认会创建一个空的HTML，自动引入打包输出的所有资源（JS/CSS）
    // 需求：需要有结构的HTML文件
    new HtmlWebpackPlugin({
      // 复制 './src/index.html' 文件，并自动引入打包输出的所有资源（JS/CSS）
      template: './src/index.html'
    })
  ],
  mode: 'development'
};

```



## 图片资源

图片资源分了两种：

* url 中的图片，使用 url-loader 进行打包
* html 标签中的图片，使用 html-loader 进行打包

```js
const { resolve } = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'built.js',
    path: resolve(__dirname, 'build')
  },
  module: {
    rules: [
      {
        test: /\.less$/,
        // 要使用多个loader处理用use
        use: ['style-loader', 'css-loader', 'less-loader']
      },
      {
        // 问题：默认处理不了html中img图片
        // 处理图片资源
        test: /\.(jpg|png|gif)$/,
        // 使用一个loader
        // 下载 url-loader file-loader
        loader: 'url-loader',
        options: {
          // 图片大小小于8kb，就会被base64处理
          // 优点: 减少请求数量（减轻服务器压力）
          // 缺点：图片体积会更大（文件请求速度更慢）
          limit: 8 * 1024,
          // 问题：因为url-loader默认使用es6模块化解析，而html-loader引入图片是commonjs
          // 解析时会出问题：[object Module]
          // 解决：关闭url-loader的es6模块化，使用commonjs解析
          esModule: false,
          // 给图片进行重命名
          // [hash:10]取图片的hash的前10位
          // [ext]取文件原来扩展名
          name: '[hash:10].[ext]'
        }
      },
      {
        test: /\.html$/,
        // 处理html文件的img图片（负责引入img，从而能被url-loader进行处理）
        loader: 'html-loader'
      }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html'
    })
  ],
  mode: 'development'
};

```



## 其他资源

* 先用 exclude 排除 js、html、css、less文件
* 使用 file-loader 打包其他文件

```js
const { resolve } = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'built.js',
    path: resolve(__dirname, 'build')
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader']
      },
      // 打包其他资源(除了html/js/css资源以外的资源)
      {
        // 排除css/js/html资源
        exclude: /\.(css|js|html|less)$/,
        loader: 'file-loader',
        options: {
          name: '[hash:10].[ext]'
        }
      }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html'
    })
  ],
  mode: 'development'
};
```



## devServer 自动化

devServer 可以用来自动化编译、自动打开浏览器、自动刷新浏览器

特点：只会在内存中编译打包，不会有任何输出

需要在 `module.exports` 中配置以下内容：

```js
// 开发服务器 devServer：用来自动化（自动编译，自动打开浏览器，自动刷新浏览器~~）
  // 特点：只会在内存中编译打包，不会有任何输出
  // 启动devServer指令为：npx webpack-dev-server
  devServer: {
    // 项目构建后路径
    contentBase: resolve(__dirname, 'build'),
    // 启动gzip压缩
    compress: true,
    // 端口号
    port: 3000,
    // 自动打开浏览器
    open: true
  }
```

最后使用 `npx webpack-dev-server` 指令执行



# 生产环境配置

## CSS

### 提取 CSS 成单文件

开发环境 css 是这样处理的：

* 通过 css-loader 将 css 整合到 js 中
* 通过 style-loader 生成 style 标签插入html中

生产环境下，我们要将 css 提取成单文件：

* 首先通过 css-loader 将 css 整合到 js 中
* 引入 MiniCssExtractPlugin 插件，将 js 中的 css 提取成单文件

```js
const { resolve } = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = {
  entry: './src/js/index.js',
  output: {
    filename: 'js/built.js',
    path: resolve(__dirname, 'build')
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          // 创建style标签，将样式放入
          // 'style-loader', 
          // 这个loader取代style-loader。作用：提取js中的css成单独文件
          MiniCssExtractPlugin.loader,
          // 将css文件整合到js文件中
          'css-loader'
        ]
      }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html'
    }),
    new MiniCssExtractPlugin({
      // 对输出的css文件进行重命名
      filename: 'css/built.css'
    })
  ],
  mode: 'development'
};

```

### CSS 兼容性处理

对于不同的浏览器，需要对 CSS 进行兼容性处理，需要用到 `postcss-loader postcss-preset-env`

* 首先我们要在 package.json 中配置 browserlist

```js
"browserslist": {
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ],
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ]
  },
```

* 在 webpack.config.js 中配置 loader
  * 默认会按照生产环境打包，如果想要按开发环境打包，则需要设置 node 环境变量
  * 在开头加上 `process.env.NODE_ENV = 'development'` 修改环境变量

```js
const { resolve } = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

// 设置nodejs环境变量
// process.env.NODE_ENV = 'development';

module.exports = {
  entry: './src/js/index.js',
  output: {
    filename: 'js/built.js',
    path: resolve(__dirname, 'build')
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          MiniCssExtractPlugin.loader,
          'css-loader',
          /*
            css兼容性处理：postcss --> postcss-loader postcss-preset-env
            帮postcss找到package.json中browserslist里面的配置，通过配置加载指定的css兼容性样式
          */
          // 使用loader的默认配置
          // 'postcss-loader',
          // 修改loader的配置
          {
            loader: 'postcss-loader',
            options: {
              ident: 'postcss',
              plugins: () => [
                // postcss的插件
                require('postcss-preset-env')()
              ]
            }
          }
        ]
      }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html'
    }),
    new MiniCssExtractPlugin({
      filename: 'css/built.css'
    })
  ],
  mode: 'development'
};

```

### 压缩 CSS

css 压缩后体积会更小，加载更快

* 下载插件`optimize-css-assets-webpack-plugin`
* 引入 `const OptimizeCssAssetsWebpackPlugin = require('optimize-css-assets-webpack-plugin')`
* 在 plugin 中配置

```js
plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html'
    }),
    new MiniCssExtractPlugin({
      filename: 'css/built.css'
    }),
    // 压缩css
    new OptimizeCssAssetsWebpackPlugin()
  ],
```



## JS

### ESLint

* 首先在 package.json 中 eslintConfig 中设置

```js
"eslintConfig": {
                "extends": "airbnb-base"
}
```

* 配置 eslint loader，需要先下载它的两个依赖
  * exclue 排除 node_modules ，不检查安装的包

```js
rules: [
      /*
        语法检查： eslint-loader  eslint
          注意：只检查自己写的源代码，第三方的库是不用检查的
            airbnb --> eslint-config-airbnb-base  eslint-plugin-import eslint
      */
      {
        test: /\.js$/,
        exclude: /node_modules/,
        loader: 'eslint-loader',
        options: {
          // 自动修复eslint的错误
          fix: true
        }
      }
    ]
```

* 在代码中如果想要下一行 eslint 所有规则都失效，则添加注释：

```js
// eslint-disable-next-line
console.log(add(2, 5))
```

### js 兼容性处理

```js
    rules: [
      /*
        js兼容性处理：babel-loader @babel/core 
          1. 基本js兼容性处理 --> @babel/preset-env
            问题：只能转换基本语法，如promise高级语法不能转换
          2. 全部js兼容性处理 --> @babel/polyfill  
            问题：我只要解决部分兼容性问题，但是将所有兼容性代码全部引入，体积太大了~
          3. 需要做兼容性处理的就做：按需加载  --> core-js
      */  
      {
        test: /\.js$/,
        exclude: /node_modules/,
        loader: 'babel-loader',
        options: {
          // 预设：指示babel做怎么样的兼容性处理
          presets: [
            [
              '@babel/preset-env',
              {
                // 按需加载
                useBuiltIns: 'usage',
                // 指定core-js版本
                corejs: {
                  version: 3
                },
                // 指定兼容性做到哪个版本浏览器
                targets: {
                  chrome: '60',
                  firefox: '60',
                  ie: '9',
                  safari: '10',
                  edge: '17'
                }
              }
            ]
          ]
        }
      }
    ]
```

### js 和 html 压缩

* 压缩 js 代码，直接修改 `mode: 'production'` 

* 压缩 html 代码，在 `HtmlWebpackPlugin` 插件中添加：

```js
plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html'
    })
  ],
```



# 优化环境配置

### HMR 热模块替换

作用：一个模块发生变化，只会重新打包这一个模块，极大地提升构建速度

使用：在 devServer 中添加

```js
devServer: {
    contentBase: resolve(__dirname, 'build'),
    compress: true,
    port: 3000,
    open: true,
    // 开启HMR功能
    // 当修改了webpack配置，新配置要想生效，必须重新webpack服务
    hot: true
  }
```

* 样式文件：可以使用 HMR，通过 style-loader 内部实现
* html 文件：默认不使用 HMR，且热更新失效
  * 解决：修改 entry 入口，添加 html 文件
  * 这样问题虽然解决了，但是本质上只有一个 html 文件，他一旦使用 HMR，又会导致所有的文件更新，所以没有必要开启
* js 文件：默认不使用 HMR
  * 解决：需要向 js 文件内添加代码，例子如下

```js
// 引入
import print from './print';
import '../css/iconfont.css';
import '../css/index.less';

console.log('index.js文件被加载了~');

print();

function add(x, y) {
  return x + y;
}

console.log(add(1, 3));

if (module.hot) {
  // 一旦 module.hot 为true，说明开启了HMR功能。 --> 让HMR功能代码生效
  module.hot.accept('./print.js', function() {
    // 方法会监听 print.js 文件的变化，一旦发生变化，其他模块不会重新打包构建。
    // 会执行后面的回调函数
    print();
  });
}
```



### source-map 错误定位

一种提供源代码到构建后代码映射技术，如果构建后代码出错了，通过映射可以追踪源代码错误

* 使用方法：添加 `devtool: 'eval-source-map'`

`[inline-|hidden-|eval-][nosources-][cheap-[module-]]source-map`

* source-map：外部
  * 错误代码准确信息 和 源代码的错误位置

* inline-source-map：内联
  * 只生成一个内联source-map
  * 错误代码准确信息 和 源代码的错误位置

* hidden-source-map：外部
  * 错误代码错误原因，但是没有错误位置
  * 不能追踪源代码错误，只能提示到构建后代码的错误位置

* eval-source-map：内联
  * 每一个文件都生成对应的source-map，都在eval
  * 错误代码准确信息 和 源代码的错误位置

* nosources-source-map：外部
  * 错误代码准确信息, 但是没有任何源代码信息

* cheap-source-map：外部
  * 错误代码准确信息 和 源代码的错误位置 
  * 只能精确的行

* cheap-module-source-map：外部
  * 错误代码准确信息 和 源代码的错误位置 
  * module会将loader的source map加入



内联 和 外部的区别：1. 外部生成了文件，内联没有 2. 内联构建速度更快



* 开发环境：速度快，调试更友好

  * 速度快(eval>inline>cheap>...)

    * eval-cheap-souce-map

    * eval-source-map
    
  * 调试更友好  
    * souce-map
    
    * cheap-module-souce-map
  
    * cheap-souce-map
    
  * --> eval-source-map  / eval-cheap-module-souce-map



* 生产环境：源代码要不要隐藏? 调试要不要更友好
  * 内联会让代码体积变大，所以在生产环境不用内联
  * nosources-source-map 全部隐藏
  * hidden-source-map 只隐藏源代码，会提示构建后代码错误信息
  * --> source-map / cheap-module-souce-map



### 缓存

* babel缓存
  * `catchDirectory: true`
  * 让第二次打包构建速度更快
* 文件资源缓存
  * hash：每次wepack构建时会生成一个唯一的hash值
    * 问题：因为js和css同时使用一个hash值。如果重新打包，会导致所有缓存失效。（可能我却只改动一个文件）
  * chunkhash：根据chunk生成的hash值。如果打包来源于同一个chunk，那么hash值就一样
    * 问题: js和css的hash值还是一样的，因为css是在js中被引入的，所以同属于一个chunk
  * contenthash: 根据文件的内容生成hash值。不同文件hash值一定不一样
    * 最终的解决方案，可以使代码上线运行缓存更好用

```js
const { resolve } = require('path');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
const OptimizeCssAssetsWebpackPlugin = require('optimize-css-assets-webpack-plugin');
const HtmlWebpackPlugin = require('html-webpack-plugin');

// 定义nodejs环境变量：决定使用browserslist的哪个环境
process.env.NODE_ENV = 'production';

// 复用loader
const commonCssLoader = [
  MiniCssExtractPlugin.loader,
  'css-loader',
  {
    // 还需要在package.json中定义browserslist
    loader: 'postcss-loader',
    options: {
      ident: 'postcss',
      plugins: () => [require('postcss-preset-env')()]
    }
  }
];

module.exports = {
  entry: './src/js/index.js',
  output: {
    filename: 'js/built.[contenthash:10].js',
    path: resolve(__dirname, 'build')
  },
  module: {
    rules: [
      {
        // 在package.json中eslintConfig --> airbnb
        test: /\.js$/,
        exclude: /node_modules/,
        // 优先执行
        enforce: 'pre',
        loader: 'eslint-loader',
        options: {
          fix: true
        }
      },
      {
        // 以下loader只会匹配一个
        // 注意：不能有两个配置处理同一种类型文件
        oneOf: [
          {
            test: /\.css$/,
            use: [...commonCssLoader]
          },
          {
            test: /\.less$/,
            use: [...commonCssLoader, 'less-loader']
          },
          /*
            正常来讲，一个文件只能被一个loader处理。
            当一个文件要被多个loader处理，那么一定要指定loader执行的先后顺序：
              先执行eslint 在执行babel
          */
          {
            test: /\.js$/,
            exclude: /node_modules/,
            loader: 'babel-loader',
            options: {
              presets: [
                [
                  '@babel/preset-env',
                  {
                    useBuiltIns: 'usage',
                    corejs: { version: 3 },
                    targets: {
                      chrome: '60',
                      firefox: '50'
                    }
                  }
                ]
              ],
              // 开启babel缓存
              // 第二次构建时，会读取之前的缓存
              cacheDirectory: true
            }
          },
          {
            test: /\.(jpg|png|gif)/,
            loader: 'url-loader',
            options: {
              limit: 8 * 1024,
              name: '[hash:10].[ext]',
              outputPath: 'imgs',
              esModule: false
            }
          },
          {
            test: /\.html$/,
            loader: 'html-loader'
          },
          {
            exclude: /\.(js|css|less|html|jpg|png|gif)/,
            loader: 'file-loader',
            options: {
              outputPath: 'media'
            }
          }
        ]
      }
    ]
  },
  plugins: [
    new MiniCssExtractPlugin({
      filename: 'css/built.[contenthash:10].css'
    }),
    new OptimizeCssAssetsWebpackPlugin(),
    new HtmlWebpackPlugin({
      template: './src/index.html',
      minify: {
        collapseWhitespace: true,
        removeComments: true
      }
    })
  ],
  mode: 'production',
  devtool: 'source-map'
};

```



### Tree shaking 去除无用代码

tree shaking 作用是去除 js 中没有使用的代码，见效代码体积

使用前提：

* 必须使用 ES6 模块化
* 开启 production 环境

这样即可使用，但是可能会把css / @babel/polyfill （副作用）文件干掉

因此，在 package.json 中配置：`"sideEffects": ["*.css", "*.less"]` 去除副作用



### Code split 代码分割

以往的打包过程，所有的 js 文件会打包成一个文件，如果想要分开打包成多个 js 文件，就要用到代码分割

* 方法一：修改 entry 入口，改为多入口

```js
module.exports = {
  // 单入口
  // entry: './src/js/index.js',
  entry: {
    // 多入口：有一个入口，最终输出就有一个bundle
    index: './src/js/index.js',
    test: './src/js/test.js'
  },
  output: {
    // [name]：取文件名
    filename: 'js/[name].[contenthash:10].js',
    path: resolve(__dirname, 'build')
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html',
      minify: {
        collapseWhitespace: true,
        removeComments: true
      }
    })
  ],
  mode: 'production'
};
```

* 方法二：通过 js 代码，让某个文件被单独打包成一个 chunk，动态导入

```js
function sum(...args) {
  return args.reduce((p, c) => p + c, 0);
}
/*
  通过js代码，让某个文件被单独打包成一个chunk
  import动态导入语法：能将某个文件单独打包
*/
import(/* webpackChunkName: 'test' */'./test')
  .then(({ mul, count }) => {
    // 文件加载成功~
    // eslint-disable-next-line
    console.log(mul(2, 5));
  })
  .catch(() => {
    // eslint-disable-next-line
    console.log('文件加载失败~');
  });

// eslint-disable-next-line
console.log(sum(1, 2, 3, 4));
```

### Lazy loading 懒加载

使用时才加载

```js
console.log('index.js文件被加载了~');

// import { mul } from './test';

document.getElementById('btn').onclick = function() {
  // 懒加载~：当文件需要使用时才加载~
  // 预加载 prefetch：会在使用之前，提前加载js文件 
  // 正常加载可以认为是并行加载（同一时间加载多个文件）  
  // 预加载 prefetch：等其他资源加载完毕，浏览器空闲了，再偷偷加载资源
  import(/* webpackChunkName: 'test', webpackPrefetch: true */'./test').then(({ mul }) => {
    console.log(mul(4, 5));
  });
};
```



### PWA 离线访问

PWA 是渐进式网络开发应用程序，需要用到 workbox

* `npm install workbox-webpack-plugin`
* import 引入
* 配置 plugin

```js
new WorkboxWebpackPlugin.GenerateSW({
      /*
        1. 帮助serviceworker快速启动
        2. 删除旧的 serviceworker

        生成一个 serviceworker 配置文件~
      */
      clientsClaim: true,
      skipWaiting: true
    })
```

* 在入口 index.js 文件中配置 serviceworker

```js
import { mul } from './test';
import '../css/index.css';

function sum(...args) {
  return args.reduce((p, c) => p + c, 0);
}

// eslint-disable-next-line
console.log(mul(2, 3));
// eslint-disable-next-line
console.log(sum(1, 2, 3, 4));

/*
  1. eslint不认识 window、navigator全局变量
    解决：需要修改package.json中eslintConfig配置
      "env": {
        "browser": true // 支持浏览器端全局变量
      }
   2. sw代码必须运行在服务器上
      --> nodejs
      -->
        npm i serve -g
        serve -s build 启动服务器，将build目录下所有资源作为静态资源暴露出去
*/
// 注册serviceWorker
// 处理兼容性问题
if ('serviceWorker' in navigator) {
  window.addEventListener('load', () => {
    navigator.serviceWorker
      .register('/service-worker.js')
      .then(() => {
        console.log('sw注册成功了~');
      })
      .catch(() => {
        console.log('sw注册失败了~');
      });
  });
}

```



### 多进程打包 thread-loader

开启多进程打包。 进程启动大概为600ms，进程通信也有开销。只有工作消耗时间比较长，才需要多进程打包。

```js
{
      loader: 'thread-loader',
      options: {
        workers: 2 // 进程2个
      }
},
```



### DLL 第三方库打包

* 创建 webpack.dll.js 文件

```js
/*
  使用dll技术，对某些库（第三方库：jquery、react、vue...）进行单独打包
    当你运行 webpack 时，默认查找 webpack.config.js 配置文件
    需求：需要运行 webpack.dll.js 文件
      --> webpack --config webpack.dll.js
*/

const { resolve } = require('path');
const webpack = require('webpack');

module.exports = {
  entry: {
    // 最终打包生成的[name] --> jquery
    // ['jquery'] --> 要打包的库是jquery
    jquery: ['jquery'],
  },
  output: {
    filename: '[name].js',
    path: resolve(__dirname, 'dll'),
    library: '[name]_[hash]' // 打包的库里面向外暴露出去的内容叫什么名字
  },
  plugins: [
    // 打包生成一个 manifest.json --> 提供和jquery映射
    new webpack.DllPlugin({
      name: '[name]_[hash]', // 映射库的暴露的内容名称
      path: resolve(__dirname, 'dll/manifest.json') // 输出文件路径
    })
  ],
  mode: 'production'
};

```

* 运行 `webpack --config webpack.dll.js`

* 在 webpack.config.js 中编辑，告诉 webpack 哪些库不需要打包

```js
plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html'
    }),
    // 告诉webpack哪些库不参与打包，同时使用时的名称也得变~
    new webpack.DllReferencePlugin({
      manifest: resolve(__dirname, 'dll/manifest.json')
    }),
    // 将某个文件打包输出去，并在html中自动引入该资源
    new AddAssetHtmlWebpackPlugin({
      filepath: resolve(__dirname, 'dll/jquery.js')
    })
  ],
```

