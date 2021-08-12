# 文件操作

## 文件操作函数

| 函数  |	描述   |
|  ----  | ----  |
|  fcontent(path)      |  读取整个文本文件的内容  |
|  flines(path)) |  逐行读取整个文件，返回一个字符串数组   |
|  fjson(path)     |  读取整个json文件, 返回一个json对象  |
|  fout(path, content)     |  清空指定文件，并写入数据 |
|  fappend(path, content)  |  向指定文件以追加的方式写入数据  |
|  fargs(path)  |  从参数文件中获取参数  |
|  fprops(path) | 读取配置文件, 返回一个json对象 |
|  fscan(path)  |  获取指定目录下所有文件的绝对路径  |

### 函数 fargs(path)
参数文件 `/home/xp/ws/test/inputFile` 内容为
```
name age salary
tom  9   1000
jerry 5  5000
```

参数文件 `/home/xp/ws/test/inputFile2` 内容为
```
chenlh.cn, 192.1.1.1
github.com, 192.168.0.1
```
对以上两个文件进行数据获取
```js

args = fargs("/home/xp/ws/test/inputFile")
println(args) // [["name", "age", "salary"], ["tom", "9", "1000"], ["jerry", "5", "5000"]]


args = fargs("/home/xp/ws/test/inputFile2")
println(args) // [["chenlh.cn", "192.1.1.1"], ["github.com", "192.168.0.1"]]

```

### 函数 fprops(path)
配置文件 `/home/xp/ws/test/aprops`
```
# dev mode: true or false
mode=

# service unique name
name=changlie server

port=502
```
配置文件读取
```js
props = fprops("/home/xp/ws/test/aprops")
println("config -> ", props) // config ->  {"name":"changlie server", "port":"502", "mode":""}

```