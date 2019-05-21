## DOMContentLoaded与load的区别

[![EzOicV.md.png](https://s2.ax1x.com/2019/05/21/EzOicV.md.png)](https://imgchr.com/i/EzOicV)

### DOM 文档的加载步骤

- 解析HTML结构
- 加载外部脚本和样式表文件
- 解析并执行脚本
- 构建 HTML DOM模型     // DOMContentLoaded
- 加载外部资源文件（image等）
- 页面渲染完成           // load


### DOMContentLoaded    （对应 jQuery 中的  $(document).ready()）

> MDN: 当初始的 HTML 文档被完全加载和解析完成之后，DOMContentLoaded 事件被触发，而无需等待样式表、图像和子框架的完成加载


### load       （对应 jQuery 中的  $(document).load()）

> 页面上所有的资源（图片，音频，视频等）被加载以后才会触发load事件。所以 load 所需要的时间必然大于等于 DOMContentLoaded 所需要的时间。


### HTML 页面的生命周期

> 主要有三个重要的事件

- DOMContentLoaded， DOM已经构建好，可以对DOM节点进行操作

```
document.addEventListener('DOMContentLoaded', cb)
```

- load，所有资源加载完毕，可以对资源进行一系列操作，比如获取图片宽高等~

```
window.onload = function() {}
```
- beforeunload/unload(基本不会用到)，当浏览器窗口关闭或者刷新时，会触发beforeunload事件。当前页面不会直接关闭，可以点击确定按钮关闭或刷新，也可以取消关闭或刷新。我们可以检查用户是否保存了修改，并提示他是否确定离开当前页面

```
window.onbeforeunload = function() {
    return "There are unsaved changes. Leave now?";
}
```
[![VSkMIx.png](https://s2.ax1x.com/2019/05/21/VSkMIx.png)](https://imgchr.com/i/VSkMIx)

[相关知识点：document​.ready​State](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/readyState)