# MintUI 组件

## 相关文章

- [Github 仓储地址](https://github.com/ElemeFE/mint-ui)


- [Mint-UI官方文档](http://mint-ui.github.io/#!/zh-cn)
- [官网首页](http://dev.dcloud.net.cn/mui/)
- [文档地址](http://dev.dcloud.net.cn/mui/ui/)
- [如何生成SSH公钥](http://git.mydoc.io/?t=154712)
- [babel-plugin-transform-remove-strict-mode](https://github.com/genify/babel-plugin-transform-remove-strict-mode)
- [vue-preview](https://github.com/LS1231/vue-preview)
- http://www.cnblogs.com/pearl07/p/6589114.html
- https://developer.mozilla.org/zh-CN/docs/Web/CSS/touch-action

## 步骤

### CSS Components

- CSS组件中，做了导入组件导入样式表之后，不需要再做别的导入，直接做标签就可以了
- 导入所有组件，也就是相当于把所有组件注册为全局组件，标签中就可以直接引用
  - plain属性，幽灵按钮，中间是空白的，周围是带颜色的边框，默认值是false
  - disable属性，禁用状态，默认值是false
  - type属性，按钮的显示样式，default、primary、danger三种值
  - size属性，尺寸，small、normal、target三种值
  - icon属性，图标，back、more两种值，出现响应的箭头效果

```javascript
//导入所有MintUI组件
import MintUI from 'mint-ui'
//导入样式表
//这里可以省略node_modules这一层目录
import 'mint-ui/lib/style.css'
//在 vue 中使用 MintUI中的Button按钮和Toast弹框提示
Vue.use(MintUI)
//使用的例子
<mt-button type="primary" size="large">primary</mt-button>
```

### JS Components

- 使用之前需要额外导入组件
- toast，调用toast时传入一个对象即可配置更多选项，执行toast方法会返回一个toast实例，每个实例都有close方法，用于手动关闭toast
  - message，文本内容，string类型
  - duration，持续时间，如果是-1，则弹出之后不消失，默认是3000
  - position，toast的位置，top、bottom、middle三种值。默认值是middle
  - iconClassicon图标的类名，设置图标的类
  - className，toast的类名，可以添加自定义类名，string类型


- .babelrc中进行配置

```
{
  "presets": ["env", "stage-0"],
  "plugins": ["transform-runtime", ["component", [
    {
      "libraryName": "mint-ui",
      "style": true
    }
  ]]]
}
```

- 按需导入toast

  ```javascript
  // 按需导入 Toast 组件
  import { Toast } from "mint-ui";

  export default {
    data() {
      return {
        toastInstanse: null
      };
    },
    created() {
      this.getList();
    },
    methods: {
      getList() {
        // 模拟获取列表的 一个 AJax 方法
        // 在获取数据之前，立即 弹出 Toast 提示用户，正在加载数据
        this.show();
        setTimeout(() => {
          //  当 3 秒过后，数据获取回来了，要把 Toast 移除
          this.toastInstanse.close();
        }, 3000);
      },
      show() {
        // Toast("提示信息");
        this.toastInstanse = Toast({
          message: "这是消息",
          duration: -1, // 如果是 -1 则弹出之后不消失
          position: "top",
          iconClass: "glyphicon glyphicon-heart", // 设置 图标的类
          className: "mytoast" // 自定义Toast的样式，需要自己提供一个类名
        });
      }
    }
  };
  ```

- # 按需导入button

  - button.name是一个字符串，表示my-button

  ```javascript
  import Vue from 'vue'
  // 1. 导入 vue-router 包
  import VueRouter from 'vue-router'
  // 2. 手动安装 VueRouter 
  Vue.use(VueRouter)
  // 导入bootstrap样式
  import 'bootstrap/dist/css/bootstrap.css'
  import './css/app.css'
  // 导入 MUI 的样式表， 和 Bootstrap 用法没有差别
  import './lib/mui/css/mui.min.css'
  // 按需导入 Mint-UI组件
  import { Button } from 'mint-ui'
  // 使用 Vue.component 注册 按钮组件
  Vue.component(Button.name, Button)
  // console.log(Button.name)
  // 导入 app 组件
  import app from './App.vue'
  // 导入 自定义路由模块
  import router from './router.js'
  var vm = new Vue({
    el: '#app',
    render: c => c(app), // render 会把 el 指定的容器中，所有的内容都清空覆盖，所以 不要 把 路由的 router-view 和 router-link 直接写到 el 所控制的元素中
    router // 4. 将路由对象挂载到 vm 上
  })

  ```


# MUI 

## MUI&Mint-UI

- MUI 不同于 Mint-UI，MUI只是开发出来的一套好用的代码片段，里面提供了配套的样式、配套的HTML代码段，类似于 Bootstrap
-  Mint-UI是真正的组件库，是使用 Vue 技术封装出来的成套的组件，可以无缝的和VUE项目进行集成开发
- Mint-UI体验更好，因为这是别人帮我们开发好的现成的Vue组件
- MUI并不能使用  npm 去下载，需要自己手动从 github 上，下载现成的包，自己解压出来，然后手动拷贝到项目中使用
- MUI和Bootstrap类似
- 任何项目都可以使用MUI或Bootstrap，但是，MInt-UI只适用于Vue项目

## 步骤

- 导入 MUI 的样式表

```
import '../lib/mui/css/mui.min.css'
```

- 在webpack.config.js中添加新的loader规则

```
{ test: /\.(png|jpg|gif|ttf)$/, use: 'url-loader' }
```

- 根据官方提供的文档和example，尝试使用相关的组件

## 托管

- 点击头像 -> 修改资料 -> SSH公钥


- 创建自己的空仓储，使用 git config --global user.name "用户名" 和 git config --global user.email ***@**.com 来全局配置提交时用户的名称和邮箱


- 使用 git init 在本地初始化项目


- 使用 touch README.md 和 touch .gitignore 来创建项目的说明文件和忽略文件；


- 使用 git add . 将所有文件托管到 git 中


- 使用 git commit -m "init project" 将项目进行本地提交


- 使用 git remote add origin 仓储地址将本地项目和远程仓储连接，并使用origin最为远程仓储的别名


- 使用 git push -u origin master 将本地代码push到仓储中

## App.vue设置

- 头部的固定导航栏使用 Mint-UI 的 Header 组件


- 底部的页签使用 mui 的 tabbar


- 购物车的图标，使用 icons-extra 中的 mui-icon-extra mui-icon-extra-cart，同时，应该把其依赖的字体图标文件 mui-icons-extra.ttf，复制到 fonts 目录下


- 将底部的页签，改造成 router-link 来实现单页面的切换


- Tab Bar 路由激活时候设置高亮的两种方式

- 全局设置样式如下：

```css
.router-link-active{
  color:#007aff !important;
}
```

- 或者在 new VueRouter 的时候，通过 linkActiveClass 来指定高亮的类

```javascript
// 创建路由对象
var router = new VueRouter({
  routes: [
    { path: '/', redirect: '/home' }
  ],
  linkActiveClass: 'mui-active'
});
```

## tabbar

- 将 tabbar 改造成 router-link 形式，并指定每个连接的 to 属性


- 在入口文件中导入需要展示的组件，并创建路由对象

```javascript
// 导入需要展示的组件
import Home from './components/home/home.vue'
import Member from './components/member/member.vue'
import Shopcar from './components/shopcar/shopcar.vue'
import Search from './components/search/search.vue'
// 创建路由对象
var router = new VueRouter({
  routes: [
    { path: '/', redirect: '/home' },
    { path: '/home', component: Home },
    { path: '/member', component: Member },
    { path: '/shopcar', component: Shopcar },
    { path: '/search', component: Search }
  ],
  linkActiveClass: 'mui-active'
});
```

## mt-swipe

- 定义一个空数组，用来放轮播的数据


- 引入轮播图组件

```html
<!-- Mint-UI 轮播图组件 -->
<div class="home-swipe">
  <mt-swipe :auto="4000">
    <mt-swipe-item v-for="(item, i) in lunbo" :key="i">
      <img :src="item" alt="">
    </mt-swipe-item>
  </mt-swipe>
</div>
</div>
```

## vue-resource

- 运行cnpm i vue-resource -S安装模块


- 导入 vue-resource 组件

```javascript
import VueResource from 'vue-resource'
```

- 在vue中使用 vue-resource 组件
  - 
    Vue.use(VueResource)

## tab-top-webview-main

### 兼容问题

1. 和 App.vue 中的 `router-link` 身上的类名 `mui-tab-item` 存在兼容性问题，导致tab栏失效，可以把`mui-tab-item`改名为`mui-tab-item1`，并复制相关的类样式，来解决这个问题；

```
    .mui-bar-tab .mui-tab-item1.mui-active {
      color: #007aff;
    }

    .mui-bar-tab .mui-tab-item1 {
      display: table-cell;
      overflow: hidden;
      width: 1%;
      height: 50px;
      text-align: center;
      vertical-align: middle;
      white-space: nowrap;
      text-overflow: ellipsis;
      color: #929292;
    }

    .mui-bar-tab .mui-tab-item1 .mui-icon {
      top: 3px;
      width: 24px;
      height: 24px;
      padding-top: 0;
      padding-bottom: 0;
    }

    .mui-bar-tab .mui-tab-item1 .mui-icon~.mui-tab-label {
      font-size: 11px;
      display: block;
      overflow: hidden;
      text-overflow: ellipsis;
    }
```

1. `tab-top-webview-main`组件第一次显示到页面中的时候，无法被滑动的解决方案：

- 先导入 mui 的JS文件:

```
 import mui from '../../../lib/mui/js/mui.min.js'
```

- 在 组件的 `mounted` 事件钩子中，注册 mui 的滚动事件：

```
 	mounted() {
    	// 需要在组件的 mounted 事件钩子中，注册 mui 的 scroll 滚动事件
        mui('.mui-scroll-wrapper').scroll({
          deceleration: 0.0005 //flick 减速系数，系数越大，滚动速度越慢，滚动距离越小，默认值0.0006
        });
  	}
```

1. 滑动的时候报警告：`Unable to preventDefault inside passive event listener due to target being treated as passive. See https://www.chromestatus.com/features/5093566007214080`

```
解决方法，可以加上* { touch-action: none; } 这句样式去掉。
```

原因：（是chrome为了提高页面的滑动流畅度而新折腾出来的一个东西） 



一个Vue集成PhotoSwipe图片预览插件

# 大项目

- 页面内容改变，头部header和底部的导航不改变，所以将中心区域渲染不同vue就可以了
- 底部四个按钮做路由链接
- header部分用Mint-UI中组件，组件脱标，所以最外层div需要添加padding属性
- router-view中渲染路由内容，用transition包裹起来，做动画效果
- 购物车的字体图标需要额外的样式和tff文件，将文件拷贝到自己的项目中，导入
- 将原有模板的a链接改造成router-link，href属性改成to属性
- mui-active是MUI提供的一个类，有按钮高亮显示的效果
- 给整体添加overflow-x:hidden表示x方向的内容隐藏，取消滚动条。添加position:absolute，页面固定，不会再切换的时候出现一个上一个下的漂浮效果。进入之前从右面移进来，所以是正的100%。离开之后从左面离开，所以应该是负的100%
- 按需导入组件，Vue.component表示全局注册
- linkActiveClass属性，在点击这个链接的时候触发，这里让mui-active类覆盖之前的类名，之前默认的类名是router-link-active
- 项目中的一些文件不需要上传到GitHub，WebStorm打开之后默认生成一个.idea后缀文件，里面放的是WebStorm的相关配置，这个文件可以被忽略
- VSCode提供了一些功能，可以不再执行上面命令行，简化了我们的操作，修改的行前面有蓝色标记，添加的行前面有绿色标记。被修改的文件会有提示，被修改的文件，可以恢复修改之前的状态，可以将修改内容添加到本地，文本框中添加提示信息，点击对勾是commit操作，点击后面的更多选项，推送，可以将本地内容提交到远程仓库
- mt-swipe-item标签用v-for循环渲染，使用key定义关键字，资源的路径肯定是唯一的，一个url地址肯定对应一个资源，任何url地址都是唯一的，所以可以把url作为关键字
- 轮播图整体添加一个高度，撑起这个元素。轮播的每个页都有mint-swipe-item类，这个类中使用nth-child交集选择器，对每个页面进行设置。mint-swipe-item:nth-child(1)可以写成scss的形式，交集选择器，前面一定添加&符号

