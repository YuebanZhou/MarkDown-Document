# DOM和BOM

## DOM
### 概念

+ DOM:Document Object Model 文档对象模型。
+ DOM作用：操作页面中的元素。
+ 顶级对象是document 就是指HTML或者XML文件。
+ HTML侧重于展示数据，XML侧重于存储数据，XHTML写的是HTML代码，遵循的是XML 的规范。
+ 每一个HTML文件都可以看成是一个文档对象，里面所有的标签的层次关系都可以看成是一个树形结构图，树状图。
+ 页面中所有的内容都是节点：标签节点，属性节点，文本节点。IE8中会忽略空白节点
+ 节点属性
  * nodeType 如果是标签，值为1；如果是属性，值为2；如果是文本，值为3
  * nodeName 如果是标签，值为大写标签名字；如果是属性，值为小写属性名字；如果是文本，值为#text
  * nodeValue 如果是标签，值为 null ；如果是属性，值为属性值；如果是文本，值为文本内容
+ 页面中的标签，标签就是元素，元素就可以看成是对象，标签也是节点。


  + 节点比元素大。
  + 根元素：页面中最外边的标签
  + 文档元素：文档中的第一个元素，HTML文档元素就是< html>

### 绑定和解绑

+ 第一种写法
  * 对象.on+"事件名字"=事件处理函数 
  * 对象.on+"事件名字"=null
+ 第二种写法
  * 对象.addEventListener("事件名字",命名函数,false);
  * 对象.revemoEventListener("事件名字",命名函数的名字,false);
+ 第三种写法
  * 对象.attachEvent("事件名字",命名函数);
  * 对象.detachEvent("事件名字",命名函数的名字);

### 事件冒泡

+ 元素A中嵌套了另一个元素B，里面元素B和外面元素A注册了相同的事件，如果里面元素B的事件触发了，外面的元素A的该事件也会自动的触发。
+ 阻止事件冒泡的两种方法 window.event.cancelBubble=true 或者是 e.stopPropagation();

### 事件的三个阶段

+ 事件捕获阶段，事件目标阶段，事件冒泡阶段

+ 事件阶段有一个属性，这个属性是需要通过事件参数对象.eventPhase来获取的

+ 属性的值是：1->捕获阶段2->目标阶段3->冒泡阶段

+ e.type获取的是当前触发该事件的事件类型

  ```html
  <script>
    var objs=[my$("dv1"),my$("dv2"),my$("dv3")];
    objs.forEach(function(element){
        element.addEventListener("click",function(e){
            console.log(this.id+"==="+e.eventPhase+"==="+e.type);
        },false);
    });
  </script>
  ```

  false值由内向外，一般采用false

  dv3===2===click

  dv2===3===click

  dv1===3===click

  ```html
  <script>
    var objs=[my$("dv1"),my$("dv2"),my$("dv3")];
    objs.forEach(function(element){
        element.addEventListener("click",function(e){
            console.log(this.id+"==="+e.eventPhase+"==="+e.type);
        },true);
    });
  </script>
  ```

  true值由外向内

  dv1===1===click

  dv2===1===click

  dv3===2===click

### DOM级别

+ DOM0 初级阶段
+ DOM1 规定了节点的类型Node，一般使用DOM1
+ DOM2 新增了一些方法，但是很多浏览器并不支持
+ DOM3 大多数浏览器都没有支持

### 全局变量和隐式全局变量

+ 全局变量不会被删除，隐式全局变量会被删除
```html
<script>
  var num=10;//全局变量
  number=20;//隐式全局变量
  delete num;//删除全局变量
  delete number;//删除隐式全局变量
  console.log(typeof num);//number
  console.log(typeof number);//undefined
</script>
```
### innerText和innerHTML

+ 设置文本内容的时候，用两个都一样
+ 设置标签内容的时候
  * innerText设置标签内容，显示的是标签+文本，标签实际上是转义出来了
  * innerHTML设置标签内容，显示的是效果
+ 如果想要设置文本，用谁都可以，如果想要有标签效果，用innerHTML
+ 获取标签中的文本内容，使用innerText和innerHTML都可以，如果获取的是元素中的标签和文本内容，应该使用innerHTML

### innerText和textContent

+ innerText：谷歌支持，低版本火狐不支持，高版本火狐支持，IE8支持
+ textContent：谷歌支持，火狐支持，IE8不支持
+ 浏览器不支持某属性时，该属性的类型是undefined

### className

+ html标签中的class属性，在js 中是关键字，不能直接使用。所以， 对象.class="值"; 这种写法是错误的。应该这么写：对象.className="值";
+ 对象.style.属性名="值";  div.style.backgroundColor="red";
+ 对象.className="值";  div.className="cls";

### 自定义属性

+ 获取自定义属性的值 对象.getAttribute(“属性的名字”); 返回值是该属性的值
+ 设置自定义属性的值 对象.setAttribute(“属性的名字”,”值”);
+ removeAttribute，getAttribute，setAttribute三个方法不仅可以操作元素的自定义属性及值，还可以操作元素的自带属性

### 隐藏方式

```html
<script>
  zy$("btn").onclick=function(){
    zy$("div").style.display="none";//不占位置      
    zy$("div").style.visibility="hidden";//占位置
    zy$("div").style.opacity=0;//占位置
    zy$("div").style.width=0;//占位置
    zy$("div").style.height=0;
  }
</script>
```
### 设置样式

- 如果样式的属性是在style属性中设置的，是可以直接获取的
- 如果样式的属性是在style标签中设置的，不能直接获取

### 获取节点元素12个

```html
<script>
 console.log(zy$("uu").childNodes);
 console.log(zy$("uu").children);//推荐使用
 console.log(zy$("uu").parentNode);//推荐使用
 console.log(zy$("uu").parentElement);
 console.log(zy$("uu").firstChild);
 console.log(zy$("uu").firstElementChild);
 console.log(zy$("uu").lastChild);
 console.log(zy$("uu").lastElementChild);
 console.log(zy$("uu").previousSibling);
 console.log(zy$("uu").previousElementSibling);
 console.log(zy$("uu").nextSibling);
 console.log(zy$("uu").nextElementSibling);
</script>
```
### 创建元素的三种方式

+ 第一种document.write
+ 第二种 对象.innerHTML=”标签代码及内容”
+ 第三种 document.creatElement

### 定时器

#### setInterval()

* 参数：代码
* 参数：时间----1000毫秒---1秒
* 返回值：该定时器的id值
* 执行过程：当页面加载完毕后，过了一段时间才执行里面的代码，再过一段时间再次里面的代码，反复执行
* clearInterval(timeId);//清理定时器

#### setTimeout()

* 参数：代码
* 参数：时间----1000毫秒---1秒
* 返回值：该定时器的id值
* 执行过程：当页面加载完毕后，过了一段时间才执行里面的代码，再过一段时间再次里面的代码，只执行一次
* clearTimeout(timeId2);//清理定时器

### 三大系列

#### offset系列

* offsetLeft：元素相对左边的横坐标
* offsetTop：元素相对上面的纵坐标
* offsetWidth：元素的宽度，有边框
* offsetHeight：元素的高度，有边框
* offset系列获取的值都是数字类型
* offsetWidth（offsetHeight）获取的元素本身的宽（高）+元素边框的宽（高）
* 如果父级元素脱离文档流，子级元素此时的offsetLeft获取的是相对父级元素的pading+自己的margin
* 如果元素自己脱离文档流，此时的offsetLeft获取的事自己的left+自己的margin

#### scroll系列

* scrollLeft：向左卷曲出去的横坐标
* scrollTop：向上卷曲出去的纵坐标
* scrollWidth：内容实际的宽度，没有内容就是元素的宽度，没有边框
* scrollHeight：内容实际的高度，没有内容就是元素的高度，没有边框

#### client系列

* clientX：可视区域的横坐标
* clientY：可视区域的纵坐标
* clientWidth：可视区域的宽
* clientHeight：可视区域的高

## BOM
### 概述

+ 浏览器中的顶级对象window，页面中的顶级对象document
+ 页面中所有的内容都是window的，变量是属于window的，函数是属于window的。
+ 因为页面中所有的内容都是window，所以，window是可以省略不写的。

### 系统对话框

+ alert() //不同浏览器中的外观是不一样的
+ confirm();//true确定,false取消
+ prompt()  //不推荐使用

### 窗口对象

+ Window.open()  打开窗口
  * 参数1:地址(内部的地址,外部的地址)
  * 参数2:打开的方式：self 是在当前的页面中打开，blank是在新的选项卡中打开
  * 参数3:好多的代码
+ window.close()  关闭窗口
+ Window.location对象
  * location相当于浏览器地址栏，可以将url解析成独立的片段
+ Window.navigator对象
  * window.navigator 的一些属性可以获取客户端(浏览器)的一些信息：
  * userAgent用户当前浏览器信息
  * platform用户系统信息（不准确）
+ Window.history对象
  * 历史记录管理：
  * 后退：history.back()    history.go(-1)
  * 前进：history.forward()  history.go(1)
  * 操作之后生成历史记录