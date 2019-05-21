### 数据类型


#### 基本数据类型

- Undefined 
> 变量定义但未被初始化，其值即为 Undefined。undefined 派生自 null ，所以 undefined == null 

```
var a;
console.log(a);   // undefined
```

- Null 
> 空指针对象，一般定义一个变量是用来存储对象的话，一般初始化为 null

```
var a = null
```

- Boolean
> true or false

```
var isOk = true
```

- Number 
> 数值类型

```
var num1 = 123;
var num2 = 123.34;
var num3 = Infinity;   // 正无穷大
var num4 = -Infinity;  // 负无穷大
var nan = NaN;   // Not a Number

NaN == NaN;    // false
isNaN(nan);    // true
```

- String
> '' or ""

```
var str = 'hello world';
```

- Symbol
> ES6内容



#### 复杂数据类型

- Object

```
var o1 = new Object();
var o2 = {
    name: 'hello'
}
```
