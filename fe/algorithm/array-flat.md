###  数组扁平化


1. 循环 + 递归

```
function flattern(arr, result = []) {
    var length = arr.length
    for(var i = 0; i < length; i++) {
        if(Array.isArray(arr[i])) {
            flattern(arr[i], result)
        }else {
            result.push(arr[i])
        }
    }
    return result
}

var a = [1,2,3,4,[5,6,[7,8,9,10]]]
flattern(a)   // [1,2,3,4,5,6,7,8,9,10]
```

2. toString

```
function flattern(arr) {
    var arrString = arr.toString()
    return arrString.split(',').map(item => parseInt(item))
}

var a = [1,2,3,4,[5,6,[7,8,9,10]]]
flattern(a)   // [1,2,3,4,5,6,7,8,9,10]
```

3. ES6 展示符

```
function flattern(arr) {
    while(arr.some(item => Array.isArray(item))){
        arr = [].concat(...arr)
    }
    return arr
}

var a = [1,2,3,4,[5,6,[7,8,9,10]]]
flattern(a)   // [1,2,3,4,5,6,7,8,9,10]
```