# Promise

## 封装读取文件

- 读取文件需要引入fs模块和path模块
- 普通读取文件，利用readFile，抛出错误，代码立即停止
  - 这个方法是异步的，在后面调用的时候，结果是undefined，所以这里不能用return，可以使用回调函数
- readFile中使用回调函数
  - 如果路径传入异常，throw会立即停止程序，这里将err处理也交给用户
  - 改进一下，callback 中，有两个参数，第一个参数，是 失败的结果，第二个参数是成功的结果
  - 同时，我们规定了， 如果成功后，返回的结果，应该位于 callback 参数的第二个位置，此时， 第一个位置 由于没有出错，所以，放一个 null。  如果失败了，则 第一个位置放 Error对象，第二个位置防止一个 undefined

```javascript
const fs = require('fs')
const path = require('path')

// 这是普通读取文件的方式
/* fs.readFile(path.join(__dirname, './files/1.txt'), 'utf-8', (err, dataStr) => {
  if (err) throw err
  console.log(dataStr)
}) */

// 初衷： 给定文件路径，返回读取到的内容
function getFileByPath(fpath, callback) {
  fs.readFile(fpath, 'utf-8', (err, dataStr) => {
    // 如果报错了，进入if分支后，if后面的代码就没有必要执行了
    if (err) return callback(err)
    // console.log(dataStr)
    // return dataStr
    callback(null, dataStr)
  })
}

/* var result = getFileByPath(path.join(__dirname, './files/1.txt'))
console.log(result) */
getFileByPath(path.join(__dirname, './files/11.txt'), (err, dataStr) => {
  // console.log(dataStr + '-----')
  if (err) return console.log(err.message)
  console.log(dataStr)
})
```

## 进一步封装

- 上面的回调函数，也可以将成功回调和失败回调分离开，调用的时候，对应着传参就可以了
- 决定文件的执行顺序，可以使用嵌套的方式，不过这样比较麻烦，缩进严重

```javascript
const fs = require('fs')
const path = require('path')

function getFileByPath(fpath, succCb, errCb) {
  fs.readFile(fpath, 'utf-8', (err, dataStr) => {
    if (err) return errCb(err)
    succCb(dataStr)
  })
}

// getFileByPath(path.join(__dirname, './files/11.txt'), function (data) {
//   console.log(data + '娃哈哈，成功了！！！')
// }, function (err) {
//   console.log('失败的结果，我们使用失败的回调处理了一下：' + err.message)
// })

// 需求： 先读取文件1，再读取文件2，最后再读取文件3
// 回调地狱

getFileByPath(path.join(__dirname, './files/1.txt'), function (data) {
  console.log(data)

  getFileByPath(path.join(__dirname, './files/2.txt'), function (data) {
    console.log(data)

    getFileByPath(path.join(__dirname, './files/3.txt'), function (data) {
      console.log(data)
    })
  })
})
```

## promise

- 使用ES6中的promise来解决回调地狱的问题，promise本质是解决回调地狱问题，并不能减少代码量
- 串联应用.then
- promise是一个构造函数，可以new一个promise，得到一个promise的实例对象
- 在promise上有两个函数，resolve和reject，前面是成功之后的回掉函数，后面是失败之后的回调函数
- 在promise构造函数的prototype属性上有一个.then方法，只要是promise构造函数创建的实例，都可以访问到.then方法
- promise表示一个异步操作，每当我们new一个promise的实例，这个实例就是一个具体的异步操作
- 既然promise创建的实例，是一个异步操作，那么这个异步操作只能有两种状态
  - 第一种状态，异步执行成功，需要在内部调用成功的回调函数resolve，将结果返回。
  - 第二种状态，异步执行失败，需要在内部调用成功的回调函数reject，将结果返回
- 形式上的异步操作和具体的异步操作者，区分只在一个function

```javascript
var promise = new Promise()
var promise = new Promise(function(){
  // 这个 function 内部写的就是具体的异步操作
}) 
```

- new的时候，除了能够得到实例之外，还能立即调用function中的异步代码

```javascript
var promise = new Promise(function () {
  fs.readFile('./files/2.txt', 'utf-8', (err, dataStr) => {
    if (err) throw err
    console.log(dataStr)
  })
}) 
```

- 如果不想要立即执行，被调用的时候再执行

  - 将内容放到一个函数中
  - 只有调用这个函数的时候，所有内容才会执行
  - 按需决定这个promise是否要执行

- p是函数内部返回的结果，用p.then调动两个回调

  - 直接将实例return出去，之后调用的时候，就是在调用实例，可以直接点then

- 成功的回调必须传，失败的回调可以省略不传

- 在上一个.then中返回一个新的promise实例，可以继续用下一个.then来处理

- 当需要，前边报错不影响后面执行的时候

  - 单独为每个promise通过then指定失败回调

  ```javascript
  getFileByPath('./files/11.txt')
    .then(function (data) {
      console.log(data)

      // 读取文件2
      return getFileByPath('./files/2.txt')
    }, function (err) {
      console.log('这是失败的结果：' + err.message)
      // return 一个 新的 Promise
      return getFileByPath('./files/2.txt')
    })
    .then(function (data) {
      console.log(data)

      return getFileByPath('./files/3.txt')
    })
    .then(function (data) {
      console.log(data)
    }).then(function (data) {
      console.log(data)
    }) 
  ```

- 当需要，前面报错，后面所有内容都不执行，依赖于前面的执行结果

  在最后用catch捕获错误

  - catch作用，如果前面有任何的promise执行失败，立即终止所有的promise的执行马上进入catch中执行

  ```javascript
  getFileByPath('./files/1.txt')
    .then(function (data) {
      console.log(data)

      // 读取文件2
      return getFileByPath('./files/22.txt')
    })
    .then(function (data) {
      console.log(data)

      return getFileByPath('./files/3.txt')
    })
    .then(function (data) {
      console.log(data)
    })
    .catch(function (err) { // catch 的作用： 如果前面有任何的 Promise 执行失败，则立即终止所有 promise 的执行，并 马上进入 catch 去处理 Promise中 抛出的异常；
      console.log('这是自己的处理方式：' + err.message)
    })
  ```

## jquery

- jquery中也可以使用.then

```html
<body>
  <input type="button" value="获取数据" id="btn">
  <script src="./node_modules/jquery/dist/jquery.min.js"></script>
  <script>
    $(function () {
      $('#btn').on('click', function () {
        $.ajax({
          url: './data.json',
          type: 'get',
          dataType: 'json'
        })
          .then(function (data) {
            console.log(data)
          })
      })
    });
  </script>
</body>
```



