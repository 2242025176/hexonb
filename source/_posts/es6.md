---
title: es6常用
top: 3
date: 2021-06-27
categories: es6
tags: es6  #标签

---

# 		ES6 常用：

注：不包括se6的所有语法

> 时间-2021-4-23
>

# 1.  let  &&  const 



### 1.1 let ：

`let`命令，用来声明变量。它的用法类似于`var`，但是所声明的变量，只在`let`命令所在的代码块内有效：

案例：

```js
{
  let a = 10;
  var b = 1;
}

a // 引用错误: a is not defined.
b // 1
```

不存在变量提升：

`var`命令会发生“变量提升”现象，即变量可以在声明之前使用，值为`undefined`

为了纠正这种现象，`let`命令改变了语法行为，它所声明的变量一定要在声明后使用，否则报错。

```js
// var 的情况
console.log(foo); // 输出undefined
var foo = 2;

// let 的情况
console.log(bar); // 报错ReferenceError
let bar = 2;
```

## 1.2 const 

`const`声明一个只读的常量。一旦声明，常量的值就不能改变。

```javascript
const PI = 3.1415;
PI // 3.1415

PI = 3;
// TypeError: Assignment to constant variable.
```

`const`的作用域与`let`命令相同：只在声明所在的块级作用域内有效。

```javascript
if (true) {
  const MAX = 5;
}

MAX // Uncaught ReferenceError: MAX is not defined
```

`const`声明的常量，也与`let`一样不可重复声明。

```javascript
var message = "Hello!";
let age = 25;

// 以下两行都会报错
const message = "Goodbye!";
const age = 30;
```



# 2.字符串的扩展：

抽取官网的个别语法 不全面 

参考阮一峰es6官网字符串篇：https://es6.ruanyifeng.com/#docs/string-methods

## 2.1模板字符串：

传统的 JavaScript 语言，输出模板通常是这样写的（下面使用了 jQuery 的方法）。

```javascript
$('#result').append(
  'There are <b>' + basket.count + '</b> ' +
  'items in your basket, ' +
  '<em>' + basket.onSale +
  '</em> are on sale!'
);
```

上面这种写法相当繁琐不方便，ES6 引入了模板字符串解决这个问题。

官方解释：

​		模板字符串（template string）是增强版的字符串，用反引号（`）标识。

​		模板字符串中嵌入变量，需要将变量名写在`${}`之中。

```javascript
$('#result').append(`
  There are <b>${basket.count}</b> items
   in your basket, <em>${basket.onSale}</em>
  are on sale!
`);
```

## 2.2字符串的新增方法：

## 2.2.1实例方法：includes(), startsWith(), endsWith()

传统上，JavaScript 只有`indexOf`方法，可以用来确定一个字符串是否包含在另一个字符串中。

ES6 又提供了三种新方法。

- **includes()**：返回布尔值，表示是否找到了参数字符串。
- **startsWith()**：返回布尔值，表示参数字符串是否在原字符串的头部。
- **endsWith()**：返回布尔值，表示参数字符串是否在原字符串的尾部。

```javascript
let s = 'Hello world!';

s.startsWith('Hello') // true
s.endsWith('!') // true
s.includes('o') // true
```

这三个方法都支持第二个参数，表示开始搜索的位置。

```javascript
let s = 'Hello world!';

s.startsWith('world', 6) // true
s.endsWith('Hello', 5) // true
s.includes('Hello', 6) // false
```

上面代码表示，使用第二个参数`n`时，`endsWith`的行为与其他两个方法有所不同。它针对前`n`个字符，而其他两个方法针对从第`n`个位置直到字符串结束。

## 2.2.2 实例方法：repeat()

`repeat`方法返回一个新字符串，表示将原字符串重复`n`次。

```javascript
'x'.repeat(3) // "xxx"
'hello'.repeat(2) // "hellohello"
'na'.repeat(0) // ""
```

## 2.2.3 实例方法：replaceAll()

历史上，字符串的实例方法`replace()`只能替换第一个匹配。

```javascript
'aabbcc'.replace('b', '_')
// 'aa_bcc'
```

上面例子中，`replace()`只将第一个`b`替换成了下划线。



# 3. 数值的扩展

## 3.1 Number.isFinite() , Number.isNaN()

ES6 在`Number`对象上，新提供了`Number.isFinite()`和`Number.isNaN()`两个方法。

简单理解：`Number.isFinite()` 就检查是不是number类型的

​					`Number.isNaN()`就检查是不是 NaN 类型的 。NaN的定义是 非数字值

`Number.isFinite()`用来检查一个数值是否为有限的（finite），即不是`Infinity`。

```javascript
Number.isFinite(15); // true
Number.isFinite(0.8); // true
Number.isFinite(NaN); // false
Number.isFinite(Infinity); // false
Number.isFinite(-Infinity); // false
Number.isFinite('foo'); // false
Number.isFinite('15'); // false
Number.isFinite(true); // false
```

注意，如果参数类型不是数值，`Number.isFinite`一律返回`false`。

`Number.isNaN()`用来检查一个值是否为`NaN`。 

```javascript
Number.isNaN(NaN) // true
Number.isNaN(15) // false
Number.isNaN('15') // false
Number.isNaN(true) // false
Number.isNaN(9/NaN) // true
Number.isNaN('true' / 0) // true
Number.isNaN('true' / 'true') // true
```

如果参数类型不是`NaN`，`Number.isNaN`一律返回`false`。

## 3.2 Number.parseInt(), Number.parseFloat()

ES6 将全局方法`parseInt()`和`parseFloat()`，移植到`Number`对象上面，行为完全保持不变。

这样做的目的，是逐步减少全局性方法，使得语言逐步模块化。

```javascript
// ES5的写法
parseInt('12.34') // 12
parseFloat('123.45#') // 123.45

// ES6的写法
Number.parseInt('12.34') // 12
Number.parseFloat('123.45#') // 123.45
```

## 3.3 Math对象的扩展：

### 3.3.1 Math.trunc()

`Math.trunc`方法用于去除一个数的小数部分，返回整数部分。

```javascript
Math.trunc(4.1) // 4
Math.trunc(4.9) // 4
Math.trunc(-4.1) // -4
Math.trunc(-4.9) // -4
Math.trunc(-0.1234) // -0
```

### 3.3.2 Math.imul()

`Math.imul`方法返回两个数以 32 位带符号整数形式相乘的结果，返回的也是一个 32 位的带符号整数。

```javascript
Math.imul(2, 4)   // 8
Math.imul(-1, 8)  // -8
Math.imul(-2, -2) // 4
```

# 4.函数的扩展

## 4.1 rest 参数

ES6 引入 rest 参数（形式为`...变量名`），用于获取函数的多余参数，这样就不需要使用`arguments`对象了。rest 参数搭配的变量是一个数组，该变量将多余的参数放入数组中。

```javascript
function add(...values) {  #！！！ ...values 获取函数的多余参数
  let sum = 0;

  for (var val of values) {
    sum += val;
  }

  return sum;
}

add(2, 5, 3) // 10
```

上面代码的`add`函数是一个求和函数，利用 rest 参数，可以向该函数传入任意数目的参数。



## 4.2 严格模式

从 ES5 开始，函数内部可以设定为严格模式。

```javascript
function doSomething(a, b) {
  'use strict';
  // code
}
```

ES2016 做了一点修改，规定只要函数参数使用了默认值、解构赋值、或者扩展运算符，那么函数内部就不能显式设定为严格模式，否则会报错。

## 4.3 箭头函数 (重点方法)

### 基本用法

ES6 允许使用“箭头”（`=>`）定义函数。

```javascript
var f = v => v;

// 等同于
var f = function (v) {
  return v;
};
```

### 使用注意点

箭头函数有几个使用注意点。

（1）函数体内的`this`对象，就是定义时所在的对象，而不是使用时所在的对象。

（2）不可以当作构造函数，也就是说，不可以使用`new`命令，否则会抛出一个错误。

（3）不可以使用`arguments`对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。

（4）不可以使用`yield`命令，因此箭头函数不能用作 Generator 函数。

上面四点中，第一点尤其值得注意。`this`对象的指向是可变的，但是在箭头函数中，它是固定的。

```javascript
function foo() {
  setTimeout(() => {
    console.log('id:', this.id);
  }, 100);
}

var id = 21; //全局  一般的this指向会指向 全局对象`window`，

foo.call({ id: 42 });
// id: 42
```

上面代码中，`setTimeout()`的参数是一个箭头函数，这个箭头函数的定义生效是在`foo`函数生成时，而它的真正执行要等到 100 毫秒后。如果是普通函数，执行时`this`应该指向全局对象`window`，这时应该输出`21`。但是，箭头函数导致`this`总是指向函数定义生效时所在的对象（本例是`{id: 42}`），所以打印出来的是`42`。

## 4.4 尾调用：

就是指某个函数的最后一步是调用另一个函数。（这里省略了 尾递归 ）

```js
function f(){
    var data = 'hallo'
    return g(data)
};
 f();
function g(res){
    console.log('调用');
    console.log(res)//hallo
}
```

## 4.5 catch:

简单来讲就是 失败执行的回调操作：来处理错误返回

```js
try {
  // ...
} catch (err) {
  // 处理错误
}
```



# 5. 数组的扩展：



## 5.1：扩展运算符 `. . .`

注意，只有函数调用时，扩展运算符才可以放在圆括号中，否则会报错。

```js
 var arr = [1,2,3]
 console.log(...arr) //1 2 3 
```

扩展运算符的应用：

```js
const arr1 = ['a', 'b'];
const arr2 = ['c'];
const arr3 = ['d', 'e'];

// ES5 的合并数组
arr1.concat(arr2, arr3);
// [ 'a', 'b', 'c', 'd', 'e' ]

// ES6 的合并数组
[...arr1, ...arr2, ...arr3]
// [ 'a', 'b', 'c', 'd', 'e' ]
```

以上方法属于 浅拷贝 

这就是浅拷贝。如果修改了引用指向的值，会同步反映到新数组。



## 5.2 find 方法 && findIndex 方法：

数组实例的`find`方法，用于找出`第一个`符合条件的数组成员。

```js
var array1 = [5, 12, 8, 130, 44];
var found = array1.find(function(element) {
  return element > 10;
});
console.log(found);//第一个 大于10的 是 12
```

数组实例的`findIndex`方法的用法与`find`方法非常类似，返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回`-1`。

```js
var array1 = [5, 12, 8, 130, 44];
var found = array1.findIndex(function(element) {
  return element > 10;
});
console.log(found);// 第一个 大于10的 下标 是 1
```



# 6.对象的扩展：

## 6.1 属性的简洁表示法

ES6 允许在大括号里面，直接写入变量和函数，作为对象的属性和方法。这样的书写更加简洁。

```js
const o = {
  method() {
    return "Hello!";
  }
};
// 等同于
const o = {
  method: function() {
    return "Hello!";
  }
};
```

## 6.2 对象的扩展运算符

《数组的扩展》一章中，已经介绍过扩展运算符（`...`）。ES2018 将这个运算符[引入](https://github.com/sebmarkbage/ecmascript-rest-spread)了对象。

对象的扩展运算符（`...`）用于取出参数对象的所有可遍历属性，拷贝到当前对象之中。

```js
let z = { a: 3, b: 4 };
let n = { ...z };
n // { a: 3, b: 4 }
```

# 7.对象新增的方法：

## 7.1 `Object.assign()`方法：用于对象的合并



`Object.assign()`方法的第一个参数是目标对象，后面的参数都是源对象。

注意，如果目标对象与源对象有同名属性，或多个源对象有同名属性，则后面的属性会覆盖前面的属性。

`Object.assign()`方法实行的是浅拷贝，而不是深拷贝。当数据源更改合并的数据也会有影响。

```js
const target = { a: 1 };
const source1 = { b: 2 };
const source2 = { c: 3 };

Object.assign(target, source1, source2);
target // {a:1, b:2, c:3}
```



## 7.2：Object.keys()，Object.values()，Object.entries()

ES2017 [引入](https://github.com/tc39/proposal-object-values-entries)了跟`Object.keys`配套的`Object.values`和`Object.entries`，作为遍历一个对象的补充手段，供`for...of`循环使用。

```js
let {keys, values, entries} = Object;
let obj = { a: 1, b: 2, c: 3 };

for (let key of keys(obj)) {
  console.log(key); // 'a', 'b', 'c'
}

for (let value of values(obj)) {
  console.log(value); // 1, 2, 3
}

for (let [key, value] of entries(obj)) {
  console.log([key, value]); // ['a', 1], ['b', 2], ['c', 3]
}
```

`Object.keys`方法，返回一个数组,成员是参数对象自身的属性的`键名`

`Object.values`方法返回一个数组,成员是参数对象自身的属性的`键值`。

`Object.entries()`方法返回一个数组，成员是参数对象自身的`键值对数组`。

## 7.3 Object.fromEntries()  

`Object.fromEntries()`方法是`Object.entries()`的逆操作，用于将一个键值对`数组转为对象`。

```js
Object.fromEntries([
  ['foo', 'bar'],
  ['baz', 42]
])
// { foo: "bar", baz: 42 }
```

# 8. Symbol :`数据类型`

ES6 引入了一种新的原始数据类型`Symbol`，表示独一无二的值。

可以参考菜鸟教程的 `Symbol` 用法：https://www.runoob.com/w3cnote/es6-symbol.html

```js
let s = Symbol();

typeof s
// "symbol"
```

上面代码中，变量`s`就是一个独一无二的值。`typeof`运算符的结果，表明变量`s`是 Symbol 数据类型，而不是字符串之类的其他类型。



# 9.Set && map

## 9.1 set ：数据结构

**类似数组，无重复值。**

```js
const set = new Set([1, 2, 3, 4, 4]);
console.log(...set)  //1,2,3,4
```

**Set并不是数组** :Set可以用于数组去重,但是,需要把Set再转成数组

```js
const set = new Set([1,2,3,3,4,4,5]);
const arr = Array.from(set)
console.log(arr[0],arr.concat(['1','2']))//[1, 2, 3, 4, 5, "1", "2"]
```



## 9.2 map:

也就是说，Object 结构提供了“字符串—值”的对应，Map 结构提供了“值—值”的对应，是一种更完善的 Hash 结构实现。如果你需要“键值对”的数据结构，Map 比 Object 更合适。

```js
const m = new Map();
const o = {};
m.set(o, 'content')
m.get(o) // "content"

m.has(o) // true
m.delete(o) // true
m.has(o) // false
```

上面代码使用 Map 结构的`set`方法，将对象`o`当作`m`的一个键，然后又使用`get`方法读取这个键，接着使用`delete`方法删除了这个键。

---------------------------------------------------------------------------------

map的`键值对`的遍历方法这里就省略了  ,可以去阮一峰编写的es6 查看  ：

[传送]: https://es6.ruanyifeng.com/#docs/set-map



# 10、Proxy：拦截

Proxy 可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。



# 11、Reflect





# 12、Promise 对象

`Promise`对象有以下两个特点。

（1）对象的状态不受外界影响。

> `Promise`对象代表一个异步操作，有三种状态：`pending`（进行中）、`fulfilled`（已成功）和
>
> `rejected`（已失败）。

（2）一旦状态改变，就不会再变，任何时候都可以得到这个结果。

> `Promise`对象的状态改变，只有两种可能：从`pending`变为`fulfilled`和从`pending`变为
>
> `rejected`。只要这两种情况发生，状态就凝固了，不会再变了，会一直保持这个结果，这时就称为 resolved（已定型）。

## 12.1、基本用法：

下面代码创造了一个`Promise`实例。

```js
const promise = new Promise(function(resolve, reject) {
  // ... some code
  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
```

`resolve`函数的作用是，将`Promise`对象的状态从“未完成”变为“成功”（即从 pending 变为 resolved）。

`reject`函数的作用是，将`Promise`对象的状态从“未完成”变为“失败”（即从 pending 变为 rejected）。

------------------------------------------------------------------------------------------------------

```js
promise.then(function(value) {
  // success
}, function(error) {
  // failure
});
```

`Promise`实例生成以后，可以用`then`方法分别指定`resolved`状态和`rejected`状态的回调函数。

------

下面是一个用`Promise`对象实现的 Ajax 操作的例子。

```js
const getJSON = function(url) {
  const promise = new Promise(function(resolve, reject){
    const handler = function() {
      if (this.readyState !== 4) {
        return;
      }
      if (this.status === 200) {
        resolve(this.response);
      } else {
        reject(new Error(this.statusText));
      }
    };
    const client = new XMLHttpRequest();
    client.open("GET", url);
    client.onreadystatechange = handler;
    client.responseType = "json";
    client.setRequestHeader("Accept", "application/json");
    client.send();

  });
  return promise;
};
// ------- 请求 --------------------------
getJSON("/posts.json").then(function(json) {
  console.log('Contents: ' + json);
}, function(error) {
  console.error('出错了', error);
});
```

上面代码中，`getJSON`是对 XMLHttpRequest 对象的封装，用于发出一个针对 JSON 数据的 HTTP 请求，并且返回一个`Promise`对象。



# 13 Iterator 和 for...of 循环



## 13.1、 iterator 

- 通过 Symbol.iterator 创建一个`迭代器`，指向当前`数据结构的起始位置`
- 随后通过 `next` 方法进行向下迭代指向下一个位置， `next `方法会返回当前位置的对象，对象包含了` value `和 `done` 两个属性， `value` 是当前属性的值， `done` 用于判断是否遍历结束
- 当 `done` 为 `true` 时则遍历结束。

下面通过一个简单的例子进行说明：

```js
const items = ["zero", "one", "two"];
const it = items[Symbol.iterator]();

console.log(it.next()) 
>{value: "zero", done: false}
console.log(it.next())
>{value: "one", done: false}
console.log(it.next())
>{value: "two", done: false}
console.log(it.next())
>{value: undefined, done: true}
```

## 13.2、for ...of 循环

ES6 借鉴 C++、Java、C# 和 Python 语言，引入了`for...of`循环，作为遍历所有数据结构的统一的方法。

`for...of`循环可以使用的范围包括数组、`Set 和 Map` 结构、某些类似数组的对象（比如`arguments`对象、DOM NodeList 对象）、后文的 Generator 对象，以及字符串。

遍历数组的例子：还可以遍历对象形式的键值对 可以去`常用.md`文件去查看`for of`

```js
var arr = ['nick','freddy','mike','james'];
for(var item of arr){	
    console.log(item);
    // 输出结果：nick
     //       freddy
      //      mike
        //    james
}
```





# 14、Generator 函数:

> Generator 函数是 ES6 提供的一种异步编程解决方案，语法行为与传统函数完全不同。

## 14.1`Generator `有两个区分于普通函数的部分：



> - 一是在`function `后面，函数名之前有个` * `；
> - 函数内部有` yield` 表达式。

其中 `* `用来表示函数为 Generator 函数，`yield` 用来定义函数内部的状态。

```js
function* func(){
 console.log("one");
 yield '1';
 console.log("two");
 yield '2'; 
 console.log("three");
 return '3';
}
```

### 执行机制

调用 Generator 函数和调用普通函数一样，在函数名后面加上()即可，但是 Generator 函数不会像普通函数一样立即执行，而是返回一个指向内部状态对象的指针.

（以下代码：依次调用 函数内部的状态 ）

```js
f.next();
// one
// {value: "1", done: false}
f.next();
// two
// {value: "2", done: false}
f.next();
// three
// {value: "3", done: true}
f.next();
// {value: undefined, done: true}
```



# 15、Generator 函数的异步应用

## 传统方法

ES6 诞生以前，异步编程的方法，大概有下面四种。

- 回调函数  -- 最常见
- 事件监听
- 发布/订阅
- Promise 对象

Generator 函数将 JavaScript 异步编程带入了一个全新的阶段。

## 基本概念

### `异步`

所谓"异步"，简单说就是一个任务不是连续完成的，可以理解成`该任务`被人为`分成两段`，先执行第一段，然后转而执行其他任务，等做好了准备，再回过头执行第二段。

### `同步`

相应地，连续的执行就叫做同步。由于是连续执行，不能插入其他任务，所以操作系统从硬盘读取文件的这段时间，程序只能干等着。

## 15.1、协程的 Generator 函数实现

### `协程`

`协程`有点像函数，又有点像线程。它的运行流程大致如下。

- 第一步，协程`A`开始执行。
- 第二步，协程`A`执行到一半，进入暂停，执行权转移到协程`B`。
- 第三步，（一段时间后）协程`B`交还执行权。
- 第四步，协程`A`恢复执行。

上面流程的协程`A`，就是异步任务，因为它分成两段（或多段）执行。

```js
function* gen(x) {
  var y = yield x + 2;
  return y;
}

var g = gen(1);
g.next() // { value: 3, done: false }
g.next() // { value: undefined, done: true }
```

上面代码中，调用 `Generator` 函数，会返回一个内部指针（即遍历器）`g`。这是 Generator 函数不同于普通函数的另一个地方，即执行它不会返回结果，返回的是指针对象。调用指针`g`的`next`方法，会移动内部指针（即执行异步任务的第一段），`指向第一个`遇到的`yield`语句，上例是执行到`x + 2`为止。



# 16、async 函数

## 含义

ES2017 标准引入了 async 函数，使得异步操作变得更加方便。

async 函数是什么？一句话，它就是 Generator 函数的`语法糖`。

## 16.1 async基本用法：

`async`函数返回一个 Promise 对象，可以使用`then`方法添加回调函数。当函数执行的时候，一旦遇到`await`就会先返回，等到异步操作完成，再接着执行函数体内后面的语句。

```js
function testAwait(){
   return new Promise((resolve) => {
       setTimeout(function(){
          console.log("testAwait");
          resolve();
       }, 1000);
   });
}
 
async function helloAsync(){
   await testAwait(); //一旦遇到`await`就会先返回 表明这个是一个异步操作
   console.log("helloAsync");//异步执行完之后 在执行后面的语句
 }
helloAsync();
// testAwait
// helloAsync
```

函数前面的`async`关键字，表明该函数内部有异步操作。调用该函数时，会立即返回一个`Promise`对象。



# 17、class 类

ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，作为对象的模板。通过`class`关键字，可以定义类。

基本上，ES6 的`class`可以看作只是一个`语法糖`，它的绝大部分功能，ES5 都可以做到，新的`class`写法只是让对象原型的写法更加清晰、`更像面向对象编程`的语法而已。

基本的 面向对象：

```js
function Point(x, y) {
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
};

var p = new Point(1, 2);
```

class 类 语法糖：

```js
class Point { //像不像css 的 class 命名
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
```

上面代码定义了一个“类”，可以看到里面有一个`constructor()`方法，这就是构造方法，而`this`关键字则代表实例对象。

`Point`类除了构造方法，还定义了一个`toString()`方法。注意，定义`toString()`方法的时候，前面不需要加上`function`这个关键字，直接把函数定义放进去了就可以了。另外，方法与方法之间不需要逗号分隔，加了会报错。

## 17.2 class 类的 继承

Class 可以通过`extends`关键字实现继承，这比 ES5 的通过修改原型链实现继承，要清晰和方便很多。

简单例子：

```js
   class Point {  //父类
      constructor(name, age) {
        this.name = name;
        this.age = age;
      }
      sayName(){
            console.log(this.name);
        }
    }

    class ColorPoint extends Point {// 子类 ColorPoint 继承 Point父类
      constructor(x, y, color) {
        super(x, y); // 调用父类的constructor(x, y)
        this.color = color;
      };
      toString() {
        return this.color; 
      }
      sayName(){
        super.sayName();//调用父类的方法，name是 tcy
        console.log(this.name) //tcy
      }
    }
    var worker = new ColorPoint('tcy', 20, 'teacher');
    console.log(worker.toString()) //调用子类里的toString 方法  输出 teacher
    worker.sayName() //调用子类的sayName方法
```

上面代码中，`constructor`方法和`sayName`方法之中，都出现了`super`关键字，它在这里表示父类的构造函数，用来新建父类的`this`对象。

# 18、Module 的语法（模块、组件）

> ES6 模块不是对象，而是通过`export`命令显式指定输出的代码，再通过`import`命令输入。

## 18.1、export 命令：

模块功能主要由两个命令构成：`export`和`import`。

`export`命令用于规定模块的对外接口，`import`命令用于输入其他模块提供的功能。

列子：list.js

```js
var listname = '吴海东'
var listage = '男'
var listphone = '18511111111'
export {listname,listage,listphone}
```



## 18.2 imput 命令：

使用`export`命令定义了模块的对外接口以后，其他 JS 文件就可以通过`import`命令加载这个模块。

列子：

lindex.js

```js
import {listname,listage,listphone} from './list.js'

console.log(listname) //吴海东
console.log(listage)//男
console.log(listphone)//18511111111
```

## 18.3 在html 执行 Module  模块语法：

注意执行 `Module ` 模块语法，必须在服务器环境下 语法才会执行。所以`HBuilder X`是很好的选择。

在index.html:  

```html
<script type="module" src="./js/idnex.js"></script>
```

注意 在使用  `Module`  模块语法 时 type 类型必须更改成 module 类型。不然会报错


