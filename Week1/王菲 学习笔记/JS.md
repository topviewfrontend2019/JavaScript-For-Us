## 第五章 引用类型
### 5.1 Object类型
   **引用**

  +  new Object();
  +  对象字面量表示法;    `var person = {name: "a",age: 11};`属性名也可以用字符串`"name"` 
    + 使用方括号时将访问的属性名以字符串形式放入方括号，方括号语法可以通过变量访问属性，也适用带关键字和空格等的属性名
    + 除非使用变量访问，一般推荐点表示法
 
### 5.2 Array类型
  - new Array();括号里可以传递数组长度也可以传递包含的项，`new`可以省略
  - 数组字面量表示法`var colors = ["red","blue"]`
     + 通过设置length属性可以从数组的末尾移除或添加新项，通过这种方法添加的新项为undefined
     
  **5.2.1检测数组**

  + Array.isArray()
      + `if(Array.isArray(value)) {操作}`

  **5.2.2转换方法**

  + toLocaleString()
  + toString()
  + valueOf()
      + 前两种方法返回的是以逗号隔开的字符串，后一种返回数组，但如果使用alert（.alueOf（）），alert调用toString（），返回字符串
  + join（）：把数组转化成字符串，按指定连接符链接，连接符即为参数 `colors.join("||") = red||blue`,如果不输入参数或undefined，一般是用逗号隔开
  
  **5.2.3栈方法**
  
  + push()接收任意数量的参数，把它们逐个添加到数组末尾，并返回修改后数组的长度
  + pop()从数组末尾移除最后一项，减少数组的length值，并返回被移除的项

  **5.2.4队列方法**

+   shift()移除数组第一项并返回该项
+   unshift()在数组前端添加项并返回新数组的长度

 **5.2.5重排序方法**

+ reverse()翻转数组项并返回改变之后的数组
+ sort()默认情况下按升序排列，比较的是字符，直接使用有问题

**5.2.6操作方法**

+ concat（）
+ slice()基于某一数组创建新数组，
    + 如果只有一个参数，返回从该参数指定位置开始到末尾所有项
    + 如过有两个，返回起始和结束位置之间的项，不包括结束的项，例如`slice(1,4)`只会取[1][2][3]三项
+ splice()
    + 删除：可以删除任意数量的项，指定要删除的第一项的位置和要删除的项数。（splice(0，2)会删除前两项）
    + 插入： 可以向指定位置插入任意数量的项，需要提供起始位置、要删除的项数（0）、要插入的项，如果要插入多个项，可以继续添加参数
    + 替换：向指定位置插入任意数量的项，同时删除任意数量的项，

**5.2.7位置方法**
   
+ indexOf(value，index)从前往后查找某值，index为起点的索引值，可选
+ lastIndexOf()从后往前

**5.2.8迭代方法**

*每个方法接收两个参数：要在每一项上运行的函数和（可选的）运行该函数的作用域对象--影响this。传入这些方法的函数会接收三个参数：数组项的索引值、该项在数组中的位置、数组对象本身*


+ every() :对数组的每一项运行给定函数（以下都是对每一项运行函数，不再赘述），如果函数对每一项都返回true，则返回true
+ filter()：返回该函数会返回true的项组成的数组
+ forEach()：没有返回值
+ map()：返回每次函数调用的结果组成的数组
+ some()：如果任一项返回true，则true

**5.2.9归并方法**

+ reduce()
+ reduceRight()

###5.3Date类型
创建： new Date(),如果传参，传毫秒数

+ Date.parse()根据输入的月日年获得毫秒数，事实上不使用该方法直接创建，其中的字符串也会自动被转换或返回NaN
+ Date.UTC(),参数是年份，基于0的月份，月中的某一天，小时数，分钟，秒，毫秒（）只有年月是必须的

+ 日期格式化方法、日期组建方法P101

###5.4 RegExp






##  第六章
+ map（）：对每一个数组元素遍历
+ reduce()： 有一个可选的第二参数
+ filter（）：迭代一个数组，过滤符合的元素，回调函数返回true的留在数组，
+ sort（）：按大小算，两个参数的差值为正负零来改变位置，负不变，正改变
+ reverse（）：翻转数组
+ concat():把两个数组的内容合并
+ split():按指定分隔符将字符串分割为数组
+ join()：把数组转化成字符串，按指定连接符链接，连接符即为参数
+ **6.2**
 + 组合使用构造函数模式和原型模式P177
 + 动态原型模式（在构造函数中初始化原型）
 + 寄生构造函数模式（避免使用）
 + 稳妥构造函数模式：除了调用方法以外没有其他方式访问数据成员
+ **6.3 继承**
  + 原型链
     + 借用构造函数`call（）`：新实例调用被继承的构造函数，即执行的是初始化代码，更改一个实例的引用类型值并不影响原型，
     + 组合继承 
     + 原型式继承P188
     + 寄生式继承
     + 寄生组合式继承
         + inheritPrototype（） 
  + 确定原型和实例的关系
     + `instanceof` `alert instance instanceof Object /true`因为是Object的实例，返回true
     + `isPrototypeof();` alert(Object.prototype.isPrototypeOf(instance));


## 第七章函数表达式
 
**7.1递归**P177
```
function factorial(num){
  if (num <= 1) {
    return 1；
} else {
   return num* factorial(num-1);}
}
```
是一个递归阶乘函数

+ `arguments.callee`是一个指向正在执行函数的指针，可以用来实现对函数的递归调用
   + `return num * arguments.callee`代替属性名，这样无论如何调用都不出错
   + 严格形式下可以创建命名函数表达式传递给factorial，即使把函数赋值给其他变量，函数名仍然有效，`var factorial = (function f() {});`
 
**7.2闭包**

+ 闭包是有权访问另一个函数作用域中变量的函数
+ 而匿名函数为
```
var a = function(balabala){}
```
这种没有给函数命名的

+ 闭包只能取得包含函数的最后一个值，可以通过匿名函数，在内部包含一个闭包，这样将匿名函数赋值给数组时，创建新的闭包，就可以返回各自的值了
+ 闭包与变量this问题P183
### 7.4私有变量
+ 任何在函数中定义的变量都可以认为是私有变量，因为在函数外部无法访问
+ 私有变量包括函数的参数、局部变量和在内部定义的其他函数
+ 特权方法作为闭包有权访问构造函数中定义的所有变量和函数
+ 静态私有变量P188
+ 模块模式


**this的四种绑定**·

+ 函数中的this总指向调用它的对象
+ fn.call(object)的作用：
1.即刻调用这个函数（fn）
2.调用这个函数的时候函数的this指向object对象
+ fn.apply()
# 第八章BOM

**8.1window对象**

+ 全局变量会变成window对象的属性
+ 但全局变量不能通过delete操作符删除，而直接在window对象上定义的属性可以`window.color`
+ 尝试访问未声明的变量`var newValue = oldValue`会抛出错误,但通过查询window对象，可以知道某个未声明的变量是否存在`var newValue = window.oldValue//undefined`
+  窗口位置
   + screenLeft
   + screenTop
   + moveTo():接收xy坐标值
   + moveBy()：接收在水平和垂直方向上移动的像素数
   + 这两种方法只能对最外层的window对象使用，不适用于框架
   + innerWidth
   + innerHeight
   + outWidth
   + outHeight
   + 在chorome中四个都返回相同值，即视口而非浏览器窗口大小
   + document.documentElement.clientWidth
   + document.documentElement.clientHeight
      + 都是用来取得页面视口大小的
   + resizeTo()
   + resizeBy()
+ 
   + window.open()可以导航到一个特定的URL，也可以打开一个新的浏览器窗口、
   + close()适用于通过window.open()打开的弹出窗口
   + setTimeout()
   + clearTimeout()
   + setInterval()
   + clearInterval()
   + alert()
   + confirm()
   + prompt()
   + print()
   + find()
   
+ location对象
   +  location.search
   +  location.assign = window.location = location.href
   +  location的其他属性P209
   +  replace()


+ navigator对象
   + P210       
   + 检测插件P211  
   + 注册处理程序P213
   

+ screen对象
    + P214
    

+ history 对象
    + history.go()
    + history.back()
    + history.forward()
    + history.length
                          

#第九章 客户端检测

+ 能力检测（最优先）
    + `typeof object.sort = "function"   `
    + hasHostMethod()
    
+ 怪癖（bug）检测
    
+ 用户代理检测
    
     + 识别呈现引擎
     + 识别浏览器
     + 识别平台
     + 识别windows操作系统              
     + 识别移动设备
     + 识别游戏系统
     + 完整的代码P242    
     

#第十章 DOM


+ 节点层次 
   + Node类型
      + nodeType
      + nodeName ->元素的标签名
      + nodeValue ->返回null
      + childNodes
          + 用方括号`someNode.childNodes[0]`
          + `someNode.childNodes.item(0)`
          
      + parentNode
      + previousSibling
      + nextSibling
      + ownerDocument     
      + appendChild() ->向childNodes列表的末尾添加一个节点
      + insertBefore()P252->放在特定位置
      + replaceChild()
      + removeChild()
      + cloneNode()
      + normalize()->处理文档中的文本节点P253
   + Document类型
      + document.documentElement->对html的访问
      + document.body
      + document.title ->修改title属性的值不会改变<title>元素
      + document.URL
      + document.domain
      + document.referrerP255
      + getElementById()
      + getElementByTagName()
      + namedItem()
      + getElementByName()
      + 其他P258
      + 一致性检测P259
      + write()
      + writeln()
      + open()
      + close()
      
  + Element
     + getAttribute() ->一般不使用，只用于取得自定义特性值
     + setAttribute()
     + removeAttribute()
     + getNamedItem(name)
     + removeNameItem(name)
     + setNamedItem(node)
     + item(pos) 
     + createElement()
     + getElementByTagName()
     
  + Text
     + document.createTextNode()
     + splitText()P273
     
  + Comment
  + CDATASection
  + DocumentType
  + DocumentFragment
  + Attr
    

+ DOM操作技术
   + 操作表格P281


# 十一章DOM拓展

+ 选择符API
  + querySelector()-> 接受一个CSS选择符
  + querySelectorAll()
  + matchesSelector()
  
+ 元素遍历
  + P288
  
+ HTML5
   + getElementsByClassName()          
   + classList属性
      + add()
      + contains()
      + remove()
      + toggle()P291
   + document.activeElement 
   + focus()
   + document.hasFocus()
   + HTMLDocument的变化p292
        + readyState
        + compatMode
        + head
   + charset
   + dataset
   + 
      + innerHTMLP295     
      + outerHTML替换调用其的元素及子元素
      + insertAdjacentHTML()P297
   +   scrollIntoView()
+ 专有拓展
   + P299
   + documentMode
   + children
   + contains()->检测是否为后代节点//true//false
   + innerText
   + textContent
   + outerText
   + 滚动P303
      + scrollIntoViewIfNeeded(alignCenter)
      + scrollByLines(lineCount)
      + scrollByPages(pageCount)   
      +                                                                                                                                    
