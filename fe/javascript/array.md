### 数组 


- sort()

> sort 方法会将调用每个数组项的 toString() 方法，再进行字符串的比较。会改变原数组

```
var values = [0, 1, 5, 10, 15];
values.sort();
console.log(values)  // [0, 1, 10, 15, 5]
```
