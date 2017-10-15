# jQuery

## jQuery介绍
### 简介

+ jQuery就是JavaScript库，封装了一些函数代码。
+ JS中其他的库：Prototype、YUI(网络反响一般)、Dojo、ExtJS、jQuery等。
+ 写得少，做得多，开源，插件丰富，免费，链式编程，隐式迭代 （看不见的循环遍历）
+ jQuery的文件：一般都是两个的文件（正常版本的，压缩版本）
+ 正常版本的：开发的时候使用
+ 压缩版本的：上线的时候使用
+ jQuery中顶级对象：jQuery----$
+ jQuery中所有的方法或者属性都是要通过jQuery对象来调用的

### 基本选择器

+ id选择器 $("#id属性的值")--->元素对象
+ 类选择器 $(".类样式的名字")--->元素
+ 标签选择器 $("标签名字")--->元素

### CSS方式设置样式的写法

```html
<script>
  $(function () {
    $("#btn").click(function () {
      //第一种写法
      $("#btn").css("width","300px");
      $("#btn").css("height","200px");
      $("#btn").css("backgroundColor","green");
      //第二种写法
      $("#btn").css("width","300px").css("height","200px").css("backgroundColor","green");
      //第三种写法
      var json={
        "width":"300px",
        "height":"200px",
        "backgroundColor":"green"
      };
      $("#dv").css(json);
    });
  });
</script>
```
+ CSS方法的设置和获取，CSS方法用来设置样式之后的代码返回的是对象，CSS方法用来获取样式，返回的是该样式属性的值，调用某方法后，是设置的方式才能进行链式编程

### 链式编程

+ $("#dv").text("哈哈").siblings("div")返回来的不是原来的对象，此时可以视为断链：（不是原来的那个对象了）所以要加end( )表示结束。
+ 链式编程原理：对象调用的方法中，返回的当前的对象。
+ 对象.方法(值)---返回的是对象
+ 对象.方法()----字符串值

### DOM和jQuery互换

#### DOM转jQuery

```html
<script>
  document.getElementById("btn2").onclick=function() {
    var btnObj=document.getElementById("btn1");
    //第一种
    $("#btn1").val("hehe");
    //第二种
    //btnObj.value="haha"
  }
</script>
```
#### jQuery转DOM

```html
<script>
  $("#btn4").click(function () {
    //第一种
    $("#btn3").get(0).value="haha";
    //第二种
    //$("#btn3")[0].value="haha";
    //第三种
    //$("#btn3").val="haha";
  })
</script>
```
### 多库共存

+ 引入多个库的时候，可能会出现冲突的情况。解决方法如下：释放控制权
```html
<script>
  var xy=$.noConflict();
  var $=10;
  xy(function () {
    xy("#btn").click(function () {
      xy(this).css("backgroundColor","red")
    })
  })
</script>
```
### 插件

+ 为$对象下添加一个方法。只要是jQuery的对象就可以调用这个方法
```html
<script>
  $.fn.changeColor=function (color) {
    $(this).css("backgroundColor",color);
  }
  $(function () {
    $("input").click(function () {
      $("#changeColor").changeColor($(this));
    });
  });
</script>
```
## 事件
### 子元素

+ .children( ) 当前元素中所有的子元素
+ .children("ul") 当前元素中所有的ul元素
+ .find( ) 查找，从当前的父级元素中查找某个元素
+ :first-child第一个子元素

### 隐藏显示动画

+ .show( ) 如果没有参数，就是正常的display:block或者none
+ .hide( ) 同上
+ slideUp( ) 滑上---隐藏
+ slideDown( ) 滑下---显示
+ slideToggle( ) 切换的滑入和滑出
+ fadeIn( ) 淡入
+ fadeOut( ) 淡出
+ fadeToggle( ) 切换的淡入淡出
+ fadeTo( ) 到达什么效果
+ 参数1：这个参数的类型可以是数字类型，也可以是字符串类型。
  * 数字类型：是时间---1000---1秒--1000毫秒。
  * 字符串类型:fast，normal，slow
+ 参数2：回调函数，这个函数是在动画执行结束后才执行。
+ animate(键值对,时间,回调函数);

### 奇偶

+ :odd 奇数，在数组中用户看到是偶数
+ :even 偶数，在数组中用户看到是奇数

### 索引

+ :eq(数值) 索引为数值的元素
+ :lt(数值) 小于索引的元素 实体 &lt;为小于号 <
+ :gt(数值) 大于索引的元素 实体 &gt;为大于号 >

### 类样式

+ addClass("类样式的名字") 添加 没有点
+ removeClass("类样式的名字") 移除 没有点
+ hasClass("类样式的名字") 判断 没有点
+ toggleClass("类样式的名字") 切换类样式 没有点 

### 兄弟元素

+ .next( ) 获取的是当前元素的下一个兄弟元素
+ .prev( ) 当前元素的前一个兄弟元素
+ .nextAll( ) 后面所有的兄弟元素
+ .prevAll( ) 前面所有的兄弟元素
+ .siblings( ) 所有的兄弟元素，没有自己
+ .first( ) 第一个元素

### 加载事件 三种

```html
<script>
  $(window).load(function () {
    console.log("页面加载完了")
  });
</script>
<script>
  $(document).ready(function () {
    console.log("页面加载完了")
  });
</script>
<script>
  jQuery(function () {
    console.log("页面加载完了")
  });
</script>
```
#### DOM的写法：

* window.onload=匿名函数；页面中只能存在一个，页面中所有内容加载后才触发。

#### jQuery写法：

* $(window).load(匿名函数)；相当于DOM的window.onload写法
* $(document).ready(匿名函数)：页面中基本元素加载后就触发， 一般在插件中比较常见

+ 上面的这两种写法都是把DOM对象转成了jQuery对象
+ jQuery中有自己的页面加载事件
+ DOM对象不能调用jQuery中发的方法，jQuery对象不能调用DOM对象中的方法

### 追加

+ 父级元素.append(子级元素);
+ 子级元素.appendTo(父级元素);
+ append和appendTo都有剪切的意思，clone是复制的意思
```html
<script>
  $("#btn").click(function () {
    $("#dv2").append($("#dv1>p"));//剪切
    $("#dv2").append($("#dv1>p").clone(true));//复制
    $("#dv1>p").appendTo($("#dv2"));//剪切
  })
</script>
```
### 创建

+ 两种方式 第一种创建的会是对象，第二种创建的是字符串
```html
<script>
  $("#btn").click(function () {
    $("<p>这是p</p>");
    $("#dv").html("<a href='#'> 哈哈哈</a>")
  })
</script>
```
### 清空

+ .html( );  $("#dv").html("") 清空内容
+ .empty( );  $("#dv").empty() 清空内容，没有参数
+ .remove( );  $("#dv>p").remove() 自杀
+ html方法和empty方法中，推荐使用empty方法

### value值

+ .val()
+ input系列中（除button），value值设置，不会对文本产生影响，只是修改value 的值。下拉框设置value，不是改变value的值，是选中value为这个值的选项。

### 自定义属性

+ .attr();设置，两个参数，参数1：属性名字，参数2：值。
+ .attr("属性名字"); 获取，该属性值
+ .attr方法相当于DOM中的setAttribute()和getAttribute()方法
+ .attr()方法可以设置标签的自带属性值，也可以设置自定义属性值
+ .prop方法可以设置和获取元素是否选中的结果，也可以应用元素子自带的属性的值，类似于.attr方法。
+ 两种方法的区别：.attr方法可以对自带属性或者自定义属性操作；.prop方法主要是针对的自带的属性。自定义的属性操作推荐用.attr方法，选中的设置操作推荐用prop方法。

### 三大系列

+ .offset()方法返回的是一个对象，该对象有两个属性，分别是：left和top
+ .scrollTop()方法，获取的是向上卷曲出去的距离。
+ .scrollLeft()方法，获取的是向左卷曲出去的距离。

### 宽高

+ 在jQuery中获取元素的宽和高可以直接调用封装的方法：.width()  .height()
+ 都是数字类型，这两个方法中，设置元素的宽或者高的时候，参数可以是数字类型，不用加px。

### 为元素绑定事件

#### bind方法

* 如果是一个参数：{"事件名字":事件处理函数}
* 例子：$("#btn").bind({"click":function(){});
* 如果是两个参数：事件名字，事件处理函数
* 例子：$("#btn").bind("click",function(){});

#### delegate方法

* 父级元素调用方法为子级元素绑定事件
* delegate最少三个参数：元素，类型，事件处理函数
* 例子：$("#dv").delegate(子级元素p,"事件类型click",function(){});

#### on方法on两种写法

* 父级元素.on(事件类型,子级元素,事件处理函数);
* 对象.on("事件类型",事件处理函数);

+ bind内部调用的on，delegate内部调用的on，on本身就是这个事件的绑定方法。
+ 推荐使用最原始的on的方式
+ 为元素添加事件：对象.事件名字(事件处理函数);
+ 调用这个事件并触发：对象.事件名字( );

### 解绑事件

+ 通过什么方式绑定事件，最好使用什么方式解绑事件
+ bind对应unbind，解绑多个事件，事件名中间用空格。没有参数，所有事件被解绑。
+ delegate对应undelegate，没有参数，所有子级元素的所有事件被解绑。有参数，解绑指定事件。
+ on对应off
  * 没有参数，所有事件被干掉，*表示所有
  * 只有事件，父元素子元素的所有的相应事件解绑
  * 有事件有标签，子元素对应事件解绑

### 触发

+ 元素有事件，直接调用这个元素的事件叫做触发。
```html
<script>
  $("#txt").focus();
  $("#txt").trigger("focus");
  $("#txt").triggerHandler("focus");
</script>
```
### 事件参数

+ currentTarget当前触发该事件的对象
+ delegateTarget当前的代理对象
+ target目标对象
```html
<script>
  $("div").delegate("input","click",function (e) {
    console.log(e.currentTarget.id);//btn2
    console.log(e.delegateTarget.id);//dv1
    console.log(e.target.id);//btn2
  })
</script>
```
### 遍历

+ .each遍历元素
+ each的匿名函数中，有两个参数，第一个表示索引，第二个表示每个元素，是DOM对象，所以添加事件时应先转换成jQuery元素。
```html
<script>
  $(function () {
    $("li").each(function (x,y) {
      var opacity=(x+1)/10;
      $(y).css("opacity",opacity)
    });
  });
</script>
```
### 判断元素是否存在length

+ .length 元素获取之后看做一个集合，集合长度为0，则这个元素不存在，否则存在。
```html
<script>
  if($("#btn").length!=0) {
    console.log("存在");
  } else {
    console.log("不存在");
  }
</script>
```