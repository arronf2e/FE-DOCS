### 事件

#### DOM 事件流

- 事件捕获 (Firefox提出)
- 目标阶段
- 事件冒泡 (IE提出)


### 事件级别

- 0级事件处理程序  （事件冒泡阶段处理）

```
var btn = document.getElementById('btn')
btn.onclick = function() {
    console.log(this.id)
}

// 移除事件
btn.onclick = null
```

- 2级事件处理程序（相比0级，2级可以绑定多个事件处理程序）

```
// 添加事件
var btn = document.getElementById('btn')
var handle = function() {
    console.log(this.id)
}
btn.addEventListener('click', handle, false)

// 移除事件
btn.removeEventListener('click', handle, false)

// 绑定多个事件处理程序
var app = document.getElementById("app");
app.addEventListener('click', function() {
  console.log(this.id, '1')
})
app.addEventListener('click', function() {
  console.log(this.id, '2')
})
```
> addEventListener, removeEventListener 事件处理方法必须是同一个 handle ，第三个参数 false 冒泡阶段处理， true 捕获阶段处理

- IE事件处理程序 

```
// 添加事件
var btn = document.getElementById('btn')
btn.attachEvent('onclick', handle) {
    console.log(this)   // Window  （与上面的 addEventListener 作用域不一样）
}

// 移除事件
btn.detachEvent('onclick', handle) {}
```

#### 跨浏览器的事件处理程序 

```
var EventUtil = {
    addHandler: function(element, type, handler) {
        if(element.addEventListener) {
            element.addEventListener(type, handler, false)
        }else if(element.attachEvent) {
            element.attachEvent('on' + type, handler)
        }else {
            element['on' + type] = handler
        }
    },
    removeHandle: function(element, type, handler) {
        if(element.removeEventListener) {
            element.removeEventListener(type, handler, false)
        }else if(element.detachEvent) {
            element.detachEvent('on' + type, handler)
        }else {
            element['on' + type] = null
        }
    }
}
var btn = document.getElementById('btn')
EventUtil.addHandler(btn, 'click', handler)
```

#### 事件对象

```
var btn = document.getElementById('btn')
btn.onclick = function(event) {
    console.log(event.type)   // 'click'
}

var app = document.getElementById("app");
app.addEventListener('click', function(event) {
  console.log(event.type)  // 'click'
})
```

1. event.currentTarget 与 event.target 的区别

> event.target指向引起触发事件的元素，而event.currentTarget则是事件绑定的元素

```
// 冒泡阶段
<div id="a">
    <div id="b">
      <div id="c">
        <div id="d"></div>
      </div>
    </div>
</div>

<script>
    document.getElementById('a').addEventListener('click', function(e) {
      console.log('target:' + e.target.id + '&currentTarget:' + e.currentTarget.id);
    });    
    document.getElementById('b').addEventListener('click', function(e) {
      console.log('target:' + e.target.id + '&currentTarget:' + e.currentTarget.id);
    });    
    document.getElementById('c').addEventListener('click', function(e) {
      console.log('target:' + e.target.id + '&currentTarget:' + e.currentTarget.id);
    });    
    document.getElementById('d').addEventListener('click', function(e) {
      console.log('target:' + e.target.id + '&currentTarget:' + e.currentTarget.id);
    });
</script>

output:  
target:d&currentTarget:d
target:d&currentTarget:c
target:d&currentTarget:b
target:d&currentTarget:a


// 捕获阶段
<div id="a">
    <div id="b">
      <div id="c">
        <div id="d"></div>
      </div>
    </div>
</div>

<script>
    document.getElementById('a').addEventListener('click', function(e) {
      console.log('target:' + e.target.id + '&currentTarget:' + e.currentTarget.id);
    },true);    
    document.getElementById('b').addEventListener('click', function(e) {
      console.log('target:' + e.target.id + '&currentTarget:' + e.currentTarget.id);
    },true);    
    document.getElementById('c').addEventListener('click', function(e) {
      console.log('target:' + e.target.id + '&currentTarget:' + e.currentTarget.id);
    },true);    
    document.getElementById('d').addEventListener('click', function(e) {
      console.log('target:' + e.target.id + '&currentTarget:' + e.currentTarget.id);
    },true);
</script>

output:  
target:d&currentTarget:a
target:d&currentTarget:b
target:d&currentTarget:c
target:d&currentTarget:d
```

2. 阻止事件的默认行为

```
event.preventDefault()
```

3. 阻止冒泡或捕获，立即停止事件在DOM层中的传播

```
event.stopPropagation()
```

4. return false 、event.preventDefault()、event.stopPropagation() 三者的关系  

return false 做了三步工作：  
- event.preventDefault()
- event.stopPropagation()
- 停止执行回调函数并立即返回

5. event.stopImmediatePropagation()   阻止事件冒泡并且阻止相同事件的其他侦听器被调用

```
const btn = document.getElementById('btn')
btn.addEventListener("click", (event) => {
    alert("我是btn元素上被绑定的第一个监听函数");
}, false);

btn.addEventListener("click", (event) => {
    alert("我是btn元素上被绑定的第二个监听函数");
    event.stopImmediatePropagation();
    // 执行stopImmediatePropagation方法,阻止click事件冒泡,并且阻止btn元素上绑定的其他click事件的事件监听函数的执行.
}, false);

btn.addEventListener("click",(event) => {
    alert("我是btn元素上被绑定的第三个监听函数");
    // 该监听函数排在上个函数后面，该函数不会被执行
}, false);

document.querySelector("div").addEventListener("click", (event) => {
    alert("我是div元素,我是btn元素的上层元素");
    // p元素的click事件没有向上冒泡，该函数不会被执行
}, false);
```

6. event.eventPhase  返回一个代表当前执行阶段的 整数值

- 捕获 1
- 处于目标 2
- 冒泡 3

#### IE中的事件对象 

```
var btn = document.getElementById('btn')
btn.attachEvent('onclick', function(){
    var event = window.event
    console.log(event.type)  // 'click'
})
```

1. 阻止冒泡（只阻止冒泡，IE没有捕获阶段）

```
window.event.cancelBubble = false
```

2. 阻止默认行为

```
window.event.returnValue = false
```

3. 事件目标对象  （同上  event.target)

```
window.event.srcElement
```

#### 跨浏览器的事件对象

```
var EventUtil = {
    addHandler: function(element, type, handler) {
        if(element.addEventListener) {
            element.addEventListener(type, handler, false)
        }else if(element.attachEvent) {
            element.attachEvent('on' + type, handler)
        }else {
            element['on' + type] = handler
        }
    },
    removeHandle: function(element, type, handler) {
        if(element.removeEventListener) {
            element.removeEventListener(type, handler, false)
        }else if(element.detachEvent) {
            element.detachEvent('on' + type, handler)
        }else {
            element['on' + type] = null
        }
    },
    getEvent: function(event) {
        return event || window.event
    },
    getTarget: function(event) {
        return event.target || event.srcElement
    },
    preventDefault: function(event) {
        event.preventDefault ? event.preventDefault() : event.returnValue = false
    },
    stopPropagation: function(event) {
        event.stopPropagation ? event.stopPropagation() : event.cancelBubble = true
    }
}
var btn = document.getElementById('btn')
btn.onclick = function(event) {
    event = EventUtil.getEvent()
    var target = EventUtil.getTarget(event)
    EventUtil.preventDefault(event)
}

```

#### 事件类型

- ui 事件
 - load
 - beforeunload
 - unload
 - resize
 - scroll
- 焦点事件
 - blur
 - focus
- 鼠标与滚轮事件
 - click (鼠标左键或者回车)
 - dbclick
 - mousedown
 - mouseenter (鼠标移入元素范围内触发，不冒泡，移动到后代元素不会触发)
 - mouseleave (鼠标移入元素范围外触发，不冒泡，移动到后代元素不会触发)
 - mousemove  (鼠标在元素内部移动，重复触发)
 - mouseover  (鼠标指针位于元素外部，首次移入另一个元素的边界之内触发)
 - mouseout   (鼠标从当前元素移入另一个元素时触发)
- 文本事件
- 键盘事件  (keydown => keypress(如果是字符) => keyup，键码 event.keyCode )
 - keydown  
 - keypress (字符键)
 - keyup
- 合成事件
 - compositionstart
 - compositionupdate
 - compositionend
- 变动事件（mutation)