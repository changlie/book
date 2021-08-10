# 自定义函数

Quick中只有函数才会创建新的作用域

Quick的匿名函数需要`$`来标识，非匿名的普通函数不需要  
普通函数只需定义`函数名`，`函数形参`，`函数体`即可：
```js
add(num1, num2) {
    res = num1 + num2
    return res
}
c = add(3*3, 4*4)
println("result:", add(5, 9), c) // result: 14 25
```

Quick函数与js类似，实参数是可以比形参少的。  
当你定义了形参，却不给它传值时，它的值为null:
```js
test(a, b, c) {
    printf("a=%v, b=%v, c=%v\n", a, b, c) // a=fast, b=null, c=null
}
test("fast")
```


函数定义完成可以立即调用，这样使用方式一般是想创建新的作用域才用
```js
${
    println("It's in anonymous function")
}() // It's in anonymous function

testx(name){
    printf("It's in %v function\n", name)
}("normal") // It's in normal function
```