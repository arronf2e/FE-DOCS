#### 工厂模式

```
function createPerson(name, age, job) {
    var o = new Object()
    o.name = name
    o.age = age
    o.job = job
    o.sayName = function() {
        alert(this.name)
    }
    return o
}

var arron = createPerson('arron', 23, 'it')
arron.sayName()   // arron
```

#### 构造函数模式

```
function Person(name, age, job) {
    this.name = name
    this.age = age
    this.job = job
    this.sayName = function() {
        alert(this.name)
    }
}
var arron = new Person('arron', 23, 'it')
arron.sayName()   // arron
arron.constructor === Person  // true
arron instanceof Person       // true
arron instanceof Object       // true\
```
> 存在的问题： 每个实例都会创建一个 sayName function


#### 原型模式

```
function Person() {}
Person.prototype.name = 'arron'
Person.prototype.age = 23
Person.prototype.job = 'it'
Person.prototype.sayName = function() {
    alert(this.name)
}
var arron = new Person()
arron.sayName()   // arron

arron.name = 'jerry'
arron.sayName()
```

> 如何判断 name 是实例上的属性还是原型上的属性呢

```
arron.hasOwnProperty('name')   // true
delete arron.name
arron.hasOwnProperty('name')   // false
```

#### 构造函数+原型模式 (常用)

```
function Person(name, age, job) {
    this.name = name
    this.age = age
    this.job = job
}
Person.prototype.sayName = function() {
    alert(this.name)
}
var arron = new Person('arron', 23, 'it')
arron.sayName()  // arron
```

#### 动态原型模式

```
function Person(name, age, job) {
    this.name = name
    this.age = age
    this.job = job
    if(typeof this.sayName != 'function') {
        Person.prototype.sayName = function() {
            alert(this.name)
        }
    }
}

var arron = new Person('arron', 23, 'it')
arron.sayName()  // arron
```

#### 稳妥构造函数模式

```
function Person(name, age, job) {
    var o = new Object()
    o.sayName = function() {
        alert(name)
    }
    return o
}
var arron = Person('arron', 23, 'it')
arron.sayName()
```