# 高阶函数

Quick支持高阶函数，匿名函数。  
这意味着函数可以储存在变量中，可以作为参数传递，可以作为返回值。极大地提高了程序灵活性。

在js中用关键字`function`或`()=>`标识一个函数  
golang中用关键字`func`标识一个函数  
Quick用符号`$`来标识一个匿名函数，非匿名函数无需标识

当匿名函数只有一个返回语句时，可以`->`来表示一个`return`标识符，不写`{}`
```js
upper = $ str -> str.upper()
println(upper("hello")) // HELLO
```
当匿名函数只有一个表达式语句时且没有形参，直接在前面加一个`$`标识即可.
```js
pt = $ println("It's simple function!!!")
pt() // It's simple function!!!
```

示例一：
```js
service(name, fn) {
    println("fn is", fn) // fn is func:()
    printf("%v => %v", name, fn(name)) // tom => tom is a cat!
}

service("tom", $ name {
    return name + " is a cat!"
})
```

示例二：
```js
test(a, b, add) {
    printf("%v + %v = %v\n", a, b, add(a, b)) // 5 + 7 = 12
}

test(5, 7, $ num1, num2 -> num1 + num2)
```