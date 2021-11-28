## 字符串类型

Quick支持js那样的动态字符串：
```js
rows = [
{name:"changlie", age:18},
{name:"philip", age:30},
{name:"baby", age:1}
]

forv row : rows {
    line = `this age of student ${row.name} is ${row.age}`
    println(line)
}
```
输出
```
this age of student changlie is 18
this age of student philip is 30
this age of student baby is 1
```

普通字符串与动态字符串的区别：
1. 动态字符串可以引用变量，普通字符串不行
2. 普通字符串会对\n, \r, \t等字符进行转义，动态字符串不会

两者同点是，它们都可以跨行。


#### 字符串初始化
```js
s = ``
s1 = ""

animal = "dog"
number = 23
s2 = `the number of ${animal} is ${number}`
s4 = "China."
println(s2)
println(s4)

s5 = `++++++++++
line 1
line 2
++++++++++`
s6 = "##############
number one
number two
number three
##############"
println(s5)
println(s6)
```
输出
```
the number of dog is 23
China.
++++++++++
line 1
line 2
++++++++++
##############
number one
number two
number three
##############
```

#### 字符串长度
```
println("China".size()) // 5
println("疑是银河落九天".size()) // 7
```

#### 字符获取
```js
str = "中华人民共和国Great"
println(str[3]) // 民
println(str[8]) // r
```

#### 字符串截取
```js
str = "中华人民共和国Great"
println(str[:3]) // 中华人
println(str[4:7]) //共和国
println(str[7:]) //Great
```

### 字符串遍历
```js
str = "中华人民共和国Great"
foreach i, char : str {
    println(i, char)
}
```
输出
```
0 中
1 华
2 人
3 民
4 共
5 和
6 国
7 G
8 r
9 e
10 a
11 t
```

### 字符串方法

| 方法  |	描述   |
|  ----  | ----  |
|  size()  | 字符串长度  |
|  trim()  | 清除字符串两边的空白符  |
|  split(string)  |  根据指定字符对字符串进入切割 |
|  replace(old, new)  | 子字符串替换  |
|  lower()  | 字符串转小写  |
|  upper()  | 字符串转大写  |
|  title()  |  单词首字母转大写 |
|  upperFirst()  | 首字符转大写  |
|  contain(str)  | 别名: `has`,是否包含指定字符串  |
|  hasPrefix(str) | 是否包含相应前缀 |
|  hasSuffix(str) | 是否包含相应后缀 |
|  is(str) | 忽略大小写的字符串比较 |
```js
s = "hello world    "
println("size: ", s.size()) // size:  15

printf("trim: -%v-; %v\n", s.trim(), s.size()) // trim: -hello world-; 15
println("split: ", s.split(" ")) // split:  ["hello", "world", "", "", "", ""]
println("replace: ", s.replace("he", "wc")) // replace:  wcllo world    
println("upper: ", s.upper()) // upper:  HELLO WORLD    
println("title: ", s.title()) // title:  Hello World    
println("upperFirst: ", s.upperFirst()) // upperFirst:  Hello world    
println("contain: ", s.contain("wo"), s.contain("jk")) // contain:  true false  

s = "helle"
println(s.eic("helle")) // true
println(s.eic("heLLE")) // true
println(s.eic("heiie")) // false
println(s.eic("hei")) // false

println("====================")
println(s.hasPrefix("he")) // true
println(s.hasPrefix("hx")) // false
println(s.hasSuffix("lO")) // true
println(s.hasSuffix("lo")) // false
```
