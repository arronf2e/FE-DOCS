#### XMLHttpRequest （XHR)

```
var xhr = new XMLHttpRequest()
```

- open  启动一个请求

```
xhr.open('请求类型', 'url', 是否异步发送请求)

xhr.open('get', 'http://gank.io/api/today', false)
```

- send  发送请求

```
xhr.open('get', 'http://gank.io/api/today', false)
xhr.send(null)
console.log(xhr)
```
[![VmntfI.md.png](https://s2.ax1x.com/2019/05/28/VmntfI.md.png)](https://imgchr.com/i/VmntfI)

- response          依赖XMLHttpRequest.responseType返回不同的数据类型：DOMString、Document、FormData、Blob、File、ArrayBuffer
- responseText      返回DOMString
- responseXML       如果响应的内容类型是 "text/xml" 或 "application/xml"，保存响应数据的 XML DOM 文档
- status            响应的 http 状态
- statusText        http 状态说明

- readystate
 - 0，未初始化，还未调用  open 方法
 - 1，启动，已调用 open ,未调用 send