# 循环遍历
## for 循环
```js
println("demo1 ================")
for a = 0; a < 5; a++ {
    println("current value:", a)
}

println("demo2 ================")
arr = [1, false, true, 3.14, "changlie"]
for a = 0 ; a < arr.size(); a++ {
    println("current value:", arr[a])
}
```

## foreach 键值遍历
```js
println("array test..")
arr = [1, false, true, 3.14, "changlie"]
foreach i, item : arr {
    println("index:", i, "; item:", item)
}

println("=================")
println("object test:")
obj = {name:"changlie", age:18, addr:"sz", marriage: false}
foreach key, val : obj {
    println(key, "->", val)
}
```

## forindex 索引遍历
```js
println("array test..")
arr = [1, false, true, 3.14, "changlie"]
fori i : arr {
    println("index:", i)
}

println("=================")
println("object test:")
obj = {name:"changlie", age:18, addr:"sz"}
fori key : obj {
    println("key:", key)
}
```

## forvalue 值遍历
```js
println("array test..")
arr = [1, false, true, 3.14, "changlie"]
forv item : arr {
    println("item:", item)
}

println("=================")
println("object test:")
obj = {name:"changlie", age:18, addr:"sz"}
forv val : obj {
    println("value:", val)
}
```