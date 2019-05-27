### 文档对象模型（DOM)

常用对象： document  

常用方法：

| 方法 | 说明 | 
| ------------- |:-------------:| 
| getElementById() | 获取特定ID元素的节点 | 
| getElementsByTagName() | 获取相同元素的节点列表 | 
| getElementsByName | 获取相同名称的节点列表 | 
| getAttribute() | 获取特定元素节点属性的值 | 
| setAttribute() | 设置特定元素节点属性的值 | 
| removeAttribute() | 移除特定元素节点属性 |




### 浏览器对象模型（BOM）

核心： window  
常用对象：navigator、history、location
常用属性：

| 方法 | 说明 | 
| ------------- |:-------------:| 
| navigator.userAgent | ua | 
| navigator.geolocation | 位置相关 | 
| location.hash | hash value | 
| location.port | 端口 | 
| location.search | query | 
| location.protocol | 协议类型 |


- window

> 浏览器实例，Global 对象。全局作用域中定义的变量、函数都会变成 window 的属性与方法

```
var num = 30
function getNum() {
    console.log(this, this.num)
}
getNum()                // Window 30
console.log(window.num) // 30
window.getNum()         // Window 30
```

```
window.screenTop 返回当前窗口距离屏幕顶端的距离
window.screenLeft 返回当前窗口距离屏幕左侧边的距离

window.innerWidth   返回当前页面的宽度
window.innerHeight  返回当前页面的高度
window.outerWidth   返回整个浏览器本身的宽度
window.outerHeight  返回整个浏览器本身的高度
```