# Byte Array

`Quick`暂不提供直接操作单个字节，并尽量避免直接操作单个字节。  
字节数组一般只有操作文件时才会用到

### ByteArray 创建函数

| 函数   |	描述  |
| ----  | ----  |
| newBytes | 别名: `newbs`, 创建一个空的字节数组 |

```js
bs = newbs()
bs.add(1)
bs.show()
bs.add("a")
bs.show()
bs.add("龙")
bs.show()
```
```
00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000001 
00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000001 01100001 
00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000001 01100001 11101001 10111110 10011001
```

### ByteArray 方法

| 方法   |	描述  |
| ----  | ----  |
| at | 获取指定位置的单个字节字符，以字符串形式返回 |
| equal | 别名：`eq`， 字节数组与ByteArray或String比较 |
| str | 转字符串 |
| int | 转Integer |
| float | 转Float |
| contain | 是否包含指定ByteArray或String |
| index | 指定ByteArray或String在当前字节数组的位置 |
| split | 根据ByteArray, String, Integer或Float对字节数组进行切割 |
| add | 往字节数组里添加ByteArray, String, Integer或Float |
| size | 字节数组大小 |
| show | 以二进制形式打印字节数组 |

```js
bs = newbs()
bs.add("a1b")

println(bs.at(0), bs.at(1), bs.at(2))

bs.add(1024)
println(bs[3:].int())
```
```
a 1 b
1024
```