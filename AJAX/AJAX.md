# HTTP

HTTP（hypertext transport protocol）协议『超文本传输协议』，协议详细规定了浏览器和万维网服务器之间互相通信的规则。
约定, 规则

## 请求报文

重点是格式与参数

```
行      POST  /s?ie=utf-8  HTTP/1.1 
头      Host: atguigu.com
        Cookie: name=guigu
        Content-type: application/x-www-form-urlencoded
        User-Agent: chrome 83
空行
体      username=admin&password=admin
```

## 响应报文

```
行      HTTP/1.1  200  OK
头      Content-Type: text/html;charset=utf-8
        Content-length: 2048
        Content-encoding: gzip
空行    
体      <html>
            <head>
            </head>
            <body>
                <h1>尚硅谷</h1>
            </body>
        </html>
```

* 404
* 403
* 401
* 500
* 200



# GET

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    #result {
      width: 200px;
      height: 200px;
      border: solid 1px;
    }
  </style>
</head>

<body>
  <button>点击发送请求</button>
  <div id="result"></div>

  <script>
    var btn = document.getElementsByTagName('button')[0];
    var result = document.getElementById("result")
    btn.onclick = function () {
     //1. 创建对象
      const xhr = new XMLHttpRequest();
      //2. 初始化 设置类型与 URL
      xhr.open('GET', 'http://127.0.0.1/server');
      //3. 发送
      xhr.send();
      //4. 事件绑定
      xhr.onreadystatechange = function () {
        if (xhr.readyState === 4) {
          if (xhr.status >= 200 && xhr.status < 300) {
            console.log(xhr.status);
            console.log(xhr.statusText);
            console.log(xhr.getAllResponseHeaders());
            console.log(xhr.response);
            result.innerHTML = xhr.response;
          } else {

          }
        }
      }
    }
  </script>
</body>

</html>
```

若需要请求参数，直接通过?和&跟在URL后面`xhr.open('GET', 'http://127.0.0.1/server?a=100&b=2')`

```javascript
var express = require('express');

var app = express();

app.get('/server', function (request, response) {
  //设置响应头，允许跨域
  response.setHeader('Access-Control-Allow-Origin', '*');
  response.send('hello express');
});

app.listen(8000, () => {
  console.log("服务器已经启动");
})
```



# POST

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    #result {
      width: 200px;
      height: 100px;
      border: solid 1px #903;
    }
  </style>
</head>

<body>
  <div id="result"></div>
  <script>
    const result = document.getElementById('result');
    result.addEventListener('mouseover', function () {
      //1. 创建对象
      const xhr = new XMLHttpRequest();
      //2. 初始化 设置类型与 URL
      xhr.open('POST', 'http://127.0.0.1:8000/server');
      //设置请求头
      xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
      //3. 发送
      xhr.send();
      //4. 事件绑定
      xhr.onreadystatechange = function () {
        //判断
        if (xhr.readyState === 4) {
          if (xhr.status >= 200 && xhr.status < 300) {
            result.innerHTML = xhr.response;
          }
        }
      }
    })
  </script>
</body>

</html>
```

请求参数通过`xhr.send('a=100&b=200&c=300')`发送

# IE缓存问题

IE浏览器会将AJAX获取内容缓存起来，导致下一次AJAX请求无法返回当前值

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    #result {
      width: 200px;
      height: 200px;
      border: solid 1px;
    }
  </style>
</head>

<body>
  <button>点击发送请求</button>
  <div id="result"></div>

  <script>
    var btn = document.getElementsByTagName('button')[0];
    var result = document.getElementById("result")
    btn.onclick = function () {
      var xhr = new XMLHttpRequest();
      xhr.open('GET', 'http://127.0.0.1:8000/ie?t=' + Date.now());
      xhr.send();
      xhr.onreadystatechange = function () {
        if (xhr.readyState === 4) {
          if (xhr.status >= 200 && xhr.status < 300) {
            result.innerHTML = xhr.response;
          } else {

          }
        }
      }
    }
  </script>
</body>

</html>
```

通过在发送请求中加一个`Date.now()`时间戳来避免IE缓存

# 超时与网络异常

```html
 <script>
    var btn = document.getElementsByTagName('button')[0];
    var result = document.getElementById("result")
    btn.onclick = function () {
      var xhr = new XMLHttpRequest();
      //超时设置 2s 未响应就取消
      xhr.timeout = 2000;
      xhr.ontimeout = function () {
        alert('请求超时，请稍后重试')
      } //请求超时处理
      xhr.onerror - function () {
        alert('网络出问题了')
      } //网络异常处理
      xhr.open('GET', 'http://127.0.0.1:8000/delay');
      xhr.send();
      xhr.onreadystatechange = function () {
        if (xhr.readyState === 4) {
          if (xhr.status >= 200 && xhr.status < 300) {
            result.innerHTML = xhr.response;
          } else {

          }
        }
      }
    }
  </script>
```

**手动取消请求**

```html
<script>
  const btns = document.querySelectorAll('button');
  let x = null;
  btns[0].onclick = function () {
    x = new XMLHttpRequest();
    x.open('GET', 'http://127.0.0.1:8000/delay');
    x.send();
  }
  btns[1].onclick = function () {
    x.abort();
  }
</script>
```

**请求重复发送问题**

遇到请求重复发送，用新的请求覆盖之前的请求

```html
<script>
  const btns = document.querySelectorAll('button');
  let x = null;
  let isSending = false; //判断是否在请求中
  btns[0].onclick = function () {
    if (isSending) x.abort();
    x = new XMLHttpRequest();
    isSending = true;
    x.open('GET', 'http://127.0.0.1:8000/delay');
    x.send();
    x.onreadystatechange = function () {
      if (x.readyState === 4) {
        isSending = false;
      }
    }
  }
  btns[1].onclick = function () {
    x.abort();
  }
</script>
```



# 跨域解决方案

1. JSONP
2. CORS
