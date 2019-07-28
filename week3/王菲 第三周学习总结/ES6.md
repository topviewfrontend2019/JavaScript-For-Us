# 2.let和const命令
+ let声明的变量只在它所在的代码块有效
```
var a = [];
for (var i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 10
```
上面代码中，变量i是var命令声明的，在全局范围内都有效，所以全局只有一个变量i。每一次循环，变量i的值都会发生改变，而循环内被赋给数组a的函数内部的console.log(i)，里面的i指向的就是全局的i。也就是说，所有数组a的成员里面的i，指向的都是同一个i，导致运行时输出的是最后一轮的i的值，也就是 10。

```
var a = [];
for (let i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 6
```
----------
*不会变量提升*

-------------
*暂时性死区*
```
let x = x;
// ReferenceError: x is not defined
```

-------------
不允许重复声明
因此，不能在函数内部重新声明参数

```
function func(arg) {
  let arg;
}
func() // 报错

function func(arg) {
  {
    let arg;
  }
}
func() // 不报错
````
--------
+ 块级作用域

--------------
+ const
`const`声明一个只读的常量。一旦声明，常量的值就不能改变。

# 3.变量的解构赋值
```
let [foo, [[bar], baz]] = [1, [[2], 3]];
foo // 1
bar // 2
baz // 3

let [ , , third] = ["foo", "bar", "baz"];
third // "baz"

let [x, , y] = [1, 2, 3];
x // 1
y // 3

let [head, ...tail] = [1, 2, 3, 4];
head // 1
tail // [2, 3, 4]

let [x, y, ...z] = ['a'];
x // "a"
y // undefined
z // []
```

-------------------
默认值
解构赋值允许指定
```
let [foo = true] = [];
foo // true

let [x, y = 'b'] = ['a']; // x='a', y='b'
let [x, y = 'b'] = ['a', undefined]; // x='a', y='b'
```
注意，ES6 内部使用严格相等运算符（===），判断一个位置是否有值。所以，只有当一个数组成员严格等于undefined，默认值才会生效。
```
let [x = 1] = [undefined];
x // 1

let [x = 1] = [null];
x // null默认值。
```
---------------
## 对象的解构赋值 
```
let { foo: baz } = { foo: 'aaa', bar: 'bbb' };
baz // "aaa"
foo // error: foo is not defined
```
上面代码中，foo是匹配的模式，baz才是变量。真正被赋值的是变量baz，而不是模式foo。

# 4.字符串的扩展
```
'\z' === 'z'  // true
'\172' === 'z' // true
'\x7A' === 'z' // true
'\u007A' === 'z' // true
'\u{7A}' === 'z' // true
```
2.字符串的遍历接口：
```
for (let codePoint of 'foo') {
  console.log(codePoint)
}
// "f"
// "o"
// "o"
```
3.直接输入 U+2028 和 U+2029 
4.JSON.stringify()的改造
5.模块字符串
```
$('#list').html(`
<ul>
  <li>first</li>
  <li>second</li>
</ul>
`);
```
6.实例：模板编译-》好难啊啊啊
```
function compile(template){
  const evalExpr = /<%=(.+?)%>/g;
  const expr = /<%([\s\S]+?)%>/g;

  template = template
    .replace(evalExpr, '`); \n  echo( $1 ); \n  echo(`')
    .replace(expr, '`); \n $1 \n  echo(`');

  template = 'echo(`' + template + '`);';

  let script =
  `(function parse(data){
    let output = "";

    function echo(html){
      output += html;
    }

    ${ template }

    return output;
  })`;

  return script;
}
```
```
let parse = eval(compile(template));
div.innerHTML = parse({ supplies: [ "broom", "mop", "cleaner" ] });
//   <ul>
//     <li>broom</li>
//     <li>mop</li>
//     <li>cleaner</li>
//   </ul>
```
# 5.字符串的新增方法
1.String.fromCodePoint()
2.String.raw()
3.codePointAt()
4.normalize()
5.includes()/startsWith(),endsWith()
>传统上，JavaScript 只有indexOf方法，可以用来确定一个字符串是否包含在另一个字符串中。ES6 又提供了三种新方法。

includes()：返回布尔值，表示是否找到了参数字符串。
startsWith()：返回布尔值，表示参数字符串是否在原字符串的头部。
endsWith()：返回布尔值，表示参数字符串是否在原字符串的尾部。
```
let s = 'Hello world!';

s.startsWith('Hello') // true
s.endsWith('!') // true
s.includes('o') // true
````
这三个方法都支持第二个参数，表示开始搜索的位置。
```
let s = 'Hello world!';

s.startsWith('world', 6) // true
s.endsWith('Hello', 5) // true
s.includes('Hello', 6) // false
````
上面代码表示，使用第二个参数n时，endsWith的行为与其他两个方法有所不同。它针对前n个字符，而其他两个方法针对从第n个位置直到字符串结束。
6.repeat()重复
7.padAtart()/padEnd()补全
8.trimStart()/trimEnd()除空格
9.matchAll()

# 6.正则的扩展
1.RegExp 构造函数 
2.字符串的正则方法
> match()
replace()
search()
split()

3.u 修饰符 
4.RegExp.prototype.unicode属性
5.y修饰符
```
const REGEX = /a/g;
REGEX.lastIndex = 2;//指定开始的位置
const match = REGEX.exec('xaya');
match.index
```
6.RegExp.prototype.sticky属性->表示是否设置了y修饰符
7.RegExp.prototype.flags属性->返回正则表达式的修饰符
8.s修饰符：dotAll模式
9.后行断言
10.Unicode属性类
p{}/P{}使用时需要加上u修饰符
11.具名组匹配
```
const RE_DATE = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/;

const matchObj = RE_DATE.exec('1999-12-31');
const year = matchObj.groups.year; // 1999
const month = matchObj.groups.month; // 12
const day = matchObj.groups.day; // 31
```
上面代码中，“具名组匹配”在圆括号内部，模式的头部添加“问号 + 尖括号 + 组名”`（?<year>）`，然后就可以在`exec`方法返回结果的`groups`属性上引用该组名。同时，数字序号（`matchObj[1]`）依然有效。

具名组匹配等于为每一组匹配加上了 ID，便于描述匹配的目的。如果组的顺序变了，也不用改变匹配后的处理代码。

------
引用
如果要在正则表达式内部引用某个“具名组匹配”，可以使用\k<组名>的写法。
```
const RE_TWICE = /^(?<word>[a-z]+)!\k<word>$/;
RE_TWICE.test('abc!abc') // true
RE_TWICE.test('abc!ab') // false
```

12.String.prototype.matchAll
如果一个正则表达式在字符串里面有多个匹配，现在一般使用g修饰符或y修饰符，在循环里面逐一取出。
```
var regex = /t(e)(st(\d?))/g;
var string = 'test1test2test3';

var matches = [];
var match;
while (match = regex.exec(string)) {
  matches.push(match);
}

matches
// [
//   ["test1", "e", "st1", "1", index: 0, input: "test1test2test3"],
//   ["test2", "e", "st2", "2", index: 5, input: "test1test2test3"],
//   ["test3", "e", "st3", "3", index: 10, input: "test1test2test3"]
// ]
```
```
const string = 'test1test2test3';

// g 修饰符加不加都可以
const regex = /t(e)(st(\d?))/g;

for (const match of string.matchAll(regex)) {
  console.log(match);
}
// ["test1", "e", "st1", "1", index: 0, input: "test1test2test3"]
// ["test2", "e", "st2", "2", index: 5, input: "test1test2test3"]
// ["test3", "e", "st3", "3", index: 10, input: "test1test2test3"]
```
遍历器转为数组是非常简单的，使用...运算符和Array.from方法就可以
```
// 转为数组方法一
[...string.matchAll(regex)]

// 转为数组方法二
Array.from(string.matchAll(regex));
```
# 数值的扩展
1.二进制和八进制
2.Number.isFinite()/Number.isNaN()
这两个方法只对数值有效
3.Number.parseInt()/Number.parseFloat
4.Number.isInterger()
5.Number.EPSION
6.安全整数和Number.isSafeInterger()
7.Math.trunc()
Math.sign()
