### Object.defineProperty

> 在一个对象上定义一个新的属性，或者是修改已存在的属性。最终这个方法会返回该对象。

1. 语法  

```
Object.defineProperty(obj, prop, descriptor)
```

descriptor中各特性： 

- value         

> 该属性对应的值，默认为 undefined；会默认帮把writable，configurable，enumerable。都设上值，而且值还都是false

```
var obj = {name: 'arron'}
Object.defineProperty(obj, 'age', {})
obj: {name: 'arron', age: undefined}

var obj = {name: 'arron'}
Object.defineProperty(obj, 'age', {
    value: 23
})
obj: {name: 'arron', age: 23}
```


- configurable  (Boolean)

> 当且仅当该属性的 configurable 为 true 时，该属性描述符才能够被改变，同时该属性也能从对应的对象上被删除。默认为 false。

```
var a= {b: 1}
Object.defineProperty(a,"b",{
  configurable:true
})
a.b = 2

// {b: 2}

var a= {b: 1}
Object.defineProperty(a,"b",{
  configurable:false
})
delete b.b

// {b: 1}
```
- enumerable    (Boolean)

> 此属性是否可以被枚举（使用for...in或Object.keys()）

```
var a= {b: 1}
Object.defineProperty(a,"b",{
  enumerable:false
})
Object.keys(a) // []

var a= {b: 1}
Object.defineProperty(a,"b",{
  enumerable:true
})
Object.keys(a) ['b']

```

- writable      (Boolean)

> 属性的值是否可以被重写

```
var a= {b: 1}
Object.defineProperty(a,"b",{
  writable:true
})
a.b = 2

a  {b: 2}

var a= {b: 1}
Object.defineProperty(a,"b",{
  writable:false
})
a.b = 2

a  {b: 1}
```

- get           (Function)

> 当获取值的时候触发的函数

```
var a = {b: 1}
Object.defineProperty(a, 'b', {
    get: function() {
        console.log('get a.b')
    }
})
a.b     //  get a.b
```

- set           (Function)

> 当设置值的时候触发的函数

```
var a = {b: 1}
Object.defineProperty(a, 'b', {
    set: function(value) {
        console.log('set a.b, newvalue: ' + value)
    }
})
a.b = 2    //  set a.b, newvalue: 2
```

#### 同时定义多个属性

```
var person = {}
Object.defineProperties(person, {
    age: {
        value: 23
    },
    name: {
        value: 'arron',
    }
})
```

#### 读取属性的特性

```
Object.getOwnPropertyDescriptor(obj, prop)
```

