# JSON

### “一种数据格式，而并非一种编程语言”

## 一、语法（没有变量）

1. ### 简单值：字符串（必须使用双引号）、数值、布尔值和NULL（不支持undefined）

2. ### 对象：要求给键值对中的**属性加双引号**

   ```json
   {
       "name":"abc",
       "age":25,
       "school":{
           "name":"chenrj",
           "location":"nowhere"
       }
   }
   ```

3. ### 数组

   ```json
   [23,"hi",true]
   // 也可以结合对象成为对象数组
   ```

## 二、解析与序列化

1. ### JSON对象

   ```json
   // 序列化方法
   JSON.stringify(JS对象，过滤器，是否保留缩进)  // 将JS对象转为JSON字符串
   JSON.parse(JS对象，还原函数)	// 将JSON字符串转为JS对象
   // 对象Obj和JSON.parse(JSON.stringify(Obj))没有任何关系
   ```

2. ### 序列化选项

   1）过滤结果

   ```javascript
   // 过滤器是一个数组时，则质保函数组中列出的属性
   var book = {
       "title":"aaa",
       "authors":[
           "abc"
       ],
       "edition":3
   };
   var jsonText = JSON.stringify(book,["title","edition"]);
   // {"title":"aaa","edition":3}
   
   // 过滤器为一个函数（替换函数：replacer），传入的函数接收两个参数，属性名（键）和属性值
   var book = {
       "title":"aaa",
       "authors":[
           "abc"
       ],
       "edition":3,
       "year":2011
   };
   var jsonText = JSON.stringify(book,function(key, value){
       swtich(key){
           case "authors":
           	return value.join(",");
           case "edition":
           	return undefined; // 返回undefined删除该属性
           case "year":
           	return 5000;
           default:
           	return value;
       }
   });
   // {"title":"aaa","authors":"abc","year":5000}
   ```

   2) 字符串缩进

   ```javascript
   JSON.stringify(book, null, 4)
   // 每个级别缩进4个空格
   // 也可以设置为制表符，或者两个段划线之类的任意字符
   ```

   3）toJSON() 方法

   ```javascript
   var book = {
       "title":"aaa",
       "authors":[
           "abc"
       ],
       "edition":3,
       "year":2011,
       toJOSN：function(){
           return this.title;
       }
   };
   // 对过滤器的补充
   // 有toJSON方法且能通过它取得有效值，则JSON.stringify()的时候会直接调用该方法
   ```

3. ### 解析选项

   ```javascript
   // JSON.parse()方法第二个参数也是一个函数，类似于replacer，称为还原函数（reviver）
   ```

   



