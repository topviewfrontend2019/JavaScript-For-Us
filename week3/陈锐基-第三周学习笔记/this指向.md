# this的指向问题

### 函数的调用方式决定了this的指向（直接调用、方法调用和new调用，特殊方式如bind、call、apply、es6……）

## 一、直接调用 （函数名(...)）

```javascript
// this 指向全局对象，浏览器中是window，NodeJs是global
function test() {
    console.log(this);   
}
test();    // 直接调用


(function() {
    function test() {
        console.log(this);  
    }
    test();     // 非全局作用域下的直接调用
})();

// 直接调用并不是指在全局作用域下进行调用，在任何作用域下，直接通过 函数名(...) 来对函数进行调用的方式，都称为直接调用
```

## 二、通过bind()对直接调用的影响

```javascript
// 作用是将当前函数与指定的对象绑定，并返回一个新函数，这个新函数无论以什么样的方式调用，其 this 始终指向绑定的对象

var obj = {};

function test() {
    console.log(this === obj);
}

const testObj = test.bind(obj);
test();     
testObj(); 
```

## 三、call和apply对this的影响

```javascript
// 它们的第一个参数都是指定函数运行时其中的 this 指向


// 不过使用 apply 和 call 的时候仍然需要注意，如果目录函数本身是一个绑定了 this 对象的函数，那 apply 和 call 不会像预期那样执行，比如
var obj = {};

function test() {
    console.log(this === obj);
}

// 绑定到一个新对象，而不是 obj
var testObj = test.bind({});
test.apply(obj);    // true

// 期望 this 是 obj，即输出 true
// 但是因为 testObj 绑定了不是 obj 的对象，所以会输出 false
testObj.apply(obj); // false

// bind() 对函数的影响是深远的，慎用！
```

## 四、方法调用（对象.方法函数(...)）

```javascript
// 通过对象来调用其方法函数,函数中的 this 指向调用该方法的对象(同样需要注意 bind() 的影响)
var obj = {
    // 第一种方式，定义对象的时候定义其方法
    test() {
        console.log(this === obj);
    }
};

// 第二种方式，对象定义好之后为其附加一个方法(函数表达式)
obj.test2 = function() {
    console.log(this === obj);
};

// 第三种方式和第二种方式原理相同
// 是对象定义好之后为其附加一个方法(函数定义)
function t() {
    console.log(this === obj);
}
obj.test3 = t;

// 这也是为对象附加一个方法函数
// 但是这个函数绑定了一个不是 obj 的其它对象
var obj = {};
obj.test4 = (function() {
    console.log(this === obj);
    console.log(this);
}).bind({});

obj.test();     // true
obj.test2();    // true
obj.test3();    // true

// 受 bind() 影响，test4 中的 this 指向不是 obj
obj.test4();    // false  {}
```

## 五、方法中this指向全局对象的情况

```javascript
// 不是方法调用
// 方法中的this指向全局对象，如果不是因为bind()，那就一定是因为不是用方法调用方式
var obj = {
    test() {
        console.log(this === obj);
    }
};
obj.test();
var t = obj.test;
t();   
```

## 六、new调用

```javascript

// 在 es5 中，用 new 调用一个构造函数，会创建一个新对象，而其中的 this 就指向这个新对象。
var data = "Hi";    // 全局变量

function AClass(data) {
    this.data = data;
}

var a = new AClass("Hello World");
console.log(a.data);    // Hello World
console.log(data);      // Hi

var b = new AClass("Hello World");
console.log(a === b);   // false
```

## 七、箭头函数中的this

```javascript
// 箭头函数没有自己的 this 绑定。箭头函数中使用的 this，其实是直接包含它的那个函数或函数表达式中的 this
var obj = {
    test() {
        var arrow = () => {
            // 这里的 this 是 test() 中的 this，
            // 由 test() 的调用方式决定
            console.log(this === obj);
        };
        arrow();
    },

    getArrow() {
        return () => {
            // 这里的 this 是 getArrow() 中的 this，
            // 由 getArrow() 的调用方式决定
            console.log(this === obj);
        };
    }
};

obj.test();     // true

var arrow = obj.getArrow();
arrow();        // true

// this 都是由箭头函数的直接外层函数(方法)决定的，而方法函数中的 this 是由其调用方式决定的

// 箭头函数让大家在使用闭包的时候不需要太纠结 this
// ES6
const obj = {
    getArrow() {
        return () => {
            console.log(this === obj);
        };
    }
}    
// ES5，由 Babel 转译
var obj = {
    getArrow: function getArrow() {
        var _this = this;
        return function () {
            console.log(_this === obj);
        };
    }
};

```



- <https://segmentfault.com/a/1190000008400124>