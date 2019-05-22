### 数组 

> 只列举一些需要注意的方法


- sort()

> sort 方法会将调用每个数组项的 toString() 方法，再进行字符串的比较。会改变原数组

```
var values = [0, 1, 5, 10, 15];
values.sort();
console.log(values)  // [0, 1, 10, 15, 5]


// 如果第一个参数应该位于第二个之前，则返回一个负数，如果两数相等返回为0，如果第一个参数应该位于第二个之后 ，返回一个正数
function campare(value1, value2) {
    if(value1 < value2) {
        return -1;
    }else if(value1 > value2) {
        return 1;
    }else {
        return 0;
    }
}

values.sort(campare)  // [0, 1, 5, 10, 15]
```

> Google Chrome 对 sort 做了特殊处理，对于长度 <= 10 的数组使用的是插入排序(稳定排序算法) ，>10 的数组使用的是快速排序。快速排序是不稳定的排序算法。


- slice(pos1, pos2) 

> 不会改变原数组，取 pos1 到 pos2 的数组值，返回一个新数组，如 pos2 不传，则返回从 pos1 到数组末的一个新数组

```
var arr = ['a', 'b','c']
var c = arr.slice(0,1)   // ['a']
var d = arr.slice(1)     // ['b', 'c']
```

- splice()

> 会改变原数组，返回值为被移除的元素

```
// 基本语法 
array.splice(start, deleteCount, item1, item2 ....)


// 删除
var arr = [1,2,3,4,5]
var removed = arr.splice(0, 2)
console.log(arr, removed) // [3,4,5]   [1,2]


// 插入
var arr = [1,2,3,4,5]
var arr2 = arr.splice(2, 0, 7, 8)
console.log(arr, arr2)   // [1,2,7,8,3,4,5]  []

// 替换
var arr = [1,2,3,4,5]
var arr2 = arr.splice(2, 2, 7, 8)
console.log(arr, arr2)   // [1,2,7,8,5]  [3,4]
```

- reduce

> 迭代数组的所有项，返回一个最终的值 

```
// 累加
array.reduce(function(prev, cur, index, array) {
    return prev + cur
})

// 累积
array.reduce(function(prev, cur, index, array) {
    return prev * cur
})
```