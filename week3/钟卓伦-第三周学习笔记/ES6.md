## ES
### ECMA Script
1. 它是一种由ECMA组织（前身为欧洲计算机制造商协会）制定和发布的脚本语言规范

2. 而我们学的JavaScript是ECMA的实现, 但术语ECMAScript和JavaScript平时表达同一个意思

3. JS包含三个部分：

	1). ECMAScript（核心）

	2). 浏览器端扩展

		1). DOM（文档对象模型）

		2). BOM（浏览器对象模型）

	3). 服务器端扩展

		1). Node

4. ES的几个重要版本

	ES5 : 09年发布

	ES6(ES2015) : 15年发布, 也称为ECMA2015

	ES7(ES2016) : 16年发布, 也称为ECMA2016  (变化不大)

5. 扩展学习参考:

	1). ES5 : 

		http://www.zhangxinxu.com/wordpress/2012/01/introducing-ecmascript-5-1/

		http://www.ibm.com/developerworks/cn/web/wa-ecma262/

	2). ES6

		http://es6.ruanyifeng.com/

	3). ES7

		http://www.w3ctech.com/topic/1614
### ES5

* * *

* <u>**浏览器对ES5的支持:**</u>

1. IE8只支持defineProperty、getOwnPropertyDescriptor的部分特性和JSON的新特性

2. IE9不支持严格模式, 其它都可以

3. IE10和其他主流浏览器都支持了

4. PC端开发需要注意IE9以下的兼容, 但移动端开发时不需要

* * *

* <u>**严格模式**</u>
1. 理解:

	- 除了正常运行模式(混杂模式)，ES5添加了第二种运行模式："严格模式"（strict mode）。

   - 顾名思义，这种模式使得Javascript在更严格的语法条件下运行

2.  目的/作用

	- 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为

	- 消除代码运行的一些不安全之处，保证代码运行的安全

	- 为未来新版本的Javascript做好铺垫

3. 使用

    - 在全局或函数的第一条语句定义为: 'use strict';

    - 如果浏览器不支持, 只解析为一条简单的语句, 没有任何副作用

4. 语法和行为改变

	- 必须用var声明变量

	- 创建eval作用域

	- 禁止this指向window

	- 对象不能有重名的属性

	- 函数不能有重名的形参

5. 学习参考:

	http://www.ruanyifeng.com/blog/2013/01/javascript_strict_mode.html

* * *

* <u>**SON对象**</u>
1. JSON.stringify(obj/arr)

    js对象(数组)转换为json对象(数组)

2. JSON.parse(json)

    json对象(数组)转换为js对象(数组)

* * *

* <u>**Object扩展**</u>
ES5给Object扩展了好一些静态方法, 常用的3个:

1. Object.create(prototype[, descriptors]) : 创建一个新的对象

    1). 以指定对象为原型创建新的对象

    2). 指定新的属性, 并对属性进行描述

        value : 指定值

        writable : 标识当前属性值是否是可修改的, 默认为true

        get : 用来得到当前属性值的回调函数

        set : 用来监视当前属性值变化的回调函数

2. Object.defineProperties(object, descriptors) : 为指定对象定义扩展多个属性

* * *

* <u>**Array扩展**</u>
  * ES5给数组对象添加了一些方法, 常用的5个:

1. Array.prototype.indexOf(value) : 得到值在数组中的第一个下标

2. Array.prototype.lastIndexOf(value) : 得到值在数组中的最后一个下标

3. Array.prototype.forEach(function(item, index){}) : 遍历数组

4. Array.prototype.map(function(item, index){ }) : 遍历数组返回一个新的数组

5. Array.prototype.filter(function(item, index){ }) : 遍历过滤出一个新的子数组

* * *

* <u>**Function扩展**</u>
1. Function.prototype.bind(obj) :
    将函数内的this绑定为obj, 并将函数返回，不会立即执行函数
2. Function.prototype.call(obj,a,b,..) :
    将函数内的this绑定为obj, 直接从第二个参数开始，依次传入，同时会执行函数
3. Function.prototype.apply(obj，arr) :
    将函数内的this绑定为obj, 第二个参数必须是数组，参数的传入放在数组中，同时会执行函数

---

### ES6
1. ES6增加了些什么?

	1). 新的关键字: let, const, class...

	2). 语法糖(简洁/强大的语法): 如解构赋值, 箭头函数, 对象表达增强... 

	3). 新的API: Set, Map, Promise...

2. 浏览器兼容的问题:

	1). 浏览器对ES6的支持还不是特别好, 不同的浏览器支持的程度也不相同

	2). 测试浏览器对ES6的支持度: http://ruanyf.github.io/es-checker/

	3). 可以使用Babel将ES6编译为ES5: http://babeljs.io/

---




#### 常用


<u>**关键字扩展**</u>
* let关键字
    * 作用: 

	    * 与var类似, 用于声明一个变量

    * 特点:

	    * 在块作用域内有效

	    * 不能重复声明

    	* 不会预处理, 不存在提升

    * 应用:

	    * 循环遍历加监听
* const关键字
    * 作用:
    
        * 定义一个常量
    
    * 特点:
    
        * 不能修改
    
        * 也是块作用域有效
    
    * 应用:
    
        * 保存应用需要的常量数据

* * *

<u>**变量的解构赋值**</u>
* 理解: 

	* 从数组或对象中提取值, 对多个变量进行赋值

* 数组的解构赋值

	let [a,b] = [1, 'atguigu'];

* 对象的解构赋值

	let {n, a} = {n:'tom', a:12}


* 用途

	* 交换2个变量的值

	* 从函数返回多个值

* * *

<u>**模板字符串**</u>
1. 模板字符串 : 简化字符串的拼接

    1). 模板字符串必须用``

    2). 变化的部分使用${xxx}定义

* * *

**<u>对象增强表达</u>**
* 简化的对象写法

    * 省略同名的属性值
    
    * 省略方法的function
    
    * 例如:
    
      let x = 1;
    
      let y = 2;
    
      let point = {
    
        x,
    
        y,
    
        setX (x) {this.x = x}
    
      };

* * *


<u>**函数扩展**</u>
1. 箭头函数

	var fun = function (v) {

    	return v+3;

	}

	var fun2 = v => v+3;
* 作用：定义匿名函数
* 基本语法
    * 没有参数：（）=> console.log('xxx')（左边括号不可以省略）
    * 一个参数：i => i+2（左边括号可以省略）
    * 大于一个参数：（i，j）=> i+j（左边括号不可以省略）
    * 函数体不用大括号：默认返回结果
    * 函数体如果有多个语句，需要用{}包围，若有需要返回的内容，需要手动返回
* 使用场景：多用来定义回调函数 
* 箭头函数的特点：
    1.  简洁
    2.  箭头函数没有自己的this，箭头函数的this不是调用的时候决定的，而是在定义的时候处在的对象就是它的this
    3.  扩展理解：箭头函数的this看外层的是否有函数，如果有，外层函数的this就是内部箭头函数的this；如果没有，则this是window

2. 形参的默认值

	function Point(x = 1,y = 2) {

        this.x = x;

        this.y = y;

    }

3. rest(可变)参数

	function add(... values) {

        let sum = 0;

        for(value of values) {

            sum += value;

        }

        return sum;

    }

4. 扩展运算符(...)

	var arr1 = [1,3,5];

	var arr2 = [2,...arr1,6];

	arr2.push(...arr1);

* * *

<u>**class类**</u>
1. 通过class定义类

2. 在类中通过constructor定义构造方法

3. 通过new来创建类的实例

4. 通过extends来实现类的继承

5. 通过super调用父类的构造方法


![cd4f573f8f4540813c66835602f9bb5d.png](evernotecid://CEB7F35F-CF96-4521-B417-9D3060DC64F6/appyinxiangcom/25551795/ENResource/p2)
![32c0cf71b74384b5cbcc07098aa8b952.png](evernotecid://CEB7F35F-CF96-4521-B417-9D3060DC64F6/appyinxiangcom/25551795/ENResource/p1)

* * *

<u>**Promise对象**</u>
1. 理解:

  * Promise对象: 代表了未来某个将要发生的事件(通常是一个异步操作)

  * 有了promise对象, 可以将异步操作以同步的流程表达出来, 避免了层层嵌套的回调函数(俗称'回调地狱')

  * ES6的Promise是一个构造函数, 用来生成promise实例

2. 使用promise基本步骤(2步):

  * 创建promise对象

    let promise = new Promise((resolve, reject) => {

      //执行异步操作

      if(异步操作成功) {

        resolve(value);

      } else {

        reject(errMsg);

      }

    })

  * 调用promise的then()

    promise.then(function(

      result => console.log(result),

      errorMsg => alert(errorMsg)

    ))

3. promise对象的3个状态

  * pending: 初始化状态

  * fullfilled: 成功状态

  * rejected: 失败状态

4. 应用:

  * 使用promise实现超时处理

  * 使用promise封装处理ajax请求

    let request = new XMLHttpRequest();

    request.onreadystatechange = function () {

    }

    request.responseType = 'json';

    request.open("GET", url);

    request.send();
![36d704063d48ea965234cc9672675522.png](evernotecid://CEB7F35F-CF96-4521-B417-9D3060DC64F6/appyinxiangcom/25551795/ENResource/p3)

* * *

<u>**symbol**</u>
* 前言：ES5中对象的属性名都是字符串，容易造成重名，污染环境
* symbol：
    * 概念：ES6中添加了一种原始数据类型symbol（已有的原始数据类型有：String,Number,Boolean,undefined,null）
    * 特点：
        1. symbol属性对应的值是唯一的，解决命名冲突问题
        2. symbol值不能与其他数据进行计算，包括同字符串拼串
        3. for in，for of遍历时不会遍历symbol属性
    * 使用：
        1. 调用symbol函数得到symbol值
            let symbol = Symbol();
            let obj = {};
            obj[symbol] = 'hello';
        2. 传参标识
            let symbol = Symbol('one');
            let symbol2 = Symbol('two');
            console.log(symbol);//Symbol('one')
            console.log(symbol2);//Symbol('two')
        3. 内置Symbol值
            * 除了定义自己使用的symbol值以外，ES6还提供了11个内置的symbol值，指向语言内部使用的方法
            - Symbol.iterator属性，指向该对象的默认遍历器方法
          

* * *


<u>**iterator遍历器**</u>
* 概念：iterator是一种接口机制，为各种不同的数据结构提供统一的访问机制
* 作用：
    1. 为各种数据结构提供一个统一的、简便的访问接口
    2. 使得数据结构的成员能够按某种次序排列
    3. ES6创造了一种新的遍历命令for...of循环，iterator接口主要供for...of消费
* 工作原理
  * 创建一个指针对象（遍历器对象），指向数据结构的起始位置
  * 第一次调用next方法，指针会自动指向数据结构的第一个成员
  * 接下来不断调用next方法，指针会一直往后移动，直到指向最后一个成员
  * 每调用next方法返回的是一个包含value和done的对象,{value: 当前成员的值，done：布尔值}
    * value表示当前成员的值，done对应的布尔值表示当前的数据结构是否遍历结束
    * 当遍历结束的时候返回的value值是undefined，done值为false
* 原生具备iterator接口的数据（可用for of遍历）
    * 扩展理解
    1. 当数据结构上部署了Symbol.iterator接口，该数据就是可以利用for of遍历
    2. 当使用for of去遍历目标数据的时候，该数据会自动去找Symbol.iterator属性
* 数据结构部署了Symbol.iterator接口的有：
    1. Array
    2. arguments
    3. set容器
    4. map容器
    5. String
    ![19e992f8b0d5d532de96367a33292970.png](evernotecid://CEB7F35F-CF96-4521-B417-9D3060DC64F6/appyinxiangcom/25551795/ENResource/p4)
    
    ![5800e21c44ecc4cb8a2063d87e89462f.png](evernotecid://CEB7F35F-CF96-4521-B417-9D3060DC64F6/appyinxiangcom/25551795/ENResource/p5)
* * *
<u>**Generator函数**</u>
* 概念：
    1. ES6提供的解决异步编程的方案之一
    2. Generator函数是一个状态机，内部封装了不同的数据
    3. 用来生成遍历器对象
    4. 可暂停函数（惰性求值），yield可暂停，next方法可启动。每次返回的使用yield后的表达式结果
* 特点：
    1. function与函数名之间有一个星号
    2. 内部用yield表达式来定义不同的状态
    例如：
    function* generatorExample(){
        let result = yield 'hello'; //状态值为hello
        yield 'gennerator'; //状态值为generator
    }
    3. generator函数返回的是指针对象，而不会执行函数内部逻辑
    4. 调用next方法函数内部逻辑开始执行，遇到yield表达式停止，返回{value:yield后的表达式结果/undefined，done} 
    5. 再次调用next方法会从上一次停止的yield处开始,直到最后
    6. yield语句返回结果推迟为undefined，当调用next方法时，传参内容会作为启动时yield语句的返回值
![045c7641d9eda6b7a7881245a987e112.png](evernotecid://CEB7F35F-CF96-4521-B417-9D3060DC64F6/appyinxiangcom/25551795/ENResource/p6)
![12f5c054e2105b9f6af0e3612790be12.png](evernotecid://CEB7F35F-CF96-4521-B417-9D3060DC64F6/appyinxiangcom/25551795/ENResource/p7)


* * *
#### 其他

* <u>**字符串扩展**</u>

1. includes(str) : 判断是否包含指定的字符串

2. startsWith(str) : 判断是否以指定字符串开头

3. endsWith(str) : 判断是否以指定字符串结尾

4. repeat(count) : 重复指定次数

* * *

* **<u>数值扩展</u>**
1. 二进制与八进制数值表示法: 二进制用0b, 八进制用0o

2. Number.isFinite(i) : 判断是否是有限大的数

3. Number.isNaN(i) : 判断是否是NaN

4. Number.isInteger(i) : 判断是否是整数

5. Number.parseInt(str) : 将字符串转换为对应的数值

6. Math.trunc(i) : 直接去除小数部分

* * *

* <u>**数组扩展**</u>
1. Array.from(v) : 

	将伪数组对象或可遍历对象转换为真数组

2. Array.of(v1, v2, v3) : 

	将一系列值转换成数组

3. find(function(value, index, arr){return true}) : 

	找出第一个满足条件返回true的元素

4. findIndex(function(value, index, arr){return true}) : 

	找出第一个满足条件返回true的元素下标

5. keys() : 

	返回包含所有下标的可迭代对象

6. values() : 

	返回包含所有值的可迭代对象

7. entries() : 

	返回包含所有下标和值的可迭代对象
  

* * *


* <u>**对象扩展**</u>
1. Object.is(v1, v2) 

	判断2个数据是否完全相等
![584f8797f6dd92878e05fa9193165992.png](evernotecid://CEB7F35F-CF96-4521-B417-9D3060DC64F6/appyinxiangcom/25551795/ENResource/p9)

2. Object.assign(target, source1, source2..) 

	将源对象的属性复制到目标对象上

3. 显式操作__proto__属性

	var obj2 = {};

   obj2.__proto__ = obj1;
  

* * *


* <u>**克隆函数**</u>
* 拷贝数据：
    * 基本数据类型：
	    * 拷贝后会生成一份新的数据，修改拷贝以后的数据不会影响原来的数据
	* 对象/数组：
	     * 拷贝后不会生成新的数据，而是拷贝引用。修改拷贝以后的数据会影响原来的数据
* 拷贝数据的方法：
     1. 直接赋值给一个变量 // 浅拷贝
     2. Object.assign() // 浅拷贝
     3. Array.prototype.concat() // 浅拷贝
     4. Array.prototype.slice() // 浅拷贝
     5. JSON.parse(JSON.stringfy()) // 深拷贝（深度克隆），但是拷贝的数据里不能有函数，因为处理不了
* 浅拷贝（对象/数组）：
     * 特点：拷贝的引用，修改拷贝以后的数据，会影响原数据
* 深拷贝（深度克隆）：
     * 特点：拷贝的时候生成新数据，修改拷贝以后的数据不会影响原数据
* 知识储备
    * 如何判断数据类型：arr--->Array null--->Null
	    1. typeof 返回的数据类型：String, Number, Boolean, Undefined, Object, Function
	    2. Object.prototype.toString.call(obj)
![20b9da868f83f0ec2a5511f416da59b4.png](evernotecid://CEB7F35F-CF96-4521-B417-9D3060DC64F6/appyinxiangcom/25551795/ENResource/p10)
![7342782457110bf8f3a3469127d8dd63.png](evernotecid://CEB7F35F-CF96-4521-B417-9D3060DC64F6/appyinxiangcom/25551795/ENResource/p11)
```
// 检测目标数据类型
function checkedType(target) {
				return Object.prototype.toString.call(target).slice(8, -1);
			}
        // 深度克隆函数
        function clone(target) {
            let result, targetType = checkedType(target);
            if (targetType === 'Object') {
                result = {};
            } else if (targetType === 'Array') {
                result = [];
            } else {
                return target;
            }
            for(let i in target) {
                let value =target[i];
                if (checkedType(value) === 'Object' || checkedType(value) === 'Array') {
                    result[i] = clone(value);
                } else {
                    result[i] = value
                }
            }
            return result;
        }
```

* * *

* <u>**Set和Map数据结构**</u>
1. Set容器 : 无序不可重复的多个value的集合体
    1). Set()

    2). Set(array)

    3). add(value)

    4). delete(value)

    5). has(value)

    6). clear()

    7). size
![12cde2a9db718acf4ec61f705a399801.png](evernotecid://CEB7F35F-CF96-4521-B417-9D3060DC64F6/appyinxiangcom/25551795/ENResource/p14)

2. Map容器 : 无序key不重复的多个key-value的集合体

     1). Map()

     2). Map(array)

     3). set(key, value)

     4). get(key)

     5). delete(key)

     6). has(key)

     7). clear()

     8). size
    ![b51eaea2ae76757b08b6165f9873e09f.png](evernotecid://CEB7F35F-CF96-4521-B417-9D3060DC64F6/appyinxiangcom/25551795/ENResource/p12)
    

* * *


* <u>**for...of循环**</u>
1. 遍历数组

2. 遍历Set

3. 遍历Map

4. 遍历字符串

5. 遍历伪数组
### ES7
* 运算符扩展
    * 指数运算符: **
* 数组的扩展
    * Array.prototype.includes(value) : 判断数组中是否包含指定value
* async异步函数(源自ES2017)
	* 概念：真正意义上去解决异步回调的问题，同步流程表达异步操作
	* 本质：generator的语法糖
	* 语法：
>	  async function foo() {
>		  await 异步操作；
>		  await 异步操作；
>	  }
	* 特点：
	  1. 不需要像generator去调用next方法，遇到await等待，当前的异步操作完成就往下执行
	  2. 返回的总是promise对象，可以用then方法进行下一步操作
	  3. async取代generator函数的星号*，await取代generator的yield
	  4. 语义上更为明确，使用简单，经验证，暂时没有任何副作用及不良反应 
