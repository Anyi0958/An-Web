## JavaScript 简介
JavaScript 是互联网上最流行的脚本语言，这门语言可用于 HTML 和 web，更可广泛用于服务器、PC、笔记本电脑、平板电脑和智能手机等设备。

- JavaScript 是脚本语言
- JavaScript 是一种轻量级的编程语言。
- JavaScript 是可插入 HTML 页面的编程代码。
- JavaScript 插入 HTML 页面后，可由所有的现代浏览器执行。

## JavaScript 输出方式


- 使用 `window.alert()` 弹出警告框。
- 使用 `document.write()` 方法将内容写到 HTML 文档中。
- 使用 `innerHTML` 写入到 HTML 元素。
- 使用 `console.log()` 写入到浏览器的控制台。

### 注意

`document.write()`方法可以向 HTML 输出流中插入你传入的内容，浏览器会按着 HTML 元素依次顺序依次解析它们，并显示出来。
 
需要注意的是，如果在文档加载完成后（即 HTML 输出已完成），再使用 `document.write()` 方法来要求浏览器来解析你的内容，浏览器就会重写整个 document，导致最后的这个 `document.write()` 方法输出的内容会覆盖之前所有的内容。

- 实例
```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <p> 我是 p 标签 </p>
    <script>
        document.write('<p> 我是插入 HTML 输出流的内容 </p>');   
        window.onload = function(){
            setTimeout(()=>{
                document.write('<p> 文档流加载完成，我会覆盖它们！ </p>');
            },2000);
        }; 
        document.write('<p> 我是插入 HTML 输出流的内容 </p>');   
    </script>
</body>
</html>
```
- 效果
![](https://static01.imgkr.com/temp/f77862bac98647fbbf8f3dada0b7beb5.gif =40%x)



## JavaScript 数据类型

### 6 种不同的数据类型
  - string
  - number
  - boolean
  - object
  - function
  - symbol

### 3 种对象类型
  - Object
  - Date
  - Array
  
### 2 个不包含任何值的数据类型
  - null
  - undefined


## 注意
  - **`NaN` 的数据类型是 `number`**
  - **数组(`Array`)，日期(`Date`)，空(`null`) 数据类型是 `object`**
  - **`null` 和 `undefined` 区别**
      1. `null` 和 `undefined` 的值相等，都是原始类型，保存在栈中变量本地，但类型不等
      2. `undefined` 是所有没有赋值变量的默认值，自动赋值，数据类型为 `undefined`
      3. `null` 主动释放一个变量引用的对象(*释放内存*)，表示一个变量不再指向任何对象地址，数据类型是 `object`

         ```javascript
            typeof undefined             // undefined
            typeof null                  // object
            null == undefined            // true
            null === undefined           // false
            
          ```
    
## JavaScript 判断数据类型


###  使用 typeof 判断

  - 注意：`typeof` 不能区分 `null` 和 对象类型(`Array Object Date`)

```javascript
      typeof "";           // 返回 string
      typeof 0;            // 返回 number
      typeof false;        // 返回 boolean
      typeof Symbol();     // 返回 symbol
      typeof undefined;    // 返回 undefined
      typeof function(){}; // 返回 function
      typeof null;         // 返回 object
      typeof [];           // 返回 object
      typeof {};           // 返回 object
      typeof new Date();   // 返回 object
      
```

###  使用 constructor 判断

  - 原理：`constructor` 属性返回所有 `JavaScript` 变量的构造函数。

  - 注意：`constructor` 不能区分 `null` 和 `undefined`（无 `constructor` 属性，会报错 `Uncaught TypeError` ）

  ```javascript
    "".constructor.toString()            // 返回函数 function String()  { [native code] }
    (0).constructor.toString()           // 返回函数 function Number()  { [native code] }
    false.constructor.toString()         // 返回函数 function Boolean() { [native code] }
    Symbol().constructor.toString()      // 返回函数 function Symbol() { [native code] }
    [].constructor.toString()            // 返回函数 function Array()   { [native code] }
    {}.constructor.toString()            // 返回函数 function Object()  { [native code] }
    new Date().constructor.toString()    // 返回函数 function Date()    { [native code] }
    function(){}.constructor.toString()  // 返回函数 function Function(){ [native code] }
    (null).constructor.toString()        // 返回error Uncaught TypeError: Cannot read property 'constructor' of null
    (undefined).constructor.toString()   // 返回error Uncaught TypeError: Cannot read property 'constructor' of null
  ```

### 使用 toString 判断 (推荐)
  - 原理：待完善
  ```javascript
    Object.prototype.toString.call('') ;             // [object String]
    Object.prototype.toString.call(1) ;              // [object Number]
    Object.prototype.toString.call(true) ;           // [object Boolean]
    Object.prototype.toString.call(Symbol());        //[object Symbol]
    Object.prototype.toString.call(undefined) ;      // [object Undefined]
    Object.prototype.toString.call(null) ;           // [object Null]
    Object.prototype.toString.call(new Function()) ; // [object Function]
    Object.prototype.toString.call(new Date()) ;     // [object Date]
    Object.prototype.toString.call([]) ;             // [object Array]
    Object.prototype.toString.call({}) ;             // [object object]
    Object.prototype.toString.call(new RegExp()) ;   // [object RegExp]
    Object.prototype.toString.call(new Error()) ;    // [object Error]
    Object.prototype.toString.call(document) ;       // [object HTMLDocument]
    Object.prototype.toString.call(window) ;         //[object global] window 是全局对象 global 的引用
  ```
  
## JavaScript 运算符

### JavaScript 算术运算符

只展示 自增（自减同理） 算术运算符，[完整请参考此处](https://www.runoob.com/js/js-operators.html)

```javascript
  let x,y = 5;
  x = y++; // 等同于 x = y; y = y+1;
  console.log(x,y) // x = 5, y = 6
```

```javascript
  let x,y = 5;
  x = ++y; // 等同于 y = y+1; x = y; 
  console.log(x,y) // x = 6, y = 6
```
由上可以看出
  -  自增运算符( `++` )在变量左侧 ，变量自身先加一，然后进行其他运算
  -  自增运算符( `++` )在变量右侧 ，变量先进行其他运算，然后自身加一

面试题
  ```javascript
    let x,y = 5;
    x = ++y +5 + y++ + y + 6 ;
    // 此时x , y 的值为多少
    console.log(x,y) // x = 30,y = 7
  ```

## JavaScript 常用事件
### window 窗口事件

| window 窗口事件 |    描述     |
| :---------    |    :--       | 
| onload        |    浏览器已完成页面的加载 |
| onunload      |    从网页离开时发生（点击跳转，页面重载，关闭浏览器窗口等） |

### form 表单事件   

| form 表单事件    |    描述     |
| :---------    |    :--       | 
| onblur        |  当元素失去焦点时触发  |
| onchange      |  在元素的值被改变时触发 |
| onfocus       |  当元素获得焦点时触发   |
| onreset       |  当表单中的重置按钮被点击时触发  |
| onselect      |  在元素中文本被选中后触发  |
| onsubmit      |  在提交表单时触发 |


### keyboard 键盘事件

| keyboard 键盘事件    |    描述     |
| :---------          |    :--       | 
| onkeydown     | 在用户按下按键时触发  |
| onkeypress    | 在用户按下按键后  | 

### mouse 鼠标事件

| mouse 鼠标事件   |    描述     |
| :---------      |    :--       | 
| onclick         |  当在元素上发生鼠标点击时触发 |
| ondblclick      |  当在元素上发生鼠标双击时触发|
| onmousedown     |  当元素上按下鼠标按钮时触发 |
| onmousemove     |  当鼠标指针移动到元素上时触发 |
| onmouseout      |  当元素指针移出元素时触发  |
| onmouseup       |  当元素上释放鼠标按钮时触发 |
| onabort         |  当退出时触发         |
| onwaiting       |  当媒体已停止播放但打算继续播放时触发 |

更多事件列表 [JavaScript DOM事件](https://www.runoob.com/jsref/dom-obj-event.html)



## String 常用属性和方法
  - 字符串长度 `length` 
    ```javascript
      // 返回字符串的长度
     'hello JavaScript'.length
     
    ```
    
  - 字符串切割 `slice()` 
    ```javascript
     // 不改变原数据，返回切割后的字符串，包含 第一个参数 索引值 不包含 第二个参数。
        var str = "Apple, Banana, Mango";
        str.slice(7,13);   // 结果是：Banana
        str.slice(-13,-7); // 结果是：Banana
        str.slice(7);      // 结果是：Banana, Mango
        str.slice(-13);    // 结果是：Banana, Mango
     
    ```
    
  - 字符串取值 `substr()`
    ```javascript
     // 不改变原数据，类似于 slice()，不同之处在于第二个参数规定被提取部分的长度。
      var str = "Apple, Banana, Mango";
      str.substr(7,6);   // 结果是：Banana
      str.substr(7);     // 结果是：Banana, Mango
      str.substr(-5);    // 结果是：Mango
     
    ```
    
  - 字符串分割为数组`split()`
    ```javascript
     // 不改变原数据，返回分隔后的数组。
      "a,b,c,d,e".split(",");     // 用逗号分隔 结果是：["a", "b", "c", "d", "e"]
      "a,b,c,d|e".split(",");     // 用逗号分隔 结果是：["a", "b", "c", "d|e"]
      "hello".split("");          // 步长为1分隔 结果是：["h", "e", "l", "l", "o"]
     
    ``` 
    
  - 查询指定字符是否存在`includes()`
    ```javascript
     // 不改变原数据，存在返回 true，否则 false。
      "a,b,c,d,e".includes("abc");     // 结果是：false
      "a,b,c,d|e".includes("d|e");     // 结果是：true
     
    ``` 
    
  - 查找首次出现的字符索引 `indexOf()`
    ```javascript
     // 不改变原数据，方法返回字符串中指定文本首次出现的索引（位置），不存在返回 -1
      var txt = 'hello word'
      txt.indexOf("l");     // 结果是：2
      txt.indexOf("o");     // 结果是：4
      txt.indexOf("j");     // 结果是：-1
     
    ``` 
    
  - 查找最后出现的字符索引 `lastIndexOf()`
    ```javascript
     // 不改变原数据，方法返回字符串中指定文本最后出现的索引（位置），不存在返回 -1
      var txt = 'hello word'
      txt.lastIndexOf("l");     // 结果是：3
      txt.lastIndexOf("o");     // 结果是：7
      txt.lastIndexOf("j");     // 结果是：-1
     
    ``` 
    
  - 替换字符串内容 `replace()`
    ```javascript
     // 不改变原数据，方法返回修改后的字符串
      var txt = 'Hello World,Wonderful World'
      // 默认只替换第一个匹配值
      txt.replace("World","js");     // 结果是："Hello js,Wonderful World"
      // 全局匹配 g
      txt.replace(/World/g,'js');     // 结果是："Hello js,Wonderful js"
      // 默认区分大小写
      txt.replace(/world/g,'js');     // 结果是："Hello World,Wonderful World"
       // 不区分大小写 i ，并全局匹配 g
      txt.replace(/world/ig,'js');     // 结果是："Hello js,Wonderful js"
     
    ``` 
    
  - 字符串转换为小写 `toLowerCase()`
    ```javascript
     // 不改变原数据，方法返回修改后的字符串
      var txt = 'HELLO WORLD'
      txt.toLowerCase();     // 结果是："hello world"
      
    ``` 
    
  - 字符串转换为大写 `toUpperCase()`
    ```javascript
     // 不改变原数据，方法返回修改后的字符串
      var txt = 'hello world'
      txt.toUpperCase();     // 结果是："HELLO WORLD"
     
    ``` 
    
  - 去除首尾空格 `trim()`
    ```javascript
     // 不改变原数据，方法返回修改后的字符串
      var txt = ' hello world '
      txt.trim();     // 结果是："hello world"
     
    ``` 
    
  - 连接多个字符串 `concat()`
    ```javascript
     // 不改变原数据，方法返回修改后的字符串
      var txt = ''
      txt.concat('hello ','world,','wonderful ','world');     // 结果是："hello world,wonderful world"
     
    ``` 
    
    [查看完整方法可以查看此处](https://www.runoob.com/jsref/jsref-obj-string.html)
    
## Array 常用属性和方法

  - 数组长度 `length` 
    ```javascript
      // 设置或返回数组元素的个数
     ["Saab", "Volvo", "BMW"].length // 3
     
    ```
    
  - 数组拼接 `concat()` 
    ```javascript
      // 连接两个或更多的数组，并返回结果。
      let a = ["Saab", "Volvo"];
      let b = ["BMW"];
      let c = ["Tom"];
      let d = a.concat(b,c); // ["Saab", "Volvo", "BMW", "Tom"]
     
    ```
    
  - 返回数组的可迭代对象 `entries()` 
    ```javascript
      var fruits = ["Banana", "Orange", "Apple"];
      var x = fruits.entries();
      x.next().value; // [0, "Banana"]
      x.next().value; // [1, "Orange"]
      x.next().value; // [2, "Apple"]
      x.next().value; // undefined
     
    ```

  - 反转数组的元素顺序 `reverse()` 
    ```javascript
      [1,2,3].reverse() //  [3, 2, 1]
     
    ```

  - 对数组的元素进行排序 `sort()` 
    ```javascript
      // 默认排序顺序为按字母升序
      // 数字排序需要传入函数
      [40,100,1,5,25,10].sort(); // [1, 10, 100, 25, 40, 5]
      
      [40,100,1,5,25,10].sort((a,b)=>{
        return a - b;
      }); //   [1, 5, 10, 25, 40, 100]
      
     [40,100,1,5,25,10].sort((a,b)=>{
        return b - a;
      }); //  [100, 40, 25, 10, 5, 1]
     
    ```
    
    
  - 判断一个数组是否包含一个指定的值 `includes()` 
    ```javascript
      [1,2,3,4,5,6].includes(8) // false
      [1,2,3,4,5,6].includes(6) // true
     
    ```
    
  - 把数组的所有元素放入一个字符串 `join()` 
    ```javascript
      // 默认用 , 进行分隔
      [1,2,3,4,5,6].join() // "1,2,3,4,5,6"
      [1,2,3,4,5,6].join('and') // "1and2and3and4and5and6"
      [1,2,3,4,5,6].join('') // "123456"
     
    ```
  
  - 删除数组的最后一个元素并返回删除的元素 `pop()` 
    ```javascript
      let a = [1,2,3,4,5,6];
      a.pop(); // 6  a => [1,2,3,4,5]
     
    ```

  - 向数组的末尾添加一个或更多元素，并返回新的长度 `push()` 
    ```javascript
      let a = [1,2,3,4,5,6];
      a.push(7); // 7  a => [1,2,3,4,5,6,7]
     
    ```
    
  - 删除并返回数组的第一个元素 `shift()` 
     ```javascript
      let a = [1,2,3,4,5,6];
      a.shift(); // 1  a =>  [2, 3, 4, 5, 6]
     
    ```

  - 向数组的开头添加一个或更多元素，并返回新的长度 `unshift()` 
     ```javascript
      let a = [1,2,3,4,5,6];
      a.unshift(7); // 7 a =>  [7,1, 2, 3, 4, 5, 6]
     
    ```

  - 数组每个元素都执行一次回调函数 `forEach()` 
    ```javascript
      // item 当前元素 
      // index 当当前元素的索引值
      // arr 当前元素所属的数组对象
      [1,2,3,4,5,6].forEach((item,index,arr)=>{}) // false
     
    ```
    
  - 通过指定函数处理数组的每个元素，并返回处理后的数组 `map()` 
    ```javascript
      [1,2,3,4,5,6].map((item,index,arr)=>{
        return i * 2;
      }) // [2, 4, 6, 8, 10, 12]

    ```
    
  - 检测数值元素的每个元素是否都符合条件 `every()` 
    ```javascript
      [1,2,3,4,5,6].every(i=>i > 1) // false
      [1,2,3,4,5,6].every(i=>i > 0) // true
     
    ```
    
  - 检测数组元素中是否有元素符合指定条件 `some()` 
    ```javascript
      [1,2,3,4,5,6].some(i=>i > 1) // true
      [1,2,3,4,5,6].every(i=>i > 10) // false
     
    ```
    
  - 检测数值元素，并返回符合条件所有元素的数组 `filter()` 
    ```javascript
      [1,2,3,4,5,6].filter(i=>i > 1) // [2, 3, 4, 5, 6]

    ```
    
  - 累加 `reduce()` 
    ```javascript
      [1,2,3,4,5,6].reduce((a,b)=>a+b)  // 21

    ``` 
    
    [查看完整方法可以查看此处](https://www.runoob.com/jsref/jsref-obj-array.html)

## Set 方法
  - add()
  - delete()
  - has()
  - clear()
## Map 方法
  - add()
  - delete()
  - has()
  - clear()

## 异常

  - try 语句测试代码块的错误。
  - catch 语句处理错误。
  - throw 语句创建自定义错误。
  - finally 语句在 try 和 catch 语句之后，无论是否有触发异常，该语句都会执行。
  ```javascript
    try{
      throw '自定义错误'
    }catch(err){
      console.log('错误信息',err)
    }finally{
      console.log('程序是否异常,都会执行此内容')
    }
  ```

## AJAX

### 简介

- AJAX = 异步 JavaScript 和 XML。

- AJAX 是一种用于创建快速动态网页的技术。

通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

### XMLHttpRequest 对象方法

| 方法       | 	描述 | 
| :--------- | :-- |
| new XMLHttpRequest()     |  	创建新的 XMLHttpRequest 对象  |  
| abort()   |  	取消当前请求  |  
| getAllResponseHeaders() |  返回头部信息  | 
| open(method, url, async) | 规定请求的类型、URL 以及是否异步处理请求 |
| send()   |  	将请求发送到服务器，用于 GET 请求  |  
| send(string) | 	将请求发送到服务器，用于 POST 请求 |
| setRequestHeader() | 	向要发送的报头添加标签/值对 |


### XMLHttpRequest 对象属性

| 属性       | 	描述 | 
| :--------- | :-- |
| onreadystatechange  |  	存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。  |  
| readyState  |  	存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。|
| status | 返回请求的状态号 |


### readyState 状态
| 状态       | 	描述 | 
| :--------- | :-- |
| 0 | 请求未初始化  |  
| 1 | 服务器连接已建立  |
| 2 | 请求已接收  |
| 3 | 请求处理中  |
| 4 | 请求已完成，且响应已就绪  |

### 实例
```javascript
// 创建对象
let xhr;
if(window.XMLHttpRequest){
  xhr = new XMLHttpRequest();
}else{
 // ie5,ie6
  xhr = new ActiveXObject("Microsoft.XMLHTTP");
}

// 请求地址
xhr.open("GET","https://api.ixiaowai.cn/tgrj/index.php");

// 发送
xhr.send();

// 监听状态事件
xhr.onreadystatechange = function(){
  // 响应成功返回结果
  if(xhr.readyState === 4 && xhr.status === 200){
    console.log(xhr.responseText)
    document.getElementsByTagName('body')[0].innerHTML = xhr.responseText;
  }
}

```
