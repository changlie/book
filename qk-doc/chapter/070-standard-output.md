# 标准输出

- print() 普通的标准输出
- println() 自带换行符的标准输出
- printf() 格式化的标准输出

```js
println("it's ok?")

printf("NO, understand? %v-_- ---> \n", "ruic")

print("en, yeah!")

print("you are right.", "yark")
```
输出
```
it's ok?
NO, understand? ruic-_- ---> 
en, yeah!you are right.yark
```

### 格式化占位符
以下描述适用于内置函数  `printf()`, `fmt()`  
- `printf()`: 格式化后打印
- `fmt()`: 格式化后返回一个字符串  

```
通用
    %%  打印符号%
    %v  打印值
    %T  打印值的Golang类型

Boolean
    %t  打印布尔值

Integer
    %b	二进制形式打印
    %d	十进制形式打印
    %o	八进制形式打印
    %O	八进制形式打印并添加前缀0o
    %q	打印相应的Unicode字符，并用单引号'括起来
    %x	十六进制形式打印(a-f) 
    %X	b十六进制形式打印(A-F) 
    %c	打印Unicode码点对应的字符 
    %U	以 U+1234 这样的形式打印Unicode的码点 

Float
    %b	指数为二次幂的无小数科学记数法 e.g. -123456p-78
    %e	科学计数形式打印, e.g. -1.234456e+78
    %E	科学计数形式打印, e.g. -1.234456E+78
    %f	小数点形式打印, e.g. 123.456
    %F	等同于 %f

	%.2f  小数精确到两位

    %x	十六进制表示法（具有两个指数的十进制幂）, e.g. -0x1.23abcp+20
    %X	大写十六进制表示法, e.g. -0X1.23ABCP+20

String and ByteArray
    %s	字节未解析的形式
    %q	打印时，用双引号"括起来, 并对字符串内的双引号"进行转义
    %x	十六进制形式打印(a-f) 
    %X	b十六进制形式打印(A-F) 
```

