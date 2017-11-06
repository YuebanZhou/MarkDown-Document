# Express.js

## 相关文章

- [MDN - JSON.stringify()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)
- [MDN - FileReader](https://developer.mozilla.org/zh-CN/docs/Web/API/FileReader)
- [MDN - FormData](https://developer.mozilla.org/zh-CN/docs/Web/API/FormData)
- [Express - 中文网](http://www.expressjs.com.cn/)
- [Express - 英文官网](http://expressjs.com/)
- [Node.js 教程](http://www.runoob.com/nodejs/nodejs-tutorial.html)
- [菜鸟教程 - Express 4.x API 中文文档](https://www.runoob.com/w3cnote/express-4-x-api.html)
- [Express.js 4.0 的路由（Router）功能用法教學](https://blog.gtwang.org/programming/learn-to-use-the-new-router-in-expressjs-4/)
- [github - art-template](https://github.com/aui/art-template)
- [github - express-art-template](https://github.com/aui/express-art-template)
- [github - ejs](https://github.com/mde/ejs)
- [GMT和UTC有什么区别？格林尼治标准时（GMT）与世界时（UTC）是怎么回事](http://www.wbiao.cn/cartier-watches/knowledge/article-1468.html)
- [node.js中express-session配置项详解](http://blog.csdn.net/liangklfang/article/details/50998959)
- [MD5在线生成器1](http://www.cmd5.com/)
- [MD5在线生成器2](http://pmd5.com/)
- [JavaScript-MD5](https://github.com/blueimp/JavaScript-MD5)



## 概念

- Express 是一个基于 Node.js 平台的极简、灵活的 web 应用开发框架；
- Express 不对 Node.js 已有的特性进行二次抽象，只是在Node.js之上扩展了构建 Web 应用所需的基本功能。
- Express框架并没有覆盖或删除原生的API，而是基于原生的API，做了进一步的封装，提供了更好用的一些API，方便快速进行Web开发。
- res.render、res.json、res.redirect、req.query
- Node.js是Javascript的服务器端运行环境，express只是基于Node，提供了开发Web应用的框架和API。

## 对比

### 创建web服务器

#### 原始方式

```javascript
// 导入 express 模块
const http = require('http')
// 创建一个服务器
const server = http.createServer()
server.on('request', (req, res) => {
  res.end('<h1>我发中文能乱码，你能吗？？</h1>')
})
server.listen(3000, () => {
  console.log('server running at http://127.0.0.1:3000')
})
```

#### express方式

```javascript
// 导入 express 模块
const express = require('express')
// 创建一个服务器
const app = express()
// 使用 app.use 方法，接收客户端的任何method类型的任何URL地址请求
app.use('/index', (req, res) => {
  // res.end('express ok')
  // res.end('试试就试试，who 怕 who')
  res.send('<h3>试试就试试，who 怕 who</h3>')
})
// 启动express服务器
app.listen(3001, () => {
  console.log('express server running at http://127.0.0.1:3001')
})
```

### 返回不同内容

#### 原始方式

```javascript
// 导入 http 内置模块
const http = require('http')
// 创建一个 http 服务器
const server = http.createServer()
// 监听 http 服务器的 request 请求
server.on('request', function (req, res) {
  const url = req.url
  const method = req.method.toLowerCase()
  res.writeHeader(200, {
    'Content-Type': 'text/html; charset=utf-8'
  })
  if (method === 'get' && url === '/') {
    res.end('<h1>首页</h1>')
  } else if (method === 'get' && url === '/movie') {
    res.end('<h1>电影</h1>')
  } else if (method === 'post' && url === '/about') {
    res.end('<h1>关于</h1>')
  } else {
    res.end('404')
  }
})
// 指定端口号并启动服务器监听
server.listen(3000, function () {
  console.log('server listen at http://127.0.0.1:3000')
})
```

#### express方式

```javascript
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()
// 使用 app.use 可以接收所有请求  app.use(function(req, res){})
app.get('/', (req, res) => {
  res.send('<h1>express - 首页</h1>')
})
app.get('/movie', (req, res) => {
  res.send('<h1>express - 电影</h1>')
})
app.post('/about', (req, res) => {
  res.send('<h1>express - 关于</h1>')
})
app.use((req, res) => {
  res.send('404')
})
// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(3001, function () {
  console.log('Express server running at http://127.0.0.1:3001')
})
```

### 返回不同页面1

#### 原始方式

```javascript
// 导入 http 内置模块
const http = require('http')
const fs = require('fs')
// 创建一个 http 服务器
const server = http.createServer()
// 监听 http 服务器的 request 请求
server.on('request', function (req, res) {
  const url = req.url
  const method = req.method.toLowerCase()
  res.writeHeader(200, {
    'Content-Type': 'text/html; charset=utf-8'
  })
  if (method === 'get' && url === '/') {
    fs.readFile(__dirname + '/views/index.html', (err, buf) => {
      res.end(buf)
    })
  } else if (method === 'get' && url === '/movie') {
    fs.readFile(__dirname + '/views/movie.html', (err, buf) => {
      res.end(buf)
    })
  } else if (method === 'post' && url === '/about') {
    fs.readFile(__dirname + '/views/about.html', (err, buf) => {
      res.end(buf)
    })
  } else {
    res.end('404')
  }
})
// 指定端口号并启动服务器监听
server.listen(3000, function () {
  console.log('server listen at http://127.0.0.1:3000')
})
```

#### express方式

```javascript
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()
app.get('/', (req, res) => {
  // res.render('index', {})
  res.sendFile(__dirname + '/views/index.html')
})
app.get('/movie', (req, res) => {
  // res.render('movie', {})
  res.sendFile(__dirname + '/views/movie.html')
})
app.post('/about', (req, res) => {
  // res.render('about', {})
  res.sendFile(__dirname + '/views/about.html')
})
app.listen(3001, function () {
  console.log('App listening on port 3001!');
});
```

### 返回不同页面2抽离

#### 原始方式

```javascript
//入口函数
// 导入 http 内置模块
const http = require('http')
const router = require('./01.router.js')
// 创建一个 http 服务器
const server = http.createServer()
// 监听 http 服务器的 request 请求
server.on('request', function (req, res) {
  router(req, res)
})
// 指定端口号并启动服务器监听
server.listen(3000, function () {
  console.log('server listen at http://127.0.0.1:3000')
})
```

```javascript
//router函数
//导入内置模块
const fs = require('fs')
// 封装 路由模块
module.exports = function (req, res) {
  const url = req.url
  const method = req.method.toLowerCase()
  res.writeHeader(200, {
    'Content-Type': 'text/html; charset=utf-8'
  })
  if (method === 'get' && url === '/') {
    fs.readFile(__dirname + '/views/index.html', (err, buf) => {
      res.end(buf)
    })
  } else if (method === 'get' && url === '/movie') {
    fs.readFile(__dirname + '/views/movie.html', (err, buf) => {
      res.end(buf)
    })
  } else if (method === 'post' && url === '/about') {
    fs.readFile(__dirname + '/views/about.html', (err, buf) => {
      res.end(buf)
    })
  } else {
    res.end('404')
  }
}
```

#### express

```javascript
//入口函数
//引入模块
const express = require('express')
const myrouter = require('./02.express-router1.js')
// 导入自己的express路由分发模块
const router = require('./02.express-router2.js')
const app = express()
// 第一种实现express路由的形式
// myrouter(app)
// 这里的 app.use 可以引申为 注册的意思
// 将路由模块，注册到 app 服务器上
app.use(router)
app.listen(3001, function () {
  console.log('App listening on port 3001!');
});
```

```javascript
//router函数第一种
module.exports = function (app) {
  app.get('/', (req, res) => {
    // res.render('index', {})
    res.sendFile(__dirname + '/views/index.html')
  })
  app.get('/movie', (req, res) => {
    // res.render('movie', {})
    res.sendFile(__dirname + '/views/movie.html')
  })
  app.post('/about', (req, res) => {
    // res.render('about', {})
    res.sendFile(__dirname + '/views/about.html')
  })
}

//router函数第二种
const express = require('express')
//下面这行代码，创建的是一个 express 类型的 web 服务器
//const app = express()
//调用 express.Router() 方法，得到一个 路由对象
const router = express.Router()
//将创建的 router 对象，通过调用 .get  或  .post  或  .use  来绑定路由
router.get('/', (req, res, next) => {
  // res.render('index', {})
  // res.sendFile(__dirname + '/views/index.html')
  console.log('先执行了第一个处理函数')
  next();
}, (req, res) => {
  console.log('第二个处理函数')
})
router.get('/movie', (req, res) => {
  // res.render('movie', {})
  res.sendFile(__dirname + '/views/movie.html')
})
router.post('/about', (req, res) => {
  // res.render('about', {})
  res.sendFile(__dirname + '/views/about.html')
})
//把创建好的路由对象，通过模块导出的形式，暴露给外界的调用者
module.exports = router
```

### 处理静态资源

#### html页面

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>
  <h1>首页</h1>
  /*js文件中虚拟路径是什么，这里的路径就是什么*/
  <img src="./myVirtualPath/1.jpg" alt="">
  <img src="./myVirtualPath/2.jpg" alt="">
</body>
</html>
```

#### express

```javascript
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()
// 问题： 如果我访问图片的时候，很任性，就想在路径前面带上 images/  
app.use('/myVirtualPath', express.static('images'))  // 1.jpg
// 注意： 在使用 app.use(express.static('托管资源目录')) 的时候，可以在前面挂载虚拟路径
app.get('/', (req, res) => {
  res.sendFile(__dirname + '/index.html')
})
// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(3001, function () {
  console.log('Express server running at http://127.0.0.1:3001')
})
```

## 链式

express中也可以进行链式编程，挂载到app或者router上

```javascript
router
  .get('/', (req, res) => { // 挂载处理根路径的路由
    res.sendFile(path.join(__dirname, './views/index.html'))
  })
  .get('/movie', (req, res) => { // 挂载处理/movie的路由
    res.sendFile(path.join(__dirname, './views/movie.html'))
  })
```

## 中间件

### 概念

- 中间件（Middleware）是一个函数，它可以访问请求对象（request object (req)）, 响应对象（response object (res)）, 和 web 应用中处于请求-响应循环流程中的中间件，一般被命名为 next 的变量。
- 经过中间件的处理之后，express就向 req 和 res ,对象身上，挂在了一些好用的方法和属性
  - req.query
  - res.send()解决中文乱码问题
  - res.json()
  - res.use可以挂载地址，不挂载的时候，使用所有地址

### 中间件的功能

- 执行任何代码。
- 修改请求和响应对象。
- 终结请求-响应循环。
- 调用堆栈中的下一个中间件。

### 使用步骤

- 在express中，可以使用body-parser第三方中间件，去帮我们出去post提交过来的数据
- 使用npm安装
- 导入这个第三方中间件模块
- 使用app.use()注册刚才导入的中间件，到app身上
- 调多个函数的时候，前边的函数加一个参数next，然后在函数的最后调用一下next()
- res.end不影响next的执行
- 中间件res.end只能执行一次
- 任何修改都应该放到next的调用之前

### 形式上的分类

- 应用级别的中间件：所有挂载到app身上的方法，都叫做应用级别的中间件app.get，app.post，app.use
- 路由级别的中间件：挂载到了router对象上，这个router对象是经过调用express.Router()得到了，router.get，router.post，router.use
- 错误处理中间件:有四个参数err,req,res,next
- express唯一的一个内置中间件：express.static(root,[options])用于托管静态资源
- 第三方中间件：非Express官方提供的中间件，叫做第三方中间件

### express.static

- 使用express.static托管资源文件和静态页面

```javascript
//表示views文件夹下的文件全部被托管
app.use(express.static('./views'))
app.use('/node_modules', express.static('./node_modules'))
```



## 路由

- 定义路由的 router文件：

```javascript
//引包
var express = require('express');
// 使用 express 的 Router() 方法，得到一个路由实例
var router = express.Router();
// 通过 Method 和 请求路径，分发不同的请求到不同的处理函数中
router.get('/', function (req, res) {
  res.send('<h1>首页</h1>');
}).get('/movie', function (req, res) {
res.send('<h1>电影</h1>');
});
module.exports = router;
```

- 导入路由并注册使用

```javascript
var express = require('express');
// 导入路由
var router = require('./router');
// 创建一个 app 出来
var app = express();
// 注册路由
app.use(router);
// 启动 app 监听程序
app.listen(3000, function () {
  console.log('App running at http://127.0.0.1:3000');
});
```

## ejs

### ejs 的使用步骤

- 运行npm i ejs -S安装依赖包
- 使用app.set('view engine', 'ejs') 指定express渲染页面时候的默认模板引擎
- app.set('view engine', '模板引擎名称') 中的，第一个参数，view engine是固定写法，表示我们要设置默认模板引擎了
- ejs默认的模板页面后缀名是.ejs


- 默认，express 的模板页面存放路径，就是项目根目录中views文件夹；这个默认存放路径是可以修改的
- 可以手动修改 默认模板页面的存放路径
- 可以使用app.set方法，修改默认模板页面存放路径，第一个参数是固定写法 ，是 'views' 字符串，表示要设置模板页面路径， 第二个参数是模板页面的存放路径

#### app入口模块

```javascript
const express = require('express')
// 得到一个 express web 服务器     app    ->     application
const app = express()
// 导入 ejs 模块
const ejs = require('ejs')
//  使用 ejs.delimiter 修改 ejs 的界定符， 默认的界定符是 % 
ejs.delimiter = '%'
// 托管静态资源
app.use('/node_modules', express.static('./node_modules'))
// 注册路由模块
const router = require('./router.js')
app.use(router)
app.set('view engine', 'ejs')
app.set('views', './views')
app.listen(3000, function () {
  console.log('Server running at http://127.0.0.1:3000');
});
```

#### router模块

```javascript
const path=require('path')
const router=express.Router()
router
.get('/',(req,res)=>{
  	//使用express封装的res.render函数，进行服务器端页面渲染
  	//express没有提供默认的模板引擎
  	//使用res.render之前需要先自己先配置一个模板引擎，供express去调用
  	//第一个参数是模板的名称，第二个参数是模板要渲染的数据
    res.render('index',{
        title:'使用EJS渲染页面',
        hobby:['吃饭','睡觉']
    })  
})
.get('/movie',(req,res)=>{
    res.render('movie.ejs',{})
})
module.exports=router
```

#### html模板

```html
<body>
	<h1 style="color:<%= !isShow?'red':'' %>;">这是EJS的模板页面<%= username %></h1>
	<% if(!isShow){ %>
		<h3>这是一个漂亮的h3标题</h3>
	<% } %>
	<ul>
		<% hobby.forEach(function(item, i){ %>
			<li><%= item %></li>
		<% }) %>
	</ul>
</body>
```

### 公共模板

```html
<!--导入公共的头部-->
<?- include('header') ?>
<h1>ejs</h1>
  <ul>
    <? names.forEach(function(item){ ?>
      <li><?= item ?></li>
    <? }) ?>
  </ul>
<!--导入公共的底部-->
<?- include('footer') ?>
```

## 修改后缀名

### ejs方法

- 导入模块，创建服务器


- 使用app.engine自定义一个模板引擎
  - 第一个参数是字符串，表示自定义模板引擎的名称，这个名称也是模板页面后缀名
  - 第二个参数是方法的引用，表示调用哪个方法去渲染模板页面

```javascript
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()
const ejs = require('ejs')
app.engine('html', ejs.renderFile)

//宇宙最强编辑器，没有之一 ：  Visual Studio  VS  编辑器 的英文代号 叫做  IDE（集成开发环境）
//前端用的 VS Code  全称是 Visual Studio Code  是一个精简版的 VS

// 设置默认模板引擎，如果不设置 调用 res.render 会报错
app.set('view engine', 'html')
// 设置默认模板页面的存放路径
app.set('views', './views')
app.get('/', (req, res) => {
  res.render('index.html', { title: 'QQQ' })
})
// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(3001, function () {
  console.log('Express server running at http://127.0.0.1:3001')
})
```

### art-template 方法

{0}. 先安装相关的包
{0}. 使用app.engine自定义一个模板引擎
{0}. 使用app.set把自定义的模板引擎，设置为express 默认的模板引擎

```
npm install --save art-template
npm install --save express-art-template
```

```javascript
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()
//使用app.engine自定义一个模板引擎
app.engine('html', require('express-art-template'))
//使用app.set把自定义的模板引擎，设置为express 默认的模板引擎
//第二个参数表示模板引擎的名称
app.set('view engine', 'html')
app.get('/', (req, res) => {
  res.render('index', { title: 'express 渲染的页面' })
})
// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(3001, function () {
  console.log('Express server running at http://127.0.0.1:3001')
})
```



## MD5加密

- MD5的全称是Message-Digest Algorithm 5（信息-摘要算法），在90年代初由MIT Laboratory for Computer Science和RSA Data Security Inc的Ronald L. Rivest开发出来，经MD2、MD3和MD4发展而来。
- MD5加密的特性：
  - MD5加密后输出的是32位长度的字符串
  - 相同的内容使用MD5加密后，得到的内容是一致的
  - MD5加密后的字符串是无法通过算法的形式反向解密的（唯一的破解方式是暴力碰撞破解）
  - 为了防止暴力碰撞破解，我们可以对需要加密的内容，进行加盐处理
  - 加盐处理：就是在需要加密的文本内容，和一串长且复杂的文本进行拼接，这样就能防止加密后的MD5值被暴力碰撞破解。
  - 为什么要加盐加密：就是为了防止用户的密码过于简单，然后我们程序通过加盐，提高了密码的复杂性，这样能够保证用户信息的安全。
- 登录注册
  - 注册的时候，写入密码，加盐，对密码进行加密
  - 登录的时候，输入密码，服务器进行加盐处理，如果得到的结果和数据库中的内容一样，证明密码正确
  - MD5加密同一条数据，得出的结果是一样的

### 使用

{0}. 运行以下命令安装MD5加密模块：

```
npm install blueimp-md5 -S
```

{0}. 使用方式：

```
var hash = md5("需要被加密的字符串", "盐");
```

```javascript
const md5=require('blueimp-md5')
module.exprots={
    pwdSalt:'!@#$%',
  	md5Ecode(originPwd){
        return md5(originPwd,this.pwdSalt)
    }
}
```

## HTTP协议的无状态性

{0}. HTTP协议的通信模型：基于请求 - 处理 - 响应的。
{0}. 由于这个通信协议的关系，导致了HTTP每个请求之间都是没有关联的，每当一个请求完成之后，服务器就忘记之前谁曾经请求过。
{0}. 如果纯粹基于HTTP通信模型，是无法完成登录状态保持的！每次请求服务器，服务器都会把这个请求当作新请求来处理。
{0}. 我们可以通过 cookie 技术，实现状态保持，但是由于cookie是存储在客户端的一门技术，所以安全性几乎没有，因此不要使用cookie存储敏感的数据。

## cookie

### 概念

- 由于Http协议是无状态的，且传统服务器只能被动的响应请求，所以，当服务器获取到请求的时候，并不知道当前请求属于哪个客户端。
- 服务器为了能够明确区分每个客户端，需要使用一些小技术，来根据不同的请求区分不同的客户端。
- 只要有请求发生，那么必然对应一个客户端，那么，我们可以在每次客户端发起请求的时候，向服务器自动发送一个标识符，告诉服务器当前是哪个客户端正在请求服务器的数据。
- 在请求头(Request Headers)中添加一个标签，叫做cookie，这样，每次发送请求，都会把这个cookie随同其他报文一起发送给服务器，服务器可以根据报文中的cookie，区分不同的客户端浏览器。


- 在Node中可以在writeHeader的时候，通过Set-Cookie来将cookie标识通过响应报文发送给客户端。
- 客户端也可以通过一些方式来操作自己的cookie，比如通过jquery.cookie这个插件。

### 使用

```javascript
var http = require('http');
var server = http.createServer();
server.on('request', function (req, res) {
    // 解析cookie
    var cookies = {};
    var cookieStr = req.headers.cookie; // 从请求的headers中获取cookie信息
    cookieStr && cookieStr.split(';').forEach(function (item) {
        var parts = item.split('=');
        cookies[parts[0].trim()] = parts[1].trim(); // 将cookie解析出来，保存到对象中
    });
    res.writeHeader(200, {
        'Content-Type': 'text/plain; charset=utf-8',
        "Set-Cookie": ['issend=ok', 'age=20']
    });
    if(cookies.issend ==='ok'){
        res.end('不要太贪心哦！');
    }else{
        res.end('呐，赏你一朵小红花~~');
    }
});
server.listen(4000, function () {
    console.log('服务器已启动!');
});
```

### 过期时间

```javascript
// 设置 过期时间 为60秒之后
// 注意：在设置过期时间的时候，需要将时间转换为 UTC 格式
var expiresTime = new Date(Date.now() + 1000 * 60).toUTCString();
res.writeHeader(200, {
  'Content-Type': 'text/html; charset=utf-8',
  'Set-Cookie': ['isvisit=true;expires=' + expiresTime, 'test=OK']
});
res.end('<h3>你好，欢迎光临，送给你一个苹果！</h3>');
```

### 不安全

- 使用谷歌插件edit this cookie，就能伪造cookie数据，所以不要使用cookie存储敏感的数据，比如登录状态和登录信息。

- 一些敏感的数据，应该存储都服务器端。

## 登录退出及状态保存

### express-session

- 由于HTTP是无状态的，所以服务器在每次连接中持续保存客户端的私有数据，此时需要结合cookie技术，通过session会话机制，在服务器端保存每个HTTP请求的私有数据；



- 在服务器内存中开辟一块地址空间，专门存放每个客户端私有的数据，每个客户端根据cookie中保存的私有sessionId，可以获取到独属于自己的session数据。


### 使用session

- 安装session模块


```
npm install express-session -S
```

- 导入session模块


```javascript
var session = require('express-session')
```

- 在express中使用session中间件：


```javascript
// 启用 session 中间件
app.use(session({
  secret: 'keyboard cat', // 相当于是一个加密密钥，值可以是任意字符串
  resave: false, // 强制session保存到session store中
  saveUninitialized: false // 强制没有“初始化”的session保存到storage中
}))
```

- 将私有数据保存到当前请求的session会话中：


```javascript
// 将登录的用户保存到session中
req.session.user = result.dataValues;
// 设置是否登录为true
req.session.islogin = true;
```

- 通过destroy()方法清空session数据：


```javascript
req.session.destroy(function(err){
  if(err) throw err;
  console.log('用户退出成功！');
  res.redirect('/');
});
```

