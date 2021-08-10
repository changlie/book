# JSON Array

Quick的数组的功能与js的基本一致  

### 初始化
```js
arr1 = []

arr2 = [1, false, "NT"]

str = "thor"
arr3 = [str, true]
```

### 查看数组长度
```js
arr = [1, false, "NT"]
println(arr.size()) // 3
```

### 获取数组元素
```js
arr = [1, 2, 3, "a", "b", "c"]
println(arr[1]) // 2
println(arr[3]) // "a"
```

### 数组截取
```js
arr = [1, 2, 3, "a", "b", "c"]
println(arr[4:]) // ["b", "c"]
println(arr[:2]) // [1, 2]
println(arr[3:5]) // ["a", "b"]
```

### 数组元素赋值
```js
arr = [1, false, "NT"]
arr[1] = "change"
println(arr) // [1, "change", "NT"]
```

### 添加元素
```js
arr = [1, false, "NT"]
arr.add(998)
arr.add(3.14, "jerry")
println(arr) // [1, false, "NT", 998, 3.14, "jerry"]
```

### 删除元素
```js
arr = [1, false, "NT"]
arr.remove(1)
println(arr) // [1, "NT"]
```

### 根据指定字符，将数组所有元素拼接成字符串
```js
arr = [1, false, "D"]
println( arr.join(",")) // 1,false,D
println( arr.join(", ")) // 1, false, D
println( arr.join("#")) // 1#false#D
```

### for遍历
```js
arr = [1, false, "NT"]
for i=0; i<arr.size(); i++ {
    println(i, arr[i])
}
```
输出
```
0 1
1 false
2 NT
```

### foreach遍历
```js
arr = [998, true, "DONE"]
foreach i, item : arr {
    println(i, item)
}
```
输出
```
0 998
1 true
2 DONE
```


### 数组方法

| 方法 |	描述   |
|  ----  | ----  |
|  size()         | 数组元素数量 |
|  add(elem)      |  添加元素 |
|  remove(index)  |  移除元素 |
|  join(seperator)   |  根据指定字符，将数组所有元素拼接成字符串 |