### 错误处理


#### try-catch

```
try {
    // 可能会出现错误的代码    
}catch (e) {
    // 错误处理
}finally {
    // 必定执行
}
```

#### 错误事件

> 任何没有通过 try-catch 处理的错误都会触发 window.onerror 事件

```
window.onerror = function(message, url, line) {
    console.log(message, url, line)
    return false  // 防止浏览器报告错误的默认行为
}
```