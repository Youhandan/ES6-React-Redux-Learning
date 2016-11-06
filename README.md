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
***使用注意点**
箭头函数有几个使用注意点。
（1）函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。
（2）不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。
（3）不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用Rest参数代替。
（4）不可以使用yield命令，因此箭头函数不能用作Generator函数。*

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

