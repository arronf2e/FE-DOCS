#### 事件循环


[![VuetUJ.md.png](https://s2.ax1x.com/2019/05/29/VuetUJ.md.png)](https://imgchr.com/i/VuetUJ)
![https://pic2.zhimg.com/80/v2-64ab01fc0b7830a8e1b694d78a7bda3d_hd.jpg](https://pic2.zhimg.com/80/v2-64ab01fc0b7830a8e1b694d78a7bda3d_hd.jpg)


- macro-task(宏任务)：包括整体代码script，setTimeout，setInterval
- micro-task(微任务)：Promise，process.nextTick


1. setTimeout
```
// param1, param2    附加参数，一旦定时器到期，它们会作为参数传递给function
setTimeout(fn, delay, param1, param2...)
```