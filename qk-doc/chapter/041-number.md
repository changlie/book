# 数值类型
数值类型包含整型，浮点型

实例
```js
println(3.14 * 3) // 9.42
println(10 / 3.0) // 3.33333
println(10 / 3) // 3
println(24 / 6) // 4

// 负数
println(10 + -5.5) // 4.5
println(-3.14 + 2) // -1.1400000000000001
```

## 字符串转数值类型
使用内置函数`number(str)`
```js
println(fix(number("-2.2")+1, 3)) // -1.2
```

## 数值类型转字符串
加一个空字符串`""`即可
```js
-6.23 + ""
```

## 数学函数

| 函数  |	描述   |
|  ----  | ----  |
|  abs(number)      |  取绝对值     |
|  pow(number, int) |  次方计算     |
|  sqrt(number)     |  平方根计算   |
|  round(float)     |  四舍五入取整 |
|  fix(float, int)  |  精确小数位  |

实例
```js
println(abs(-3.15)) // 3.15
println(pow(4, 3)) // 64
println(sqrt(81)) // 9
println(round(3.14)) // 3
println(round(6.5)) // 7
println(fix(3.8213, 2)) // 3.82
println(fix(2.5591, 2)) // 2.56
```



## 随机数

| 函数  |	描述   |
|  ----  | ----  |
|  random(n)  | 产生[0, n)的非负随机数 |
|  random(n, m)  |  产生[n, m)的非负随机数 |

```js
for i = 0; i<20; i++ {
    println(i, "->", random(10))
}

println("----------------------")
println("######################")
println("----------------------")

for i = 0; i<20; i++ {
    println(i, "->", randomRange(10, 15))
}
```