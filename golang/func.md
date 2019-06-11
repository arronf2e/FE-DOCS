1. 定义

```
func funcName(input1 type1, input2 type2) (output1 type1, output2 type2) {
	//这里是处理逻辑代码
	//返回多个值
	return value1, value2
}
```

2. 传值与传指针

```
a := 1
b := 2

func sum(a int, b int) (sum int) {
    return a + b
}

func sum2(a *int, b *int) int {
    *a = *a + 1
    return *a * *b
}

```

3. defer 延迟语句 （后进先出）

```
for i:= 0; i < 10; i++ {
    defer fmt.Print(i)    // 9876543210
}
```

4. Panic和Recover

5. main() 适用于所有 package   init()  只应用于 package main

> 保留函数，不能有任何参数与返回值 

!(https://github.com/astaxie/build-web-application-with-golang/raw/master/zh/images/2.3.init.png?raw=true)[https://github.com/astaxie/build-web-application-with-golang/raw/master/zh/images/2.3.init.png?raw=true]


6. import 

```
import "fmt"

import ."fmt"   // 调用方法的时候不需要加前缀，直接  Printf

import f "fmt"  // 别名

import _ "fmt"  // 引入包，调用了包的 init 函数，不直接使用包里面的函数
```