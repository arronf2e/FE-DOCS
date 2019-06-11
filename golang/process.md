#### if

```
if x > 10 {

}else {

}

if x > 10 {

}else if x > 20 {
    
}else {

}
```

> Go的if还有一个强大的地方就是条件判断语句里面允许声明一个变量，这个变量的作用域只能在该条件逻辑块内，其他地方就不起作用了

```
if x := computedValue(); x > 10 {
	fmt.Println("x is greater than 10")
} else {
	fmt.Println("x is less than 10")
}
```


#### for

```
for expression1; expression2; expression3 {
	//...
}


sum := 0
for index := 0; index < 10; index++ {
    sum += index
}
fmt.Print(sum)   // 45
```

#### switch  ，每个 case 后面默认带了 break，如需强制执行后续case ，加入 fallthrough

```
switch sExpr {
    case expr1:
        some instructions
    case expr2:
        some other instructions
        fallthrough  // 继续执行以下 case
    case expr3:
        some other instructions
    default:
        other code
}
```