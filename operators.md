# 操作符

## 数字计算

标准的数学操作符与JavaScript一致。

```livescript
1 + 2 #=> 3
3 - 4 #=> -1
6 * 2 #=> 12
8 / 4 #=> 2
```

```javascript
1 + 2;
3 - 4;
6 * 2;
8 / 4;
```

取模操作符也和JavaScript中一样。- 但同时也适当添加了一个模运算符。

```livescript
-3 % 4  #=> -3
-3 %% 4 #=> 1
```

```javascript
var ref$;
-3 % 4;
((-3) % (ref$ = 4) + ref$) % ref$;
```

指数操作是右相关的，它比一元操作符有更高的优先级。`^`作为`**`的语法糖。

```livescript
2 ** 4     #=> 16
3 ^ 4      #=> 81
-2 ^ 2 ^ 3 #=> -256
```

```javascript
Math.pow(2, 4);
Math.pow(3, 4);
-Math.pow(2, Math.pow(2, 3));
```

增加值与减少值：

```livescript
n = 0
n++ #=> 0
++n #=> 2
n-- #=> 2
--n #=> 0
x = n++ #=> 0
x #=> 0
n #=> 1
x = ++n #=> 2
x #=> 2
n #=> 2
```

```javascript
var n, x;
n = 0;
n++;
++n;
n--;
--n;
x = n++;
x;
n;
x = ++n;
x;
n;
```

位与转移操作符：

```livescript
14 .&. 9   #=> 8
14 .|. 9   #=> 15
14 .^. 9   #=> 7
~9         #=> -10
9  .<<. 2  #=> 36
-9 .>>. 2  #=> -3
-9 .>>>. 2 #=> 1073741821
```

```javascript
14 & 9;
14 | 9;
14 ^ 9;
~9;
9 << 2;
-9 >> 2;
-9 >>> 2;
```

强制转换为数字类型：

```livescript
+'4' #=>  4
-'3' #=> -3
```

```javascript
+'4';
-'3';
```



## 比较

严格等价（无类型差异的相等）：

```livescript
2 + 4 == 6      #=> true
\boom is 'boom' #=> true

\boom != null   #=> true
2 + 2 is not 4  #=> false
0 + 1 isnt 1    #=> false
```

```javascript
2 + 4 === 6;
'boom' === 'boom';

'boom' !== null;
2 + 2 !== 4;
0 + 1 !== 1;
```

模糊等价（有类型差异的相等）：

```livescript
2 ~= '2'       #=> true
\1 !~= 1       #=> false
```

```javascript
2 == '2';
'1' != 1;
```

大/小于操作符和JavaScript中一致。

使用链式操作符的比较：

```livescript
1 < 2 < 4        #=> true
1 < 2 == 4/2 > 0 #=> true
```

```javascript
var ref$;
1 < 2 && 2 < 4;
1 < 2 && 2 === (ref$ = 4 / 2) && ref$ > 0;
```

最大/小值 - 返回更大/小的运算元。

```livescript
4 >? 8     #=> 8
9 - 5 <? 6 #=> 4
```

```javascript
var ref$;
4 > 8 ? 4 : 8;
(ref$ = 9 - 5) < 6 ? ref$ : 6;
```

如果一个等于操作（`==`或`is`，或它们的否定操作）的一个运算元是正则表达式形式，它将对另一个运算云进行匹配。等于操作将被编译为`exec`函数，相应的否定操作被编译为`test`函数，因此你可以继续使用这个运算结果。

```livescript
/^e(.*)/ is 'enter' #=> ["enter","nter"]
/^e(.*)/ == 'zx'    #=> null
/moo/ != 'loo'      #=> true
```

```javascript
/^e(.*)/.exec('enter');
/^e(.*)/.exec('zx');
!/moo/.test('loo');
```



## 逻辑运算

基本运算：

```livescript
true and false #=> false
true && false  #=> false

true or false  #=> true
true || false  #=> true

not false      #=> true
!false         #=> true
```

```javascript
true && false;
true && false;

true || false;
true || false;

!false;
!false;
```

有一个其它语言里不太常见的逻辑运算符 - 异或：

```livescript
false xor true  #=> true
false xor false #=> false
1 xor 0         #=> 1
1 xor 1         #=> false
```

```javascript
((true, false) || true) && !(false && true) && (false || true);
((false, false) || false) && !(false && false) && (false || false);
((0, 1) || 0) && !(1 && 0) && (1 || 0);
((1, 1) || 1) && !(1 && 1) && (1 || 1);
```

`and`、`or`和`xor`不能进行隐式调用，但`||`和`&&`可以。

```livescript
even 0 and 3 #=> 3
even 0 &&  3 #=> true
```

```javascript
even(0) && 3;
even(0 && 3);
```

你可以利用逻辑操作符调用函数。

```livescript
(f or g) 1
(f and g or h) 3 4
```

```javascript
f(1) || g(1);
f(3, 4) && g(3, 4) || h(3, 4);
```



## In/Of

利用`in`来检查一个列表中是否包含某个元素；利用`of`来检查一个对象是否拥有某个属性。

```livescript
list = [7 8 9]
2 in [1 2 3 4 5]             #=> true
3 in list                    #=> false
\id of id: 23, name: \rogers #=> true
```

```javascript
var list;
list = [7, 8, 9];
2 == 1 || 2 == 2 || 2 == 3 || 2 == 4 || 2 == 5;
in$(3, list);
'id' in {
  id: 23,
  name: 'rogers'
};
function in$(x, arr){
  var i = 0, l = arr.length >>> 0;
  while (i < l) if (x === arr[i++]) return true;
  return false;
}
```



## 管道操作

抛弃嵌套的函数调用，你可以将值传入管道中。`x |> f`和`f <| x`与`f(x)`等价。

```livescript
x = [1 2 3] |> reverse |> head #=> 3


y = reverse <| [1 2 3] #=> [3,2,1]
```

```javascript
var x, y;
x = head(
reverse(
[1, 2, 3]));
y = reverse([1, 2, 3]);
```

为了让代码结构更清晰，你可以另起一行书写。

```livescript
4
|> (+ 1)
|> even
#=> false
```

```javascript
even(
(function(it){
  return it + 1;
})(
4));
```



## 函数

可以通过组合一系列函数来创建函数（？）。LiveScript有两个用于组合函数的操作符：向前`<<`与向后`>>`。

`(f << g) x`等价于`f(g(x))`，`(f >> g) x`等价于`g(f(x))`。举个例子：

```livescript
odd     = (not) << even
odd 3   #=> true
```

```javascript
var odd;
odd = function(){
  return not$(even.apply(this, arguments));
};
odd(3);
function not$(x){ return !x; }
```

更清晰地理解这两个符号的区别：

```livescript
add-two-times-two = (+ 2) >> (* 2)
times-two-add-two = (+ 2) << (* 2)

add-two-times-two 3 #=> (3+2)*2 => 10
times-two-add-two 3 #=> (3*2)+2 => 8
```

```javascript
var addTwoTimesTwo, timesTwoAddTwo;
addTwoTimesTwo = function(){
  return (function(it){
    return it * 2;
  })((function(it){
    return it + 2;
  }).apply(this, arguments));
};
timesTwoAddTwo = function(){
  return (function(it){
    return it + 2;
  })((function(it){
    return it * 2;
  }).apply(this, arguments));
};
addTwoTimesTwo(3);
timesTwoAddTwo(3);
```

此处有一个语法糖，使用前后带空格的`.`代替`<<`，例如`f . g`，与在Haskell中一样。



## 列表

把两个列表连接起来：

```livescript
<[ one two three ]> ++ [\four]
#=> ['one','two','three','four']
```

```javascript
['one', 'two', 'three'].concat(['four']);
```

需要注意的是，这个连接操作，在`++`两侧是否添加空格必须前后一致，否则会被识别为增加变量的值。

创建包含连续重复元素的列表：

```livescript
[\ha] * 3 #=> ['ha','ha','ha']
```

```javascript
['ha', 'ha', 'ha'];
```

当右操作元是字符串，会执行`join`函数操作：

```livescript
<[ one two three ]> * \|      #=> 'one|two|three'
```

```javascript
['one', 'two', 'three'].join('|');
```

一元操作符扩展 - 当运算元是列表，将对列表中每个元素进行该一元操作。

```livescript
r = +[4 5 6]        #=> [+4, +5, +6]
t = typeof! [\b 5 {}] #=> ["String", "Number", "Object"]
c = ~[4, 5]         #=> [-5, -6]
++player<[strength hp]>
# also works with -, --, typeof, ! and delete!
i = new [some, classes]
c = ^^[copy, these, {}]
delete list[1, 2, 3]
do [a, b, c]
```

```javascript
var r, t, c, i, toString$ = {}.toString;
r = [+4, +5, +6];
t = [toString$.call('b').slice(8, -1), toString$.call(5).slice(8, -1), toString$.call({}).slice(8, -1)];
c = [~4, ~5];
++player['strength'], ++player['hp'];
i = [new some, new classes];
c = [clone$(copy), clone$(these), clone$({})];
delete list[1], delete list[2], delete list[3];
a(), b(), c();
function clone$(it){
  function fun(){} fun.prototype = it;
  return new fun;
}
```



## 字符串

字符串连接：

```livescript
'hello' + ' ' + 'world' #=> 'hello world'
string = 'say '         #=> 'say '
string += \yeah         #=> 'say yeah'
```

```javascript
var string;
'hello' + ' ' + 'world';
string = 'say ';
string += 'yeah';
```

创建包含连续相同字符的字符串：

```livescript
'X' * 3      #=> 'XXX'
```

```javascript
'XXX';
```

字符串删减与分割：

```livescript
'say yeah' - /h/ #=> 'say yea'
'say yeah' / \y  #=> ['sa',' ','eah']
```

```javascript
'say yeah'.replace(/h/, '');
'say yeah'.split('y');
```



## 包含验证

`?`在许多语法中都可以用于检验是否存在：

```livescript
bigfoot ? 'grizzly bear'     #=> 'grizzly bear'
string = \boom if window?    #=> 'boom'
document?.host               #=> 'gkz.github.com'
```

```javascript
var string;
(typeof bigfoot == 'undefined' || bigfoot === null) && 'grizzly bear';
if (typeof window != 'undefined' && window !== null) {
  string = 'boom';
}
if (typeof document != 'undefined' && document !== null) {
  document.host;
}
```



## 对象

Instanceof - 右侧使用数组，扩展表达式：

```livescript
new Date() instanceof Date           #=> true
new Date() instanceof [Date, Object] #=> true
```

```javascript
var ref$;
new Date() instanceof Date;
(ref$ = new Date()) instanceof Date || ref$ instanceof Object;
```

Typeof

```livescript
typeof /^/  #=> object
typeof! /^/ #=> RegExp
```

```javascript
var toString$ = {}.toString;
typeof /^/;
toString$.call(/^/).slice(8, -1);
```

Delete - 返回被删除元素的值。

```livescript
obj = {one: 1, two: 2}
r = delete obj.one
r #=> 1
```

```javascript
var obj, r, ref$;
obj = {
  one: 1,
  two: 2
};
r = (ref$ = obj.one, delete obj.one, ref$);
r;
```

`delete!`就如同JavaScript里的`delete`操作，且仅仅在属性存在但不可删除时才返回false，其余情况下返回true。

```livescript
obj = {one: 1, two: 2}
delete! obj.one #=> true
delete! Math.PI #=> false
```

```javascript
var obj;
obj = {
  one: 1,
  two: 2
};
delete obj.one;
delete Math.PI;
```

属性复制 - 从右到左复制可枚举属性，并赋值给左边变量。`<<<`复制自身属性，`<<<<`复制所有属性。`import`和`import all`是以上两个操作符的语法糖，省略做操作元，默认为`this`。

```livescript
obj = {one: 1, two: 2}
obj <<< three: 3 #=> {one: 1, two: 2, three: 3}
{go: true} <<<< window
import obj
```

```javascript
var obj;
obj = {
  one: 1,
  two: 2
};
obj.three = 3;
importAll$({
  go: true
}, window);
import$(this, obj);
function importAll$(obj, src){
  for (var key in src) obj[key] = src[key];
  return obj;
}
function import$(obj, src){
  var own = {}.hasOwnProperty;
  for (var key in src) if (own.call(src, key)) obj[key] = src[key];
  return obj;
}
```

Clone - 复制一个操作元。它并没有创建一个对象的深拷贝，相反，创建结果的原型是操作元。请记住，进行JSON序列化的时候，原型是被忽略的。

```livescript
obj = {one: 1}
obj2 = ^^obj
obj2.two = 2
obj2 #=> {one: 1, two: 2}
# above includes its prototype's properties
# JSON serialization would be just `{two: 2}`
obj  #=> {one: 1}
```

```javascript
var obj, obj2;
obj = {one: 1};
obj2 = clone$(obj);
obj2.two = 2;
obj2;

obj
function clone$(it){
  function fun(){} fun.prototype = it;
  return new fun;
}
```

插入词`with`集合了克隆与属性拷贝的特性，能够快速方便得创建对象。它等同于`^^obj <<< obj2`。同样需要注意同上JSON序列化的问题。

```livescript
girl = {name: \hanna, age: 22}
guy  = girl with name: \john
guy  #=> {name: 'john',  age: 22}
# the above result include the object's prototype
# in the result - the actual JSON: {name: 'john'}
girl #=> {name: 'hanna', age: 22}
```

```javascript
var girl, ref$, guy;
girl = {
  name: 'hanna',
  age: 22
};
guy = (ref$ = clone$(girl), ref$.name = 'john', ref$);
guy;
guy.age;
function clone$(it){
  function fun(){} fun.prototype = it;
  return new fun;
}
```



## 操作符作为函数

你可以部分地应用运算符并作为函数使用它们：

```livescript
(+ 2) 4         #=> 6
(*) 4 3         #=> 12

(not) true      #=> false
(in [1 to 3]) 2 #=> true
```

```javascript
(function(it){
  return it + 2;
})(4);
curry$(function(x$, y$){
  return x$ * y$;
})(4, 3);
not$(true);
(function(it){
  return it == 1 || it == 2 || it == 3;
})(2);
function curry$(f, bound){
  var context,
  _curry = function(args) {
    return f.length > 1 ? function(){
      var params = args ? args.concat() : [];
      context = bound ? context || this : this;
      return params.push.apply(params, arguments) <
          f.length && arguments.length ?
        _curry.call(context, params) : f.apply(context, params);
    } : f;
  };
  return _curry();
}
function not$(x){ return !x; }
```



## export

相比`exports`，使用`export`能更简洁地定义模块（module）。

```livescript


export func = ->

export value

export value-a, value-b, value-c



export
  a: 1
  b: -> 123



export class MyClass
```

```javascript
var func, ref$, MyClass, out$ = typeof exports != 'undefined' && exports || this;

out$.func = func = function(){};

out$.value = value;

out$.valueA = valueA;
out$.valueB = valueB;
out$.valueC = valueC;

ref$ = out$;
ref$.a = 1;
ref$.b = function(){
  return 123;
};

out$.MyClass = MyClass = (function(){
  MyClass.displayName = 'MyClass';
  var prototype = MyClass.prototype, constructor = MyClass;
  function MyClass(){}
  return MyClass;
}());
```





## require!

当需要使用`require()`引入一连串模块时，代码块总会变得凌乱不齐。使用`require!`能让你摆脱这个烦恼，它接收ID，或字符串、数组、对象作为输入参数。

如果引入的模块名字中包含`-`，你必须以字符串形式传参。

你可以使用Object的文法为引入的模块重命名。

你也可以解构引入的模块，获取值的内容。

```livescript
require! lib
require! 'lib1'

require! prelude-ls # no
require! 'prelude-ls'

require! [fs, path]

require! <[ fs path ]>


require! jQuery: $

require! {
  fs
  path
  lib: foo
}
```

```javascript
var lib, lib1, preludeLs, fs, path, $, foo;
lib = require('lib');
lib1 = require('lib1');

preludeLs = require('preludeLs');
preludeLs = require('prelude-ls');

fs = require('fs');
path = require('path');
fs = require('fs');
path = require('path');

$ = require('jQuery');


fs = require('fs');
path = require('path');
foo = require('lib');
```

你可以通过解构方便的引入模块的一部分：

```livescript
require! {
    fs: filesystem
    'prelude-ls': {map, id}
    path: {join, resolve}:p
}
```

```javascript
var filesystem, ref$, map, id, p, join, resolve;
filesystem = require('fs');
ref$ = require('prelude-ls'), map = ref$.map, id = ref$.id;
p = require('path'), join = p.join, resolve = p.resolve;
```

文件名会被自动提取作为模块名称。

```livescript
require! 'lib.js'
require! './dir/lib1.js'
```

```javascript
var lib, lib1;
lib = require('lib.js');
lib1 = require('./dir/lib1.js');
```

