# 变量作用域
`Quick`是允许变量不用显示定义(声明)的，首次赋值会自动定义。变量作用域规则如下：

- 若变量在当前作用域没定义， 父级作用域已存在变量， 则使用父级作用域的变量
- 当前作用域与父级作用域存在相同名字的变量， 则使用当前作用域的变量
- 如果变量在所有作用域未定义，默认定义在当前作用域
- 当父级作用域已定义该变量，可以使用关键字`var`让变量定义在当前作用域
- for/foreach 会默认使用当前作用域

```js

a, b = 998, "tom"

echo(a, b, "start")

demo() {
    var a, b = true, now()
    echo(a, b)
}
demo2() {
    echo("-----------------")
    echo(a, b, "20")
    var a, b
    echo(a, b, "21")
    a = 999
    b = 111
    echo(a, b, "29")
    echo("-----------------")
}
demo3() {
    echo("-----------------")
    echo(a, b, "demo3")
    var a = "xxx"
    var b = "AAA"
    echo(a, b, "demo3")
    echo("-----------------")
}

demo()
demo2()
demo3()
echo(a, b, "finally")
```