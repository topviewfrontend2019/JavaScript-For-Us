# jQuery基础
## jQuery和JS入口函数的区别
* 通过原生的JS入口函数可以拿到DOM元素
* 通过原生的JS入口函数可以拿到DOM元素的宽高
* 通过jQuery入口函数可以拿到DOM元素
* 通过jQuery入口函数不可以拿到DOM元素的宽高
* 原生的JS如果编写了多个入口函数,后面编写的会覆盖前面编写的
* jQuery中编写多个入口函数,后面的不会覆盖前面的
* 原生JS和jQuery入口函数的加载模式不同
  * 原生JS会等到DOM元素加载完毕,并且图片也加载完毕才会执行
  * jQuery会等到DOM元素加载完毕,但不会等到图片也加载完毕就会执行
## jQuery入口函数的其它写法
* 第一种写法 <br>
        $(document).ready(function () {<br>
            // alert("hello lnj");<br>
        });
* 第二种写法<br>
        jQuery(document).ready(function () {<br>
            // alert("hello lnj");<br>
        });
* 第三种写法(推荐)<br>
        $(function () {<br>
            // alert("hello lnj");<br>
        });
* 第四种写法<br>
        jQuery(function () {<br>
            alert("hello lnj");<br>
        });
## jQuery冲突问题
* 释放$的使用权
   * 注意点: 释放操作必须在编写其它jQuery代码之前编写
   * 释放之后就不能再使用$,改为使用jQuery
        jQuery.noConflict();
* 自定义一个访问符号<br>
        var nj = jQuery.noConflict();<br>
        nj(function () {<br>
            alert("hello lnj");<br>
        });
## jQuery核心函数
* $();/jQuery();就代表调用jQuery的核心函数

        // 1.接收一个函数
        $(function () {
            alert("hello lnj");
            // 2.接收一个字符串
            // 2.1接收一个字符串选择器
            // 返回一个jQuery对象, 对象中保存了找到的DOM元素
            var $box1 = $(".box1");
            var $box2 = $("#box2");
            // 2.2接收一个字符串代码片段
            // 返回一个jQuery对象, 对象中保存了创建的DOM元素
            var $p = $("<p>我是段落</p>");
            $box1.append($p);
            // 3.接收一个DOM元素
            // 会被包装成一个jQuery对象返回给我们
            var span = document.getElementsByTagName("span")[0];
            var $span = $(span);
        });
## jQuery对象
* 什么是jQuery对象
    * jQuery对象是一个伪数组
* 什么是伪数组?
    * 有0到length-1的属性, 并且有length属性
## 静态方法和实例方法
1. 定义一个类<br>
        function AClass() {
        }
2. 给这个类添加一个静态方法
   * 直接添加给类的就是静态方法<br>
       AClass.staticMethod = function () {
            alert("staticMethod");
        }
    * 静态方法通过类名调用<br>
        AClass.staticMethod();

3. 给这个类添加一个实例方法<br>
        AClass.prototype.instanceMethod = function () {<br>
            alert("instanceMethod");<br>
        }
    * 实例方法通过类的实例调用
    * 创建一个实例(创建一个对象)<br>
        var a = new AClass();
    * 通过实例调用实例方法<br>
        a.instanceMethod();
## 静态方法each（）
        var arr = [1, 3, 5, 7, 9];
        var obj = {0:1, 1:3, 2:5, 3:7, 4:9, length:5};
        // 1.利用原生就算的each静态方法遍历数组
        /*
        第一个参数: 遍历到的元素
        第二个参数: 当前遍历到的索引
        注意点:
        原生的forEach方法只能遍历数组, 不能遍历伪数组
        */
        // arr.forEach(function (value, index) {
        //     console.log(index, value);
        // });
        // obj.forEach(function (value, index) {
        //     console.log(index, value);
        // });

        // 2.利用jQuery的each静态方法遍历数组
        /*
        第一个参数: 当前遍历到的索引
        第二个参数: 遍历到的元素
        注意点:
        jQuery的each方法是可以遍历伪数组的
        */
        // $.each(arr, function (index, value) {
        //     console.log(index, value);
        // });
        $.each(obj, function (index, value) {
            console.log(index, value);
        });
## 静态方法map（）
        var arr = [1, 3, 5, 7, 9];
        var obj = {0:1, 1:3, 2:5, 3:7, 4:9, length:5};
        // 1.利用原生JS的map方法遍历
        /*
        第一个参数: 当前遍历到的元素
        第二个参数: 当前遍历到的索引
        第三个参数: 当前被遍历的数组
        注意点:
        和原生的forEach一样,不能遍历的伪数组
        */
        // arr.map(function (value, index, array) {
        //     console.log(index, value, array);
        // });
        // obj.map(function (value, index, array) {
        //     console.log(index, value, array);
        // });
        // 2.利用jQuery的map方法遍历
        /*
        第一个参数: 要遍历的数组
        第二个参数: 每遍历一个元素之后执行的回调函数
        回调函数的参数:
        第一个参数: 遍历到的元素
        第二个参数: 遍历到的索引
        注意点:
        和jQuery中的each静态方法一样, map静态方法也可以遍历伪数组
        */
        // $.map(arr, function (value, index) {
        //     console.log(index, value);
        // });
## jQuery中的其它静态方法
* $.trim(str);
    * 作用: 去除字符串两端的空格
    * 参数: 需要去除空格的字符串
    * 返回值: 去除空格之后的字符串
* $.isWindow(obj);
    * 作用: 判断传入的对象是否是window对象
    * 返回值: true/false
* $.isArray(obj);
    * 作用: 判断传入的对象是否是真数组
    * 返回值: true/false
* $.isArray(obj);
    * 作用: 判断传入的对象是否是一个函数
    * 返回值: true/false
    * 注意点:jQuery框架本质上是一个函数<br>
        (function( window, undefined ) {
            <br>
         })( window );
* $.holdReady(true); 
    * 作用: 暂停ready执行
    * $.holdReady(true);<br>
        $(document).ready(function () {<br>
            alert("ready");<br>
        });
## jQuery内容选择器
-  :empty 作用:找到既没有文本内容也没有子元素的指定元素
> var $div = $("div:empty");
-  :parent 作用: 找到有文本内容或有子元素的指定元素
> var $div = $("div:parent");
-  :contains(text) 作用: 找到包含指定文本内容的指定元素
> var $div = $("div:contains('我是div')");
-  :has(selector) 作用: 找到包含指定子元素的指定元素
> var $div = $("div:has('span')");
## 属性和属性节点
1. 什么是属性?
    * 对象身上保存的变量就是属性
2. 如何操作属性?
    * 对象.属性名称 = 值;
    * 对象.属性名称;
    * 对象["属性名称"] = 值;
    * 对象["属性名称"];
3. 什么是属性节点?
    * &lt;span name = "it">&lt;/span>
    * 在编写HTML代码时,在HTML标签中添加的属性就是属性节点
    * 在浏览器中找到span这个DOM元素之后, 展开看到的都是属性
    * 在attributes属性中保存的所有内容都是属性节点
4. 如何操作属性节点?
    * DOM元素.setAttribute("属性名称", "值");
    * DOM元素.getAttribute("属性名称");
5. 属性和属性节点有什么区别?
    * 任何对象都有属性, 但是只有DOM对象才有属性节点
## jQuery的attr方法
1. attr(name|pro|key,val|fn)
    * 作用: 获取或者设置属性节点的值
        * 可以传递一个参数, 也可以传递两个参数
        * 如果传递一个参数, 代表获取属性节点的值
        * 如果传递两个参数, 代表设置属性节点的值
    * 注意点:
        *如果是获取:无论找到多少个元素,都只会返回第一个元素指定的属性节点的值
        * 如果是设置:找到多少个元素就会设置多少个元素
        * 如果是设置: 如果设置的属性节点不存在, 那么系统会自动新增
2. removeAttr(name)
    * 作用：删除属性节点
    * 注意点: 会删除所有找到元素指定的属性节点
## jQuery的prop方法
1. prop方法
* 特点和attr方法一致
2. removeProp方法
* 特点和removeAttr方法一致
3. 注意点:
* prop方法不仅能够操作属性, 他还能操作属性节点
* 官方推荐在操作属性节点时,具有 true 和 false 两个属性的属性节点，如 checked, selected 或者 disabled 使用prop()，其他的使用 attr()
## jQuery操作类相关的方法
1. addClass(class|fn)
* 作用: 添加一个类
* 如果要添加多个, 多个类名之间用空格隔开即可
2. removeClass([class|fn])
* 作用: 删除一个类
* 如果想删除多个, 多个类名之间用空格隔开即可
3. toggleClass(class|fn[,sw])
* 作用: 切换类
* 有就删除, 没有就添加
## jQuery文本值相关的方法
1. html([val|fn])：大致和原生JS中的innerHTML一模一样
2. text([val|fn])：大致和原生JS中的innerText一模一样
3. val([val|fn|arr])：大致和原生的.value一模一样
## jQuery操作CSS样式的方法
1. 逐个设置
>             $("div").css("width", "100px");
>             $("div").css("height", "100px");
>             $("div").css("background", "red");
2. 链式设置
* 注意点: 链式操作如果大于3步, 建议分开
>             $("div").css("width", "100px").css("height", "100px").css("background", "blue");
3. 批量设置
>             $("div").css({
>                 width: "100px",
>                 height: "100px",
>                 background: "red"
>             });
4. 获取CSS样式值
>             console.log($("div").css("background"));
## jQuery位置和尺寸操作的方法
* $("div").width();获取元素的宽度
* $("div").offset();获取元素距离窗口的偏移位,返回值是一个对象
    * $("div").offset().left;获取元素距离窗口的左偏移量，返回值是一个数值
* $("div").position();获取元素距离定位元素的偏移位，返回值是一个对象
    * $("div").offset().left;获取元素距离定位元素的左偏移位，返回值是一个数值
* $("div").width("500px")；设置元素的宽度
* $(".son").offset({ left: 10});设置元素距离窗口的偏移量
* 注意点: position方法只能获取不能设置
## jQuery的scrollTop方法
* $(".scroll").scrollTop();获取滚动的偏移位
* $("body").scrollTop()+$("html").scrollTop();获取网页滚动的偏移位         
  * 注意点: 为了保证浏览器的兼容, 获取网页滚动的偏移位需要按照如上写法
* $(".scroll").scrollTop(300);设置滚动的偏移位
* $("html,body").scrollTop(300);设置网页滚动偏移位 
   * 注意点: 为了保证浏览器的兼容, 设置网页滚动偏移位的时候必须按照如上写法
## jQuery事件绑定
* jQuery中有两种绑定事件方式
    * eventName(fn);
        * 优点：编码效率略高
        * 缺点：部分事件jQuery没有实现,所以不能添加
    * on(eventName, fn);
        * 缺点：编码效率略低
        * 优点：所有js事件都可以添加
* 注意点:可以添加多个相同或者不同类型的事件,不会覆盖
>             // $("button").click(function () {
>             //     alert("hello lnj");
>             // });
>             // $("button").click(function () {
>             //     alert("hello 123");
>             // });
>             // $("button").mouseleave(function () {
>             //     alert("hello mouseleave");
>             // });
>             // $("button").mouseenter(function () {
>             //     alert("hello mouseenter");
>             // });
>             $("button").on("click", function () {
>                 alert("hello click1");
>             });
>             $("button").on("click", function () {
>                 alert("hello click2");
>             });
>             $("button").on("mouseleave", function () {
>                 alert("hello mouseleave");
>             });
>             $("button").on("mouseenter", function () {
>                 alert("hello mouseenter");
>             });
## jQuery事件移除
* off方法如果不传递参数, 会移除所有的事件
    * $("button").off();
* off方法如果传递一个参数, 会移除所有指定类型的事件
    * $("button").off("click");
* off方法如果传递两个参数, 会移除所有指定类型的指定事件
    * $("button").off("click", test1);
## jQuery事件自动触发
* trigger: 如果利用trigger自动触发事件,会触发事件冒泡
* triggerHandler: 如果利用triggerHandler自动触发事件, 不会触发事件冒泡
> $(".son").trigger("click");<br>
> $(".son").triggerHandler("click");
*  trigger: 如果利用trigger自动触发事件,会触发默认行为
* triggerHandler: 如果利用triggerHandler自动触发事件, 不会触发默认行为
## jQuery自定义事件
* 想要自定义事件, 必须满足两个条件
    1. 事件必须是通过on绑定的
    2. 事件必须通过trigger或者triggerHandler来触发
 
>             $(".son").on("myClick", function () {
>                 alert("son");
>             });
>             $(".son").triggerHandler("myClick");
## jQuery事件命名空间
* 想要事件的命名空间有效,必须满足两个条件
    1. 事件是通过on来绑定的
    2. 通过trigger或者triggerHandler触发事件
            
>             $(".son").on("click.zs", function () {
>                 alert("click1");
>             });
>             $(".son").on("click.ls", function () {
>                 alert("click2");
>             });
>             $(".son").trigger("click.zs");
>             $(".son").trigger("click.ls");
* 利用trigger触发子元素带命名空间的事件, 那么父元素带相同命名空间的事件也会被触发. ++而父元素没有命名空间的事件不会被触发++
* 利用trigger触发子元素不带命名空间的事件,那么子元素所有相同类型的事件和父元素所有相同类型的事件都会被触发
## jQuery事件委托
* 什么是事件委托?
    * 请别人帮忙做事情, 然后将做完的结果反馈给我们
>             $("button").click(function () {
>                 $("ul").append("<li>我是新增的li</li>");
>             })
* 在jQuery中,如果通过核心函数找到的元素不止一个, 那么在添加事件的时候,jQuery会遍历所有找到的元素,给所有找到的元素添加事件
>              $("ul>li").click(function () {
>                  console.log($(this).html());
>              });
* 以下代码的含义, 让ul帮li监听click事件
    * 之所以能够监听, 是因为入口函数执行的时候ul就已经存在了, 所以能够添加事件
    * 之所以this是li,是因为我们点击的是li, 而li没有click事件, 所以事件冒泡传递给了ul,ul响应了事件,  既然事件是从li传递过来的,所以ul必然指定this是谁
>             $("ul").delegate("li", "click", function () {
>                 console.log($(this).html());
>             });
## jQuery移入移出事件
* mouseover/mouseout事件, 子元素被移入移出也会触发父元素的事件
 
>             $(".father").mouseover(function () {
>                 console.log("father被移入了");
>             });
>             $(".father").mouseout(function () {
>                 console.log("father被移出了");
>             });
* mouseenter/mouseleave事件, 子元素被移入移出不会触发父元素的事件
            推荐大家使用
           
>             
>             $(".father").mouseenter(function () {
>                 console.log("father被移入了");
>             });
>             $(".father").mouseleave(function () {
>                 console.log("father被移出了");
>             });
>             
* hovers事件，是mouseenter和mouseleave事件的结合体
>             
>             $(".father").hover(function () {
>                 console.log("father被移入了");
>             },function () {
>                 console.log("father被移出了");
>             });
>             $(".father").hover(function () {
>                 console.log("father被移入移出了");
>             });
## jQuery显示和隐藏动画
* $("div").show(ms, function(){})
    * 注意：这里的时间是毫秒
    * 作用: 以动画效果显示元素
    * 回调函数：动画执行完毕之后调用
* $("div").hide(ms, function (){})
    * 注意：这里的时间是毫秒
    * 作用: 以动画效果隐藏元素
    * 回调函数：动画执行完毕之后调用
* $("div").toggle(ms, function () {})
    * 注意：这里的时间是毫秒
    * 作用: 以动画效果切换元素的显示和隐藏状态
    * 回调函数：动画执行完毕之后调用
## jQuery展开和收起动画
* $("div").slideDown(ms, function(){})
    * 注意：这里的时间是毫秒
    * 作用: 以动画效果展开
    * 回调函数：动画执行完毕之后调用
* $("div").slideUp(ms, function (){})
    * 注意：这里的时间是毫秒
    * 作用: 以动画效果收起
    * 回调函数：动画执行完毕之后调用
* $("div").slideToggle(ms, function () {})
    * 注意：这里的时间是毫秒
    * 作用: 以动画效果切换元素的展开收起状态
    * 回调函数：动画执行完毕之后调用
## jQuery淡入淡出动画
* $("div").fadeIn(ms, function(){})
    * 注意：这里的时间是毫秒
    * 作用: 以动画效果淡入
    * 回调函数：动画执行完毕之后调用
* $("div").fadeOut(ms, function (){})
    * 注意：这里的时间是毫秒
    * 作用: 以动画效果淡出
    * 回调函数：动画执行完毕之后调用
* $("div").fadeToggle(ms, function () {})
    * 注意：这里的时间是毫秒
    * 作用: 以动画效果切换元素的淡入淡出状态
    * 回调函数：动画执行完毕之后调用
* $("div").fadeTo(ms, opacity，function () {})
    * 注意：这里的时间是毫秒
    * 作用: 以动画效果淡出至哪种程度
    * 回调函数：动画执行完毕之后调用
## jQuery自定义动画
>               $("button").eq(0).click(function () {
>                 /*
>                 $(".one").animate({
>                     width: 500
>                 }, 1000, function () {
>                     alert("自定义动画执行完毕");
>                 });
>                 */
>                 $(".one").animate({
>                     marginLeft: 500
>                 }, 5000, function () {
>                     // alert("自定义动画执行完毕");
>                 });
* 第一个参数: 接收一个对象, 可以在对象中修改属性
* 第二个参数: 指定动画时长
* 第三个参数: 指定动画节奏, 默认就是swing
* 第四个参数: 动画执行完毕之后的回调函数
>                 $(".two").animate({
>                     marginLeft: 500
>                 }, 5000, "linear", function () {
>                     // alert("自定义动画执行完毕");
>                 });
>             })
>             $("button").eq(1).click(function () {
>                 $(".one").animate({
>                     width: "+=100"
>                 }, 1000, function () {
>                     alert("自定义动画执行完毕");
>                 });
>             });
>             $("button").eq(2).click(function () {
>                 $(".one").animate({
>                     // width: "hide"
>                     width: "toggle"
>                 }, 1000, function () {
>                     alert("自定义动画执行完毕");
>                 });
## jQuery的stop和delay方法
* 在jQuery的{}中可以同时修改多个属性, 多个属性的动画也会同时执行
>                 $(".one").animate({
>                     width: 500
>                     // height: 500
>                 }, 1000);
> 
>                 $(".one").animate({
>                     height: 500
>                 }, 1000);
* delay方法的作用就是用于告诉系统延迟时长
>                
>                 $(".one").animate({
>                     width: 500
>                     // height: 500
>                 }, 1000).delay(2000).animate({
>                     height: 500
>                 }, 1000);
>                 $(".one").animate({
>                     width: 500
>                 }, 1000);
>                 $(".one").animate({
>                     height: 500
>                 }, 1000);
> 
>                 $(".one").animate({
>                     width: 100
>                 }, 1000);
>                 $(".one").animate({
>                     height: 100
>                 }, 1000);
>             });
* stop方法
>             $("button").eq(1).click(function () {
>                 // 立即停止当前动画, 继续执行后续的动画
>                 // $("div").stop();
>                 // $("div").stop(false);
>                 // $("div").stop(false, false);
> 
>                 // 立即停止当前和后续所有的动画
>                 // $("div").stop(true);
>                 // $("div").stop(true, false);
> 
>                 // 立即完成当前的, 继续执行后续动画
>                 // $("div").stop(false, true);
> 
>                 // 立即完成当前的, 并且停止后续所有的
>                 $("div").stop(true, true);
## 51-jQuery添加节点相关方法
* 内部插入
    * 会将元素添加到指定元素内部的最后
        * append(content|fn)
        * appendTo(content)
    * 会将元素添加到指定元素内部的最前面
        * prepend(content|fn)
        * prependTo(content)
* 外部插入
    * 会将元素添加到指定元素外部的后面   
       * after(content|fn)
       * insertAfter(content)
    * 会将元素添加到指定元素外部的前面
       * before(content|fn)
       * insertBefore(content)          
>           $("button").click(function () {
>                 // 1.创建一个节点
>                 var $li = $("<li>新增的li</li>");
>                 // 2.添加节点
>                 $("ul").append($li);
>                 $("ul").prepend($li);
> 
>                 // $li.appendTo("ul");
>                 // $li.prependTo("ul");
> 
> 
>                 // $("ul").after($li);
>                 // $("ul").before($li);
>                 // $li.insertAfter("ul");
>             });
## jQuery删除节点相关方法
* 删除
    * remove([expr])
    删除指定元素，返回一个无法响应的事件的元素
    * empty()
    删除指定元素的内容和子元素, 指定元素自身不会被删除
    * detach([expr])
    删除指定元素，返回一个可以响应的事件的元素
>             */
>             $("button").click(function () {
>                 // $("div").remove();
>                 // $("div").empty();
>                 // $("li").remove(".item");
> 
>                 // 利用remove删除之后再重新添加,原有的事件无法响应
>                 // var $div = $("div").remove();
>                 // 利用detach删除之后再重新添加,原有事件可以响应
>                 var $div = $("div").detach();
>                 // console.log($div);
>                 $("body").append($div);
>             });
>              $("div").click(function () {
>                 alert("div被点击了");
>             });
## jQuery替换节点相关方法
* 替换
    * replaceWith(content|fn)
    * replaceAll(selector)
        * 替换所有匹配的元素为指定的元素
>             */
>             $("button").click(function () {
>                 // 1.新建一个元素
>                 var $h6 = $("<h6>我是标题6</h6>");
>                 // 2.替换元素
>                 // $("h1").replaceWith($h6);
>                 $h6.replaceAll("h1");
>             });
## jQuery复制节点相关方法
* clone([Even[,deepEven]])
    * 如果传入false就是浅复制, 如果传入true就是深复制
        * 浅复制只会复制元素, 不会复制元素的事件
        * 深复制会复制元素, 而且还会复制元素的事件
>             */
>             $("button").eq(0).click(function () {
>                 // 1.浅复制一个元素
>                 var $li = $("li:first").clone(false);
>                 // 2.将复制的元素添加到ul中
>                 $("ul").append($li);
>             });
>             $("button").eq(1).click(function () {
>                 // 1.深复制一个元素
>                 var $li = $("li:first").clone(true);
>                 // 2.将复制的元素添加到ul中
>                 $("ul").append($li);
>             });
> 
>             $("li").click(function () {
>                 alert($(this).html());
>             });
