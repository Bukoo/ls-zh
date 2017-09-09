# 安装

[**npm**](http://npmjs.org/)安装：`sudo npm install -g livescript`。

或下载压缩包（[zip](https://github.com/gkz/LiveScript/zipball/1.5.0), [tar.gz](https://github.com/gkz/LiveScript/tarball/1.5.0)），解压后进入根目录，运行`sudo make install`。也可以通过`git`下载：`git clone git://github.com/gkz/LiveScript.git && cd LiveScript && sudo make install`（需要先安装Node.js）。

也可通过script标签（标签应使用属性`type="text/ls" `) 直接引入文件LiveScript/browser/livescript.js，在浏览器中直接使用。但必须在代码中事先调用`require("livescript").go()`，而所有LiveScript相关代码，应在`livescript.ls`文件后引入。

举个例子：

```javascript
<script src="livescript.js"></script>
<script type="text/ls">
    console.log "boom #{window.location}"
</script>
<script>
    var LiveScript = require("livescript");
    LiveScript.go();
</script>
```

