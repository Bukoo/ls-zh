# 介绍

就像许多现代编程语言一样，LiveScript靠空格缩进来界定代码块，使用换行代替分号来终止一条语句（但如果你想在一行里写多条代码语句，你仍然可以使用分号）。

举个例子：

```livescript
# livescript
if 2 + 2 == 4
  do-something()
```

```javascript
// javascript
if (2 + 2 === 4) {
  doSomething();
}
```

为了让代码变得更清晰，在调用函数的时候，可以省略括号。

```livescript
add 2, 3
```

```javascript
add(2, 3);
```

注释是这样的：

```livescript
# from here to the end of the line.
```

```javascript
// from here to the end of the line.
```

> 有一个对于Lisp编程语言的拥护者们来说的好消息是：允许在变量名与函数名中使用`-`，它在被编译后将转化为驼峰式命名风格。比如：`my-value = 42` == `myValue = 42`。

LiveScript的文件后缀名是`ls`。

## 定义函数

在LiveScript中定义函数是十分轻便的。

```livescript
(x, y) -> x + y

-> # an empty function

times = (x, y) ->
  x * y
# multiple lines, and be assigned to
# a var like in JavaScript
```

```javascript
var times;
(function(x, y){ return x + y; });

(function(){});

times = function(x, y){
  return x * y;
};
```

如上所示，函数定义的语句明显变得简短了，同时省略了`return`。在LiveScript中，几乎所有的语句都是表达式，放在最后的语句将会自动执行`return`返回。但仍然，可以使用`return `强制返回语句，另外，可在箭头前增加`!`来制止自动返回`no-ret = (x) !-> ...`。

## 赋值

基本的赋值如`variable = value`，且不需要声明变量。但不同于CoffeeScript，必须使用`:=`来使用上层作用域的变量。

```livescript
x = 10


do ->
  x = 5

x #=> 10

do ->
  x := 2

x #=> 2

```

```javascript
var x;
x = 10;

(function(){
  var x;
  return x = 5;
})();
x;

(function(){
  return x = 2;
})();
x;
```

几乎所有语句都是表达式，这意味着：

```livescript
x = if 2 + 2 == 4
    then 10
    else 0
x #=> 10
```

```javascript
var x;
x = 2 + 2 === 4 ? 10 : 0;

x;
```

再例如循环、选择语句，甚至try/catch语句也都是表达式。

如果只要简单声明一个变量而不初始化它，使用`var`。

```livescript
var x
```

```javascript
var x;
```

也可以在LiveScript里使用`const`声明变量。它们将会在编译阶段被检查 - 编译出的JavaScript是一样的。

```livescript
const x = 10
x = 0
```

以上代码会抛出提示`redeclaration of constant "x" on line 2`。

但，被声明为常量的对象不是不可改变的 - 他们的属性仍然可操作。你可以使用`-k`或`--const`参数强制所有变量为常量。

> 由LiveScript编译出的JavaScript代码全都是被安全包裹的`(function(){...contents...}).call(this);` - 在例子中为了简介，都已经省略了。

