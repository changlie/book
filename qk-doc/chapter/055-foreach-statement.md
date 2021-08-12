# foreach 遍历

`foreach`, `fori`, `forv` 同属一个类型，`fori`, `forv`为更方便而提供。  
只有`String`, `JSONObject`, `JSONArray`三种类型可以使用`foreach`

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