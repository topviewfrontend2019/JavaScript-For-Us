## jQuery原理

### 构造函数

- jQuery（）
- $() ------》这是jQuery的别名

### jQuery实例属性

- length，返回jQuery对象中匹配元素的个数
- jQuery当前版本库号
- 下标（索引）：dom 结点

### jQuery代码延迟

- jQuery（document).ready(fn)
  - 此方法传入一个匿名函数
  - 页面渲染完成时执行，代替window.onload
  - 简写方法：jQuery（function（$）{}）

### 注意

- ​	编写jQuery代码只需要两部=步
  - 选择元素
  - 操作元素

- jQuery和$都可以实现选择器的功能，但是为了避免和其他库的冲突建议使用jQuery

- 若要使用$可以用匿名函数模拟块级作用域

  ```javascript
  (function($){
      $(function(){
          let obj = $('.box');
          console.log(obj);
      })
  })(jQuery)
  ```

### 加载模式

#### 原生加载模式

- 等到dom元素加载完毕并且图片也加载完毕才会执行
- 原生js如果写了多个入口函数，后写的会覆盖前面写的

#### jQuery加载模式

- jQuery会等到dom元素加载完毕但不会等到图片也加载完毕
- jQuery中后写的入口函数**不会覆盖先写的函数**

### jQuery入口函数的其他写法

#### 复杂写法

```javascript
$(document).ready(function() {
    // alert("hello world")
});
```

#### 第二种写法

```javascript
jQuery(document).ready(function(){
    alert("hello world")
})
```

#### 第三种写法（推荐）

```javascript
$(function(){ })
```

#### 第四种写法

```javascript
jQuery(function(){})
```

#### 安全写法

- ```javascript
  jQuery(function($){
  	//可以安全的使用$符号啦
  })
  ```

  

### 解决冲突的方法

#### 1.释放$使用权

- ```javascript
  //注意释放操作要在前面
  jQuery.noConflict();//该语句会释放$符号的使用权
  jQuery(function() {
      //代码
  });
  ```

#### 2自定义符号

- ```javascript
  var nj = jQuery.noConflict(); //将$释放，并且将$变为nj
  ```

## jQuery核心函数

### $()

- 可以接受一个函数

- 可以接收一个字符串

  - 字符串选择器（返回一个jQuery对象，对象中保存着**所有**符合该选择器的对象（jquery对象是一个**伪数组**））

  - 接收一个代码片段 （返回一个jQuery对象，保存着创建的dom对象）

    ```javascript
    //可以根据代码片段创建dom结构
     $(function() {
                var $p = $("<p>我是一个文段</p>");//f返回的是一个数组
                console.log($p);
                document.body.append($p[0]);//在body中添加一个p元素
            })
    ```

    

- 接收一个Dom元素 
  
  - 会包装成jQuery对象返回给我们 

## jq静态方法和实例方法

### 步骤

- 定义一个类
- 给这个类添加一个实例方法
- 调用实例方法

## jQuery方法

### jQuery.each()

- 在原生js中arr.forEach(value,index) ，（注意该方法只可以遍历数组）

- each(arr,function(index,value ))传入一个数组及回调函数

  - ```javascript
       var arr = [3,5,6,2,8];
                $.each(arr,function(index,value){
                    console.log(index,value);
                })
    //遍历数组中发原生并且打印
    ```

  - 该方法可以遍历伪数组（如对象）

    ```javascript
     var obj = {"ling":1,"yi":2,"er":3}
     $.each(obj,function(index,value) {
                    console.log(index,value);
                })//打印的结果为键与值
    ```

### jQuery的map方法

#### 原生

- ```javascript
  //第一个参数当前被遍历到的元素的值，第二个参数是当前元素的索引，第三个参数为当前被遍历的数组
  //无法遍历伪数组
  var arr = [1,3,5,7,9]
  arr.map(function(value,index,array)) {
  	console.log(index,value,array);
  }
  ```

#### jq中的map方法

- 即可以遍历数组也可以遍历伪数组

  

#### map和each的区别

- each（）方法的返回值是，遍历谁返回谁，each方法不支持对函数的修改
- map（）方法默认返回一个空数组，在函数里面加return可以返回处理过后的**新数组**

### jq的trim（）方法

- $.trim(string)
- 去除字符串前后的空格，并返回的是一个新的数组

### isWindow方法

- 检查传进的对象是不是window，返回值是true或者false

### isArray方法

- 判断传入的对象是不是真数组

### isFunction方法

- 判断传入对象是不是函数

## 选择器

### 使用方法

- $("选择器") ---》返回的是一个jQuery对象，那么就可以调用jQuery对象上的方法
