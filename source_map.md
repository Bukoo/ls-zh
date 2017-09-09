# Source Map

在编译时使用`-m,--map`参数可生成source map。它可选一下几种取值：`none` - 默认，`linked`，`linked-src`，`embedded`和`debug`。

生成source map的时候一共涉及三个文件：

1. LiveScript源代码
2. Source Map
3. 生成的JavaScript代码

`1`可选择嵌入到`2`中，`2`可以选择性地作为一条注释嵌入到`3`中。

`linked-src`：没有嵌入，`3`通过相对路径链接到`2`，`2`到`1`也一样。

`embedded`：所有相关文件都嵌入到`3`。

`debug`：与`linked`一致，但额外生成一份可读的源代码节点映射（与`ast`方法的输出类似）文件，后缀为`.map.debug`。

如果需要将`lsc`编译之后的文件直接发给浏览器，可以使用`linked`或`linked-src` - （即：不执行进一步的处理）。它们保持源代码分离，因此生成的JavaScript文件也很小。`linked-src`仅意味着生成的文件比`linked`模式少一个，能稍微减小JavaScript文件大小。

在其它情况下，请使用`embedded`。它生成的是自包含所有内容的一个文件，另外大多数工具，如browserify也仅接受这一种形式作为输入。这个文件会明显地增大，但仍有补救措施：在项目的自动化构建工作流末尾，运行一个分离工具，将文件分离成`linked`形式。