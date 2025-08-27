# Bypass_Debugger

## Intro

该脚本可bypass：

1. new Function --> debugger
2. constructor --> debugger
3. eval --> debugger

## 注意事项

1. 本脚本在油猴里的运行时期为`document-start`。

2. 如果发现hook后打开F12依然存在debugger：

- **建议开着F12在刷新一次。** 
- 请检查油猴或其他插件加载的脚本是不是做了同样的操作，例如重写Function等等，个人建议使用时除不是自己写的脚本(指没有做本脚本同样动作的)都关闭。

3. 我的这段Bypass Debugger脚本，目前已知的只有以下这两种情况不能被bypass掉：
```js
var dbg = function (){
    debugger;
}
setInterval(dbg,3000);
```
![1733639165304](image/README/1733639165304.png)

以及直接将debugger写在script当中的：

![1733639172782](image/README/1733639172782.png)

以上这两种设条件断点就能过(如果不知道怎么设置条件断点的可以去看一下我之前写的反调试与反反调试一文)，或者替换也行，不需要hook的，所以我就暂时没去管这个。

4. 如果hook后站点js出现异常，是因为eval的作用域问题导致的，此时可以考虑将chrome的`来自eval或控制台的匿名脚本`设置打开：
![1756209045846](image/README/1756209045846.png)
![1756207983716](image/README/1756207983716.png)
现在就能解决掉由eval和Function引起的无限debugger。但如果你不想忽略掉来自eval和Function的匿名脚本,可以考虑使用`Bypass_Debugger(备用)`，该脚本只会hook Function和Function.prototype.constructor，并不会影响到eval，所以如果目标网站是由eval引起的debugger就没办法了。

## Contact

如有bug或其他问题可提交issues。