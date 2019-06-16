### JS 原型链

> 名词：prototype, '__proto__', constructor, Object.prototype, Function.prototype, new 

- constructor

```
// constructor
function Person(name, age) {
    this.name = name
    this.age = age
}
var steven = new Person('steven', 23)   // instance
var arron = new Person('arron', 25)     // instance


// 给原型添加一些方法
function Person(name, age) {
    this.name = name
    this.age = age
    this.log = function() {
        console.log(`${this.name}: ${this.age} years old`)
    }
}
var steven = new Person('steven', 23)   // instance
var arron = new Person('arron', 25)     // instance
steven.log()     // steven: 23 years old
arron.log()      // arron: 25 years old
steven.log === arron.log    // false
```

这时候就会发现一个问题， 两个实例的 log 实现的功能是一样的，但却占了不同的空间，怎么优化呢？  将 function 提到到 Person.prototype 上

- prototype

```
function Person(name, age) {
    this.name = name
    this.age = age
}
Person.prototype.log = function() {
    console.log(`${this.name}: ${this.age} years old`)
}
var steven = new Person('steven', 23)   // instance
var arron = new Person('arron', 25)     // instance
steven.log()     // steven: 23 years old
arron.log()      // arron: 25 years old
steven.log === arron.log    // true
```

那么 instance 是通过什么去 Person.prototye 上去找 log 这个方法呢，答案就是 __proto__

- __proto__

```
function Person(name, age) {
    this.name = name
    this.age = age
}
Person.prototype.log = function() {
    console.log(`${this.name}: ${this.age} years old`)
}
var steven = new Person('steven', 23)   // instance
steven.log()     // steven: 23 years old
steven.__proto__ === Person.prototype
```

如果在 Person.prototype 上也找不到该方法呢？就会去 Person.prototype.__proto__ 上去找，找到某个东西的 __proto__ 是 null 为止。

```
function Person(name, age) {
    this.name = name
    this.age = age
}
Person.prototype.log = function() {
    console.log(`${this.name}: ${this.age} years old`)
}
var steven = new Person('steven', 23)   // instance
console.log(steven.__proto__ === Person.prototype)              // true
console.log(Person.prototype.__proto__ === Object.prototype)    // true
console.log(Object.prototype.__proto__ === null)                // true
```

那么如何判断找到的方法是实例上还是原型上的叫？  hasOwnProperty

- hasOwnProperty

```
function Person(name, age) {
    this.name = name
    this.age = age
}
Person.prototype.log = function() {
    console.log(`${this.name}: ${this.age} years old`)
}
var steven = new Person('steven', 23)   // instance
steven.hasOwnProperty('log')   // false
steven.__proto__.hasOwnProperty('log')   // true
```

- instance

```
a instance A    // 判断 a 是否是 A 的一个实例

function Person(name, age) {
    this.name = name
    this.age = age
}
Person.prototype.log = function() {
    console.log(`${this.name}: ${this.age} years old`)
}
var steven = new Person('steven', 23)   // instance
steven instanceof Person   // true
steven instanceof Object   // true
steven instanceof Array    // false

// 实现一个自己的 instance0f

function instance0f(a, A) {
    if(!a) {
        return false
    }
    return a.__proto__ === A.prototype ? true : instanceOf(a.__proto__, A)
}
```

有趣的现象：
```
// 互为彼此的 instance
console.log(Function instanceof Object); // true
console.log(Object instanceof Function); // true
  
// Function 的 __proto__ 會指向 Function.prototype
// 而 Function.prototype 的 __proto__ 會指向 Object.prototype
console.log(Function.__proto__ === Function.prototype); // true
console.log(Function.__proto__.__proto__ === Object.prototype); //true
  
// Object 的 __proto__ 會指向 Function.prototype
console.log(Object.__proto__ === Function.prototype); // true
```

- constructor  每个 prototype 都有一个 constructor 的属性，该属性指向构造函数

```
function Person(name, age) {
    this.name = name
    this.age = age
}
Person.prototype.log = function() {
    console.log(`${this.name}: ${this.age} years old`)
}
var steven = new Person('steven', 23)   
steven.constructor                               // Person        
steven.hasOwnProperty('constructor')             // false
Person.prototype.constructor === Person          // true
Person.prototype.hasOwnProperty('constructor')   // true
```

- new 
    - 创建一个新的 object
    - 把 object 的 __proto__ 指向 构造函数的 prototype
    - 把 object 当作上下文，调用构造函数
    - 返回 object

```
function Person(name, age) {
  this.name = name;
  this.age = age;
}
Person.prototype.log = function () {
  console.log(`${this.name}: ${this.age} years old`)
}
function _new(Constructor, arguments) {
    var o = new Object()
    o.__proto__ = Constructor.prototype
    Constructor.apply(o, arguments)
    return o
}
var steven = _new(Person, ['steven', 23])
steven.log()                            // steven: 23 years old
```