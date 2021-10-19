# 内置函数

`Quick`的标准库通过内置函数提供，它本身毫无扩展性可言。  
但你要做的事在它的服务范围内，它可能是个很好的选择。

### 命令行相关
使用这些命令使得我们可以用`Quick`替代 Shell脚本， windows的批处理脚本(`cmd`)

| 函数   |	描述  |
| ----  | ----  |
| cmd | 命令行调用 (windows下用的`cmd.exe`, 每次只能执行单个命令； linux下用的`bash`, 一次可执行多个命令) |
| setpwd | 别名：`cd`,  设置工作路径（命令行的当前路径） |

### 系统相关

| 函数   |	描述  |
| ----  | ----  |
| sys | 获取当前系统名称 |
| cpuNum | 获取cpu的逻辑核数 |
| envs | 获取所有环境变量 |
| env | 获取单个环境变量 |
| setenv | 设置环境变量(仅对当前脚本有效) |
| home | 获取并打印环境变量QK_HOME |
| cost | 统计脚本耗时 |
| openBrowser(url) | 别名`ob`, 在浏览器中打开指定url |

### 常用函数

| 函数   |	描述  |
| ----  | ----  |
|  sleep(ms)  |  使当前协程进入休眠状态，单位为ms  |
|  uuid()  | 返回32个随机字符[0-9a-z]组成的字符串 |
|  uuidRaw()  | 带'-'的uuid |
|  key16()  | 生成16字节长度的随机key,以base64形式返回 |
|  key24()  | 生成24字节长度的随机key,以base64形式返回 |
|  key32()  | 生成32字节长度的随机key,以base64形式返回 |

### 编码相关

| 函数   |	描述  |
| ----  | ----  |
|  base64Encode  |  别名`base64`, base64编码  |
|  base64Decode  |  别名`debase64`, base64解码  |
|  gzipEncode  |  别名`gzip`, gzip编码  |
|  gzipDecode  |  别名`degzip`, gzip解码  |
|  md5  |  md5编码  |
|  aesEncrypt(data, key)  |  别名`aes`, AES对称加密  |
|  aesDecrypt(data, key)  |  别名`deaes`, AES对称解密  |

```js
tmp = gzip("中华人民共和国")
println(tmp)
printf("%X\n", tmp)
println(degzip(tmp))
println(base64(tmp))
println(degzip(tmp).str())

println("-----------------------")
tmp = base64("一念花开，君临天下")
println(tmp)
println(debase64(tmp))
println(debase64(tmp).str())

println("-----------------------")
tmp = md5("一念天堂，一念地狱。上穷碧落下黄泉，我主沉浮。")
println(tmp)
println(md5(123456))

println("AES-----------------------")
k = key32()
data = "繁星璀璨，独赏明月"
tmp = aes(data, k)
println(k)
println(tmp)
println(deaes(tmp, k))
```