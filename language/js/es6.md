

## 函数
### 箭头函数
ES6允许使用“箭头”（=>）定义函数。
```js
var f = () => 5;
// 等同于
var f = function () { return 5 };

var sum = (num1, num2) => num1 + num2;
// 等同于
var sum = function(num1, num2) {
  return num1 + num2;
};
```
如果箭头函数的代码块部分多于一条语句，就要使用大括号将它们括起来，并且使用`return`语句返回。
```
var sum = (num1, num2) => { return num1 + num2; }
```
由于大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上括号。
```
var getTempItem = id => ({ id: id, name: "Temp" });
```

### 使用注意点
（1）函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。  
（2）不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。  
（3）不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用Rest参数代替。  
（4）不可以使用yield命令，因此箭头函数不能用作Generator函数。  

## Class
```
//定义类
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
```

### constructor方法

### 类的实例对象
与ES5一样，类的所有实例共享一个原型对象。  

### 私有方法
ES6 不提供私有方法  
类和模块的内部，默认就是严格模式，所以不需要使用use strict指定运行模式。只要你的代码写在类或模块之中，就只有严格模式可用。

### 不存在变量提升

### name属性
由于本质上，ES6的类只是ES5的构造函数的一层包装，所以函数的许多特性都被Class继承，包括name属性。
```
class Point {}
Point.name // "Point"
```
`name`属性总是返回紧跟在`class`关键字后面的类名。

### Class的继承
Class之间可以通过extends关键字实现继承，这比ES5的通过修改原型链实现继承，要清晰和方便很多

### String
```js
var s = 'Hello world!';
s.startsWith('Hello') // true
s.endsWith('!') // true
s.includes('o') // true

'x'.repeat(3) // "xxx"
'hello'.repeat(2) // "hellohello"

'x'.padStart(5, 'ab') // 'ababx'
'x'.padStart(4, 'ab') // 'abax'
'x'.padEnd(5, 'ab') // 'xabab'
'x'.padEnd(4, 'ab') // 'xaba'
```
传统的JavaScript语言，输出模板通常是这样写的。
```
$('#result').append(
  'There are <b>' + basket.count + '</b> ' +
  'items in your basket, ' +
  '<em>' + basket.onSale +
  '</em> are on sale!'
);
```
上面这种写法相当繁琐不方便，ES6引入了模板字符串解决这个问题。
```
$('#result').append(`
  There are <b>${basket.count}</b> items
   in your basket, <em>${basket.onSale}</em>
  are on sale!
`);
```

模板字符串中嵌入变量，需要将变量名写在`${}`之中。大括号内部可以放入任意的JavaScript表达式，可以进行运算，以及引用对象属性。如果模板字符串中的变量没有声明，将报错。
```
`Hello ${'World'}`  // "Hello World"

var x = 1;
var y = 2;
`${x} + ${y} = ${x + y}`
// "1 + 2 = 3"

function fn() {
  return "Hello World";
}
`foo ${fn()} bar`
// foo Hello World bar

```

### 数值的扩展
```
// Number.isFinite()用来检查一个数值是否为有限的（finite）。
Number.isFinite(15); // true
Number.isFinite(0.8); // true
Number.isFinite(NaN); // false

// Number.isNaN()用来检查一个值是否为NaN。
Number.isNaN(NaN) // true
Number.isNaN(15) // false
Number.isNaN('15') // false
```

## Module 的语法
ES6 模块不是对象，而是通过export命令显式指定输出的代码，再通过import命令输入。
```
// ES6模块
import { stat, exists, readFile } from 'fs';
```
上面代码的实质是从fs模块加载3个方法，其他方法不加载。这种加载称为“编译时加载”或者静态加载，即 ES6 可以在编译时就完成模块加载，效率要比 CommonJS 模块的加载方式高。当然，这也导致了没法引用 ES6 模块本身，因为它不是对象。

## Set和Map
Set类似于数组，但是成员的值都是唯一的，没有重复的值。  
Set 本身是一个构造函数，用来生成 Set 数据结构。
```
const s = new Set();
[2, 3, 5, 4, 5, 2, 2].forEach(x => s.add(x));
for (let i of s) {
  console.log(i);
}
// 2 3 5 4

// 去除数组的重复成员
[...new Set(array)]
```
在Set内部，两个NaN是相等。  

JavaScript的对象（Object），本质上是键值对的集合（Hash结构），但是传统上只能用字符串当作键。
ES6提供了Map数据结构。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。

## Symbol
Symbol类型是独一无二的，可以保证不会与其他属性名产生冲突。
> ES6引入了一种新的原始数据类型Symbol，表示独一无二的值。它是JavaScript语言的第七种数据类型，前六种是：Undefined、Null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。

## Proxy
Proxy 用于修改某些操作的默认行为，等同于在语言层面做出修改，所以属于一种“元编程”（meta programming），即对编程语言进行编程。  
Proxy 可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。Proxy 这个词的原意是代理，用在这里表示由它来“代理”某些操作，可以译为“代理器”。

## async
ES2017 标准引入了 async 函数，使得异步操作变得更加方便。  
async 函数是什么？一句话，它就是 Generator 函数的语法糖。

## 编程风格
1. let 取代 var
2. 全局常量和线程安全
在let和const之间，建议优先使用const，尤其是在全局环境，不应该设置变量，只应设置常量。
3. 静态字符串一律使用单引号或反引号，不使用双引号。动态字符串使用反引号。
4. 使用数组成员对变量赋值时，优先使用解构赋值。
5. 单行定义的对象，最后一个成员不以逗号结尾。多行定义的对象，最后一个成员以逗号结尾。
对象尽量静态化，一旦定义，就不得随意添加新的属性。如果添加属性不可避免，要使用Object.assign方法。
6. 使用扩展运算符（...）拷贝数组。
`const itemsCopy = [...items];`  
使用Array.from方法，将类似数组的对象转为数组。
7. 立即执行函数可以写成箭头函数的形式。
```
(() => {
  console.log('Welcome to the Internet.');
})();
```
8. 注意区分Object和Map，只有模拟现实世界的实体对象时，才使用Object。如果只是需要key: value的数据结构，使用Map结构。因为Map有内建的遍历机制。
9. 总是用Class，取代需要prototype的操作。因为Class的写法更简洁，更易于理解。  
使用extends实现继承，因为这样更简单，不会有破坏instanceof运算的危险。
10. Module语法是JavaScript模块的标准写法，坚持使用这种写法。使用import取代require  
使用export取代module.exports。  
如果模块只有一个输出值，就使用export default，如果模块有多个输出值，就不使用export default，不要export default与普通的export同时使用。
不要在模块输入中使用通配符。因为这样可以确保你的模块之中，有一个默认输出（export default）。
如果模块默认输出一个函数，函数名的首字母应该小写。  
如果模块默认输出一个对象，对象名的首字母应该大写。
11. ESLint是一个语法规则和代码风格的检查工具，可以用来保证写出语法正确、风格统一的代码。

