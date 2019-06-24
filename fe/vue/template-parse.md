### 模板解析

```
class Compile {
    constructor(el, vm) {
        this.$vm = vm
        this.$el = this.isElementNode(el) ? el : document.querySelector(el)
        if(this.$el) {
            // 取出所有子节点
            this.$fragment = this.node2Fragment(this.$el)
            // 编译 fragment 中所有层次节点
            this.init()
            // 将编译后的frament添加到 el
            this.$el.appendChild(this.$fragment)
        }else {
            throw new Error('el is needed')
        }
    }

    // 编译
    init() {
        this.compileElement(this.$fragment)
    }

    compileElement(el) {
        var childNodes = el.childNodes
        Array.prototype.slice.call(childNodes).forEach(node => {
            // 得到节点的文本内容
            var text = node.textContent
            var reg = /\{\{(.*)\}\}/    // 匹配 {{}}, () 表示子匹配，方便后续取到 {{}} 中的变量, 保存到 RegExp 对象中
            if(this.isElementNode(node)) {
                // 编译指令
                this.compile(node)
            }else if(this.isTextNode(node) && reg.test(text)) {
                // 编译带{{}}的文本节点
                this.compileText(node, RegExp.$1)
            }
            if(node.childNodes && node.childNodes.length) {
                this.compileElement(node)  // 递归编译所有子节点
            }
        })
    }

    // 编译指令
    compile(node) {
        var attributes = node.attributes
        Array.prototype.slice.call(attributes).forEach(attr => {
            var attrName = attr.name
            if(this.isDirective(attrName)) {
                var expValue = attr.value
                var dir = attrName.substring(2) // v-on:click  =>  on:click
                // 判断是否是事件指令
                if(this.isEventDirective(dir)) {
                    compileUtil.eventHandler(node, this.$vm, expValue, dir)
                }else {
                    // 普通指令
                    compileUtil[dir] && compileUtil[dir](node, this.$vm, expValue)
                }
                // 移除自定义指令属性
                node.removeAttribute(attrName)
            }
        })
    }

    // 文本编译
    compileText(node, exp) {
        compileUtil.text(node, this.$vm, exp)
    }

    node2Fragment(el) {
        var fragment = document.createDocumentFragment(),
            child
        // 将原生节点拷贝至 fragment
        while (child = el.firstChild) {
            fragment.appendChild(child)
        }
        return fragment
    }

    isElementNode(node) {
        return node.nodeType === 1
    }

    isTextNode(node) {
        return node.nodeType === 3
    }

    isDirective(attrName) {
        return attrName.indexOf('v-') === 0
    }
    isEventDirective(dir) {
        return dir.indexOf('on') === 0
    }
}

// 解析指令方法集合
var compileUtil = {

    // v-text
    text(node, vm, exp) {
        this.bind(node, vm, exp, 'text')
    },
    // v-html
    html(node, vm, exp) {
        this.bind(node, vm, exp, 'html')
    },
    // v-class
    class(node, vm, exp) {
        this.bind(node, vm, exp, 'class')
    },
    // v-model
    model(node, vm, exp) {
        this.bind(node, vm, exp, 'model')
    },

    bind(node, vm, exp, updaterType) {
        var updateFn = updater[`${updaterType}Updater`]
        updateFn && updateFn(node, this._getVMVal(vm, exp))
    },

    // 从vm中取到相应的值
    _getVMVal(vm, exp) {
        var data = vm._data
        var value
        exp = exp.split('.')
        exp.forEach(k => {
            value = data[k]
        })
        return value
    },

    eventHandler(node, vm, expValue, dir) {
        // 获取事件类型
        var eventType = dir.split(':')[1],
            // 从 methods 中配置中获取对应事件的回调函数
            fn = vm.$options.methods && vm.$options.methods[expValue]
        if(eventType && fn) {
            // 绑定事件， 必须 bind ，指定 this 为 vm
            node.addEventListener(eventType, fn.bind(vm), false)
        }else {
            throw new Error('event not found !')
        }
    }
}

// 更新节点方法集合
var updater = {
    // 更新节点 textContent
    textUpdater(node, value) {
        node.textContent = typeof value == 'undefined' ? '' : value
    },
    // 更新节点 innerHTML
    htmlUpdater(node, value) {
        node.innerHTML = value
    },
    // 更新节点 classList
    classUpdater(node, value) {
        var className = node.className
        // 合并动、静态 class 值
        node.className = className ? className += ` ${value}` : value
    },
    // 更新节点 value
    modelUpdater() {

    }
}
```