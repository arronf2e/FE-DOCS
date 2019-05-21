### defer  延迟脚本
> 立即下载，但延迟执行
> 不阻塞页面渲染  
> 肯定会在 DOMContentLoaded 事件触发之前执行，依次执行 a.js ,b.js

```
<script defer src='a.js'></script>
<script defer src='b.js'></script>
```

### async  异步脚本 

> 异步下载，下载完之后立即执行
> 不阻塞页面渲染  
> 肯定会在 load 事件触发之前执行，在 DOMContentLoaded 之前或之后触发均有可能，c.js、d.js 执行顺序不定

```
<script async src='c.js'></script>
<script async src='d.js'></script>
```
