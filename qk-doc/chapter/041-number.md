# 数值类型
数值类型包含整型`Integer`，浮点型`Float`, 它们皆占64个比特

实例
```js
println(3.14 * 3) // 9.42
println(10 / 3.0) // 3.33333
println(10 / 3) // 3
println(24 / 6) // 4

// 负数
println(10 + -5.5) // 4.5
println(-3.14 + 2) // -1.1400000000000001
echo(-1 + 9.8, 7.3 + - 1.1)
```

## String 转 Number

```js
echo("98".int(), "98".int().type())
echo("0.5".float(), "0.5".float().type())
echo("110".number(), "110".number().type())
echo("6.28".number(), "6.28".number().type())
echo("a".int(), "b".float(), "c".number())
```
```
98 Int
0.5 Float
110 Int
6.28 Float
-1 -1 -1

```

## Number 转 String  
加一个空字符串`""`即可
```js
str = -6.23 + ""
echo(str, str.type())
```
```
-6.23 String
```

## Number 转 ByteArray
```js
i = 10086
f = 3.14
i.bytes().show()
f.bytes().show()
```
```
00000000 00000000 00000000 00000000 00000000 00000000 00100111 01100110 
00011111 10000101 11101011 01010001 10111000 00011110 00001001 01000000 
```
