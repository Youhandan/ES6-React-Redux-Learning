# ES6-React-Redux-Learning
##ES6
###ES6的6种声明变量方法
1. var
2. function
3. let 只在声明所在的块级作用域内有效；声明的常量不提升，存在暂时性死区，只能在声明的位置后面使用；不可重复声明
4. const 声明的变量不得改变值，这意味着，const一旦声明变量，就必须立即初始化；只在声明所在的块级作用域内有效；声明的常量不提升，存在暂时性死区，只能在声明的位置后面使用；不可重复声明
5. import
6. class

###解构的用途

1.交换变量的值
```
[x, y] = [y, x]
```
上面代码交换变量x和y的值，这样的写法不仅简洁，而且易读，语义非常清晰。

2.从函数返回多个值  
函数只能返回一个值，如果要返回多个值，只能将它们放在数组或对象里返回。有了解构赋值，取出这些值就非常方便。

```
// 返回一个数组

function example() {
  return [1, 2, 3];
}
var [a, b, c] = example();

// 返回一个对象

function example() {
  return {
    foo: 1,
    bar: 2
  };
}
var { foo, bar } = example();

```
3.函数参数的定义  
解构赋值可以方便地将一组参数与变量名对应起来。

```
// 参数是一组有次序的值
function f([x, y, z]) { ... }
f([1, 2, 3]);

// 参数是一组无次序的值
function f({x, y, z}) { ... }
f({z: 3, y: 2, x: 1});
```

4.提取JSON数据  
解构赋值对提取JSON对象中的数据，尤其有用。

```
var jsonData = {
  id: 42,
  status: "OK",
  data: [867, 5309]
};

let { id, status, data: number } = jsonData;

console.log(id, status, number);
// 42, "OK", [867, 5309]
上面代码可以快速提取JSON数据的值。
```

5.函数参数的默认值

```
jQuery.ajax = function (url, {
  async = true,
  beforeSend = function () {},
  cache = true,
  complete = function () {},
  crossDomain = false,
  global = true,
  // ... more config
}) {
  // ... do stuff
};
```  
指定参数的默认值，就避免了在函数体内部再写var foo = config.foo || 'default foo';这样的语句。

6.遍历Map结构  
任何部署了Iterator接口的对象，都可以用for...of循环遍历。Map结构原生支持Iterator接口，配合变量的解构赋值，获取键名和键值就非常方便。

```
var map = new Map();
map.set('first', 'hello');
map.set('second', 'world');

for (let [key, value] of map) {
  console.log(key + " is " + value);
}
// first is hello
// second is world
如果只想获取键名，或者只想获取键值，可以写成下面这样。

// 获取键名
for (let [key] of map) {
  // ...
}

// 获取键值
for (let [,value] of map) {
  // ...
}
```

7.输入模块的指定方法  
加载模块时，往往需要指定输入那些方法。解构赋值使得输入语句非常清晰。

```
const { SourceMapConsumer, SourceNode } = require("source-map");
```

###字符串的扩展
1. 字符的Unicode表示法，codePointAt()，String.fromCodePoint()，字符串的遍历器接口，at()均为解决Unicode编号大于0xFFFF的字符。字符串的遍历器接口使得字符串可以被for...of循环遍历。
2. includes(), startsWith(), endsWith()，用于确定一个字符串是否包含在另一个字符串中，三个方法均匀以String实例为调用对象，返回值为布尔。
3. repeat()方法返回一个新字符串，表示将原字符串重复n次；参数如果是小数，会被取整；参数NaN等同于0；如果repeat的参数是字符串，则会先转换成数字。
4. padStart()，padEnd()，ES7推出了字符串补全长度的功能。如果某个字符串不够指定长度，会在头部或尾部补全。padStart用于头部补全，padEnd用于尾部补全。padStart和padEnd一共接受两个参数，第一个参数用来指定字符串的最小长度，第二个参数是用来补全的字符串。padStart的常见用途是为数值补全指定位数，提示字符串格式。  

```
'12'.padStart(10, 'YYYY-MM-DD') // "YYYY-MM-12"
'09-12'.padStart(10, 'YYYY-MM-DD') // "YYYY-09-12"
```
5.模板字符串。模板字符串（template string）是增强版的字符串，用反引号标识。模板字符串中嵌入变量，需要将变量名写在${}之中。

###正则的扩展  

1.RegExp.escape()  
字符串转义以后，可以使用RegExp构造函数生成正则模式。

```
var str = 'hello. how are you?';
var regex = new RegExp(RegExp.escape(str), 'g');
assert.equal(String(regex), '/hello\. how are you\?/g');
```

###数值扩展

1.指数运算符。ES7新增了一个指数运算符（**），目前Babel转码器已经支持

```
2 ** 2 // 4  
2 ** 3 // 8
```
2.Math对象的扩展  
（1）Math.trunc()  
    Math.trunc方法用于去除一个数的小数部分，返回整数部分。  
（2）Math.sign()  
    Math.sign方法用来判断一个数到底是正数、负数、还是零。  
    它会返回五种值。
       
    - 参数为正数，返回+1；
    - 参数为负数，返回-1；
    - 参数为0，返回0；
    - 参数为-0，返回-0;
    - 其他值，返回NaN。
（3）Math.cbrt()  
   Math.cbrt方法用于计算一个数的立方根。
（4）Math.hypot()  
    Math.hypot方法返回所有参数的平方和的平方根。
    
    Math.hypot(3, 4);        // 5
    Math.hypot(3, 4, 5);     // 7.0710678118654755
（5）Math.expm1()  
   Math.expm1(x)返回ex - 1，即Math.exp(x) - 1。
（6）Math.log1p()  
   Math.log1p(x)方法返回1 + x的自然对数，即Math.log(1 + x)。如果x小于-1，返回NaN。
（7）Math.log10()  
   Math.log10(x)返回以10为底的x的对数。如果x小于0，则返回NaN。
（8）Math.log2()   
   Math.log2(x)返回以2为底的x的对数。如果x小于0，则返回NaN。
（9）三角函数方法
   ES6新增了6个三角函数方法。  
   Math.sinh(x) 返回x的双曲正弦（hyperbolic sine）  
   Math.cosh(x) 返回x的双曲余弦（hyperbolic cosine）  
   Math.tanh(x) 返回x的双曲正切（hyperbolic tangent）  
   Math.asinh(x) 返回x的反双曲正弦（inverse hyperbolic sine）  
   Math.acosh(x) 返回x的反双曲余弦（inverse hyperbolic cosine）  
   Math.atanh(x) 返回x的反双曲正切（inverse hyperbolic tangent）  
3.二进制和八进制表示法  
  ES6提供了二进制和八进制数值的新的写法，分别用前缀0b（或0B）和0o（或0O）表示。  
4.Number.isFinite(), Number.isNaN()  
  ES6在Number对象上，新提供了Number.isFinite()和Number.isNaN()两个方法。  
5.Number.parseInt(), Number.parseFloat()  
  ES6将全局方法parseInt()和parseFloat()，移植到Number对象上面，行为完全保持不变。  
6.Number.isInteger()  
  Number.isInteger()用来判断一个值是否为整数。需要注意的是，在JavaScript内部，整数和浮点数是同样的储存方法，所以3和3.0被视为同一个值。  

###数组的扩展
1.Array.from()  
   Array.from方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括ES6新增的数据结构Set和Map）。

2.Array.of()  
   Array.of方法用于将一组值，转换为数组。
   
```   
   Array.of(3, 11, 8) // [3,11,8]
   Array.of(3) // [3]
   Array.of(3).length // 1
```

3.数组实例的copyWithin()  
   数组实例的copyWithin方法，在当前数组内部，将指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组。也就是说，使用这个方法，会修改当前数组。
   `Array.prototype.copyWithin(target, start = 0, end = this.length)`
   它接受三个参数。
   
   target（必需）：从该位置开始替换数据。
   start（可选）：从该位置开始读取数据，默认为0。如果为负值，表示倒数。
   end（可选）：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示倒数。  
   
4.数组实例的find()和findIndex()  
数组实例的find方法，用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为true的成员，然后返回该成员。如果没有符合条件的成员，则返回undefined。  
数组实例的findIndex方法的用法与find方法非常类似，返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回-1。  
另外，这两个方法都可以发现NaN，弥补了数组的IndexOf方法的不足。

```
[NaN].indexOf(NaN)
// -1

[NaN].findIndex(y => Object.is(NaN, y))
// 0
上面代码中，indexOf方法无法识别数组的NaN成员，但是findIndex方法可以借助Object.is方法做到。
```

5.数组实例的fill()
  fill方法使用给定值，填充一个数组。
  
```  
  ['a', 'b', 'c'].fill(7)
  // [7, 7, 7]
  
  new Array(3).fill(7)
  // [7, 7, 7]
```
  上面代码表明，fill方法用于空数组的初始化非常方便。数组中已有的元素，会被全部抹去。
  
  fill方法还可以接受第二个和第三个参数，用于指定填充的起始位置和结束位置。
  
  ```
  ['a', 'b', 'c'].fill(7, 1, 2)
  // ['a', 7, 'c']
  ```
  
  上面代码表示，fill方法从1号位开始，向原数组填充7，到2号位之前结束。
  
6.数组实例的entries()，keys()和values()
  ES6提供三个新的方法——entries()，keys()和values()——用于遍历数组。它们都返回一个遍历器对象（详见《Iterator》一章），可以用for...of循环进行遍历，唯一的区别是keys()是对键名的遍历、values()是对键值的遍历，entries()是对键值对的遍历。
  
  ```
  for (let index of ['a', 'b'].keys()) {
    console.log(index);
  }
  // 0
  // 1
  
  for (let elem of ['a', 'b'].values()) {
    console.log(elem);
  }
  // 'a'
  // 'b'
  
  for (let [index, elem] of ['a', 'b'].entries()) {
    console.log(index, elem);
  }
  // 0 "a"
  // 1 "b"
  ```

7.数组实例的includes()
  Array.prototype.includes方法返回一个布尔值，表示某个数组是否包含给定的值，与字符串的includes方法类似。该方法属于ES7，但Babel转码器已经支持。
  
  ```
  [1, 2, 3].includes(2);     // true
  [1, 2, 3].includes(4);     // false
  [1, 2, NaN].includes(NaN); // true
  ```
  该方法的第二个参数表示搜索的起始位置，默认为0。如果第二个参数为负数，则表示倒数的位置，如果这时它大于数组长度（比如第二个参数为-4，但数组长度为3），则会重置为从0开始。
  
  ```
  [1, 2, 3].includes(3, 3);  // false
  [1, 2, 3].includes(3, -1); // true
  ```
8.ES6则是明确将空位转为undefined。

###函数扩展
1.函数参数的默认值  
应用  
利用参数默认值，可以指定某一个参数不得省略，如果省略就抛出一个错误。

````
function throwIfMissing() {
  throw new Error('Missing parameter');
}

function foo(mustBeProvided = throwIfMissing()) {
  return mustBeProvided;
}

foo()
// Error: Missing parameter
````
上面代码的foo函数，如果调用的时候没有参数，就会调用默认值throwIfMissing函数，从而抛出一个错误。
从上面代码还可以看到，参数mustBeProvided的默认值等于throwIfMissing函数的运行结果（即函数名之后有一对圆括号），这表明参数的默认值不是在定义时执行，而是在运行时执行（即如果参数已经赋值，默认值中的函数就不会运行）。
另外，可以将参数默认值设为undefined，表明这个参数是可以省略的。

````
function foo(optional = undefined) { ··· }
````

2.rest参数  
  ES6引入rest参数（形式为“...变量名”），用于获取函数的多余参数，这样就不需要使用arguments对象了。rest参数搭配的变量是一个数组，该变量将多余的参数放入数组中。  
下面是一个rest参数代替arguments变量的例子。

````
// arguments变量的写法
function sortNumbers() {
  return Array.prototype.slice.call(arguments).sort();
}

// rest参数的写法
const sortNumbers = (...numbers) => numbers.sort();

````
**注意，rest参数之后不能再有其他参数（即只能是最后一个参数），否则会报错。**  
函数的length属性，不包括rest参数。

````
(function(a) {}).length  // 1
(function(...a) {}).length  // 0
(function(a, ...b) {}).length  // 1
````

3.扩展运算符  
  含义  
  扩展运算符（spread）是三个点（...）。它好比rest参数的逆运算，将一个数组转为用逗号分隔的参数序列。  
  该运算符主要用于函数调用。
  
  ````
  function push(array, ...items) {
    array.push(...items);
  }
  
  function add(x, y) {
    return x + y;
  }
  
  var numbers = [4, 38];
  add(...numbers) // 42
  ````
  
**替代数组的apply方法**  
由于扩展运算符可以展开数组，所以不再需要apply方法，将数组转为函数的参数了。  
  一个例子是通过push函数，将一个数组添加到另一个数组的尾部。
  
  ````
  // ES5的写法
  var arr1 = [0, 1, 2];
  var arr2 = [3, 4, 5];
  Array.prototype.push.apply(arr1, arr2);
  
  // ES6的写法
  var arr1 = [0, 1, 2];
  var arr2 = [3, 4, 5];
  arr1.push(...arr2);
  ````
**扩展运算符的应用**  
（1）合并数组，扩展运算符提供了数组合并的新写法。

````
var arr1 = ['a', 'b'];
var arr2 = ['c'];
var arr3 = ['d', 'e'];
// ES5的合并数组
arr1.concat(arr2, arr3);
// [ 'a', 'b', 'c', 'd', 'e' ]

// ES6的合并数组
[...arr1, ...arr2, ...arr3]
// [ 'a', 'b', 'c', 'd', 'e' ]
````
（2）与解构赋值结合，扩展运算符可以与解构赋值结合起来，用于生成数组。

````
const [first, ...rest] = [1, 2, 3, 4, 5];
first // 1
rest  // [2, 3, 4, 5]
````
**如果将扩展运算符用于数组赋值，只能放在参数的最后一位，否则会报错。**  
（3）函数的返回值，JavaScript的函数只能返回一个值，如果需要返回多个值，只能返回数组或对象。扩展运算符提供了解决这个问题的一种变通方法。

```
var dateFields = readDateFields(database);
var d = new Date(...dateFields);
```
上面代码从数据库取出一行数据，通过扩展运算符，直接将其传入构造函数Date。  
（4）字符串，扩展运算符还可以将字符串转为真正的数组。

````
[...'hello']
// [ "h", "e", "l", "l", "o" ]
````
上面的写法，有一个重要的好处，那就是能够正确识别32位的Unicode字符。  
（5）实现了Iterator接口的对象，任何Iterator接口的对象，都可以用扩展运算符转为真正的数组。

````
var nodeList = document.querySelectorAll('div');
var array = [...nodeList];
````
上面代码中，querySelectorAll方法返回的是一个nodeList对象。它不是数组，而是一个类似数组的对象。这时，扩展运算符可以将其转为真正的数组，原因就在于NodeList对象实现了Iterator接口。  
对于那些没有部署Iterator接口的类似数组的对象，扩展运算符就无法将其转为真正的数组。

````
let arrayLike = {
  '0': 'a',
  '1': 'b',
  '2': 'c',
  length: 3
};

// TypeError: Cannot spread non-iterable object.
let arr = [...arrayLike];
````
上面代码中，arrayLike是一个类似数组的对象，但是没有部署Iterator接口，扩展运算符就会报错。这时，可以改为使用Array.from方法将arrayLike转为真正的数组。  
（6）Map和Set结构，Generator函数，扩展运算符内部调用的是数据结构的Iterator接口，因此只要具有Iterator接口的对象，都可以使用扩展运算符，比如Map结构。

````
let map = new Map([
  [1, 'one'],
  [2, 'two'],
  [3, 'three'],
]);

let arr = [...map.keys()]; // [1, 2, 3]
````
Generator函数运行后，返回一个遍历器对象，因此也可以使用扩展运算符。

````
var go = function*(){
  yield 1;
  yield 2;
  yield 3;
};

[...go()] // [1, 2, 3]
````
上面代码中，变量go是一个Generator函数，执行后返回的是一个遍历器对象，对这个遍历器对象执行扩展运算符，就会将内部遍历得到的值，转为一个数组。
如果对没有iterator接口的对象，使用扩展运算符，将会报错。  

4.name属性  
函数的name属性，返回该函数的函数名。

````
function foo() {}
foo.name // "foo"
````

5.箭头函数  
**基本用法**  
ES6允许使用“箭头”（=>）定义函数。  

````
var f = () => 5;
// 等同于
var f = function () { return 5 };

var sum = (num1, num2) => num1 + num2;
// 等同于
var sum = function(num1, num2) {
  return num1 + num2;
};

````
**如果箭头函数的代码块部分多于一条语句，就要使用大括号将它们括起来，并且使用return语句返回。**

`var sum = (num1, num2) => { return num1 + num2; }`
**由于大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上括号。**
`var getTempItem = id => ({ id: id, name: "Temp" });`

**箭头函数可以与变量解构结合使用。**

```
const full = ({ first, last }) => first + ' ' + last;

// 等同于
function full(person) {
  return person.first + ' ' + person.last;
}
```
**rest参数与箭头函数结合的例子。**

```
const numbers = (...nums) => nums;
numbers(1, 2, 3, 4, 5)
// [1,2,3,4,5]
const headAndTail = (head, ...tail) => [head, tail];
headAndTail(1, 2, 3, 4, 5)
// [1,[2,3,4,5]]
```
**使用注意点**
箭头函数有几个使用注意点。  
（1）函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。  
（2）不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。  
（3）不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用Rest参数代替。  
（4）不可以使用yield命令，因此箭头函数不能用作Generator函数。  

**嵌套的箭头函数**
箭头函数内部，还可以再使用箭头函数。下面是一个ES5语法的多重嵌套函数。

````
function insert(value) {
  return {into: function (array) {
    return {after: function (afterValue) {
      array.splice(array.indexOf(afterValue) + 1, 0, value);
      return array;
    }};
  }};
}

insert(2).into([1, 3]).after(1); //[1, 2, 3]
````
上面这个函数，可以使用箭头函数改写。

````
let insert = (value) => ({into: (array) => ({after: (afterValue) => {
  array.splice(array.indexOf(afterValue) + 1, 0, value);
  return array;
}})});

insert(2).into([1, 3]).after(1); //[1, 2, 3]
````

6.绑定this
函数绑定运算符是并排的两个双冒号（::），双冒号左边是一个对象，右边是一个函数。该运算符会自动将左边的对象，作为上下文环境（即this对象），绑定到右边的函数上面。

````
foo::bar;
// 等同于
bar.bind(foo);

foo::bar(...arguments);
// 等同于
bar.apply(foo, arguments);

const hasOwnProperty = Object.prototype.hasOwnProperty;
function hasOwn(obj, key) {
  return obj::hasOwnProperty(key);
}
````
如果双冒号左边为空，右边是一个对象的方法，则等于将该方法绑定在该对象上面。

````
var method = obj::obj.foo;
// 等同于
var method = ::obj.foo;

let log = ::console.log;
// 等同于
var log = console.log.bind(console);
````
由于双冒号运算符返回的还是原对象，因此可以采用链式写法。

````
// 例一
import { map, takeWhile, forEach } from "iterlib";

getPlayers()
::map(x => x.character())
::takeWhile(x => x.strength > 100)
::forEach(x => console.log(x));

// 例二
let { find, html } = jake;

document.querySelectorAll("div.myClass")
::find("p")
````

7.尾调用优化（难，以后需要再看）  

###对象的扩展

1.属性的简洁表达  
如果某个方法的值是一个Generator函数，前面需要加上星号。 
 
````
var obj = {
  * m(){
    yield 'hello world';
  }
};
````  
2.属性名表达式  
注意，属性名表达式与简洁表示法，不能同时使用，会报错。  

``````
// 报错
var foo = 'bar';
var bar = 'abc';
var baz = { [foo] };
// 正确
var foo = 'bar';
var baz = { [foo]: 'abc'};
``````

3.方法的name属性  
有两种特殊情况：bind方法创造的函数，name属性返回“bound”加上原函数的名字；Function构造函数创造的函数，name属性返回“anonymous”。
  
````
(new Function()).name // "anonymous"

var doSomething = function() {
  // ...
};
doSomething.bind().name // "bound doSomething"
````

4.Object.is()   

```
+0 === -0 //true
NaN === NaN // false

Object.is(+0, -0) // false
Object.is(NaN, NaN) // true
```
5.Object.assign() 
Object.assign方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。

````
var target = { a: 1 };

var source1 = { b: 2 };
var source2 = { c: 3 };

Object.assign(target, source1, source2);
target // {a:1, b:2, c:3}
Object.assign方法的第一个参数是目标对象，后面的参数都是源对象。
````
注意，如果目标对象与源对象有同名属性，或多个源对象有同名属性，则后面的属性会覆盖前面的属性。

6.属性的遍历  
ES6一共有5种方法可以遍历对象的属性。

（1）for...in

for...in循环遍历对象自身的和继承的可枚举属性（不含Symbol属性）。

（2）Object.keys(obj)

Object.keys返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含Symbol属性）。

（3）Object.getOwnPropertyNames(obj)

Object.getOwnPropertyNames返回一个数组，包含对象自身的所有属性（不含Symbol属性，但是包括不可枚举属性）。

（4）Object.getOwnPropertySymbols(obj)

Object.getOwnPropertySymbols返回一个数组，包含对象自身的所有Symbol属性。

（5）Reflect.ownKeys(obj)

Reflect.ownKeys返回一个数组，包含对象自身的所有属性，不管是属性名是Symbol或字符串，也不管是否可枚举。

以上的5种方法遍历对象的属性，都遵守同样的属性遍历的次序规则。

- 首先遍历所有属性名为数值的属性，按照数字排序。
- 其次遍历所有属性名为字符串的属性，按照生成时间排序。
- 最后遍历所有属性名为Symbol值的属性，按照生成时间排序。

```
Reflect.ownKeys({ [Symbol()]:0, b:0, 10:0, 2:0, a:0 })
// ['2', '10', 'b', 'a', Symbol()]
```
上面代码中，Reflect.ownKeys方法返回一个数组，包含了参数对象的所有属性。这个数组的属性次序是这样的，首先是数值属性2和10，其次是字符串属性b和a，最后是Symbol属性。

7.Object.values()，Object.entries()   
8.对象的扩展运算符  
目前，ES7有一个提案，将Rest运算符（解构赋值）/扩展运算符（...）引入对象。Babel转码器已经支持这项功能。

###Set和Map数据结构
1.Set  

**基本用法**  

ES6提供了新的数据结构Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。Set本身是一个构造函数，用来生成Set数据结构。  

Set内部判断两个值是否不同，使用的算法叫做“Same-value equality”，它类似于精确相等运算符（===），主要的区别是NaN等于自身，而精确相等运算符认为NaN不等于自身。

另外，两个对象总是不相等的。  

这就提供了去除数组重复成员的另一种方法。

```
function dedupe(array) {
  return Array.from(new Set(array));
}

dedupe([1, 1, 2, 3]) // [1, 2, 3]
```

**Set实例的属性和方法**  

Set结构的实例有以下属性。

- Set.prototype.constructor：构造函数，默认就是Set函数。
- Set.prototype.size：返回Set实例的成员总数。  

Set实例的方法分为两大类：*操作方法（用于操作数据）*和*遍历方法（用于遍历成员）*。下面先介绍四个操作方法。

- add(value)：添加某个值，返回Set结构本身。
- delete(value)：删除某个值，返回一个布尔值，表示删除是否成功。
- has(value)：返回一个布尔值，表示该值是否为Set的成员。
- clear()：清除所有成员，没有返回值。

**遍历操作**

Set结构的实例有四个遍历方法，可以用于遍历成员。

- keys()：返回键名的遍历器
- values()：返回键值的遍历器
- entries()：返回键值对的遍历器
- forEach()：使用回调函数遍历每个成员  

需要特别指出的是，Set的遍历顺序就是插入顺序。这个特性有时非常有用，比如使用Set保存一个回调函数列表，调用时就能保证按照添加顺序调用。   

2.WeakSet    

WeakSet结构与Set类似，也是不重复的值的集合。但是，它与Set有两个区别。

首先，WeakSet的成员只能是对象，而不能是其他类型的值。

其次，WeakSet中的对象都是弱引用，即垃圾回收机制不考虑WeakSet对该对象的引用，也就是说，如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于WeakSet之中。这个特点意味着，无法引用WeakSet的成员，因此WeakSet是不可遍历的。

WeakSet的一个用处，是储存DOM节点，而不用担心这些节点从文档移除时，会引发内存泄漏。

3.Map

**实例的属性和操作方法**

(1）size属性

size属性返回Map结构的成员总数。

```
let map = new Map();
map.set('foo', true);
map.set('bar', false);

map.size // 2
```
（2）set(key, value)

set方法设置key所对应的键值，然后返回整个Map结构。如果key已经有值，则键值会被更新，否则就新生成该键。

```
var m = new Map();

m.set("edition", 6)        // 键是字符串
m.set(262, "standard")     // 键是数值
m.set(undefined, "nah")    // 键是undefined
```
set方法返回的是Map本身，因此可以采用链式写法。

```
let map = new Map()
  .set(1, 'a')
  .set(2, 'b')
  .set(3, 'c');
```
（3）get(key)

get方法读取key对应的键值，如果找不到key，返回undefined。

```
var m = new Map();

var hello = function() {console.log("hello");}
m.set(hello, "Hello ES6!") // 键是函数

m.get(hello)  // Hello ES6!
```
（4）has(key)

has方法返回一个布尔值，表示某个键是否在Map数据结构中。

```
var m = new Map();

m.set("edition", 6);
m.set(262, "standard");
m.set(undefined, "nah");

m.has("edition")     // true
m.has("years")       // false
m.has(262)           // true
m.has(undefined)     // true
```
（5）delete(key)

delete方法删除某个键，返回true。如果删除失败，返回false。

```
var m = new Map();
m.set(undefined, "nah");
m.has(undefined)     // true

m.delete(undefined)
m.has(undefined)       // false
```
（6）clear()

clear方法清除所有成员，没有返回值。

```
let map = new Map();
map.set('foo', true);
map.set('bar', false);

map.size // 2
map.clear()
map.size // 0 
```

**遍历方法**

- keys()：返回键名的遍历器。
- values()：返回键值的遍历器。
- entries()：返回所有成员的遍历器。
- forEach()：遍历Map的所有成员。
 
**与其他数据结构的互相转换**  

（1）Map转为数组

前面已经提过，Map转为数组最方便的方法，就是使用扩展运算符（...）。

```
let myMap = new Map().set(true, 7).set({foo: 3}, ['abc']);
[...myMap]
// [ [ true, 7 ], [ { foo: 3 }, [ 'abc' ] ] ]
```
（2）数组转为Map

将数组转入Map构造函数，就可以转为Map。

```
new Map([[true, 7], [{foo: 3}, ['abc']]])
// Map {true => 7, Object {foo: 3} => ['abc']}
```
（3）Map转为对象

如果所有Map的键都是字符串，它可以转为对象。

```
function strMapToObj(strMap) {
  let obj = Object.create(null);
  for (let [k,v] of strMap) {
    obj[k] = v;
  }
  return obj;
}

let myMap = new Map().set('yes', true).set('no', false);
strMapToObj(myMap)
// { yes: true, no: false }
```
（4）对象转为Map

```
function objToStrMap(obj) {
  let strMap = new Map();
  for (let k of Object.keys(obj)) {
    strMap.set(k, obj[k]);
  }
  return strMap;
}

objToStrMap({yes: true, no: false})
// [ [ 'yes', true ], [ 'no', false ] ]
```
（5）Map转为JSON

Map转为JSON要区分两种情况。一种情况是，Map的键名都是字符串，这时可以选择转为对象JSON。

```
function strMapToJson(strMap) {
  return JSON.stringify(strMapToObj(strMap));
}

let myMap = new Map().set('yes', true).set('no', false);
strMapToJson(myMap)
// '{"yes":true,"no":false}'
```
另一种情况是，Map的键名有非字符串，这时可以选择转为数组JSON。

```
function mapToArrayJson(map) {
  return JSON.stringify([...map]);
}

let myMap = new Map().set(true, 7).set({foo: 3}, ['abc']);
mapToArrayJson(myMap)
// '[[true,7],[{"foo":3},["abc"]]]'
```
（6）JSON转为Map

JSON转为Map，正常情况下，所有键名都是字符串。

```
function jsonToStrMap(jsonStr) {
  return objToStrMap(JSON.parse(jsonStr));
}

jsonToStrMap('{"yes":true,"no":false}')
// Map {'yes' => true, 'no' => false}
```
但是，有一种特殊情况，整个JSON就是一个数组，且每个数组成员本身，又是一个有两个成员的数组。这时，它可以一一对应地转为Map。这往往是数组转为JSON的逆操作。

```
function jsonToMap(jsonStr) {
  return new Map(JSON.parse(jsonStr));
}

jsonToMap('[[true,7],[{"foo":3},["abc"]]]')
// Map {true => 7, Object {foo: 3} => ['abc']}
```

4.WeakMap  
WeakMap结构与Map结构基本类似，唯一的区别是它只接受对象作为键名（null除外），不接受其他类型的值作为键名，而且键名所指向的对象，不计入垃圾回收机制。

###Iterator 和 for... of 循环

1.Iterator遍历接口。Iterator的遍历过程是这样的。

（1）创建一个指针对象，指向当前数据结构的起始位置。也就是说，遍历器对象本质上，就是一个指针对象。  
（2）第一次调用指针对象的next方法，可以将指针指向数据结构的第一个成员。  
（3）第二次调用指针对象的next方法，指针就指向数据结构的第二个成员。  
（4）不断调用指针对象的next方法，直到它指向数据结构的结束位置。  

每一次调用next方法，都会返回数据结构的当前成员的信息。具体来说，就是返回一个包含value和done两个属性的对象。其中，value属性是当前成员的值，done属性是一个布尔值，表示遍历是否结束。

2.for ... of用于遍历具有Iterator的对象。

**for...in循环有几个缺。**

- 数组的键名是数字，但是for...in循环是以字符串作为键名“0”、“1”、“2”等等。
- for...in循环不仅遍历数字键名，还会遍历手动添加的其他键，甚至包括原型链上的键。
- 某些情况下，for...in循环会以任意顺序遍历键名。

总之，for...in循环主要是为遍历对象而设计的，不适用于遍历数组。

**for...of循环相比上面几种做法，有一些显著的优点**

```
for (let value of myArray) {
  console.log(value);
}
```
- 有着同for...in一样的简洁语法，但是没有for...in那些缺点。
- 不同用于forEach方法，它可以与break、continue和return配合使用。
- 提供了遍历所有数据结构的统一操作接口。

下面是一个使用break语句，跳出for...of循环的例子。

```
for (var n of fibonacci) {
  if (n > 1000)
    break;
  console.log(n);
}

```
上面的例子，会输出斐波纳契数列小于等于1000的项。如果当前项大于1000，就会使用break语句跳出for...of循环。

###Promise对象
####1.Promise的特点
1. 对象的状态不受外界影响。Promise对象代表一个异步操作，有三种状态：*Pending（进行中）*、*Resolved（已完成，又称Fulfilled）*和*Rejected（已失败）*。  

2. 一旦状态改变，就不会再变，任何时候都可以得到这个结果。Promise对象的状态改变，只有两种可能：从Pending变为Resolved和从Pending变为Rejected。

####2.基本用法 
ES6规定，Promise对象是一个构造函数，用来生成Promise实例。

下面代码创造了一个Promise实例。

````
var promise = new Promise(function(resolve, reject) {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
````
Promise构造函数接受一个函数作为参数，该函数的两个参数分别是resolve和reject。  

resolve函数的作用是，将Promise对象的状态从“未完成”变为“成功”（即从Pending变为Resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去；reject函数的作用是，将Promise对象的状态从“未完成”变为“失败”（即从Pending变为Rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

Promise实例生成以后，可以用then方法分别指定Resolved状态和Reject状态的回调函数。

下面是异步加载图片的例子。

````
function loadImageAsync(url) {
  return new Promise(function(resolve, reject) {
    var image = new Image();

    image.onload = function() {
      resolve(image);
    };

    image.onerror = function() {
      reject(new Error('Could not load image at ' + url));
    };

    image.src = url;
  });
}
````
上面代码中，使用Promise包装了一个图片加载的异步操作。如果加载成功，就调用resolve方法，否则就调用reject方法。

下面是一个用Promise对象实现的Ajax操作的例子。

````
var getJSON = function(url) {
  var promise = new Promise(function(resolve, reject){
    var client = new XMLHttpRequest(); client.open("GET", url);
    client.onreadystatechange = handler;
    client.responseType = "json";
    client.setRequestHeader("Accept", "application/json");
    client.send();

    function handler() {
      if (this.readyState !== 4) {
        return;
      }
      if (this.status === 200) {
        resolve(this.response);
      } else {
        reject(new Error(this.statusText));
      }
    };
  });

  return promise;
};

getJSON("/posts.json").then(function(json) {
  console.log('Contents: ' + json);
}, function(error) {
  console.error('出错了', error);
});
````
上面代码中，getJSON是对XMLHttpRequest对象的封装，用于发出一个针对JSON数据的HTTP请求，并且返回一个Promise对象。需要注意的是，在getJSON内部，resolve函数和reject函数调用时，都带有参数。

###异步操作和Async函数
####基本概念
#####Promise
回调函数本身并没有问题，它的问题出现在多个回调函数嵌套。假定读取A文件之后，再读取B文件，代码如下。

````
fs.readFile(fileA, function (err, data) {
  fs.readFile(fileB, function (err, data) {
    // ...
  });
});
````
不难想象，如果依次读取多个文件，就会出现多重嵌套。代码不是纵向发展，而是横向发展，很快就会乱成一团，无法管理。这种情况就称为"回调函数噩梦"（callback hell）。

Promise就是为了解决这个问题而提出的。它不是新的语法功能，而是一种新的写法，允许将回调函数的嵌套，改成链式调用。采用Promise，连续读取多个文件，写法如下。

````
var readFile = require('fs-readfile-promise');

readFile(fileA)
.then(function(data){
  console.log(data.toString());
})
.then(function(){
  return readFile(fileB);
})
.then(function(data){
  console.log(data.toString());
})
.catch(function(err) {
  console.log(err);
});
````
上面代码中，我使用了fs-readfile-promise模块，它的作用就是返回一个Promise版本的readFile函数。Promise提供then方法加载回调函数，catch方法捕捉执行过程中抛出的错误。

Promise 的最大问题是代码冗余，原来的任务被Promise 包装了一下，不管什么操作，一眼看去都是一堆 then，原来的语义变得很不清楚。

####Generator函数
协程
协程有点像函数，又有点像线程。它的运行流程大致如下。

1. 第一步，协程A开始执行。
2. 第二步，协程A执行到一半，进入暂停，执行权转移到协程B。
3. 第三步，（一段时间后）协程B交还执行权。
4. 第四步，协程A恢复执行。
上面流程的协程A，就是异步任务，因为它分成两段（或多段）执行。

举例来说，读取文件的协程写法如下。

```
function *asyncJob() {
  // ...其他代码
  var f = yield readFile(fileA);
  // ...其他代码
}
```
上面代码的函数asyncJob是一个协程，它的奥妙就在其中的yield命令。它表示执行到此处，执行权将交给其他协程。也就是说，yield命令是异步两个阶段的分界线。

协程遇到yield命令就暂停，等到执行权返回，再从暂停的地方继续往后执行。

####Thunk函数 
#####Thunk函数的含义
编译器的"传名调用"实现，往往是将参数放到一个临时函数之中，再将这个临时函数传入函数体。这个临时函数就叫做Thunk函数。

```
function f(m){
  return m * 2;
}

f(x + 5);

// 等同于

var thunk = function () {
  return x + 5;
};

function f(thunk){
  return thunk() * 2;
}
```
#####JavaScript语言的Thunk函数
avaScript语言是传值调用，它的Thunk函数含义有所不同。在JavaScript语言中，Thunk函数替换的不是表达式，而是**多参数函数**，将其替换成**单参数**的版本，且只接受回调函数作为参数。

````
// 正常版本的readFile（多参数版本）
fs.readFile(fileName, callback);

// Thunk版本的readFile（单参数版本）
var readFileThunk = Thunk(fileName);
readFileThunk(callback);

var Thunk = function (fileName){
  return function (callback){
    return fs.readFile(fileName, callback);
  };
};
````
上面代码中，fs模块的readFile方法是一个多参数函数，两个参数分别为文件名和回调函数。经过转换器处理，它变成了一个单参数函数，只接受回调函数作为参数。这个单参数版本，就叫做Thunk函数。

####async函数 
#####1.含义
S7提供了async函数，使得异步操作变得更加方便。async函数是什么？一句话，async函数就是Generator函数的语法糖。

前文有一个Generator函数，依次读取两个文件。

````
var fs = require('fs');

var readFile = function (fileName) {
  return new Promise(function (resolve, reject) {
    fs.readFile(fileName, function(error, data) {
      if (error) reject(error);
      resolve(data);
    });
  });
};

var gen = function* (){
  var f1 = yield readFile('/etc/fstab');
  var f2 = yield readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};
````
写成async函数，就是下面这样。

````
var asyncReadFile = async function (){
  var f1 = await readFile('/etc/fstab');
  var f2 = await readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};
````
一比较就会发现，async函数就是将Generator函数的星号（*）替换成async，将yield替换成await，仅此而已。

#####2.语法 
1）async函数返回一个Promise对象。

async函数内部return语句返回的值，会成为then方法回调函数的参数。

```
async function f() {
  return 'hello world';
}

f().then(v => console.log(v))
// "hello world"
```
上面代码中，函数f内部return命令返回的值，会被then方法回调函数接收到。

async函数内部抛出错误，会导致返回的Promise对象变为reject状态。抛出的错误对象会被catch方法回调函数接收到。

```
async function f() {
  throw new Error('出错了');
}

f().then(
  v => console.log(v),
  e => console.log(e)
)
// Error: 出错了
```

2）async函数返回的Promise对象，必须等到内部所有await命令的Promise对象执行完，才会发生状态改变。也就是说，只有async函数内部的异步操作执行完，才会执行then方法指定的回调函数。

3）正常情况下，await命令后面是一个Promise对象。如果不是，会被转成一个立即resolve的Promise对象。

await命令后面的Promise对象如果变为reject状态，则reject的参数会被catch方法的回调函数接收到。

只要一个await语句后面的Promise变为reject，那么整个async函数都会中断执行。

```
async function f() {
  await Promise.reject('出错了');
  await Promise.resolve('hello world'); // 不会执行
}
```
上面代码中，第二个await语句是不会执行的，因为第一个await语句状态变成了reject。

为了避免这个问题，可以将第一个await放在try...catch结构里面，这样第二个await就会执行。

```
async function f() {
  try {
    await Promise.reject('出错了');
  } catch(e) {
  }
  return await Promise.resolve('hello world');
}

f()
.then(v => console.log(v))
// hello world
```
另一种方法是await后面的Promise对象再跟一个catch方面，处理前面可能出现的错误。

```
async function f() {
  await Promise.reject('出错了')
    .catch(e => console.log(e));
  return await Promise.resolve('hello world');
}

f()
.then(v => console.log(v))
// 出错了
// hello world
```
如果有多个await命令，可以统一放在try...catch结构中。

```
async function main() {
  try {
    var val1 = await firstStep();
    var val2 = await secondStep(val1);
    var val3 = await thirdStep(val1, val2);

    console.log('Final: ', val3);
  }
  catch (err) {
    console.error(err);
  }
}
```

#####3.async 函数的用法
async函数返回一个Promise对象，可以使用then方法添加回调函数。当函数执行的时候，一旦遇到await就会先返回，等到触发的异步操作完成，再接着执行函数体内后面的语句。

下面是一个例子。

```
async function getStockPriceByName(name) {
  var symbol = await getStockSymbol(name);
  var stockPrice = await getStockPrice(symbol);
  return stockPrice;
}

getStockPriceByName('goog').then(function (result) {
  console.log(result);
});
```
上面代码是一个获取股票报价的函数，函数前面的async关键字，表明该函数内部有异步操作。调用该函数时，会立即返回一个Promise对象。

下面的例子，指定多少毫秒后输出一个值。

```
function timeout(ms) {
  return new Promise((resolve) => {
    setTimeout(resolve, ms);
  });
}

async function asyncPrint(value, ms) {
  await timeout(ms);
  console.log(value)
}

asyncPrint('hello world', 50);
```
上面代码指定50毫秒以后，输出"hello world"。

Async函数有多种使用形式。

```
// 函数声明
async function foo() {}

// 函数表达式
const foo = async function () {};

// 对象的方法
let obj = { async foo() {} };
obj.foo().then(...)

// Class 的方法
class Storage {
  constructor() {
    this.cachePromise = caches.open('avatars');
  }

  async getAvatar(name) {
    const cache = await this.cachePromise;
    return cache.match(`/avatars/${name}.jpg`);
  }
}

const storage = new Storage();
storage.getAvatar('jake').then(…);

// 箭头函数
const foo = async () => {};
```
#####4.注意点
第一点，await命令后面的Promise对象，运行结果可能是rejected，所以最好把await命令放在try...catch代码块中。

```
async function myFunction() {
  try {
    await somethingThatReturnsAPromise();
  } catch (err) {
    console.log(err);
  }
}

// 另一种写法

async function myFunction() {
  await somethingThatReturnsAPromise()
  .catch(function (err) {
    console.log(err);
  };
}

```
第二点，多个await命令后面的异步操作，如果不存在继发关系，最好让它们同时触发。

```
let foo = await getFoo();
let bar = await getBar();
```
上面代码中，getFoo和getBar是两个独立的异步操作（即互不依赖），被写成继发关系。这样比较耗时，因为只有getFoo完成以后，才会执行getBar，完全可以让它们同时触发。

```
// 写法一
let [foo, bar] = await Promise.all([getFoo(), getBar()]);

// 写法二
let fooPromise = getFoo();
let barPromise = getBar();
let foo = await fooPromise;
let bar = await barPromise;
```
上面两种写法，getFoo和getBar都是同时触发，这样就会缩短程序的执行时间。

第三点，await命令只能用在async函数之中，如果用在普通函数，就会报错。

```
async function dbFuc(db) {
  let docs = [{}, {}, {}];

  // 报错
  docs.forEach(function (doc) {
    await db.post(doc);
  });
}
```
上面代码会报错，因为await用在普通函数之中了。但是，如果将forEach方法的参数改成async函数，也有问题。

```
async function dbFuc(db) {
  let docs = [{}, {}, {}];

  // 可能得到错误结果
  docs.forEach(async function (doc) {
    await db.post(doc);
  });
}
```
上面代码可能不会正常工作，原因是这时三个db.post操作将是并发执行，也就是同时执行，而不是继发执行。正确的写法是采用for循环。

```
async function dbFuc(db) {
  let docs = [{}, {}, {}];

  for (let doc of docs) {
    await db.post(doc);
  }
}
```
如果确实希望多个请求并发执行，可以使用Promise.all方法。

```
async function dbFuc(db) {
  let docs = [{}, {}, {}];
  let promises = docs.map((doc) => db.post(doc));

  let results = await Promise.all(promises);
  console.log(results);
}

// 或者使用下面的写法

async function dbFuc(db) {
  let docs = [{}, {}, {}];
  let promises = docs.map((doc) => db.post(doc));

  let results = [];
  for (let promise of promises) {
    results.push(await promise);
  }
  console.log(results);
}
```

####6.实例：按顺序完成异步操作
实际开发中，经常遇到一组异步操作，需要按照顺序完成。比如，依次远程读取一组URL，然后按照读取的顺序输出结果。

并发发出远程请求。

````
async function logInOrder(urls) {
  // 并发读取远程URL
  const textPromises = urls.map(async url => {
    const response = await fetch(url);
    return response.text();
  });

  // 按次序输出
  for (const textPromise of textPromises) {
    console.log(await textPromise);
  }
}
````
上面代码中，虽然map方法的参数是async函数，但它是并发执行的，因为只有async函数内部是继发执行。

###Class

####1.Class基本语法 
#####概述

```
class Point {
  constructor(){
    // ...
  }

  toString(){
    // ...
  }

  toValue(){
    // ...
  }
}

// 等同于

Point.prototype = {
  toString(){},
  toValue(){}
};
```

在类的实例上面调用方法，其实就是调用原型上的方法。


```
class B {}
let b = new B();
b.constructor === B.prototype.constructor // true
```

上面代码中，b是B类的实例，它的constructor方法就是B类原型的constructor方法。

由于类的方法都定义在prototype对象上面，所以类的新方法可以添加在prototype对象上面。Object.assign方法可以很方便地一次向类添加多个方法。

```
class Point {
  constructor(){
    // ...
  }
}
Object.assign(Point.prototype, {
  toString(){},
  toValue(){}
});
```
prototype对象的constructor属性，直接指向“类”的本身，这与ES5的行为是一致的。
```
Point.prototype.constructor === Point // true
```
另外，类的内部所有定义的方法，都是不可枚举的（non-enumerable）。

class Point {
  constructor(x, y) {
    // ...
  }

  toString() {
    // ...
  }
}

Object.keys(Point.prototype)
// []
Object.getOwnPropertyNames(Point.prototype)
// ["constructor","toString"]
上面代码中，toString方法是Point类内部定义的方法，它是不可枚举的。这一点与ES5的行为不一致。

#####constructor方法
（1）constructor方法是类的默认方法，通过new命令生成对象实例时，自动调用该方法。一个类必须有constructor方法，如果没有显式定义，一个空的constructor方法会被默认添加。  
（2）constructor方法默认返回实例对象（即this），完全可以指定返回另外一个对象。   
（3）类的构造函数，不使用new是没法调用的，会报错。这是它跟普通构造函数的一个主要区别，后者不用new也可以执行。 
#####类的实例对象 
（1）生成类的实例对象的写法，与ES5完全一样，也是使用new命令。如果忘记加上new，像函数那样调用Class，将会报错。  
（2）与ES5一样，实例的属性除非显式定义在其本身（即定义在this对象上），否则都是定义在原型上（即定义在class上）。

#####不存在变量提升 
#####Class表达式
采用Class表达式，可以写出立即执行的Class。

```
let person = new class {
  constructor(name) {
    this.name = name;
  }

  sayName() {
    console.log(this.name);
  }
}('张三');

person.sayName(); // "张三"
```
#####this的指向 
类的方法内部如果含有this，它默认指向类的实例。但是，必须非常小心，一旦单独使用该方法，很可能报错。

```
class Logger {
  printName(name = 'there') {
    this.print(`Hello ${name}`);
  }

  print(text) {
    console.log(text);
  }
}

const logger = new Logger();
const { printName } = logger;
printName(); // TypeError: Cannot read property 'print' of undefined
```
上面代码中，printName方法中的this，默认指向Logger类的实例。但是，如果将这个方法提取出来单独使用，this会指向该方法运行时所在的环境，因为找不到print方法而导致报错。

解决方案一

一个比较简单的解决方法是，在构造方法中绑定this，这样就不会找不到print方法了。

```
class Logger {
  constructor() {
    this.printName = this.printName.bind(this);
  }

  // ...
}
```
解决方案二----使用箭头函数。

```
class Logger {
  constructor() {
    this.printName = (name = 'there') => {
      this.print(`Hello ${name}`);
    };
  }

  // ...
}
```
方案三----使用Proxy，获取方法的时候，自动绑定this。

#####name属性
由于本质上，ES6的类只是ES5的构造函数的一层包装，所以函数的许多特性都被Class继承，包括name属性。

```
class Point {}
Point.name // "Point"
```
name属性总是返回紧跟在class关键字后面的类名。

####2.Class的继承 
#####基本用法
Class之间可以通过extends关键字实现继承，这比ES5的通过修改原型链实现继承，要清晰和方便很多。

```
class ColorPoint extends Point {}
```
上面代码定义了一个ColorPoint类，该类通过extends关键字，继承了Point类的所有属性和方法。但是由于没有部署任何代码，所以这两个类完全一样，等于复制了一个Point类。

```
class ColorPoint extends Point {
  constructor(x, y, color) {
    super(x, y); // 调用父类的constructor(x, y)
    this.color = color;
  }

  toString() {
    return this.color + ' ' + super.toString(); // 调用父类的toString()
  }
}
```
上面代码中，constructor方法和toString方法之中，都出现了super关键字，它在这里表示父类的构造函数，用来新建父类的this对象。

子类必须在constructor方法中调用super方法，否则新建实例时会报错。这是因为子类没有自己的this对象，而是继承父类的this对象，然后对其进行加工。如果不调用super方法，子类就得不到this对象。

#####super 关键字 
super这个关键字，既可以当作函数使用，也可以当作对象使用。在这两种情况下，它的用法完全不同。

第一种情况:   
super作为函数调用时，代表父类的构造函数。ES6 要求，子类的构造函数必须执行一次super函数。

```
class A {}

class B extends A {
  constructor() {
    super();
  }
}
```
上面代码中，子类B的构造函数之中的super()，代表调用父类的构造函数。super虽然代表了父类A的构造函数，但是返回的是子类B的实例，即super内部的this指的是B，因此super()在这里相当于A.prototype.constructor.call(this)。

注意，作为函数时，super()只能用在子类的**构造函数**之中，用在其他地方就会报错。

第二种情况:  
super作为对象时，指向父类的原型对象。
```
class A {
  p() {
    return 2;
  }
}

class B extends A {
  constructor() {
    super();
    console.log(super.p()); // 2
  }
}

let b = new B();
```
上面代码中，子类B当中的super.p()，就是将super当作一个对象使用。这时，super指向A.prototype，所以super.p()就相当于A.prototype.p()。

这里需要注意，由于super指向**父类的原型对象**，所以定义在**父类实例上的方法或属性**，是无法通过super调用的。

```
class A {
  constructor() {
    this.p = 2;
  }
}

class B extends A {
  get m() {
    return super.p;
  }
}

let b = new B();
b.m // undefined
```
上面代码中，p是父类A实例的属性，super.p就引用不到它。

如果属性定义在父类的原型对象上，super就可以取到。

```
class A {}
A.prototype.x = 2;

class B extends A {
  constructor() {
    super();
    console.log(super.x) // 2
  }
}

let b = new B();
```
上面代码中，属性x是定义在A.prototype上面的，所以super.x可以取到它的值。

ES6 有一个特别规定，就是通过super调用父类的方法时，super会绑定**子类的this**。

```
class A {
  constructor() {
    this.x = 1;
  }
  print() {
    console.log(this.x);
  }
}

class B extends A {
  constructor() {
    super();
    this.x = 2;
  }
  m() {
    super.print();
  }
}

let b = new B();
b.m() // 2
```
上面代码中，super.print()虽然调用的是A.prototype.print()，但是A.prototype.print()会绑定子类B的this，导致输出的是2，而不是1。也就是说，实际上执行的是super.print.call(this)。

由于绑定子类的this，所以如果通过super对某个属性赋值，这时super就是this，赋值的属性会变成子类实例的属性。

```
class A {
  constructor() {
    this.x = 1;
  }
}

class B extends A {
  constructor() {
    super();
    this.x = 2;
    super.x = 3;
    console.log(super.x); // undefined
    console.log(this.x); // 3
  }
}

let b = new B();
```
上面代码中，super.x赋值为3，这时等同于对this.x赋值为3。而当读取super.x的时候，读的是A.prototype.x，所以返回undefined。

*注意，使用super的时候，必须显式指定是作为函数、还是作为对象使用，否则会报错。*

####3.Class的取值函数（getter）和存值函数（setter）
与ES5一样，在Class内部可以使用get和set关键字，对某个属性设置存值函数和取值函数，拦截该属性的存取行为。

```
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
```
上面代码中，prop属性有对应的存值函数和取值函数，因此赋值和读取行为都被自定义了。

####4.Class的静态方法
类相当于实例的原型，所有在类中定义的方法，都会被实例继承。如果在一个方法前，加上static关键字，就表示该方法不会被实例继承，而是直接通过类来调用，这就称为“静态方法”。

```
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
父类的静态方法，可以被子类继承。

```
class Foo {
  static classMethod() {
    return 'hello';
  }
}

class Bar extends Foo {
}

Bar.classMethod(); // 'hello'
```
上面代码中，父类Foo有一个静态方法，子类Bar可以调用这个方法。

静态方法也是可以从super对象上调用的。

####5.Class的静态属性和实例属性 
ES7有一个静态属性的提案，目前Babel转码器支持。

这个提案对实例属性和静态属性，都规定了新的写法。

（1）类的实例属性

类的实例属性可以用等式，写入类的定义之中。

```
class MyClass {
  myProp = 42;

  constructor() {
    console.log(this.myProp); // 42
  }
}
```
上面代码中，myProp就是MyClass的实例属性。在MyClass的实例上，可以读取这个属性。

以前，我们定义实例属性，只能写在类的constructor方法里面。

```
class ReactCounter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }
  }
  ```
上面代码中，构造方法constructor里面，定义了this.state属性。

有了新的写法以后，可以不在constructor方法里面定义。

```
class ReactCounter extends React.Component {
  state = {
    count: 0
  };
}
```
这种写法比以前更清晰。
为了可读性的目的，对于那些在constructor里面已经定义的实例属性，新写法允许直接列出。

```
class ReactCounter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }
  state;
}
```
（2）类的静态属性

类的静态属性只要在上面的实例属性写法前面，加上static关键字就可以了。

```
class MyClass {
  static myStaticProp = 42;

  constructor() {
    console.log(MyClass.myProp); // 42
  }
}
```
同样的，这个新写法大大方便了静态属性的表达。

```
// 老写法
class Foo {
}
Foo.prop = 1;

// 新写法
class Foo {
  static prop = 1;
}
```
上面代码中，老写法的静态属性定义在类的外部。整个类生成以后，再生成静态属性。这样让人很容易忽略这个静态属性，也不符合相关代码应该放在一起的代码组织原则。另外，新写法是显式声明（declarative），而不是赋值处理，语义更好。

###修饰器Decorator
####1.类的修饰 
修饰器（Decorator）是一个函数，用来修改类的行为。这是ES7的一个提案，目前Babel转码器已经支持。

修饰器对类的行为的改变，是代码编译时发生的，而不是在运行时。这意味着，修饰器能在编译阶段运行代码。

```
function testable(target) {
  target.isTestable = true;
}

@testable
class MyTestableClass {}

console.log(MyTestableClass.isTestable) // true
```
上面代码中，@testable就是一个修饰器。它修改了MyTestableClass这个类的行为，为它加上了**静态属性**isTestable。
基本上，修饰器的行为就是下面这样。

```
@decorator
class A {}

// 等同于

class A {}
A = decorator(A) || A;
```
也就是说，修饰器本质就是编译时执行的函数。

修饰器函数的第一个参数，就是所要修饰的目标类。上面代码中，testable函数的参数target，就是会被修饰的类。

如果觉得一个参数不够用，可以在修饰器外面再封装一层函数。

```
function testable(isTestable) {
  return function(target) {
    target.isTestable = isTestable;
  }
}

@testable(true)
class MyTestableClass {}
MyTestableClass.isTestable // true

@testable(false)
class MyClass {}
MyClass.isTestable // false
```

前面的例子是为类添加一个静态属性，如果想添加**实例属性**，可以通过目标类的prototype对象操作。

```
function testable(target) {
  target.prototype.isTestable = true;
}

@testable
class MyTestableClass {}

let obj = new MyTestableClass();
obj.isTestable // true
```
上面代码中，修饰器函数testable是在目标类的prototype对象上添加属性，因此就可以在实例上调用。

####2.方法的修饰
修饰器不仅可以修饰类，还可以修饰类的属性。

```
class Person {
  @readonly
  name() { return `${this.first} ${this.last}` }
}
```
上面代码中，修饰器readonly用来修饰“类”的name方法。

此时，修饰器函数一共可以接受三个参数，第一个参数是所要修饰的目标对象，第二个参数是所要修饰的属性名，第三个参数是该属性的描述对象。

```
function readonly(target, name, descriptor){
  // descriptor对象原来的值如下
  // {
  //   value: specifiedFunction,
  //   enumerable: false,
  //   configurable: true,
  //   writable: true
  // };
  descriptor.writable = false;
  return descriptor;
}

readonly(Person.prototype, 'name', descriptor);
// 类似于
Object.defineProperty(Person.prototype, 'name', descriptor);
```
上面代码说明，修饰器（readonly）会修改属性的描述对象（descriptor），然后被修改的描述对象再用来定义属性。

修饰器有注释的作用。

```
@testable
class Person {
  @readonly
  @nonenumerable
  name() { return `${this.first} ${this.last}` }
}
```
从上面代码中，我们一眼就能看出，Person类是可测试的，而name方法是只读和不可枚举的。

###Module
ES6模块的设计思想，是尽量的**静态化**，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。ES6模块不是对象，而是通过export命令显式指定输出的代码，输入时也采用静态命令的形式。

**自理解**  
CommonJS是运行时加载，ES6模块是编译时加载，效率更高。

####1.export命令

```
// profile.js
export var firstName = 'Michael';
export var lastName = 'Jackson';
export var year = 1958;
```
上面代码是profile.js文件，保存了用户信息。ES6将其视为一个模块，里面用export命令对外部输出了三个变量。

export的写法，除了像上面这样，还有另外一种。
```
// profile.js
var firstName = 'Michael';
var lastName = 'Jackson';
var year = 1958;

export {firstName, lastName, year};
```
上面代码在export命令后面，使用大括号指定所要输出的一组变量。它与前一种写法（直接放置在var语句前）是等价的，但是**应该优先考虑使用这种写法**。因为这样就可以在脚本尾部，一眼看清楚输出了哪些变量。

export命令除了输出变量，还可以输出函数或类（class）。

```
export function multiply(x, y) {
  return x * y;
};
```
上面代码对外输出一个函数multiply。

通常情况下，export输出的变量就是本来的名字，但是可以使用as关键字重命名。

```
function v1() { ... }
function v2() { ... }

export {
  v1 as streamV1,
  v2 as streamV2,
  v2 as streamLatestVersion
};
```
上面代码使用as关键字，重命名了函数v1和v2的对外接口。重命名后，v2可以用不同的名字输出两次。

需要特别注意的是，export命令规定的是对外的接口，必须与模块内部的变量建立一一对应关系。

正确的写法是下面这样。

````
// 写法一
export var m = 1;

// 写法二
var m = 1;
export {m};

// 写法三
var n = 1;
export {n as m};
````
####2.import命令
使用export命令定义了模块的对外接口以后，其他JS文件就可以通过import命令加载这个模块（文件）。

```
// main.js

import {firstName, lastName, year} from './profile';

function setName(element) {
  element.textContent = firstName + ' ' + lastName;
}
```
上面代码的import命令，就用于加载profile.js文件，并从中输入变量。import命令接受一个对象（用大括号表示），里面指定要从其他模块导入的变量名。大括号里面的变量名，必须与被导入模块（profile.js）对外接口的名称相同。

如果想为输入的变量重新取一个名字，import命令要使用as关键字，将输入的变量重命名。

```
import { lastName as surname } from './profile';
```
*注意，import命令具有提升效果，会提升到整个模块的头部，首先执行。*

如果在一个模块之中，先输入后输出同一个模块，import语句可以与export语句写在一起。

```
export { es6 as default } from './someModule';

// 等同于
import { es6 } from './someModule';
export default es6;
```
上面代码中，export和import语句可以结合在一起，写成一行。但是从可读性考虑，不建议采用这种写法，而应该采用标准写法。

另外，ES7有一个提案，简化先输入后输出的写法，拿掉输出时的大括号。

```
// 提案的写法
export v from 'mod';

// 现行的写法
export {v} from 'mod';
```
import语句会执行所加载的模块，因此可以有下面的写法。
```
import 'lodash';
```
上面代码仅仅执行lodash模块，但是不输入任何值。

####3.模块的整体加载 
除了指定加载某个输出值，还可以使用整体加载，即用星号（*）指定一个**对象**，所有输出值都加载在这个对象上面。

下面是一个circle.js文件，它输出两个方法area和circumference。

```
// circle.js

export function area(radius) {
  return Math.PI * radius * radius;
}

export function circumference(radius) {
  return 2 * Math.PI * radius;
}
```
整体加载的写法如下。

```
import * as circle from './circle';

console.log('圆面积：' + circle.area(4));
console.log('圆周长：' + circle.circumference(14));
```

####4.export default命令 

```
// 输出
export default function crc32() {
  // ...
}
// 输入
import crc32 from 'crc32';

// 输出
export function crc32() {
  // ...
};
// 输入
import {crc32} from 'crc32';
```
上面代码的两组写法，第一组是使用export default时，对应的import语句不需要使用大括号；第二组是不使用export default时，对应的import语句需要使用大括号。

export default命令用于指定模块的默认输出。显然，一个模块只能有一个默认输出，因此export default命令只能使用一次。所以，import命令后面才不用加大括号，因为只可能对应一个方法。

####5.跨模块常量 
const声明的常量只在当前代码块有效。如果想设置跨模块的常量（即跨多个文件），可以采用下面的写法。

```
// constants.js 模块
export const A = 1;
export const B = 3;
export const C = 4;

// test1.js 模块
import * as constants from './constants';
console.log(constants.A); // 1
console.log(constants.B); // 3

// test2.js 模块
import {A, B} from './constants';
console.log(A); // 1
console.log(B); // 3
```

###编程风格
####1.块级作用域
（1）let取代var

ES6提出了两个新的声明变量的命令：let和const。其中，let完全可以取代var，因为两者语义相同，而且let没有副作用。  
（2）全局常量和线程安全

在let和const之间，建议优先使用const，尤其是在全局环境，不应该设置变量，只应设置常量。这符合函数式编程思想，有利于将来的分布式运算。

```
// bad
var a = 1, b = 2, c = 3;

// good
const a = 1;
const b = 2;
const c = 3;

// best
const [a, b, c] = [1, 2, 3];
```

####2.字符串
静态字符串一律使用单引号或反引号，不使用双引号。动态字符串使用反引号。

```
// bad
const a = "foobar";
const b = 'foo' + a + 'bar';

// acceptable
const c = `foobar`;

// good
const a = 'foobar';
const b = `foo${a}bar`;
const c = 'foobar';
```

####3.解构赋值
使用数组成员对变量赋值时，优先使用解构赋值。

```
const arr = [1, 2, 3, 4];

// bad
const first = arr[0];
const second = arr[1];

// good
const [first, second] = arr;
```

函数的参数如果是对象的成员，优先使用解构赋值。

```
// bad
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;
}

// good
function getFullName(obj) {
  const { firstName, lastName } = obj;
}

// best
function getFullName({ firstName, lastName }) {
}
```
如果函数返回多个值，优先使用对象的解构赋值，而不是数组的解构赋值。这样便于以后添加返回值，以及更改返回值的顺序。

```
// bad
function processInput(input) {
  return [left, right, top, bottom];
}

// good
function processInput(input) {
  return { left, right, top, bottom };
}

const { left, right } = processInput(input);
```

####4.对象
(1)单行定义的对象，最后一个成员不以逗号结尾。多行定义的对象，最后一个成员以逗号结尾。

```
// bad
const a = { k1: v1, k2: v2, };
const b = {
  k1: v1,
  k2: v2
};

// good
const a = { k1: v1, k2: v2 };
const b = {
  k1: v1,
  k2: v2,
};
```

(2)对象尽量静态化，一旦定义，就不得随意添加新的属性。如果添加属性不可避免，要使用Object.assign方法。

```
// bad
const a = {};
a.x = 3;

// if reshape unavoidable
const a = {};
Object.assign(a, { x: 3 });

// good
const a = { x: null };
a.x = 3;
```

(3)如果对象的属性名是动态的，可以在创造对象的时候，使用属性表达式定义。

```
// bad
const obj = {
  id: 5,
  name: 'San Francisco',
};
obj[getKey('enabled')] = true;

// good
const obj = {
  id: 5,
  name: 'San Francisco',
  [getKey('enabled')]: true,
};
```

上面代码中，对象obj的最后一个属性名，需要计算得到。这时最好采用属性表达式，在新建obj的时候，将该属性与其他属性定义在一起。这样一来，所有属性就在一个地方定义了。

(4)另外，对象的属性和方法，尽量采用简洁表达法，这样易于描述和书写。

```
var ref = 'some value';

// bad
const atom = {
  ref: ref,

  value: 1,

  addValue: function (value) {
    return atom.value + value;
  },
};

// good
const atom = {
  ref,

  value: 1,

  addValue(value) {
    return atom.value + value;
  },
};
```

####5.数组
(1)使用扩展运算符（...）拷贝数组。

```
// bad
const len = items.length;
const itemsCopy = [];
let i;

for (i = 0; i < len; i++) {
  itemsCopy[i] = items[i];
}

// good
const itemsCopy = [...items];
```
(2)使用Array.from方法，将类似数组的对象转为数组。

```
const foo = document.querySelectorAll('.foo');
const nodes = Array.from(foo);
```

####6.函数
(1)立即执行函数可以写成箭头函数的形式。

```
(() => {
  console.log('Welcome to the Internet.');
})();
```

(2)那些需要使用函数表达式的场合，尽量用箭头函数代替。因为这样更简洁，而且绑定了this。

```
// bad
[1, 2, 3].map(function (x) {
  return x * x;
});

// good
[1, 2, 3].map((x) => {
  return x * x;
});

// best
[1, 2, 3].map(x => x * x);
```

(3)箭头函数取代Function.prototype.bind，不应再用self/_this/that绑定 this。

```
// bad
const self = this;
const boundMethod = function(...params) {
  return method.apply(self, params);
}

// acceptable
const boundMethod = method.bind(this);

// best
const boundMethod = (...params) => method.apply(this, params);
```

简单的、单行的、不会复用的函数，建议采用箭头函数。如果函数体较为复杂，行数较多，还是应该采用传统的函数写法。

(4)所有配置项都应该集中在一个对象，放在最后一个参数，布尔值不可以直接作为参数。

```
// bad
function divide(a, b, option = false ) {
}

// good
function divide(a, b, { option = false } = {}) {
}
```

(5)不要在函数体内使用arguments变量，使用rest运算符（...）代替。因为rest运算符显式表明你想要获取参数，而且arguments是一个类似数组的对象，而rest运算符可以提供一个真正的数组。

```
// bad
function concatenateAll() {
  const args = Array.prototype.slice.call(arguments);
  return args.join('');
}

// good
function concatenateAll(...args) {
  return args.join('');
}
使用默认值语法设置函数参数的默认值。

// bad
function handleThings(opts) {
  opts = opts || {};
}

// good
function handleThings(opts = {}) {
  // ...
}
```

####7. Map结构
注意区分Object和Map，只有模拟现实世界的实体对象时，才使用Object。如果只是需要key: value的数据结构，使用Map结构。因为Map有内建的遍历机制。

```
let map = new Map(arr);

for (let key of map.keys()) {
  console.log(key);
}

for (let value of map.values()) {
  console.log(value);
}

for (let item of map.entries()) {
  console.log(item[0], item[1]);
}
```

####8.Class
总是用Class，取代需要prototype的操作。因为Class的写法更简洁，更易于理解。

```
// bad
function Queue(contents = []) {
  this._queue = [...contents];
}
Queue.prototype.pop = function() {
  const value = this._queue[0];
  this._queue.splice(0, 1);
  return value;
}

// good
class Queue {
  constructor(contents = []) {
    this._queue = [...contents];
  }
  pop() {
    const value = this._queue[0];
    this._queue.splice(0, 1);
    return value;
  }
}
```
使用extends实现继承，因为这样更简单，不会有破坏instanceof运算的危险。

```
// bad
const inherits = require('inherits');
function PeekableQueue(contents) {
  Queue.apply(this, contents);
}
inherits(PeekableQueue, Queue);
PeekableQueue.prototype.peek = function() {
  return this._queue[0];
}

// good
class PeekableQueue extends Queue {
  peek() {
    return this._queue[0];
  }
}
```

####9.模块
首先，Module语法是JavaScript模块的标准写法，坚持使用这种写法。使用import取代require。

```
// bad
const moduleA = require('moduleA');
const func1 = moduleA.func1;
const func2 = moduleA.func2;

// good
import { func1, func2 } from 'moduleA';
```

使用export取代module.exports。

```
// commonJS的写法
var React = require('react');

var Breadcrumbs = React.createClass({
  render() {
    return <nav />;
  }
});

module.exports = Breadcrumbs;

// ES6的写法
import React from 'react';

const Breadcrumbs = React.createClass({
  render() {
    return <nav />;
  }
});

export default Breadcrumbs
```

如果模块只有一个输出值，就使用export default，如果模块有多个输出值，就不使用export default，不要export default与普通的export同时使用。

不要在模块输入中使用通配符。因为这样可以确保你的模块之中，有一个默认输出（export default）。

```
// bad
import * as myObject './importModule';

// good
import myObject from './importModule';
```

如果模块默认输出一个函数，函数名的首字母应该小写。

```
function makeStyleGuide() {
}

export default makeStyleGuide;
```
如果模块默认输出一个对象，对象名的首字母应该大写。

```
const StyleGuide = {
  es6: {
  }
};

export default StyleGuide;
```

####10.ESLint的使用
ESLint是一个语法规则和代码风格的检查工具，可以用来保证写出语法正确、风格统一的代码。





  


##Redux
###1. Redux动机
1. JavaScript 需要管理比任何时候都要多的 state （状态）。 这些 state 可能包括服务器响应、缓存数据、本地生成尚未持久化到服务器的数据，也包括 UI 状态，如激活的路由，被选中的标签，是否显示加载动效或者分页器等等
2. state 在什么时候，由于什么原因，如何变化已然不受控制。 当系统变得错综复杂的时候，想重现问题或者添加新功能就会变得举步维艰。
3. 这里的复杂性很大程度上来自于：我们总是将两个难以厘清的概念混淆在一起：变化和异步。
4. 一些库如 React 试图在视图层禁止异步和直接操作 DOM 来解决这个问题。美中不足的是，React 依旧把处理 state 中数据的问题留给了你。Redux就是为了帮你解决这个问题。
5. 通过限制更新发生的时间和方式，Redux 试图让 state 的变化变得可预测。

**自理解**  
全局变量，一个状态改变会影响其他组件的state，或者需要再次浏览的数据不想再从服务器获取，缓存到本地的数据需要用redux在action里走一圈然后放到store里。

###2. Redux三大原则
####单一数据源

整个应用的 state 被储存在一棵 object tree 中，并且这个 object tree 只存在于**唯一**一个 **store**中。

####State 是只读的

惟一改变 state 的方法就是触发 **action**，action 是一个用于描述已发生事件的普通对象。

####使用纯函数来执行修改

为了描述 action 如何改变 state tree ，你需要编写 reducers。reducers用action来改变原来的state，返回新的state。

```
import { combineReducers, createStore } from 'redux'
let reducer = combineReducers({ visibilityFilter, todos })
let store = createStore(reducer)
```

combineReducers用于合并纯函数生成一个reducer，createStore用生成的reducer创建store。

**自理解**
reducer的作用是统一管理react中修改state的逻辑实现

###3. 基础
####3.1 Action
Action 是把数据从应用（译者注：这里之所以不叫 view 是因为这些数据有可能是服务器响应，用户输入或其它非 view 的数据 ）传到 store 的有效载荷。它是 store 数据的唯一来源。一般来说你会通过` store.dispatch() `将 action 传到 store。

Action 本质上是 **JavaScript 普通对象**。我们约定，action 内必须使用一个字符串类型的 `type` 字段来表示将要执行的动作。多数情况下，type 会被定义成字符串常量。当应用规模越来越大时，建议使用单独的模块或文件来存放 action。

#####Action 创建函数

Action 创建函数 就是生成 action 的方法。“action” 和 “action 创建函数” 这两个概念很容易混在一起，使用时最好注意区分。

在 Redux 中的 action 创建函数只是简单的返回一个 action:

```
function addTodo(text) {
  return {
    type: ADD_TODO,
    text
  }
}
```
**自理解**  
action是一个创建好的普通对象，action创建函数是一个创建action的函数，可传入参数动态创建。

Redux 中只需把 action 创建函数的结果传给 `dispatch()` 方法即可发起一次 dispatch 过程。

```
dispatch(addTodo(text))
dispatch(completeTodo(index))
```
或者创建一个 被绑定的 action 创建函数 来自动 dispatch：

```
const boundAddTodo = (text) => dispatch(addTodo(text))
const boundCompleteTodo = (index) => dispatch(completeTodo(index))
```
然后直接调用它们：

```
boundAddTodo(text);
boundCompleteTodo(index);
```

store 里能直接通过 `store.dispatch()` 调用` dispatch() `方法，但是多数情况下你会使用 react-redux 提供的 connect() 帮助器来调用。

####3.2 Reducer
Action 只是描述了有事情发生了这一事实，并没有指明应用如何更新 state。而这正是 reducer 要做的事情。

#####3.2.1 设计 State 结构
尽量把这些数据与 UI 相关的 state 分开。 
 
**处理 Reducer 关系时的注意事项**  
开发复杂的应用时，不可避免会有一些数据相互引用。建议你尽可能地把 state 范式化，不存在嵌套。把所有数据放到一个对象里，每个数据以 ID 为主键，不同实体或列表间通过 ID 相互引用数据。把应用的 state 想像成数据库。例如，实际开发中，在 state 里同时存放 `todosById: { id -> todo } `和 `todos: array<id> `是比较好的方式，本文中为了保持示例简单没有这样处理。

#####3.2.2 Action 处理

现在我们已经确定了 state 对象的结构，就可以开始开发 reducer。reducer 就是一个纯函数，接收旧的 state 和 action，返回新的 state。

保持 reducer 纯净非常重要。永远不要在 reducer 里做这些操作：

- 修改传入参数；
- 执行有副作用的操作，如 API 请求和路由跳转；
- 调用非纯函数，如 Date.now() 或 Math.random()。  

在高级篇里会介绍如何执行有副作用的操作。现在只需要谨记 reducer 一定要保持纯净。**只要传入参数相同，返回计算得到的下一个 state 就一定相同。没有特殊情况、没有副作用，没有 API 请求、没有变量修改，单纯执行计算。**

**注意:**

不要修改 state。 使用 `Object.assign() `新建了一个副本。不能这样使用 `Object.assign(state, { visibilityFilter: action.filter })`，因为它会改变第一个参数的值。你必须把第一个参数设置为空对象。你也可以开启对ES7提案对象展开运算符的支持, 从而使用 `{ ...state, ...newState }` 达到相同的目的。

在 default 情况下返回旧的 state。遇到未知的 action 时，一定要返回旧的 state。

#####3.2.3 处理多个 action

#####拆分 Reducer

两种合成 reducer 方法完全等价：

```
const reducer = combineReducers({
  a: doSomethingWithA,
  b: processB,
  c: c
})
function reducer(state = {}, action) {
  return {
    a: doSomethingWithA(state.a, action),
    b: processB(state.b, action),
    c: c(state.c, action)
  }
}
```

`combineReducers()` 所做的只是生成一个函数，这个函数来调用你的一系列 reducer，每个 reducer 根据它们的 key 来筛选出 state 中的一部分数据并处理，然后这个生成的函数再将所有 reducer 的结果合并成一个大的对象。

**ES6 用户使用注意**

`combineReducers` 接收一个对象，可以把所有顶级的 reducer 放到一个独立的文件中，通过 export 暴露出每个 reducer 函数，然后使用 `import * as reducers `得到一个以它们名字作为 key 的 object：

```
import { combineReducers } from 'redux'
import * as reducers from './reducers'

const todoApp = combineReducers(reducers)
```

由于 import * 还是比较新的语法，为了避免困惑，我们不会在本文档中使用它。但在一些社区示例中你可能会遇到它们。

####3.3 Store
使用 action 来描述“发生了什么”，和使用 reducers 来根据 action 更新 state 的用法。

Store 就是把它们联系到一起的对象。Store 有以下职责：

- 维持应用的 state 
- 提供 getState() 方法获取 state；
- 提供 dispatch(action) 方法更新 state；
- 通过 subscribe(listener) 注册监听器;
- 通过 subscribe(listener) 返回的函数注销监听器。
再次强调一下 Redux 应用只有一个单一的 store。当需要拆分数据处理逻辑时，你应该使用 reducer 组合 而不是创建多个 store。

根据已有的 reducer 来创建 store 是非常容易的。将其导入，并传递 createStore()。

```
import { createStore } from 'redux'
import todoApp from './reducers'
let store = createStore(todoApp)
```

createStore() 的第二个参数是可选的, 用于设置 state 初始状态。这对开发同构应用时非常有用，服务器端 redux 应用的 state 结构可以与客户端保持一致, 那么客户端可以将从网络接收到的服务端 state 直接用于本地数据初始化。

``
let store = createStore(todoApp, window.STATE_FROM_SERVER)
``

####3.4数据流
严格的单向数据流是 Redux 架构的设计核心。

Redux 应用中数据的生命周期遵循下面 4 个步骤：

1.调用 store.dispatch(action)。Action 就是一个描述“发生了什么”的普通对象

2.Redux store 调用传入的 reducer 函数。Store 会把两个参数传入 reducer： 当前的 state 树和 action。

3.根 reducer 应该把多个子 reducer 输出合并成一个单一的 state 树。Redux 原生提供combineReducers()辅助函数，来把根 reducer 拆分成多个函数，用于分别处理 state 树的一个分支。

4.Redux store 保存了根 reducer 返回的完整 state 树。这个新的树就是应用的下一个 state！所有订阅 store.subscribe(listener) 的监听器都将被调用；监听器里可以调用 store.getState() 获得当前 state。


##React
###1.验证器说明如下

```
React.createClass({
  propTypes: {
    // 可以声明 prop 为指定的 JS 基本数据类型，默认情况，这些数据是可选的
   optionalArray: React.PropTypes.array,
    optionalBool: React.PropTypes.bool,
    optionalFunc: React.PropTypes.func,
    optionalNumber: React.PropTypes.number,
    optionalObject: React.PropTypes.object,
    optionalString: React.PropTypes.string,

    // 可以被渲染的对象 numbers, strings, elements 或 array
    optionalNode: React.PropTypes.node,

    //  React 元素
    optionalElement: React.PropTypes.element,

    // 用 JS 的 instanceof 操作符声明 prop 为类的实例。
    optionalMessage: React.PropTypes.instanceOf(Message),

    // 用 enum 来限制 prop 只接受指定的值。
    optionalEnum: React.PropTypes.oneOf(['News', 'Photos']),

    // 可以是多个对象类型中的一个
    optionalUnion: React.PropTypes.oneOfType([
      React.PropTypes.string,
      React.PropTypes.number,
      React.PropTypes.instanceOf(Message)
    ]),

    // 指定类型组成的数组
    optionalArrayOf: React.PropTypes.arrayOf(React.PropTypes.number),

    // 指定类型的属性构成的对象
    optionalObjectOf: React.PropTypes.objectOf(React.PropTypes.number),

    // 特定 shape 参数的对象
    optionalObjectWithShape: React.PropTypes.shape({
      color: React.PropTypes.string,
      fontSize: React.PropTypes.number
    }),

    // 任意类型加上 `isRequired` 来使 prop 不可空。
    requiredFunc: React.PropTypes.func.isRequired,

    // 不可空的任意类型
    requiredAny: React.PropTypes.any.isRequired,

    // 自定义验证器。如果验证失败需要返回一个 Error 对象。不要直接使用 `console.warn` 或抛异常，因为这样 `oneOfType` 会失效。
    customProp: function(props, propName, componentName) {
      if (!/matchme/.test(props[propName])) {
        return new Error('Validation failed!');
      }
    }
  },
  /* ... */
});
```

###2.React 组件生命周期
在本章节中我们将讨论 React 组件的生命周期。

组件的生命周期可分成三个状态：

- Mounting：已插入真实 DOM
- Updating：正在被重新渲染
- Unmounting：已移出真实 DOM

生命周期的方法有：

- componentWillMount 在渲染前调用,在客户端也在服务端。
- componentDidMount : 在第一次渲染后调用，只在客户端。之后组件已经生成了对应的DOM结构，可以通过this.getDOMNode()来进行访问。 如果你想和其他JavaScript框架一起使用，可以在这个方法中调用setTimeout, setInterval或者发送AJAX请求等操作(防止异部操作阻塞UI)。
- componentWillReceiveProps 在组件接收到一个新的prop时被调用。这个方法在初始化render时不会被调用。
- shouldComponentUpdate 返回一个布尔值。在组件接收到新的props或者state时被调用。在初始化时或者使用forceUpdate时不被调用。 
可以在你确认不需要更新组件时使用。
- componentWillUpdate在组件接收到新的props或者state但还没有render时被调用。在初始化时不会被调用。
- componentDidUpdate 在组件完成更新后立即调用。在初始化时不会被调用。
- componentWillUnmount在组件从 DOM 中移除的时候立刻被调用。










