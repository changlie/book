# foreach 遍历

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