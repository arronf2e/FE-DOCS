### this

1. what is this

> this 是 js 的关键字之一，它是对象自动生成的一个内部对象，只能在对象内部使用。随着方法调用场合的不同，this 的指向也会发生变化；this 指向什么，完全取决于什么地方以什么方式调用，而不是创建时


2. this

- 纯粹的调用（没啥意义）
 - 非严格模式 nodejs -> global
 - 非严格模式 web  - > window
 - 严格模式下 undefined

```
// nodejs 环境
var name = 'arron'
function foo() {
    console.log(this)
}
foo()    // global

// web 环境
function bar() {
    console.log(this)   
}
bar()  // window

// 严格环境
'use strict'
function bar() {
    console.log(this)   
}
bar()  // undefined
```

- call、apply，第一个参数就是 this 指向的值

```
'use strict'
function hello(a,b) {
    console.log(this, a, b)
}
hello(1, 2)  // undefined 1 2
hello.call(undefined, 1, 2)   // undefined 1 2
hello.apply(undefined, [1,2])  // undefined 1 2
hello.apply('hi', [1,2])      // hi 1 2
```

- bind

```
'use strict'
function hello() {
    console.log(this)
}
var myHello = hello.bind({})
myHello()   //  {}
```

- 作为对象的方法调用

```
function sayName() {
    console.log(this.name)
}
var name = '全局name'
var arron = {
    name: '局部name',
    sayName: sayName
}
sayName()   // 全局name
arron.sayName()  // 局部name
```

- Arrow Function  this 指向定义箭头函数的上下文

```
const obj = {
  x: 1,
  hello: function(){
    console.log(this)     
    const test = () => {
      console.log(this.x)
    }
    test()
  }
}
  
obj.hello() // 1
const hello = obj.hello
hello() // window
```