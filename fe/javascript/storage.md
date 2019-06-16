### cookie

> Cookie指某些网站为了辨别用户身份而储存在用户本地终端上的数据(通常经过加密)。 cookie是服务端生成，客户端进行维护和存储

1. 格式：

```
_ga=GA1.2.26943092.1548316167; _octo=GH1.1.1579653845.1548316167; tz=Asia%2FShanghai; ignored_unsupported_browser_notice=false; has_recent_activity=1; _gat=1
```

2. 应用场景 

 - 记住密码，下次自动登录
 - 购物车功能
 - 记录用户的行为，进行定向推送广告

3. 原理及生成方式

![VTUaCD.png](https://s2.ax1x.com/2019/06/16/VTUaCD.png)

生成方式：  

 - Set-cookie
 - document.cookie

 4. 缺陷

  - 存储空间太小：4MB
  - 同域下的所有请求，都会携带cookie信息，大量请求下cookie带来的开销是非常大的
  - 安全问题

  ![https://camo.githubusercontent.com/f8a3b6567eff966f59b3ddc0d8882ad07d0d5fb3/68747470733a2f2f757365722d676f6c642d63646e2e786974752e696f2f323031392f332f32352f313639623037333963323266383461373f773d35333426683d32353926663d706e6726733d3139333230](https://camo.githubusercontent.com/f8a3b6567eff966f59b3ddc0d8882ad07d0d5fb3/68747470733a2f2f757365722d676f6c642d63646e2e786974752e696f2f323031392f332f32352f313639623037333963323266383461373f773d35333426683d32353926663d706e6726733d3139333230)

### Web Storage

1. localStorage

特点： 

 - 数据长期存在，除非手动清除
 - 大小： 5MB
 - 仅存储在客户端，不和服务端通信
 - api封装良好
 - 同源跨标签访问
 - 只能存储字符串数据

```
localStorage.setItem(key, value)
localStorage.getItem(key)
localStorage.clear()
localStorage.removeItem()
```

2. sessionStorage

特点：

 - 会话级别的客户端存储
 - 大小： 5MB
 - 仅存储在客户端，不和服务端通信
 - api封装良好
 - 不支持跨标签访问
 - 只能存储字符串数据

 ```
 sessionStorage.setItem(key, value)
 sessionStorage.getItem(key)
 sessionStorage.clear()
 sessionStorage.removeItem()
 ```

 ### IndexedDB

 > IndexedDB（对象数据库）可以说是浏览器端非关系型数据库，可以被网页脚本程序创建和操作。它允许储存大量数据，提供查找接口，还能建立索引
 > 在IndexedDB API中，一个数据库就是一个命名对象仓库（object store）的集合，对象存储区存储的是对象。

 特点： 

  - 键值对存储：在对象仓库中，数据以“键值对”的形式保存，每一个数据都有对应的键名，键名是独一无二的，不能有重复，否则会抛出一个错误
  - 支持二进制储存---IndexedDB 不仅可以储存字符串，还可以储存二进制数据（ArrayBuffer 对象和 Blob 对象）
  - 同域限制：IndexedDB数据库的作用域是限制在包含它们的文档源中，每一个数据库对应创建该数据库的域名，两个同源的Web页面互相之间可以访问对方的数据，但非同源的页面就不行
  - 支持事务：IndexedDB支持事务，这就是说对数据库的查询和更新都是包含在一个事务（transaction）中，以此来确保这些操作要么是一起成功，要么是一起失败，并且永远不会让数据库出现更新到一半的情况
  - 异步：IndexedDB的操作不会阻塞浏览器的UI主线程
  - 储存空间大：IE的储存上限是250MB，Chrome和Opera是剩余空间的某个百分比，Firefox则没有上限。  

 检测浏览器是否支持：

 ```
 if('indexedDB' in window){
    //支持
 }else{
    //不支持
 }
```

操作：

 - 打开数据库
 ```
 // 数据库名称
 var dbName = 'project'
 // 版本
 var version = 1
 // 数据库数据结果
 var db
 var dbOpenRequest = indexedDB.open(dbName, version)
 dbOpenRequest.onerror = function(event) {
     console.log('数据库打开失败')
 }
 dbOpenRequest.onsuccess = function(event) {
     db = dbOpenRequest.result
     console.log(db, 'db')
 }

 ```

 - 关闭数据库
 ```
 db.close()
 ```

 - 删除数据库
 ```
 indexedDB.deleteDatabase(dbName)
 ```