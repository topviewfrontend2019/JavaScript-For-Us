# 20.1 语法
## 20.1.1简单值
+ JSON字符串必须使用双引号
## 20.1.2对象
+ JavaScript中的对象字面量：
```
var person = {
    "name": "Nicholas",
    "age": 29
};
```
JSON:
```
{
         "name": "Nicholas",
         "age": 29
}
```
>相比较，JSON没有声明变量也没有末尾的分号，对象的属性必须加双引号

## 20.1.3数组
JavaScript：
```
var values = [25, "hi", true];
```
JSON:
```
[25, "hi", true]
```
>同上，没有变量和分号

# 20.2解析与序列化
## 20.2.1JSON对象
+ eval()
+ JSON.stringify()把JS对象序列化为JSON字符串
+ JSON.parse()把JSON字符串解析为原生JS值
## 20.2.2序列化选项
JSON.stringify()另外接收两个参数，第一个是过滤器，第二个是是否保留缩进的选项
1.过滤结果
+ 如果过滤器参数是数组，那JSON.stringify()的结果只包含数组中列出的属性
+ 如果是函数，传入的函数接收两个参数，属性名和属性值
```
var jsonText = JSON.stringify(book,function(key,value) {
   switch(key) {
       case "authors": 
          return value.join(",");

     case "editon": 
            return undefined;//如果值为undefined删除该属性
}

});
```
2.字符串缩进
+ 是数值，则代表每个级别缩进的格数
+是字符串，则该字符串被用作缩进字符
3.toJSON()方法
## 20.2.3解析对象
JSON.parse()也可以接收一个函数，称为还原函数，一样接收两个参数，一个键一个值，而且都需要返回一个值。
> 如果返回undefined，表示要从结果中删除对应键，返回其他则插入
