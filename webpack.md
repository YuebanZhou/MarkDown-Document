#  Webpack

## 相关文章

- [babel-preset-env：你需要的唯一Babel插件](https://segmentfault.com/p/1210000008466178)
- [Runtime transform 运行时编译es6](https://segmentfault.com/a/1190000009065987)
- [webpack官网](http://webpack.github.io/)

## 注意

- 装包过程被打断，停止，再继续的时候，程序可能会报错
  - node_modules删除
  - npm中cache删除
  - 因为有package.json所以cnpm init就可以把原来的包全都下载下来 

## 静态资源

- JS
  - .js  .jsx  .coffee  .ts（TypeScript  类 C# 语言）
  - .coffee和.ts是中间语言，不能直接运行，需要进一步编译


- CSS
  - .css  .less   .sass  .scss
  - .sass更新之后是.scss


- Images
  - .jpg   .png   .gif   .bmp   .svg


- 字体文件（Fonts）
  - .svg   .ttf   .eot   .woff   .woff2


- 模板文件
  - .ejs   .jade  .vue(这是在webpack中定义组件的方式，推荐这么用)
  - .jade是模板名，和.ejs类似


- 网页加载速度慢，因为我们要发起很多的二次请求


- 要处理错综复杂的依赖关系


- 解决
  - 合并、压缩、精灵图、图片的Base64编码
  - 可以使用之前学过的requireJS、也可以使用webpack可以解决各个包之间的复杂依赖关系
  - 图片默认有一个src属性，指向一个地址，图片base64可以将src指向一个64位字符串，适用小图片

## 概念

- webpack 是前端的一个项目构建工具，它是基于 Node.js 开发出来的一个前端工具


- 使用Gulp， 是基于 task 任务的


- 使用Webpack， 是基于整个项目进行构建的
- webpack可以处理JS文件之间的互相依赖关系
- webpack 能够处理JS的兼容问题，把高级的浏览器不识别的语法转为低级的浏览器能正常识别的语法

## 安装

- 运行npm i webpack -g全局安装webpack，这样就能在全局使用webpack的命令


- 在项目根目录中运行npm i webpack --save-dev安装到项目依赖中

## 隔行变色案例

- 运行npm init初始化项目，使用npm管理项目中的依赖包


- 创建项目基本的目录结构


- 使用cnpm i jquery --save安装jquery类库


- 创建main.js并书写各行变色的代码逻辑

```javascript
// 导入jquery类库
import $ from 'jquery'
// 设置偶数行背景色，索引从0开始，0是偶数
$('#list li:even').css('backgroundColor','lightblue');
// 设置奇数行背景色
$('#list li:odd').css('backgroundColor','pink');
```

- 直接在页面上引用main.js会报错，因为浏览器不认识import这种高级的JS语法，这种语法属于ES6，需要使用webpack进行处理，webpack默认会把这种高级的语法转换为低级的浏览器能识别的语法


- 运行webpack 入口文件路径，输出文件路径对main.js进行处理，生成一个bundle.js文件

```
webpack src/js/main.js dist/bundle.js
```

## 配置文件

### 初步

- 在项目根目录中创建webpack.config.js
- 每次更新main.js之后都要重新执行"webpack 要打包的文件的路径 打包好的输出的文件的路径"指令，比较麻烦，可以将路径打包进配置文件
- webpack是基于node的，所以node中的模块，webpack都可以使用，path可以直接导入使用

```javascript
// 导入处理路径的模块
var path = require('path');
// 导出一个配置对象，将来webpack在启动的时候，会默认来查找webpack.config.js，并读取这个文件中导出的配置对象，来进行打包处理
module.exports = {
  // 项目入口文件
  entry: path.resolve(__dirname, 'src/js/main.js'), 
  // 配置输出选项
  output: { 
    // 配置输出的路径
    path: path.resolve(__dirname, 'dist'), 
    // 配置输出的文件名
    filename: 'bundle.js' 
  }
}
```

- 经过上面的配置之后，每次执行webpack就可以了

### 实时编译

- 进一步简洁操作，使用webpack-dev-server来实现代码实时打包编译，当修改代码之后，会自动进行打包构建。


- 运行cnpm i webpack-dev-server --save-dev安装到开发依赖


- 安装完成之后，在命令行直接运行webpack-dev-server来进行打包，发现报错
- 因为这个工具是本地安装的，无法在powershell中执行，只有-g的工具才能正常执行
- 此时需要借助于package.json文件中的指令，来进行运行webpack-dev-server命令，
- 在scripts节点下新增"dev": "webpack-dev-server"指令

```
"scripts": {
	"test": "echo \"Error: no test specified\" && exit 1",
	"dev": "webpack-dev-server"
},
```

- dist目录下并没有生成bundle.js文件，这是因为webpack-dev-server将打包好的文件放在了内存中
- 把bundle.js放在内存中的好处是：由于需要实时打包编译，所以放在内存中速度会非常快

### 直接访问

- 这个时候访问webpack-dev-server启动的http://localhost:8080/网站，发现是一个文件夹的面板，需要点击到src目录下，才能打开我们的index首页，此时引用不到bundle.js文件，需要修改index.html中script的src属性为:\<script src="../bundle.js">\</script>
- 为了能在访问http://localhost:8080/的时候直接访问到index首页，可以使用--contentBase src指令来修改dev指令，指定启动的根目录：

```
"scripts": {
	"test": "echo \"Error: no test specified\" && exit 1",
	"dev": "webpack-dev-server --contentBase src"
},
```

-  同时修改index页面中script的src属性为\<script src="bundle.js">\</script>

### 端口号

- port设置localhost后面的端口号，不一定是8080，可以手动设置成3000

```
"scripts": {
	"test": "echo \"Error: no test specified\" && exit 1",
	"dev2": "webpack-dev-server --open --port 3000 --contentBase src --hot"
},
```

### 热加载

-  dev的配置中添加--hot表示热重载热更新，不会完全生成文件，局部刷新，样式设置的文件不刷新页面

-  上面的一系列内容可以一直到配置文件webpack.config.js中

```javascript
devServer: { 
  // 这是配置 dev-server 命令参数的第二种形式，相对来说，这种方式麻烦一些
  //  --open --port 3000 --contentBase src --hot
  open: true, // 自动打开浏览器
  port: 3000, // 设置启动时候的运行端口
  contentBase: 'src', // 指定托管的根目录
  hot: true // 启用热更新 的 第1步
},
```

- 这里的热更新不起作用，还需要进行两步操作
- 导入webpack包

```javascript
const webpack=require('webpack')
```

- plugins中进行设置，这里的plugins是一个数组，多个插件的集合

```javascript
plugins: [ // 配置插件的节点
	new webpack.HotModuleReplacementPlugin(), // new 一个热更新的 模块对象， 这是 启用热更新的第 3 步
],
```

- 修改完一系列配置之后需要npm run  dev来重启服务器

## html-webpack-plugin

- 除了js文件，页面也可以放到内存中
- 这里需要引用插件html-webpack-plugin

- 运行cnpm i html-webpack-plugin --save-dev安装到开发依赖


- 修改webpack.config.js配置文件如下：

```javascript
// 导入处理路径的模块
var path = require('path');
// 导入自动生成HTMl文件的插件
var htmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  // 项目入口文件
  entry: path.resolve(__dirname, 'src/js/main.js'), 
  // 配置输出选项
  output: { 
    // 配置输出的路径
    path: path.resolve(__dirname, 'dist'), 
    // 配置输出的文件名
    filename: 'bundle.js' 
  },
  // 添加plugins节点配置插件
  plugins:[ 
    // new 一个热更新的 模块对象， 这是 启用热更新的第 3 步
    new webpack.HotModuleReplacementPlugin(), 
    new htmlWebpackPlugin({
    	//模板路径
      	template:path.resolve(__dirname, 'src/index.html'),
    	//自动生成的HTML文件的名称
      	filename:'index.html'
    })
  ]
}
```

- 修改package.json中script节点中的dev指令

```
"dev": "webpack-dev-server"
```

- 内存里面的页面和物理磁盘页面相比，引入了一个标签
- 将index.html中script标签注释掉，因为html-webpack-plugin插件会自动把bundle.js注入到index.html页面中

## 打包

- webpack 打包的时候会先校验文件类型，如果是js ，直接打包，如果不是js 会去找校验规则

- 在webpack1.X的版本中-loader是可以省略的

- webpack处理第三方文件的过程：

  - 发现不是JS文件，然后去配置文件中有没有对应的第三方loader规则


  - 如果能找到对应的规则，调用对应的loader处理这种文件类型


  - 在调用loader的时候是从后往前调用的


  - 当最后的loader调用完毕会把处理的结果直接交给webpack进行打包合并 最终输出到bundle中去

### CSS

- 运行cnpm i style-loader css-loader --save-dev


- 修改webpack.config.js这个配置文件
- loader校验顺序，从右到左

```javascript
// 用来配置第三方loader模块的
module: { 
  // 文件的匹配规则
  rules: [ 
    //处理css文件的规则
    //css中的处理结果交给style，style将结果交给webpack进行合并打包
    { test: /\.css$/, use: ['style-loader', 'css-loader'] }
  ]
}
```

- use表示使用哪些模块来处理test所匹配到的文件，use中相关loader模块的调用顺序是从后向前调用的

### less

- 运行cnpm i less-loader less -D


- 修改webpack.config.js这个配置文件
- less是样式文件，需要依赖style和css的loader

```javascript
{ test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] },
```

### sass

- 运行cnpm i sass-loader node-sass --save-dev
- node-sass用npm装不下来，需要用cnpm


- 在webpack.config.js中添加处理sass文件的loader模块
- sass是样式文件，需要依赖style和css的loader
- sass的文件后缀名是scss，这里需要注意

```javascript
{ test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader'] }
```

### 路径

- 运行cnpm i url-loader file-loader --save-dev


- 在webpack.config.js中添加处理url路径的loader模块
- file-loader是url-loader内部定义的，use中不需要写明
- 图片自动生成base64的编码格式

```
{ test: /\.(png|jpg|gif)$/, use: 'url-loader' }
```

- 可以通过limit指定进行base64编码的图片大小，只有小于指定字节（byte）的图片才会进行base64编码。
- 给定limit值大于图片实际大小的时候，还是base64的编码格式
- 给定值等于或者小于图片实际大小的时候，变成一个真正的url地址

```
{ test: /\.(png|jpg|gif)$/, use: 'url-loader?limit=43960' }
```

- 这里变成url地址之后，文件名很长，目的是为了区分，防止图片名字一样
- 为了方便识别，加参数，可以让url中文件的名字和原来的名字一样
- ext表示后缀

```
{ test: /\.(png|jpg|gif)$/, use: 'url-loader?limit=43960&name=[name].[ext]' }
```

- 加入引入两个名字一样的图片，这里可以借助hash区分
- 每张图片的hash值都是32位且不同的，这里取前八位拼接到name前面，区分图片

```
{ test: /\.(jpg|png|gif|bmp|jpeg)$/, use: 'url-loader?limit=43960&name=[hash:8]-[name].[ext]' }
```

- url-loader也可以处理字体文件
- 字体文件和图片文件最好分开写，这样更清晰

```
{ test: /\.(ttf|eot|svg|woff|woff2)$/, use: 'url-loader' }
```

## babel

### 概念

- 在webpack中，默认只能处理一部分ES6新语法，一些更高级的ES6语法或者ES7语法，webpack是处理不了的，这时候就需要借助第三方的loader来帮助webpack处理这些高级的语法，当第三方loader把高级语法转为低级的语法时候，会把结果交给webpack去打包到bundle.js中

### 步骤

- 在webpack中，可以运行下面两套命令，安装两套包

  - 第一套包 cnpm i babel-core babel-loader babel-plugin-transform-runtime -D
  - 第二套包 cnpm i babel-preset-env babel-preset-stage-0 -D

- 打开webpack的配置文件，在module节点下的rules数组中，添加一个新的匹配规则

  - 配置loader规则的时候，必须把node_modules目录通过exclude删掉，如果不删除babel就会把所有node_modules中的JS进行转换，浪费内存，程序也不一定会正常运行

    ```
    {test:/\.js$/, use: 'babel-loader', exclude:/node_modules/ }
    ```

- 在项目根目录中添加.babelrc文件，这个文件属于json格式，不能写注释，字符串必须用双引号，并修改这个配置文件如下：

```
{
    "presets":["es2015", "stage-0"],
    "plugins":["transform-runtime"]
}
```

- 注意：语法插件babel-preset-es2015可以更新为babel-preset-env，它包含了所有的ES相关的语法
- 目前，我们安装的 babel-preset-env，是比较新的ES语法，之前，我们安装的是 babel-preset-es2015, 现在，出了一个更新的语法插件，叫做 babel-preset-env ，它包含了所有的 和 es***相关的语法

## 静态属性

- 使用static关键字定义静态属性
- 静态属性就是可以直接通过类名，直接访问的属性
- 实例属性只能通过类的实例来访问

```javascript
class Person {
  static info = { name: 'zs', age: 20 }
}
// 访问 Person 类身上的  info 静态属性
console.log(Person.info)

```

