# 01-What is jQuery？
+ find： 
```
jQuery("h1");
$("h1");
$("h1").text();
```
```
jQuery(document).ready(function(){
   <code>
});//等到ready再执行
```

# 02-Using jQuery
# 03-Searching the DOM
```
$("#destinations li");//找出ID为destinations下面的li
$("#destinations > li")//找出直属子元素li
$(".class, #id");//可以选择多个元素，用逗号隔开
$("#destinations li: first");//选中第一个
$("#destinations li:last");//最后一个
$("#destinations li: odd");//只选索引值为奇数
:even//偶数
```
# 04-Traversing the DOM遍历
```
$("#destinations").find("li");
$("#destinations").first();
$("#destinations").last();
$("li").first().next();
.prev()//上一个
$("li").first().parent();//找到父元素
$("#destinations").children();//找到直系子元素
```
# 05-Manipulating the DOM
```
$(document).ready(function(){
   var price = $('<p>From $399.99</p>');
   $('.vacation').append(price);//把段落节点添加到vacation的子元素最后
});
```
方法名：
+ remove()
```
price.remove();
```
+ before()前面的节点
+ after()后面的节点
+ prepend() 添加到第一个子节点
+ append() 最后一个子节点
+ appendTo（）
+ prependTo()
+ insertAfter()
+ insertBefore()//只是参考点放在后面
```
price.appendTo($(".vacation"));
```

# 06-Acting on Interaction
.on();
```
$('button').on("click", funtion{

});

```
```
$("button").on("click", "button1", function(){

});//事件委托监听button1上的点击事件
```

# 07-Refactor using Traversing
   ```
$(this).closest('.vacation').append(price);//遍历DOM来找到类为vacation的父节点并添加price
$(this).remove();
```
+ closest() 只会查找0或1个父节点，最邻近的
+ parents()会查找所有父节点

# 08-Traversing and Filtering
 ```
$(".vacation").filter(".onsale")//找到vacation类，然后筛选含有onsale类的
addClass();
```

# 09-On DOM Load
 + .slidedown()显示
+ .slideup()隐藏
+ .slideToggle()

# 10-Expanding on on（）监听
+ click
+ focusin
+ mousedown
+ mousemove 
+ mouseover
+ mouseenter
+ dblclick
+ focusout
+ mouseup
+ mouseout
+ mouseleave

# 11-Keyboard Events
1.
+ keypress
+ keydown
+ keyup

2.
+ blur 
+ select
+ change 
+ focus
+ submit

```
$(document).ready(function() {
  $(".vacation").on("keyup", ".quantity", function() {
     var price = +$(this).closest(".vacation").data("price");//+号将字符串变成数值
    var quantity = +$(this).val();
    $("total").text(price *quantity);
});
});
```

# 12-LINK LAYOVER
+ 淡入显示`.fadeIn()`
+ `.fadeOut()`
+ `.fadeToggle()`
+ `.stopPropagation()`阻止冒泡
+ `.preventDefault()`阻止默认行为

# 13-Taming CSS
+ css(<attr>, <value>)
```
$(this).css("background-color", "black");

$(this).css("background-color", "green")
          .css("border-color", "black");

```
+ css(<object>)
```
$(this).css({"background-color": "black",
                   "border-color: "black"});

```
+ `.show()`
+ `.hide()`
+ addClass()
+ removeClass()
+ toggleClass()
+ 可以将样式储存在css的一个类中，在js中调用这个类即可

# 14-Animation
+ `.animate(<object>,"fast")`第二个参数可以没有，可以设置成数值
+ `.hasClass()

# JQuery
##方法
 + .addClass()
 + .removeClass()
 + .class()
+ .prop()
+ .html()
+ .remove()
+ appendTo()
+ clone()
+ parent()
+ childen()
+ jQuery 用CSS选择器来选取元素，`target:nth-child(n)` CSS选择器允许你按照索引顺序**(从1开始)**选择目标元素的所有子元素。
+ 示例：获取class为target且索引为奇数的所有元素，并给他们添加class。
```
$(".target:odd").addClass("animated shake");
```
偶数：`：even`
记住，jQuery里的索引是从0开始的，也就是说：:odd 选择第2、4、6个元素，因为target#2(索引为1)，target#4(索引为3)，target6(索引为5。


-------------------
## 入口函数的写法
```
$(function(){
});
```
>`jQuery.noConflict();`释放$的使用权->解决冲突
`var nj = jQuery.noConflict()`
------------------
## 06-核心函数
>`$();`就代表调用jQ的核心函数
     
+ 接收函数
+ 接收字符串选择器
+ 接收字符串代码片段
+ 接收DOM元素

----------------
## 07-对象
伪数组

## 08-静态方法和实例方法
 + 静态方法直接添加给类
 + 实例方法赋给原型，创建新的实例来获得balabala

## 09-静态方法each方法
 `arr.forEach(function(value, index) {})`原生方法,不能遍历伪数组
  `$.each(arr, function(index, value){})`注意索引和值的顺序，可以遍历伪数组

## 10-静态方法map方法
`arr.map(function(value, index, array){})`原生，第三个是当前被遍历的数组
`$.map(arr, function(value, index){})`\
>> each静态方法默认返回值是被遍历的数组,不支持在回调函数中对遍历的数组进行处理
>> >map返回空数组,可以在回调函数中通过return对遍历的数组进行处理，生成新的数组返回

## 11-其他静态方法
1.  $.trim();  ->
> 去除字符串两端的空格
> >>参数是字符串
> >>>返回去除之后的字符串

2. $.isWindow();
>>判断传入的对象是否是window对象，返回true/false

3. $.isArray();判断是否是真数组
4. $.isFunction();

## 12-静态方法holdReady方法

`$.holdReady(true)`暂停入口函数的执行

false则恢复执行

## 14-内容选择器
+ :contains(text) ->找到包含指定文本内容的指定元素
+ :has(selector) -> 找到包含指定子元素的指定元素
+ :parent ->找到有文本内容或者有子元素的
+ :empty ->找到内容为空且没有子元素的`div:empty`

## 15-属性和属性节点
1. 什么是属性
2. 如何操作属性
3. 什么是属性节点
4. 如何操作属性节点
5. 属性和属性节点有什么区别
