# 变量语法

> 太过简单的示例代码已省略

## 数字

`.4`形式是不合法的，必须以0开头，如：`0.4`。

下划线与附加的字母将会被省略。

```livescript
# livescript
64_000km
```

```javascript
// javascript
64000;
```

使用`~`来表示2到36间的任何数字进制。

```livescript
6~12
2~1000
16~ff
```

```javascript
8;
8;
255;
```

## 布尔，未定义与空

使用与CoffeeScript一致的代称。

```livescript
true
false
on
off
yes
no
```

```javascript
true;
false;
true;
false;
true;
false;
```

在JavaScript中，`undefined`可以被重定义，所以更为谨慎的办法是使用`void`操作符来进行undefined赋值。

`void`在顶级作用域（不做为表达式的时候）中不会被编译成具体内容（只作为一个占位符）- 它必须作为一个值被编译。

```livescript
void

x = void

null
```

```javascript
var x;
// void compiles to nothing here!
x = void 8;

null;
```

## 字符串

单、双引号都可以表示字符串。

也可以用反斜杠代替引号来表示字符串，但这类字符串中不能包含`,;])}`或空格。

```livescript
\word
func \word, \word;
(func \word)
[\word]
{prop:\word}
```

```javascript
'word';
func('word', 'word');
func('word');
['word'];
({
  prop: 'word'
});
```

双引号字符串允许在字符串内插值。单引号字符串通过as-is传值。简单变量插入到字符串时可省略双花括号。

```livescript
"The answer is #{2 + 2}"
'As #{is}'

variable = "world"
"Hello #variable"
```

```javascript
var variable;
"The answer is " + (2 + 2);
'As #{is}';

variable = "world";
"Hello " + variable;
```

在有插值的字符串前加上`%`，将得到一个由原始内容组成的数组。这能让开发者按照自己所想组合数组。

```livescript
%"#x #y"
```

```javascript
[x, " ", y];
```

多行字符串（多行字符串如果有插值，则要使用双引号）：

```livescript
multiline = 'string can be multiline
            and go on and on
            beginning whitespace is
            ignored'
heredoc = '''
            string can be multiline
            with newlines
            and go on and on
            beginning whitespace is
            ignored
'''
```

```javascript
var multiline, heredoc;
multiline = 'string can be multiline and go on and on beginning whitespace is ignored';

heredoc = 'string can be multiline\nwith newlines\nand go on and on\nbeginning whitespace is\nignored';
```

## 注释

`#`起头表示单行注释。它们不会被包含在编译结果里。

多行注释则被保留到编译结果。

## 对象

双花括号可写可不写：

```livescript
obj = {prop: 1, thing: 'moo'}



person =
  age:      23
  eye-color: 'green'
  height:   180cm

oneline = color: 'blue', heat: 4
```

```javascript
var obj, person, oneline;
obj = {
  prop: 1,
  thing: 'moo'
};
person = {
  age: 23,
  eyeColor: 'green',
  height: 180
};
oneline = {
  color: 'blue',
  heat: 4
};
```

动态键：

```livescript
obj =
  "#variable": 234
  (person.eye-color): false
```

```javascript
var ref$, obj;
obj = (ref$ = {}, ref$[variable + ""] = 234, ref$[person.eyeColor] = false, ref$);
```

属性赋值语法糖 - 如果希望属性名与变量名一致，可方便地通过变量设置属性。

```livescript
x = 1
y = 2
obj = {x, y}
```

```javascript
var x, y, obj;
x = 1;
y = 2;
obj = {
  x: x,
  y: y
};
```

设置标识符的语法糖 - 便捷设置布尔类型属性。

```livescript
{ +debug, -live }
```

```javascript
({
  debug: true,
  live: false
});
```

This指针 - 不需要使用`.`来访问属性。

```livescript
this
@
@location
```

```javascript
this;
this;
this.location;
```

## 正则表达式

正则表达式使用`/`来界定范围。

```livescript
/moo/gi
```

```javascript
/moo/gi;
```

使用`//`界定范围 - 支持多行，注释与空格！

```livescript
//
| [!=]==?             # equality
| @@                  # constructor
| <\[(?:[\s\S]*?\]>)? # words
//g
```

```javascript
/|[!=]==?|@@|<\[(?:[\s\S]*?\]>)?/g;
```

## 列表

标准的列表语法使用方括号来表示。

如果前一个元素不可调用，那么它们之间的逗号也不是必需的：

```livescript
[1 2 3 true void \word 'hello there']
```

```javascript
[1, 2, 3, true, void 8, 'word', 'hello there'];
```

利用缩进的代码块可以创建一个隐式地列表。但这个列表中至少应有两个元素。如果只有一个元素，可在最后一行添加`...`来强制隐式创建列表。

```livescript
my-list =
  32 + 1
  person.height
  'beautiful'

one-item =
  1
  ...
```

```javascript
var myList, oneItem;
myList = [32 + 1, person.height, 'beautiful'];



oneItem = [1];
```

当隐式创建列表时，可以使用星号`*`来明确隐式的数据结构，例如隐式的对象和列表结构。这个星号不会成为一个列表的实际内容，仅标识出一个隐式结构，以免两个隐式结构相互搞混。

```livescript
tree =
  * 1
    * 2
      3
    4
  * 5
    6
    * 7
      8
      * 9
        10
    11

obj-list =
  * name: 'tessa'
    age:  23
  * name: 'kendall'
    age:  19


obj =
  * name: 'tessa'
    age:  23

obj-one-list =
  * name: 'tessa'
    age:  23
  ...
```

```javascript
var tree, objList, obj, objOneList;
tree = [[1, [2, 3], 4], [5, 6, [7, 8, [9, 10]], 11]];









objList = [
  {
    name: 'tessa',
    age: 23
  }, {
    name: 'kendall',
    age: 19
  }
];
obj = {
  name: 'tessa',
  age: 23
};
objOneList = [{
  name: 'tessa',
  age: 23
}];
```

单词列表：

```livescript
<[ list of words ]>
```

```javascript
['list', 'of', 'words'];
```

## 范围列举

`to`表示小于等于一个数字的范围。`til`表示小于一个数字的范围。同时可以选择性增加一个`by`参数来定义列举元素间的间隙宽度。

如果省略范围起始点的数字，将默认为0。

使用数字/字符串语法：

```livescript
[1 to 5]       #=> [1, 2, 3, 4, 5]
[1 til 5]      #=> [1, 2, 3, 4]
[1 to 10 by 2] #=> [1, 3, 7, 9]
[4 to 1]       #=> [4, 3, 2, 1]
[to 5]         #=> [0, 1, 2, 3, 4, 5]
[\A to \D]     #=> ['A', 'B', 'C', D']
```

```javascript
var i$;
[1, 2, 3, 4, 5];
[1, 2, 3, 4];
[1, 3, 5, 7, 9];
[4, 3, 2, 1];
[0, 1, 2, 3, 4, 5];
["A", "B", "C", "D"];
```

使用任何表达式的时候 - 如果范围列举使用了表达式，且希望列举元素递减（如：数字从大到小），必须显示的设置`by -1`。

```livescript
x = 4
[1 to x]       #=> [1, 2, 3, 4]
[x to 0 by -1] #=> [4, 3, 2, 1, 0]
```

```javascript
var x, i$;
x = 4;
for (i$ = 1; i$ <= x; ++i$) {
  i$;
}
for (i$ = x; i$ >= 0; --i$) {
  i$;
}
```

## 其它

标签（在嵌套循环中很有用）：

```livescript
:label 4 + 2
```

```javascript
label: {
  4 + 2;
}
```

`constructor`语法糖。

```livescript
@@
@@x
x@@y
```

```javascript
constructor;
constructor.x;
x.constructor.y;
```

占位符：

```livescript
...
```

```javascript
throw Error('unimplemented');
```

