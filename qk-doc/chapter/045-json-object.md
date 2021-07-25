# JSON对象类型

## 常用方法
| 方法 |	描述   |
|  ----  | ----  |
|  size()       | 键值对数量  |
|  remove(key)  | 根据指定键移除键值对  |
|  contain(key)  |  判断是否包含相应键 |

```js
color = "strawberry"

// 初始化
obj = {
    name: "car",
    special: "carry",
    food: "oil",
    colors: ["red", color, "black"]
}

color = "gray"
println("after change color value:", color)

printf("size: %v, values: %v \n", obj.size(), obj)

// 新增键值对
obj.weight = 998
obj.isNew = false
printf("size: %v, values: %v \n", obj.size(), obj)

// 移除键值对
obj.remove("special")
printf("size: %v, values: %v \n", obj.size(), obj)

println("contain name:", obj.contain("name"))
println("contain special:", obj.contain("special"))

list = obj.colors
println("arr vals:", list, list.size())
println("arr value:", list[1])
```

## 新增键值对
```js
obj = {}
k = "name"
obj[k] = "changlie" // way 1
obj.age = 18 // way 2
obj["addr"] = "sz" // way 3
println(obj)
```