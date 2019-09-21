### 一、class的基本语法
#### 1.简介
传统方法（构造函数）生成实例对象
```javascript
function PersonClass(name) {
  this.name = name;
}

PersonClass.prototype.sayName = function () {
    console.log(this.name);
};

var p = new PersonClass('cxk');
```
由于和其他面向对象语言如C++、Java差异比较大，所以引入了class这个概念来定义类，可以看做是一个**语法糖**
> 指计算机语言中添加的某种语法，这种语法对语言的功能没有影响，但是更方便程序员使用

用ES6改写一下，就成下面这样
```javascript
class PersonClass {
  // 默认方法，通过new命令生成对象实例的时候，自动调用该方法，必须有该方法，如果没有显式定义，则一个空的constructor方法会被默认添加
  // 等价于 Point 构造函数
  constructor(name) {
    this.name = name;
    // 该方法默认返回实例对象（this）
  } 
  
  // 等价于PersonClass.prototype.sayName()
  sayName() {
    console.log(this.name);
  }
}

---------------------------
typeof PersonClass // "function"
typeof PersonClass.prototype.sayName // "function"

PersonClass === PersonClass.prototype.constructor // true
```
#### 注意：
- constructor方法就是**构造方法**，而this关键字则代表**实例对象**
- 定义“类”中的方法的时候，**前面不需要加function关键字**
- 方法之间**不需要**加逗号分隔
- ES6的类可以看做是构造函数的另外一种写法
- 只能通过**new**调用类
- 与ES5一样，类的所有实例**共享一个原型对象**(会影响到所有的实例)
- 声明**不能被提升**
- 类声明中的代码将自动运行在**严格模式**下，而且无法强行脱离
- 类内部定义的方法都是不可枚举的

---
用法类似构造函数
```javascript
class Bar {
  doStuff() {
    console.log('stuff');
  }
}

var b = new Bar();
b.doStuff() // "stuff"
```
----
构造函数的prototype属性，在 ES6 的“类”上面继续存在。事实上，**类的所有方法都定义在类的prototype属性上面**。
```javascript
class Point {
  constructor() {
    // ...
  }

  toString() {
    // ...
  }
}

// 等同于

Point.prototype = {
  constructor() {},
  toString() {}
};
```
类的实例上调用方法 → 调用原型上的方法。

由于类的方法都定义在prototype对象上，所以类的新方法可以添加在prototype对象上。利用**Object.assign**方法可以很方便地一次向类添加多个方法。

```javascript
class Point {
  constructor(){
    // 给实例添加属性方法...
  }
}

Object.assign(Point.prototype, {
  toString(){},
  toValue(){}
});
```

---

#### getter & setter 访问器属性
与 ES5 一样，在“类”的内部可以使用get和set关键字，对某个属性设置存值函数和取值函数
```javascript
class MyClass {
  constructor() {
    // ...
  }
  get prop() {
    return 'getter';
  }
  set prop(value) {
    console.log('setter: '+value);
  }
}

let inst = new MyClass();

inst.prop = 123;
// setter: 123

inst.prop
// 'getter'

// 存值函数和取值函数是设置在属性的 Descriptor 对象上的。
let descriptor = Object.getOwnPropertyDescriptor(
  MyClass.prototype, "prop"
);
"get" in descriptor  // true
"set" in descriptor  // true
```
---
#### 类属性名可以采用属性表达式（可计算成员名称）
```javascript
let methodName = 'getArea';

class Square {
  constructor() {
  }

  [methodName]() {
    // ...
  }
}
```
---
#### Class表达式
> 与函数一样，除了声明形式，类也可以使用表达式的形式定义。
```javascript
// 外部使用该类只能引用MyClass
const MyClass = class Me { 
  // Me就是类名，但是只能在内部使用
  getClassName() {
    return Me.name;
  }
};
```
如果内部没用到Me的话可以省略
```javascript
const MyClass = class { /* ... */ };
// 等同于 class MyClass {};

// const func = function() { /* ... */ }
```
采用class表达式可以写出立即执行的class
```javascript
let person = new class {
  constructor(name) {
    this.name = name;
  }
  
  sayName() {
    console.log(this.name);
  }
}('cxk');

person.sayName(); // cxk
```

#### 注意：

1. 类和模块内部都是默认严格模式，ES6实际上把整个语言升级到了严格模式
2. 类不存在变量提升（与类继承有关）
```javascript
{
  let Foo = class {};
  class Bar extends Foo {
  }
}
```
3. name属性总是返回紧跟在class关键字后面的类名
4. **this指向**：默认指向类的实例(一旦单独使用该方法，很可能报错)(**如下代码**)
```javascript
class Logger {
  printName(name = 'there') {
    this.print(`Hello ${name}`);
  }

  print(text) {
    console.log(text);
  }
}

const logger = new Logger();
const { printName } = logger; // 获取该方法
printName(); // TypeError: Cannot read property 'print' of undefined
```
解决方法之一：
```javascript
class Logger {
  constructor() {
  // 在构造方法中绑定this
    this.printName = this.printName.bind(this);
  }

  // ...
}
```

#### 2.静态方法
>如果在一个方法前，加上static关键字，就表示该方法**不会被实例继承**，而是直接**通过类来调用**，这就称为“静态方法”。
```javascript
class Foo {
  static classMethod() {
    return 'hello';
  }
}

Foo.classMethod() // 'hello'

var foo = new Foo();
foo.classMethod()
// TypeError: foo.classMethod is not a function
```
- 如果静态方法包含this关键字，这个this指的是类，而不是实例。
- 父类的静态方法可以被子类继承

#### 3.实例属性的新写法
```javascript
class IncreasingCounter {
  constructor() {
    this._count = 0;
  }
}
// 可以写成如下
class IncreasingCounter {
  _count = 0;
  constructor() {
  }
}
```

#### 4.静态属性
> Class本身的属性，而不是在实例对象(this)的属性
```javascript
// 老写法
class Foo {
  // ...
}
Foo.prop = 1;

// 新写法
class Foo {
  static prop = 1;
}
```

#### 5.私有方法和私有属性
- 属性名之前，使用#表示。
```javascript
class IncreasingCounter {
  #count = 0;
  get value() {
    console.log('Getting the current value!');
    return this.#count;
  }
  log() {
	console.log(this.#count);
  }
  increment() {
    this.#count++;
	this.log();
  }
}

let a = new IncreasingCounter();

a.increment(); // 1
a.increment(); // 2
a.increment(); // 3
```

#### 6.new.target属性
> ES6 为new命令引入了一个new.target属性，该属性一般用在构造函数之中，**返回new命令作用于的那个构造函数**，如果不是new或Reflect.construct()调用的，返回undefined<br><br>子类继承父类时，会返回子类
```javascript
class Rectangle {
  constructor(length) {
    console.log(new.target === Rectangle);
    console.log(new.target === Square);
    // ...
  }
}

class Square extends Rectangle {
  constructor(length) {
    super(length);
  }
}

var obj = new Square(3); 
// false
// true
```
