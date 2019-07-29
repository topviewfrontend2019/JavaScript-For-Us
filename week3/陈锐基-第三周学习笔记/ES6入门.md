# ES6(ES2015)

## 一、兼容性和新特性

IE10+、Chrome、FireFox、移动端、NodeJS

1. 在线转换 （引入browser.js == babel）
2. 提前编译

------------------------------------------------------------------

ES6新特性：

1. 变量
2. 函数
3. 数组
4. 字符串
5. 面向对象
6. Promise 
7. generator
8. 模块化

## 二、变量let和const

### var         

1. 可以重复声明

2. 无法限制修改

3. 没有块级作用域

   ```javascript
   for(var  i = 0; i<btn.length; i++){
       btn[i].onclick = function(){
           alert(i); 
       }
   }
   // 3,3,3
   ```

### let

1. 不可以重复声明

2. 变量——可以修改

3. 有块级作用域 

   ```javascript
   for(let i = 0; i<btn.length; i++){
       btn[i].onclick = function(){
           alert(i); 
       }
   }
   // 0,1,2
   ```

### const

1. 不可以重复声明
2. 常量——不能修改
3. 有块级作用域

## 三、箭头函数

```javascript
function show(){
}
let show=()=>{
}
// 去function 加箭头
function(){
}
()=>{ 
}
```

1. 如果**只有**一个参数，()可以省略
2. 如果**只有**一个return，{}可以省

## 四、函数参数

### 1. 参数扩展/展开

1. 收集剩余的参数 (a,b, ...args)，Rest Parameter 必须作为最后一个参数

2. 展开一个数组   （...数组名） 

   ```javascript
   let arr1 = [1,2,3];
   let arr2 = [5,6,7];
   let arr = [...arr1, ...arr2]; // 1,2,3,5,6,7
   // 展开后的效果，跟直接把数组的内容写在这的效果一样
   
   let a;
   let arr = [1,2,3];
   a=...arr;  // error!!!!!
   ```

### 2. 默认参数

```javascript
function show(a, b=5, c=12) {
    console.log(a, b, c);
}
show(99); // 99,5,12
show(99,19,88); // 99,19,88
```

## 五、解构赋值

1. 左右两边结构必须一样
2. 右边必须是个东西
3. 声明和赋值不能分开 （必须在一句话里完成，不能先声明后在别的行赋值）

```javascript
let [a,b,c]=[1,2,3];
console.log(a, b, c); // 1,2,3
let {a,b,c}={a:12, b:5, c:8};
console.log(a, b, c); // 12,5,8

let [{a, b}, [n1, n2, n3], num ,str]=[{a: 12, b: 5}, [12, 5, 8], 8, '123'];
console.log(a,b,n1,n2,n3,num,str);
let [obj, arr, num ,str]=[{a: 12, b: 5}, [12, 5, 8], 8, '123'];
console.log(obj, arr, num, str); 
```

## 六、数组

1. map  映射 (一对一)

   ```javascript
   let arr=[12, 5, 8];
   let result=arr.map(function (item){
       return item*2;
   });
   let result=arr.map(item=>item*2);
   console.log(result); // 24,10,16
   
   let score = [10,99];
   let result = score.map(item=>item >= 60 ? '及格' : '不及格');
   // 不及格，及格
   ```

2. reduce 汇总 （一堆出来一个）

3. filter 过滤器

   ```javascript
   let arr = [12,11,5];
   let result = arr.filter(item=>{
       if(item % 3 == 0){
           return true;
       } else {
           return false;
       }
   }); 
   let result = arr.filter(item=>item%3==0); // 简化后
   console.log(result); // 12
   ```

4. forEach 循环（迭代）

## 七、字符串

1. 多了两个新方法

   ```javascript
   字符串1.startsWith('字符串2')：字符串1是否是以字符串2开头的
   字符串1.endsWith('字符串2')：字符串1是否是以字符串2结束的
   ```

2. 字符串模板

   1) 可以把东西塞到字符串里面    ${东西} 

   2) 可以拆行

## 八、ES6的面向对象

1. class 关键字

   ```javascript
   class User{
       constructor(name, pass){
           this.name = name;
           this.pass = pass;
       }
       
       showName(){
           alert(this.name);
       }
       showPass(){
           alert(this.pass);
       }
   }
   
   let u1 = new User("blue", '123');
   u1.showName();  // "blue"
   u1.showPass();	// '123'
   ```

   1)  class关键字、构造器和类分开了

   2）class里面直接加方法

   ![1564131690832](C:\Users\53232\AppData\Roaming\Typora\typora-user-images\1564131690832.png)

2. 继承 

   ```javascript
   // ES5 
   function VipUser(name, pass, level){
       User.call(this, name, pass);
       this.level = level;
   }
   VipUser.prototype = new User();
   VipUser.prototype.constructor = VipUser;
   
   VipUser.prototype.showLevel = function(){
       alert(this.level);
   };
   // ES6
   class VipUser extends User {
       constructor(name, pass, level){
           super(name, pass);
           
           this.level = level;
       }
       showLevel(){
           alert(this.level);
       }
   }
   //////
   var v1 = new VipUser("blue","123456",3);
   v1.showName();	// blue
   v1.showPass();  // 123456
   v1.showLevel(); // 3
   
   ```

## 九、面向对象的应用——React

### React

1. 组件化——class
2. 依赖于JSX（JSX == babel == browser.js）

## 十、JSON

1. JSON对象

2. 简写

   1）名值一样留一个也可以

   2）方法（去掉":function"）

## 十一、Promise（用同步方式书写异步代码）

> 异步：操作之间没有关系，同时进行多个操作（代码更复杂 ）
>
> 同步：同时只能做一件事（代码简单）

```javascript
let p = new Promise(function (resolve, reject){
    // 异步代码
    // resolve——成功了
    // reject——失败了
    $.ajax({
        url: 'xxx'
        dataType: 'xxx',
        success(arr){
        	resolve(arr);
    	},
        error(err){
		 	reject(err);
        }
    });
});

p.then(function(){
    // 成功的时候调用
},function(){
    // 失败的时候调用
})
// -------------------------------------------------------------------------------
// 封装一个函数
function createPromise(url){
    return new Promise(function(resolve, reject){
       $.ajax({
            url,
            dataType: 'xxx',
            success(arr){
                resolve(arr);
            },
            error(err){
                reject(err);
            }
    	});     
    });
}
// promise的方法
Promise.all([
    createPromise(url1);
    createPromise(url2);
]).then(function (arr){
    let [res1, res2] = arr;
    // ……
   	// 成功了
}, function(){
  	// 失败了；  
});
// -------------------------------------------------------------------------------
Promise.all([
    $.ajax({xxxxxxx1}),
    $.ajax({xxxxxxx2})
    // ajax返回值有promise
]).then(function(){
    // 成功了
},function(){
   // 失败了 
});
// -------------------------------------------------------------------------------
Promise.all([$.ajax(), $.ajax()]).then(result=>{
    // 成功了
}, err=>{
    // 失败了
});
```

1. Promise.all()
2. Promise.race()

## 十二、generator（生成器）

>普通函数——一路到底
>
>generator函数——中间能停 (踹一脚走一步)

```javascript
function *show(){  // generator 函数加 * 号
    alert('a');
    yield;  // 中断标识
    alert('b');
}

let genObj = show();
genObj.next(); // a 
genObj.next(); // b
// -------------------------------------------------------------------------------
function *函数名(){ 
    代码……
    yield ajax(xxx);  // 等待数据返回
    代码……
}
```

>**yield 传参/返回**

```javascript
// 传参
function *show(){  // generator 函数加 * 号
    let a = yield;  // 中断标识
    alert(a); // 5
}

let genObj = show();
genObj.next(12); // 执行至yield（前半段），没法给yield传参
genObj.next(5);  // 后半段
// -------------------------------------------------------------------------------
function *show(){
    // 代码……
    yield 12; 
    // 代码……
    return 55; 
}
let gen = show();
let res1 = gen.next(); // {value: 12, done: false}
let res2 = gen.next(); // {value: 55, done: true}
```

![1564146060647](C:\Users\53232\AppData\Roaming\Typora\typora-user-images\1564146060647.png)

>异步操作：
>
>1. 回调
>2. Promise
>3. generator
>
>```javascript
>// 回调
>$.ajax({
>   	url:xxx
>    dataType: 'json',
>    success(data1){
>    	// 成功
>        $.ajax({
>            url:xxx
>            dataType: 'json',
>            success(data2){
>			 // 成功
>              // …… 
>            },
>            error(){
>              // 失败
>            }
>    	});
>    },
>    error(){
>      // 失败
>    }
>});
>
>// Promise （适合一次读一堆）
>Promise.all([
>    $.ajax({url: xxx, dataType: 'json'}),
>    $.ajax({url: xxx, dataType: 'json'}),
>    $.ajax({url: xxx, dataType: 'json'})
>]).then(results=>{
>    // 完事儿
>}, err=>{
>    // 错了
>});
>
>// generator （适合逻辑性判断比较多的）
>runner(function *(){
>    let data1 =  $.ajax({url: xxx, dataType: 'json'});
>    let data2 =  $.ajax({url: xxx, dataType: 'json'});
>    let data3 =  $.ajax({url: xxx, dataType: 'json'});
>    // 完事儿
>});
>```
>
>