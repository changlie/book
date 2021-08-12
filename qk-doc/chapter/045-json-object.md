# JSON Object

JSON Object功能基本与js一致。


### 初始化
```js
// way 1
obj = {}

// way 2
obj = {name:"tom", age: 88}

// way 3
color = "strawberry"
obj = {
    name: "car",
    special: "carry",
    food: "oil",
    colors: ["red", color, "black"]
}
```

### 键值数量获取
```js
obj = {name:"tom", age: 88}
println(obj.size()) // 2
```

### 键值添加
```js
obj = {}
// way 1
obj["name"] = "jerry"
// way 2
obj.age = 3
println(obj) // {"name":"jerry", "age":3}
```

### 值修改
```js
obj = {"name":"jerry", "age":3}
// way 1
obj["name"] = "tom"
// way 2
obj.age = 18
println(obj) // {"name":"tom", "age":18}
```

### 键值删除
```js
obj = {name:"tom", age: 88}
obj.remove("age")
println(obj) // {"name":"tom"}
```

### 判断是否包含相应键
```js
obj = {name:"tom", age: 88}
println(obj.contain("name")) // true
println(obj.contain("addr")) // false
```

### 遍历
```js
obj = {name:"tom", age: 88}
foreach k, v : obj {
    println(k, v)
}
```
输出
```
age 88
name tom
```


## JSON Object 方法
| 方法 |	描述   |
|  ----  | ----  |
|  size()       | 键值对数量  |
|  remove(key)  | 根据指定键移除键值对  |
|  contain(key))  |  判断是否包含相应键 |