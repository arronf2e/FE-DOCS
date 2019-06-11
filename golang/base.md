### 基础 

#### 变量

```
// 定义单个变量
var variable type

// 定义多个变量
var variable1, variable2, variable3 type

// 初始化
var variable type = value

// 同时初始化多个
var variable1, variable2, variable3 type = val1, val2, val3

// 简单一点
var variable1, variable2, variable3 = val1, val2, val3

// 再简单一点，只能在函数内部使用
variable1, variable2, variable3 = val1, val2, val3
```

> 已声明未赋值的变量，在编译阶段会报错

```
var name string        // name declared and not used
```


#### 常量

```
const constantName = value
//如果需要，也可以明确指定常量的类型：
const Pi float32 = 3.1415926
```

#### 基础数据类型

- boolean

- 数值类型

> 整数类型有无符号和带符号两种。Go同时支持int和uint，这两种类型的长度相同，但具体长度取决于不同编译器的实现。Go里面也有直接定义好位数的类型：rune, int8, int16, int32, int64和byte, uint8, uint16, uint32, uint64。其中rune是int32的别称，byte是uint8的别称。  

- string  

Go 中的字符串是不可变的

```
var name string = "steven"
name[1] = 'c'   // cannot assign to name[1]

// 修改字符串
s := "hello"
c := []byte(s)  // 将字符串 s 转换为 []byte 类型
c[0] = 'c'
s2 := string(c)  // 再转换回 string 类型
fmt.Printf("%s\n", s2)

// 多行字符串
m := `hello
    world`
```

- 错误类型

```
err := errors.New("error message")
fmt.Print(err)
```

![https://github.com/astaxie/build-web-application-with-golang/raw/master/zh/images/2.2.basic.png?raw=true](https://github.com/astaxie/build-web-application-with-golang/raw/master/zh/images/2.2.basic.png?raw=true)


#### array

```
var arr [n]type

var a [3] int
a := [3]int{1, 2, 3}

doubleArr := [2][4]int{[4]int{1, 2, 3, 4}, [4]int{5, 6, 7, 8}}
easyArray := [2][4]int{{1, 2, 3, 4}, {5, 6, 7, 8}}
```

#### 动态数组 slice

> slice并不是真正意义上的动态数组，而是一个引用类型。slice总是指向一个底层array，slice的声明也可以像array一样，只是不需要长度。

```
var fslice []int

slice := []byte {'a', 'b', 'c', 'd'}
```

#### map 字典 

> 与 slice 一样，也是一个引用类型

```
// 声明一个key是字符串，值为int的字典,这种方式的声明需要在使用之前使用make初始化
var numbers map[string]int
// 另一种map的声明方式
numbers = make(map[string]int)
numbers["one"] = 1  //赋值
numbers["ten"] = 10 //赋值
numbers["three"] = 3

fmt.Println("第三个数字是: ", numbers["three"]) // 读取数据
// 打印出来如:第三个数字是: 3
```
