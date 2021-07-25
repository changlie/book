## 字符串类型

### 字符串常用方法

| 方法名  |	描述   |
|  ----  | ----  |
|  size()  | 字符串长度  |
|  trim()  | 清除字符串两边的空白符  |
|  split(string)  |  根据指定字符对字符串进入切割 |
|  replace(old, new)  | 字符串替换  |
|  upper()  | 字符串转大写  |
|  title()  |  单词首字母转大写 |
|  upperFirst()  | 首字符转大写  |
|  sub(start[, end])  |  根据索引获取子字符串 |
|  contain(str)  | 是否包含指定字符串  |
| hasPrefix(str) | 是否包含相应前缀 |
| hasSuffix(str) | 是否包含相应后缀 |
| eic(str) | equalsIgnoreCase() 忽略大小写的字符串比较 |
```js
s = "hello world    "
println("size: ", s.size()) // size:  15

printf("trim: -%v-; %v\n", s.trim(), s.size()) // trim: -hello world-; 15
println("split: ", s.split(" ")) // split:  ["hello", "world", "", "", "", ""]
println("replace: ", s.replace("he", "wc")) // replace:  wcllo world    
println("upper: ", s.upper()) // upper:  HELLO WORLD    
println("title: ", s.title()) // title:  Hello World    
println("upperFirst: ", s.upperFirst()) // upperFirst:  Hello world    
println("sub: ", s.sub(2), "; ", s.sub(3, 7)) // sub:  llo world     ;  lo w
println("contain: ", s.contain("wo"), s.contain("jk")) // contain:  true false

s = "hellO"
println(s.eic("hello")) // true
println(s.eic("hellO")) // true
println(s.eic("hell0")) // false

println("====================")
println(s.hasPrefix("he")) // true
println(s.hasPrefix("hx")) // false
println(s.hasSuffix("lO")) // true
println(s.hasSuffix("lo")) // false
```


### 其他函数
| 函数  |	描述   |
|  ----  | ----  |
|  str_uuid()  |  32位随机字符 |
|  str_rawUUID()  | 原始uuid  |
|  str_format(fmt, args...)  | 字符串格式化 |

```js

s = str_uuid()
println("uuid:", s) // uuid: 10795f4d31032b44a65bb1905c140cb3

s1 = str_rawUUID()
println("rawuuid:", s1) // rawuuid: 0eb9b200-9841-d514-f185-102320132bd4

println("string format testing=============")
println(str_format("He is %v, a blue %v", "tom", "cat")) // He is tom, a blue cat
println(str_format("number format: %.3f", 9.3126789)) // number format: 9.313
println(str_format("number format: %.3f", 3.14)) // number format: 3.140
```