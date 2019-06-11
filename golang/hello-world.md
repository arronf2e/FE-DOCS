```
package main  // 告诉程序当前文件属性哪个包，main 代表它是一个可独立运行的包，它在编译后可产生可执行文件

import "fmt"

func main() {
	fmt.Printf("hello world")
}
```

Go 程序是通过 Package 来组织的

> 每一个可独立运行的Go程序，必定包含一个package main，在这个main包中必定包含一个入口函数main，而这个函数既没有参数，也没有返回值。