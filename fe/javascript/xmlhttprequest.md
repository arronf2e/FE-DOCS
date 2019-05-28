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
 - GET
    ```
    xhr.open('GET', 'http://gank.io/api/today', false)
    xhr.send(null)
    console.log(xhr)
    ```
 - POST
    ```
    xhr.open('POST', url, true)
    //设置发送数据的请求格式，方便服务端获取 post data
    xhr.setRequestHeader('content-type', 'application/x-www-form-urlencoded');
    xhr.send(data)
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
 - 2，已调用  send 方法，但未收到响应
 - 3，接收，已经接收到部分数据
 - 4，完成，数据完全接收

- abort 取消异步请求
```
xhr.abort()
```

- 进度事件
 - loadstart 在接收到响应数据的第一个字节触发
 - progress  在接收响应期间持续不断地触发  (可用于计算文件下载的进度，做进度条)
 - error     在请求发生错误时触发
 - abort     在调用 abort 方法时触发
 - load      在接收到完整的响应数据时触发
 - loadend   在通信完成或者 error、abort 或 load 事件后触发 （浏览器支持情况堪忧）


 #### Web Sockets  （不受同源策略影响，只要服务器端支持，就能实现）

 > 目标：在一个持久连接上提供全双工、双向通信

 - 协议
 ```
 ws://
 wss: //
 ```

 - 创建与关闭
 ```
 var socket = new WebSocket(url)
 socket.close() 
 ```

 - 发送与接收数据

 > 发送的数据只能是纯文本数据，如遇复杂数据结构，必须序列化；同样返回的数据也是纯文本

```
var socket = new WebSocket(url)

// 发送
socket.send('hello world')

// 接收 
socket.onmessage = function(event) {
    console.log(event.data)  // 接收的数据
}

// 序列化
var data = {
    name: 'arron',
    age: 26
}
socket.send(JSON.stringify(data))
socket.onmessage = function (event) {
    console.log(JSON.parse(event.data))
}

```

- 状态 
 - 0，正在建立连接
 - 1，已经建立连接
 - 2，正在关闭连接
 - 3，已经关闭连接

- 事件 （只支持DOM 0 级事件）
 - open，成功建立连接时触发
 - error，发生错误时触发，连接不能持续
 - close，关闭连接时触发

```
var socket = new WebSocket(url)
socket.onopen = function () {
    console.log('ws open')
}
socket.onerror = function () {
    console.log('ws error')
}
socket.onclose = function () {
    console.log('ws close')
}
```