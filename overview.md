---
typora-copy-images-to: ipic
---

# 概述

**LiveScript**是一种**JavaScript**的**预编译语言**。它能直观地被编译为JavaScript，并帮助开发者略过重复冗余的代码格式，专注于书写拥有更高可读性的代码。LiveScript增添了许多特性去支持函数式编程，同时为便于开发者做面向对象与命令式编程开发做了大量改进。

LiveScript本是[Coco](http://satyr.github.io/coco/)的一个分支，同时是CoffeeScript的一个衍生与扩展，两者之间有良好的兼容性。

`1.5.0`: [`zip`](https://github.com/gkz/LiveScript/zipball/1.5.0) [`tar.gz`](https://github.com/gkz/LiveScript/tarball/1.5.0) [`View project on Github`](https://github.com/gkz/LiveScript) 

相关精选博客：[**LiveScript 1.4.0 - Source Maps and more!**](http://livescript.net/blog/livescript-1.4.0-source-maps-more.html)

###### 一些例子

（省略某些代码示例）

非嵌套的回调函数书写方式与无需`()`的链式调用：

```livescript
# LiveScript
<- $ 'h1' .on 'click'
alert 'boom!'
```

```javascript
// JavaScript
$('h1').on('click', function(){
  return alert('boom!');
});
```

