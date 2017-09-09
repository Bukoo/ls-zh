# 标准库

使用LiveScript时推荐将[prelude.ls](http://preludels.com/)作为基础库，有了它你可以例如这样写代码：

```livescript
[1 2 3] |> map (* 2) |> filter (> 3) |> fold1 (+)
#=> 10
```

使用`-d`或`--prelude`参数就可以自动将prelude.ls引入REPL。