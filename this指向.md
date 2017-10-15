# this的指向

- 函数内this指向
  + 普通函数调用，指向window，严格模式下是undefined
  + 构造函数调用，指向实例对象，原型方法中this也是实例对象
  + 对象方法调用，指向方法所属对象，紧挨着的对象
  + 事件绑定方法，指向绑定事件对象
  + 定时器函数，指向window
  + 事件处理函数内部的this，始终都是点击的事件源DOM元素
  + 数组遍历方法（forEach，find等）内部的this都指向window
  + 如果在函数内部调用一个普通函数，该函数内部的this指向的是window
- 例子
  + 创建一个构造函数Person，这里是xjj接收Person的实例，所以this指向xjj
  ```html
  <script>
    function Person(name,age) {
      this.name=name;
      this.age=age;
    }
    var xjj=new Person('linan',16);
    console.log(xjj);
  </script>
  ```
  + 返回值return简单类型的时候，不会发生变化。返回值是复杂类型的时候，输出会发生变化
- 例子
  + name定义在全局，相当于window的name，调用handle的时候，this指向window，所以输出global
  ```html
  <script>
    var name='global';
    function handle() {
      console.log(this.name)
    }
    handle();//global
  </script>
  ```
  + 不管是在哪里被调用，handle函数的输出始终是不变的，所以这里的输出是global
  ```html
  <script>
    var name='global';
    function handle() {
      console.log(this.name)
    }
    var obj={
      name:'obj',
      foo:function(fn) {
        this.name='local';
        fn();
      }
    }
    obj.foo(handle);//global
  </script>
  ```
  + 直接输出obj的name，就是obj
  ```html
  <script>
    var name='global';
    function handle() {
      console.log(this.name)
    }
    var obj={
      name:'obj',
      foo:function(fn) {
        this.name='local';
        fn();
      }
    }
    console.log(obj.name)//obj
  </script>
  ```
  + 调用foo函数的情况下，后面的local覆盖了obj，所以obj的name变成了local
  ```html
  <script>
    var name='global';
    function handle() {
      console.log(this.name)
    }
    var obj={
      name:'obj',
      foo:function(fn) {
        this.name='local';
        fn();
      }
    }
    obj.foo(handle);//global
    console.log(obj.name)//local
  </script>
  ```
  + argument表示传入的参数组成的伪数组，argument[0]表示第一个参数，也就是fn
  + 这里得出的结果是undefined，因为argument[0]没有name这个属性
  ```html
  <script>
    var name='global';
    function handle() {
      console.log(this.name)
    }
    var obj={
      name:'obj',
      foo:function(fn) {
        this.name='local';
        arguments[0]();
      }
    }
    obj.foo(handle);//global
  </script>
  ```
  + 如果手动加一个name属性，就会有值，输出hehe
  ```html
  <script>
    var name='global';
    function handle() {
      console.log(this.name)
    }
    var obj={
      name:'obj',
      foo:function(fn) {
        this.name='local';
        arguments.name='hehe';
        arguments[0]();
      }
    }
    obj.foo(handle);//global
  </script>
  ```
