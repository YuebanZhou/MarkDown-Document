# Vue.js

## 相关文章

- [vue.js 1.x 文档](https://v1-cn.vuejs.org/)
- [vue.js 2.x 文档](https://cn.vuejs.org/)
- [String.prototype.padStart(maxLength, fillString)](http://www.css88.com/archives/7715)
- [js 里面的键盘事件对应的键码](http://www.cnblogs.com/wuhua1/p/6686237.html)
- [Vue.js双向绑定的实现原理](http://www.cnblogs.com/kidney/p/6052935.html)
- [Vue.js devtools - 翻墙安装方式 - 推荐](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?hl=zh-CN)
- [自定义指令](https://cn.vuejs.org/v2/guide/custom-directive.html)
- [vue.js 1.x 文档](https://v1-cn.vuejs.org/)
- [vue.js 2.x 文档](https://cn.vuejs.org/)
- [String.prototype.padStart(maxLength, fillString)](http://www.css88.com/archives/7715)
- [js 里面的键盘事件对应的键码](http://www.cnblogs.com/wuhua1/p/6686237.html)
- [pagekit/vue-resource](https://github.com/pagekit/vue-resource)
- [navicat如何导入sql文件和导出sql文件](https://jingyan.baidu.com/article/a65957f4976aad24e67f9b9b.html)
- [贝塞尔在线生成器](http://cubic-bezier.com/#.4,-0.3,1,.33)
- [vue实例的生命周期](https://cn.vuejs.org/v2/guide/instance.html#实例生命周期)
- [vue-resource 实现 get, post, jsonp请求](https://github.com/pagekit/vue-resource)
- [生命周期钩子](https://cn.vuejs.org/v2/api/#选项-生命周期钩子)
- [Vue中的动画](https://cn.vuejs.org/v2/guide/transitions.html)
- [使用第三方 CSS 动画库](https://cn.vuejs.org/v2/guide/transitions.html#自定义过渡类名)
- [v-for 的列表过渡](https://cn.vuejs.org/v2/guide/transitions.html#列表的进入和离开过渡)
- [URL中的hash（井号）](http://www.cnblogs.com/joyho/articles/4430148.html)
- [第三方类库GitHub](https://daneden.github.io/animate.css/)
- [URL中的hash（井号）](http://www.cnblogs.com/joyho/articles/4430148.html)

## 概念

- Vue.js 是目前最火的一个前端框架，React是最流行的一个前端框架（React除了开发网站，还可以开发手机App， Vue语法也是可以用于进行手机App开发的，需要借助于Weex）
- Vue.js 是前端的主流框架之一，和Angular.js、React.js 一起，并成为前端三大主流框架。
- Vue.js 是一套构建用户界面的框架，只关注视图层，它不仅易于上手，还便于与第三方库或既有项目整合。（Vue有配套的第三方类库，可以整合起来做大型项目的开发）
- 前端的主要工作，主要负责MVC中的V这一层，主要工作就是和界面打交道，来制作前端页面效果。


- 企业中，使用框架，能够提高开发的效率。


- 提高开发效率的发展历程：原生JS -> Jquery之类的类库 -> 前端模板引擎 -> Angular.js / Vue.js
- 框架能够帮助我们减少不必要的DOM操作，提高渲染效率，双向数据绑定的概念，通过框架提供的指令，我们前端程序员只需要关心数据的业务逻辑，不再关心DOM是如何渲染的了。

## 框架和库

- 框架：是一套完整的解决方案，对项目的侵入性较大，项目如果需要更换框架，则需要重新架构整个项目。
  - node 中的 express；


- 库（插件）：提供某一个小功能，对项目的侵入性较小，如果某个库无法完成某些需求，可以很容易切换到其它库实现需求。
  - 从Jquery 切换到 Zepto
  - 从 EJS 切换到 art-template

## 代码和指令

### 基本代码

- 先导入Vue的包
- 在一个元素上添加id为app，这个元素不能是body，也就是不能在body上添加app，这里和angular不同
- html部分就是MVVM中的V
- new一个Vue的实例，这个实例对象就是MVVM中的VM
- 对象中的data就是MVVM中的M，用来保存每个页面的数据
- data中放的就是methods中要使用的数据
- methods是一个对象，不是数组
- 在实例中如果想要调用data上的数据或者想要调用methods中的方法，必须通过this点数据属性名或this点方法名来进行访问，这里的this就表示new出来的实例对象
- 用箭头函数，解决this指向的问题

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="./lib/vue-2.4.0.js"></script>
</head>
<body>
  <!-- 将来new的Vue实例，会控制这个元素中的所有内容 -->
  <div id="app">
    <p>{{ msg }}</p>
  </div>
  <script>
    // 当我们导入包之后，在浏览器的内存中，就多了一个Vue构造函数
    var vm = new Vue({
      el: '#app',// 表示控制页面上的哪个区域
      data: { 
        msg: '欢迎学习Vue' 
      },
      methods: { // 这个 methods属性中定义了当前Vue实例所有可用的方法
        show: function () {
          alert('Hello')
        }
      }
    })
  </script>
</body>
</html>
```

### 基本指令

- v-cloak解决闪烁问题，Vue没有加载出来之前，标签有v-cloak这个属性，Vue加载出来之后，标签的v-cloak属性消失
- v-text没有闪烁问题，但是会覆盖掉标签之间的内容，不过只是用插值表达式替换这个内容，不会清除
- v-html解析内容里的html标签，渲染到页面上
- v-bind用于绑定属性，可以写JS代码，缩写是英文格式的冒号，绑定的时候可以拼接内容:title="btnTitle + ', 这是追加的内容'"，只能实现数据的单向绑定
- v-on用于绑定事件，缩写是@符号

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    [v-cloak] {
      /* display: none; */
    }
  </style>
</head>
<body>
  <div id="app">
    <p v-cloak>++++++++ {{ msg }} ----------</p>
    <h4 v-text="msg">==================</h4>
    <div>{{msg2}}</div>
    <div v-text="msg2"></div>
    <div v-html="msg2">1212112</div>
    <input type="button" value="按钮" v-bind:title="mytitle + '123'">
    <input type="button" value="按钮" :title="mytitle + '123'" v-on:click="alert('hello')">
   <input type="button" value="按钮" @click="show">
  </div>
  <script src="./lib/vue-2.4.0.js"></script>
  <script>
    var vm = new Vue({
      el: '#app',
      data: {
        msg: '123',
        msg2: '<h1>哈哈，我是一个大大的H1， 我大，我骄傲</h1>',
        mytitle: '这是一个自己定义的title'
      },
      methods: { // 这个 methods属性中定义了当前Vue实例所有可用的方法
        show: function () {
          alert('Hello')
        }
      }
    })
  </script>
</body>
</html>
```

### v-model

- 唯一一个实现数据绑定的指令
- v-model="需要同步的内容"
- 实现双向绑定
- 只能运用在表单元素中

```html
<div id="app">
    <h4>{{ msg }}</h4>
    <input type="text" style="width:100%;" v-model="msg">
</div>
<script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      	el: '#app',
      	data: {
          msg: '大家都是好学生，爱敲代码，爱学习，爱思考 '
      	},
      	methods: {
      	}
    });
</script>
```

### v-for

- 作用
  - 遍历普通数组
  - 遍历对象数组
  - 遍历对象的属性
  - 迭代数字，count从1开始
- 组件中使用v-for的时候，key是必须的，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素
- key只接受字符串和number
- 当 Vue.js 用 v-for 正在更新已渲染过的元素列表时，它默认用 “就地复用” 策略。如果数据项的顺序被改变，Vue将不是移动 DOM 元素来匹配数据项的顺序， 而是简单复用此处每个元素，并且确保它在特定索引下显示已被渲染过的每个元素。

```html
<!-- 迭代普通数组 -->
<ul>
  <li v-for="(item, i) in list">
    索引：{{i}} --- 姓名：{{item.name}} --- 年龄：{{item.age}}
  </li>
</ul>

<!-- 迭代对象数组 -->
<p v-for="(user, i) in list">
  Id：{{ user.id }} --- 名字：{{ user.name }} --- 索引：{{i}}
</p>
<!-- 迭代对象中的属性 -->
<div v-for="(val, key, i) in userInfo">
  {{val}} --- {{key}} --- {{i}}
</div>
<!-- 迭代数字 -->
<p v-for="count in 10">这是第 {{ count }} 次循环</p>
<!-- 以key为关键字 -->
<p v-for="item in list" :key="item.id">
  <input type="checkbox">{{item.id}} --- {{item.name}}
</p>
```

### v-if&v-show

- v-if有更高的切换消耗，如果运行时条件不大可能改变，用v-if比较好
- v-show有更高的初始渲染消耗，需要频繁切换的时候，用v-show比较好

### 事件修饰符

- .stop阻止冒泡，阻止所有冒泡
- .prevent阻止默认事件
- .capture添加事件侦听器时使用事件捕获模式
- .self只当事件在该元素本身（比如不是子元素）触发时触发回调，只能阻止当前元素冒泡
- .once事件只触发一次
- 事件修饰符是可以串联的，.once和其他修饰符连用的时候，不在乎先后顺序


```html
<div id="app">
	<!-- 使用  .stop  阻止冒泡 -->
	<div class="inner" @click="div1Handler">
		<input type="button" value="戳他" @click.stop="btnHandler">
	</div>

  	<!-- 使用 .prevent 阻止默认行为 -->
  	<a href="http://www.baidu.com" @click.prevent="linkClick">
      	有问题，先去百度
  	</a>

  	<!-- 使用  .capture 实现捕获触发事件的机制 -->
  	<div class="inner" @click.capture="div1Handler">
		<input type="button" value="戳他" @click="btnHandler">
	</div>

  	<!-- 使用 .self 实现只有点击当前元素时候，才会触发事件处理函数 -->
  	<div class="inner" @click="div1Handler">
		<input type="button" value="戳他" @click="btnHandler">
	</div>

  	<!-- 使用 .once 只触发一次事件处理函数 -->
  	<a href="http://www.baidu.com" @click.prevent.once="linkClick">
      	有问题，先去百度
  	</a>

  	<!-- 演示： .stop 和 .self 的区别 -->
  	<div class="outer" @click="div2Handler">
		<div class="inner" @click="div1Handler">
			<input type="button" value="戳他" @click.stop="btnHandler">
		</div>
	</div>

  	<!-- .self 只会阻止自己身上冒泡行为的触发，并不会真正阻止 冒泡的行为 -->
  	<div class="outer" @click="div2Handler">
		<div class="inner" @click.self="div1Handler">
			<input type="button" value="戳他" @click="btnHandler">
		</div>
	</div>
</div>
```




## 案例

### 跑马灯效果

```html
<!-- html结构 -->
<div id="app">
	<p>{{info}}</p>
    <input type="button" value="开启" v-on:click="go">
    <input type="button" value="停止" v-on:click="stop">
</div>
```

```javascript
// 创建 Vue 实例，得到 ViewModel
var vm = new Vue({
	el: '#app',
	data: {
        info: '猥琐发育，别浪~！',
        intervalId: null
    },
    methods: {
		go() {
            // 如果当前有定时器在运行，则直接return
            if (this.intervalId != null) {
              return;
            }
            // 开始定时器
            this.intervalId = setInterval(() => {
            this.info = this.info.substring(1) + this.info.substring(0, 1);
            }, 500);
        },
        stop() {
          	//清理定时器的时候，访问不到另一个函数中定时器的名字，所以这个例子中把定时器的名字放到了data中，给定了一个初始值
          	clearInterval(this.intervalId);
        }
    }
});
```



### 简易计算器案例

```html
<!-- html结构 -->
<div id="app">
<input type="text" v-model="n1">
    <select v-model="opt">
      <option value="0">+</option>
      <option value="1">-</option>
      <option value="2">*</option>
      <option value="3">÷</option>
    </select>
    <input type="text" v-model="n2">
    <input type="button" value="=" v-on:click="getResult">
    <input type="text" v-model="result">
</div>
```

```javascript
// 创建 Vue 实例，得到 ViewModel
var vm = new Vue({
  	el: '#app',
  	data: {
    	n1: 0,
    	n2: 0,
    	result: 0,
    	opt: '0'
  	},
  	methods: {
    	getResult() {
            switch (this.opt) {
                case '0':
                this.result = parseInt(this.n1) + parseInt(this.n2);
                break;
                case '1':
                this.result = parseInt(this.n1) - parseInt(this.n2);
                break;
                case '2':
                this.result = parseInt(this.n1) * parseInt(this.n2);
                break;
                case '3':
                this.result = parseInt(this.n1) / parseInt(this.n2);
                break;
            }
          	//或者switch部分可以替换成下面的内容
          	// 注意：这是投机取巧的方式，正式开发中，尽量少用
          var codeStr = 
              'parseInt(this.n1) ' + this.opt + ' parseInt(this.n2)'
          //eval方法将字符串中内容解析执行
          this.result = eval(codeStr)
    	}
  	}
});
```

## 使用样式

### 使用class样式

- 类名用单引号包起来，用逗号连接
- 对象的属性，可以带双引号，也可以不带
- 如果属性中有横杠的连接符，必须用引号括起来
- 直接用对象的时候，可以抽离到data中

```html
<!-- 数组 -->
<h1 :class="['red', 'thin']">这是一个邪恶的H1</h1>
<!-- 数组中使用三元 -->
<h1 :class="['red', 'thin', isactive?'active':'']">这是一个邪恶的H1</h1>
<!-- 数组中嵌套对象 -->
<h1 :class="['red', 'thin', {'active': isactive}]">这是一个邪恶的H1</h1>
<!-- 直接使用对象 -->
<h1 :class="{red:true, italic:true, active:true, thin:true}">这是一个邪恶的H1</h1>
```

### 使用内联样式

- 直接在元素上通过 `:style` 的形式，书写样式对象

```html
<h1 :style="{color: 'red', 'font-size': '40px'}">这是一个善良的H1</h1>
```

- 将样式对象，定义到data中，并直接引用到:style中


```javascript
//在data上定义样式
data: {
        h1StyleObj: { color: 'red', 'font-size': '40px', 'font-weight': '200' }
}
```

```html
<!-- 在元素中，通过属性绑定的形式，将样式对象应用到元素中 -->
<h1 :style="h1StyleObj">这是一个善良的H1</h1>
```

- 在:style中通过数组，引用多个data上的样式对象
   - 在data上定义样式：
```javascript
//在data上定义样式
data: {
        h1StyleObj: { color: 'red', 'font-size': '40px', 'font-weight': '200' },
        h1StyleObj2: { fontStyle: 'italic' }
}
```

```html
<!-- 在元素中，通过属性绑定的形式，将样式对象应用到元素中 -->
<h1 :style="[h1StyleObj, h1StyleObj2]">这是一个善良的H1</h1>
```

## 过滤器

### 概念

- Vue.js 允许你自定义过滤器，可被用作一些常见的文本格式化。
- 过滤器可以用在两个地方：mustache 插值和 v-bind 表达式。
- 过滤器应该被添加在 JavaScript 表达式的尾部，由管道符指示。

### 私有过滤器

- 私有过滤器只能在当前vm对象所控制的View区域进行使用
- 参数列表中通过pattern=""来指定形参默认值，防止报错
- 私有过滤器定义在实例对象中，和data、methods同级
- padStart填充0的方法，第一个参数表示填充之后的位数，第二个参数表示填充物

```html
<!-- html中的结构 -->
<td>{{item.ctime | dataFormat('yyyy-mm-dd')}}</td>
```

```javascript
//私有的filter方式
filters: { 
    dataFormat(input, pattern = "") { 
        var dt = new Date(input);
        // 获取年月日
        var y = dt.getFullYear();
        var m = (dt.getMonth() + 1).toString().padStart(2, '0');
        var d = dt.getDate().toString().padStart(2, '0');
        //传进来的字符串转换小写之后，等于yyyy-mm-dd，就返回年月日
        //传进来的字符串不是标准格式，返回年月日时分秒
        if (pattern.toLowerCase() === 'yyyy-mm-dd') {
          	return `${y}-${m}-${d}`;
        } else {
          // 获取时分秒
          var hh = dt.getHours().toString().padStart(2, '0');
          var mm = dt.getMinutes().toString().padStart(2, '0');
          var ss = dt.getSeconds().toString().padStart(2, '0');
          return `${y}-${m}-${d} ${hh}:${mm}:${ss}`;
        }
    }
  }
```

### 全局过滤器

- 全局过滤器，所有的vm实例都可以使用
- 有局部和全局两个名称相同的过滤器的时候，就近原则进行调用，一般就是采用局部过滤器

```javascript
// 定义一个全局过滤器
Vue.filter('dataFormat', function (input, pattern = '') {
  var dt = new Date(input);
  // 获取年月日
  var y = dt.getFullYear();
  var m = (dt.getMonth() + 1).toString().padStart(2, '0');
  var d = dt.getDate().toString().padStart(2, '0');
  if (pattern.toLowerCase() === 'yyyy-mm-dd') {
    return `${y}-${m}-${d}`;
  } else {
    // 获取时分秒
    var hh = dt.getHours().toString().padStart(2, '0');
    var mm = dt.getMinutes().toString().padStart(2, '0');
    var ss = dt.getSeconds().toString().padStart(2, '0');
    return `${y}-${m}-${d} ${hh}:${mm}:${ss}`;
  }
});
```

## 键盘修饰符

- 通过Vue.config.keyCodes.名称 = 按键值来自定义案件修饰符的别名


```javascript
Vue.config.keyCodes.f2 = 113;
```

- 使用自定义的按键修饰符


```html
<input type="text" v-model="name" @keyup.f2="add">
```

## 自定义指令

- 自定义指令，定义的时候，可以不加v，调用的时候，必须加v-前缀
- directive也可以自定义成私有的，放在函数中要加s，是一个对象

```javascript
// 全局
Vue.directive('focus', {
  inserted: function (el) { // inserted 表示被绑定元素插入父节点时调用
    el.focus();
  }
});
// 局部
directives: {
  color: { // 为元素设置指定的字体颜色
    bind(el, binding) {
      el.style.color = binding.value;
    }
  },
    'font-weight': function (el, binding2) { // 自定义指令的简写形式，等同于定义了 bind 和 update 两个钩子函数
      el.style.fontWeight = binding2.value;
    }
}
```



```html
<input type="text" v-model="searchName" v-focus v-color="'red'" v-font-weight="900">
```

## 钩子函数

- bind每当指令绑定到元素上的时候，就会执行bind 只绑定一次

- inserted 元素插入到DOM的时候，会执行insert 只触发一次

- updated当VNode更新的时候，执行updated

- 每个函数中，第一个参数必须是el

- 设置样式的时候，不需要关心是否插入到了DOM中，所以样式的操作可以写到bind中

- 和JS行为有关的，最好在inserted中执行，方式不生效

- value和expression的区别就是，一个原样输出，一个计算之后输出

- 样式只要绑定给了元素，不管这个元素是否插入到了页面中去，这个元素肯定有了一个样式

- 在元素刚绑定指令的时候，还没有插入到DOM中

- 钩子函数可以简写，这个函数相当于把代码写到了bind和update中

- ​

  ​

## vue实例的生命周期

- 从Vue实例创建、运行、到销毁期间，总是伴随着各种各样的事件，这些事件，统称为生命周期。
- 生命周期钩子，就是生命周期事件的别名而已
- 生命周期钩子=生命周期函数=生命周期事件
- 主要的生命周期函数分类：
  - 创建期间的生命周期函数
    - beforeCreate函数中data和methods还未初始化
    - created函数中data和methods已经被初始化了
    - beforeMount表示在挂载之前，表示模板已经编译完成，在模板中，但是尚未渲染到页面中去，页面中的元素还没有被替换过来，只是模板之前的字符串
    - mounted内存中的模板已经挂载到了页面中，用户已经可以看到渲染好的页面了，是实例创建期间的最后一个生命周期函数，执行完mounted 表示这个实例已经完全被创建好了，如果想要操作页面上的DOM 最早在mounted中进行
  - 运行期间的生命周期函数
    - beforeUpdate这两个函数会根据data的改变，有选择性的触发0次或多次。执行beforeUpdate的时候，页面中的数据还是旧的，data中的数据是新的，页面尚未和data保持一致。
    - updated执行updated的时候，页面和data数据已经保持同步了
  - 销毁期间的生命周期函数
    - beforeDestroy钩子函数的时候实例已经从运行阶段进行到了销毁阶段，实例上的data和methods等都是可用状态，此时还没有执行真正的销毁过程
    - destroyed组件已经被完全被销毁了，此时组件中所有数据已经不可用了
  - 最重要的是created和mounted



