#### 同源策略

1. 含义： A网站网页中设置的 Cookie，在B网站网页不能打开，除非这两个网页"同源"。即：A与B的 协议，域名，端口号都相同(但路径可以不同)，才能互相访问对方的cookies 。

    - 协议相同
    - 域名相同 
    - 端口相同

2. 目的  

> 同源政策的目的，是为了保证用户信息的安全，防止恶意的网站窃取数据。

3. 限制范围

    - cookie、localstorage, indexDB 无法读取
    - DOM无法获取
    - 不能发送 ajax 请求