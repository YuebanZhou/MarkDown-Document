# 流行框架

## 简介

- angularjs是一款非常优秀的前端高级JS框架，由谷歌团队开发维护，能够快速构建单页web应用，化繁为简

- 无论是angularjs还是jQuery都是用原生JS封装的

- 库：对代码进行封装，调用封装的方法，简化操作

- 传统方式是用get方式获取元素，然后点方法

- jQuery库实现了对获取方式的封装，对方法的封装

- 框架：提供代码书写规则，按照规则去写代码，框架会帮我们实现响应的功能

- 核心：通过指令扩展HTML功能，通过插值表达式绑定数据到HTML，不推荐在控制器中直接操作DOM，而是通过指令操作，以数据为中心，用数据驱动DOM

- 版本：

  - 目前angularjs框架的版本是1.6.x
  - angularjs框架09年诞生，专注PCweb，并没有考虑到移动端，在移动端性能较差
  - angular2框架在16年诞生
  - angular2并不是angularjs的升级版，而是一个全新的框架
  - 2016年国内已经形成了angularjs，vue，react三足鼎立的局势，angular2占据的市场份额仍然比较小
  - 企业里面用的比较多的仍然是angularjs框架

- 获取方式

  - 在官网上下载 http://angularjs.org 

  - 通过CDN的方式引入到页面中 

    ```html
    <script src="https://cdn.bootcss.com/angular.js/1.6.4/angular.min.js" ></script>
    ```

## 插值

- {{}}这种双大括号的形式称之为插值表达式

- 可以写ng中的变量

- 可以显示字符串

- 可以在表达式中可以进行计算

- 可以在表达式中写三目运算符

- 可以调用函数

- 执行angularjs函数

- 不能写if else语句

  ```html
  <div>{{val}}</div>
  <div>{{'angularjs'+'很好很强大'}}</div>
  <div>{{1+1}}</div>
  <div>{{1==1?'相等':'不相等'}}</div>
  <div>{{getItem()}}</div>
  ```

## 基本指令

- 在使用了angularjs的页面，以ng-开头的属性，称之为指令
```html
<body ng-app></body>
<input type="text" ng-model="val" ng-init="val">
```
- ng-app
  - 页面加载完成以后angularjs会在页面中查找这个指令
  - 没有找到这个指令，angularjs将不会启动
  - 找到这个指令，angularjs将会执行指令所在标签内部包裹的代码
  - 可以接受模块名字作为参数 angularjs会将当前页面交给指令所指定的模块去管
- ng-model="变量"
  - 获取表单元素的值，实现双向数据绑定

  - ng-click=" "
    - 给指令所在元素绑定点击事件，不能写原生js代码

  - ng-init
    - 初始化数据

## 模块化

- 模块化开发带来的好处：方便管理，复用，后期维护方便

- 解决代码冲突，方便多人协作开发

- angularjs中模块的种类：入口模块、功能模块

- 定义模块时第二个参数加与不加的区别：加第二个参数是创建模块，不加第二个参数是获取模块

- 模块化四步

  - 创建模块，myApp是模块的名字，module方法，数组中要依赖的模块的名字，用逗号连接。没有要依赖的文件的话，传空数组。

    ```html
    <script>
    	var app=angular.module('myApp',[]);
    </script>
    ```

  - ng-app后面写模块的名字，告诉angularjs当前的页面由自己创建的myApp模块去管理

    ```html
    <body ng-app="myApp"></body>
    ```

  - 创建控制器，创建模块的语句的返回值就是一个模块对象，用这个对象去点方法，就是创建控制器

    ```html
    <script>
    	app.controller('demoCtrlA',function(){
            alert(1)
        });
      	app.controller('demoCtrlB',function(){
            alert(2)
        });
    </script>
    ```

  - 告诉angularjs当前区域由这个控制器去控制

    ```html
    <div class="sideBar" ng-controller="demoCtrlA"></div>
    <div class="main" ng-controller="demoCtrlB"></div>
    ```

  - 兄弟控制器设置相同的属性，不会冲突

## 双向数据绑定

- 双向：html和js

- 数据：angularjs中的变量

- body标签中的ng-app表示当前页面由myApp管理，ng-controller表示当前区域由demoCtrl这个控制器控制

- input标签中的ng-model表示获取表单元素的值

- div标签中显示这个值

- 两个按钮分别注册点击事件，一个设置值一个获取值

- 在控制器中封装两个函数

  ```html
  <body ng-app="myApp" ng-controller="demoCtrl">
  	<input type="text" ng-model="val">
    	<div>{{val}}</div>
    	<button ng-click="setValue()">设置值</button>
    	<button ng-click="setValue()">获取值</button>
    	<script src="node_modules/angular/angular.min.js"></script>
    	<script>
    		var app=angular.module('myApp',[]);
        	app.controller('demoCtrl',function($scope){
              $scope.val="我是初始值";
            	$scope.setValue=function(){
                  $scope.val="我是通过setValue方法更改的值"
              }
              $scope.getValue=function(){
                  alert($scope.val)
              }
          })
    	</script>
  </body>
  ```

## 路由

- 路由就是用来配置页面之间的跳转关系的，配置锚点与页面之间的对应关系

- 在angularjs中路由并没有集成在angular.js文件中

- 路由作为一个单独的模块存在，如果要使用路由，我们需要将路由模块作为主模块的依赖模块

- 主模块或入口模块 == 管理页面的那个模块

- angularjs中模块依赖的步骤：将要依赖的模块文件引入到页面中，将模块的名字写在主模块的第二个参数中

- $routeProvider路由配置对象，名字暂时不能改

- angularjs会将获取到的模板文件内容放在页面中有ng-view指令的元素中

- angularjs要求，锚点值必须以/开头，在路由配置中使不需要写#号

- 当我们使用了路由以后，就不需要直接在页面中写ng-controller指令

- 传参

  - 在被传递参数页面（详情页）的路由中配置参数占位符，类似于函数的形参

  - 在传递参数页面（列表页）的跳转链接中将实际的参数传递过去

  - 在被传递参数页面（详情页）的控制器中获取传递过来的参数

  - 传递多个参数，直接接在后面写，只要和后面一一对应起来就可以

    ```html
    <ul>
      	<li><a href="#!/article/1/我是第1篇文章">我是第1篇文章</a></li>
      	<li><a href="#!/article/1/我是第2篇文章">我是第2篇文章</a></li>
      	<li><a href="#!/article/1/我是第3篇文章">我是第3篇文章</a></li>
    </ul>
    <script>
    	var app=angular.module('myApp',['ngRoute'])
        app.config(function($routeProvider){
            $routeProvider
            	.when('/article/:id/:title',{
                	templateUrl:'articleTpl',
              		controller:'articleCtrl'
            	})
        });
    </script>
    ```

## 单页web应用

- 单页面应用程序的特点：整个网站由一个页面构成，公共部分只加载一次，利用Ajax局部刷新达到页面切换的目的，不会发生页面跳转白屏的现象，锚点与页面对应

- 单页web应用的应用场景：单页面应用对搜索引擎不友好，不适合做面向大众的展示型网站，网站后台管理系统、办公OA、混合App等等不需要被搜索引擎搜索到的应用

  ```html
  <script src="node_modules/angular/angular.min.js"></script>
  <script src="node_modules/angular-route/angular-route.min.js"></script>
  <body ng-app="myApp">
  	<a href="#!/index">首页</a>
    	<a href="#!/list">列表页</a>
    	<div ng-view></div>
  </body>
  <script>
  	var app=angular.module('myApp',['ngRoute'])
      app.config(function($routeProvider){
          $routeProvider
          	.when('/index',{
              	templateUrl:'./tpl/index.html',
            		controller:'indexCtrl'
          	})
        		.when('/list',{
              	templateUrl:'./tpl/list.html',
            		controller:'listCtrl'
          	})
        		.otherwise('/index')
      });
    	app.controller('indexCtrl',function($scope){
          $scope.msg="我是首页msg"
      })
    	app.controller('listCtrl',function($scope){
          $scope.msg="我是列表页msg"
      })
  </script>  
  ```

## 三种模板方式

```html
<script>
	templateUrl:'./tpl/index.html'//localhost
  	template:'<div>我是首页</div>'//file|localhosst
  	template:'indexTpl'//file|localhosst
</script>
```
## $scope

- 可以传递的参数有很多，不需要一一写出来

- 所以，angularjs中传递参数不能依靠顺序而是名字

- 如果形参名字改变了，angularjs就不知道要干什么了

- 解决方法：第二个参数写数组，回调函数放到数组中

- 压缩的时候，不会对字符串进行压缩，所以数组中传递字符串来确定参数的顺序

  ```html
  <script>
  	angular.module("myApp",[]).controller("demoCtrl",["$scope","$timeout","$http","$location",function(a,b,c,d){
          a.msg="我是msg"
      }])
  </script>
  ```

## 作用域

- 作用域就近原则
- angularjs中控制器控制的区域就是一个局部作用域，
- 也就是$scope代表局部作用域
- $rootScope代表全局作用域 
- 变量先顺着$scope找，找不到就去全局找
- 可以挂载公共属性方法

## 遍历

- ng-repeat="循环过程中的当前项 in 数据"循环数据并生成当前DOM元素

  ```html
  <ul>
  	<li ng-repeat="item in arr">{{item}}</li>
  </ul>
  ```

- 遍历数组对象，可以嵌套，有ng-repeat的标签中还可以嵌套ng-repeat的标签

  ```html
  <ul>
  	<li ng-repeat="person in person">
        	{{person.name}}{{person.age}}
        	<span ng-repeat="item in person.hobby">{{item}}</span>
    	</li> 
  </ul>
  ```

- 数组项重复，会报错

  ```html
  <ul>
  	<li ng-repeat="item in arr track by $index">{{item}}</li>
  </ul>
  ```

  ​

## 其他指令

- ng-class="{'类名1':布尔值,'类名2':布尔值}"专门用来添加或者删除类名，接收的值是一个对象，布尔值为真，添加类名，布尔值为假，删除类名
- 复选框，ng-model用来获取复选框的值，是一个布尔值
- ng-bind="数据"，将msg放到属性中进行加载，避免出现闪烁效果
- ng-bind-template="{{数据1}} {{数据2}}"
- ng-non-bindable直接得到插值表达式中的内容，只要与属性相关，都不执行
- ng-show="布尔值"，控制元素的显示和隐藏
- ng-hide="布尔值"，控制元素的显示和隐藏
- ng-if="布尔值"，控制元素的显示和隐藏 true 显示 false 隐藏
- ng-switch&ng-switch-when用法和switch-case类似
- 事件指令
  - onclick => ng-click
  - onmouseenter => ng-mouseenter
  - onchange => ng-change
  - ng-dblclick 双击事件
- ng-src没有src就不会解析就不会报错，直到angularjs加载完成，解析ng-src之后再生成src
- ng-href同上
- ng-options用来循环下拉列表，不能单独使用，需要配合ng-model一起使用

## 请求数据

- 要请求数据需要先引入js文件

- 引入的js文件作为依赖文件，控制器中必须写入$http

- $http-->请求的地址，相当于jQuery中的ajax

- method-->type请求的方式

- params-->data只用于get传参

- data可以用于post传参

- $http点then后面是两个回调函数

- 第一个回调函数是成功回调

- 第二个回调函数是失败回调

- res是形参，表示请求回来的数据

  ```html
  <script src="node_modules/angular/angular.js"></script>
  <script src="node_modules/angular-sanitize.min.js"></script>
  <script>
  	angular.module('myApp',['ngSanitize'])
    		.controller('demoCtrl',['$scope','$http',function($scope,$http){
              $http({
                  url:'./test.json',
                	method:'post',//请求方式
                	params:{//get传参
                    	a:1,
                  	b:2
                	},
                	data:{
                    	c:3,
                  	d:4
                	}
              }).then(function(res){
                	//成功回调
                  console.log(res)
              },function(){
                  //失败回调
              })
            	//另外一种写法
            	$http.get('./test.json',{params:{a:1,b:2}}).then(function(res){
                	//get方式传参
                  console.log(res)
              })
            	$http.post('./test.json',{c:3,d:4}.then(function(res){
                	//post方式传参
                  console.log(res)
              })
          }])
  </script>

  ```

## jqLite

- 为了方便DOM操作，angularjs提供了一个jQuery精简版，叫做jqLite
- $(原生的JS对象)将原生JS对象转换成jQuery对象，目的是为了使用jQuery对象下面提供的方法
- angularjs.element(原生JS对象)将原生JS对象转换成jqLite对象，目的是为了使用jqLite对象下面提供的方法
- 这里angularjs.element相当于jQuery中的$
- jqLite中方法的使用和jQuery高度相似

## $watch

- $watch用来监控数据的变化

- 第一个参数是要监控的数据，第二个参数是回调函数

- 回调函数中第一个参数newValue是用户输入的最新内容，第二个参数oldValue是上一次用户输入的内容

- 页面一上来的时候，回调函数会先执行一次

  ```html
  <script>
  	$scope.$watch('val',function(newValue,oldValue){
          if(newValue.length>10){
              $scope.tips="大于10";
          }else{
              $scope.tips="小于10"
          }
      })
  </script>
  ```

## $apply

- 当通过原生JS将angularjs中的数据做了改变以后，angularjs不知道，所以需要调用$apply()方法通知angularjs更新html页面

## 自定义指令

- return中是对DOM操作的全部内容
- templateUrl或者使用template引入模板
- replace将自定义指令标签本身删掉，只显示模板的内容
- transclude将自定义标签内部的内容保留，配合ng-transclude指令使用，模板中span标签使用了ng-transclude，所以自定义标签内部的内容会显示在span标签
- 如果自定义指令中的内容是用标签包裹的，会被解析出来

```html
<script>
	angular.module('myApp',[])
  		.directive('myHeader',[function(){
            return {
                templateUrl:'myHeaderTpl',
              	replace:true,
              	transclude:true
            }
        }])
</script>
```

- return中link是angularjs提供的专门写DOM操作的地方

- link中的函数有三个参数

  - scope向指令的模板区域暴露数据
  - element是指令所在的元素，是jqLite对象，可以直接使用jqLite方法
  - attributes是元素身上属性的集合，如果有多个元素需要制定，用attribute
  - css中内容不能写死，attribute是一个属性集合，attributes.myDir点出属性
  - return中有scope，默认是false，这时，link中的scope就是控制器中的$scope，如果将scope设置成turn，指令就有了单独的作用域

  ```html
  <script>
  	angular.module('myApp',[])
    		.directive('myDir',[function(){
              return {
                  link:function(scope,element,attributes){
                      element.css('background','red')
                    	element.css('background',attributes.myDir)
                  }
              }
          }])
  </script>
  ```

- 分类

  - 标签指令element E
  - 属性指令attributes A
  - 样式指令class C
  - 注释指令comment M
  - return中可以用restrict设置

## MVC&MVVN

- MVC后端思想
  - model模型，跟操作数据相关的方法，用angularjs中的服务来实现
  - view视图，用户界面
  - controller控制器，主要用来写一些业务逻辑
- MVVN
  - model模型，跟操作数据相关的方法
  - view视图，用户界面
  - viewmodel在双向数据绑定的框架中，$scope帮我们同步HTML页面
  - angularjs是基于MVVM思想的框架


- 过滤器

  - 过滤器：将数据格式化成我们想要的模式

  - {{ 数据模型 | 过滤器的名字:过滤器的参数:多个参数以冒号隔开 }}

  - 内置过滤器

    - currency，货币过滤器，传参表示前边的符号
    - date，日期过滤器，传参可以改变date的时间形式，可以用短横分割，也可以写汉字
    - filter，将数据按照某种规则进行过滤，模糊过滤（去数据中每一个字段中查找）和精确过滤（去数据中指定的字段中查找）
    - limitTo，限制，第一个参数limit 限制的数量，可以为负数，从后往前开始限制，第二个参数begin，从第几个开始限制
    - orderBy，排序，orderBy:'字段'  默认是升序，orderBy:'-字段' 降序，根据age字段，升序排列
    - number，数字过滤器，传参表示保留几位小数
    - uppercase，大写
    - lowercase，小写
    - json将数据一个良好的格式展示到页面中，主要用于调试，要配合HTML页面中的pre双标签有一个参数用来控制缩进

  - 自定义过滤器

    - 模块对象.filter('过滤器的名字',[function() {return function(value){return 数据}}])

      ```html
      <script>
      	angular.module('myApp',[])
        		.filter('phonestar',[function(){
                  return function(value){
                      return value.substr(0,3)+'****'+value.substr(7)
                  }
              }])
      </script>
      ```

  ## 服务

  - 模块对象.service('服务的名字',[function(){this.name="qwe";alert(this.name)}])

  ## ui-router

  - 路由模块的名字ui.router

  - 模块需要引入uirouter的依赖文件

  - 用$stateProvider配置路由的对象

  - $urlRouterProvider设置没有匹配到路由时的默认跳转位置

  - url表示锚点值

  - template渲染模板

  - name是路由名字，必须存在

    ```html
    <script>
    	angular.module('myApp',['ui.router'])
    .config(['$stateProvider','$urlRouterProvider',function($stateProvider,$urlRouterProvider){
    				// $stateProvider 配置路由的对象
    				$stateProvider
    					.state({
    						url:'/index', // 锚点值
    						templateUrl:'indexTpl',
    						name:'index',
    						controller:'indexCtrl'
    					})
    					.state({
    						url:'/list', // 锚点值
    						templateUrl:'listTpl',
    						name:'list',
    						controller:'listCtrl'
    					})
    				// 当没有匹配到的路由时 默认跳转到首页
    				$urlRouterProvider.otherwise('/index');
    			}])

    			.controller('indexCtrl',['$scope',function($scope){
    				$scope.msg = "indexCtrl";
    			}])

    			.controller('listCtrl',['$scope',function($scope){
    				$scope.msg = "listCtrl";
    			}])
    </script>
    ```

  ## gulp

  - ​ [gulp官网(英文)](https://gulpjs.com/)[gulp官网(中文)](http://www.gulpjs.com.cn/)

  - 概念:

      - 前端自动化流式构建工具
      - 我们可以使用gulp编写一些机械化的任务
      - 有效提高开发效率 改善开发体验

  - 说明

      - gulp这个工具依赖node环境 所以在使用gulp之前需要安装node环境
      - 就像我们使用bootstrap要先引入jQuery是一个道理
      - 编写gulp任务使用JS语法

  - 下载gulp

      - npm install gulp
      - 在项目的根目录运行这个命令，会自动生成一个node_modules文件夹 gulp会被下载到这个文件夹中。
      - node_modules文件夹中除了gulp以外，还会多出很多文件，这些都是gulp所要依赖的文件。

  - 使用gulp编写任务

      - gulp要求我们在项目的根目录下新建一个gulpfile.js文件，这个文件是专门用来编写gulp任务的。
      - 就像使用angularjs框架需要引包一样，要使用gulp也需要引包

      ```javascript
          // require('包名') 引包
          var gulp = require('gulp');
          // gulp变量是对象类型
          // 我们编写任务 处理任务需要用到gulp对象下面的方法
      ```

      - 编写人生中的第一个gulp任务

      ```javascript
          // gulp.task('任务名称',任务回调函数) 创建任务方法
          // 任务名称的用处:在执行任务的时候需要指定任务名称
          // 回调函数:要做的事情需要写在回调函数中 比如less解析 代码压缩...
          gulp.task('first',function(){
              // gulp.src('文件路径') 获取文件
              // 获取任务要处理的文件
              gulp.src('./css/base.css')
                  // pipe('怎样处理') 处理任务
                  // gulp.dest('文件路径') 将处理好的文件放入参数路径中
                  .pipe(gulp.dest('dist/css'))
          });
      ```

  - 执行任务

      - 任务编写在了gulpfile.js文件中，要执行任务，就需要运行这个JS文件，那么问题来了，我们以前编写的JS文件，都会引入到HTML页面中，然后运行HTML文件，JS就能执行了
      - 安装一个gulp-cli工具即可
      - 在命令行中的任意目录下执行下面的命令
      - npm install gulp-cli -g
      - -g 代表全局安装 目的是在其他项目中也可以使用这个工具
      - 安装完成以后在项目的根目录下输入以下命令就可以执行任务了
      - gulp 任务名称

  - gulp中提供的方法

      - gulp.src() 获取任务要处理的文件
      - gulp.dest() 输出文件
      - gulp.task() 建立gulp任务
      - gulp.watch() 监控文件的变化
      - gulp本身提供的方法不多,大多数的任务都是由插件完成的

  - [gulp插件地址](https://gulpjs.com/plugins/)

      - 图片压缩 [gulp-imagemin](https://www.npmjs.com/package/gulp-imagemin)
      - CSS压缩  [gulp-clean-css](https://github.com/scniro/gulp-clean-css)
      - JS压缩   [gulp-uglify](https://github.com/terinjokes/gulp-uglify)
      - HTML压缩 [gulp-htmlmin](https://github.com/jonschlinkert/gulp-htmlmin)
      - 文件合并 [gulp-concat](https://github.com/contra/gulp-concat)
      - LESS转换 [gulp-less](https://www.npmjs.com/package/gulp-less)
      - es6转es5 [gulp-babel](https://www.npmjs.com/package/gulp-babel/)
      - 静态资源服务 [gulp-browser-sync](http://www.browsersync.cn/docs/gulp/)
