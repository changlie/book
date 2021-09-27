# 内置变量

为了便利，`Quick`提供了一系列的内置变量

### 路径相关

为了快速定位到我们想操作的文件， `Quick`内置了几个变量`qkDir`, `root`, `pwd`, 用于表示一些常用的路径
- `qkDir`： `Quick`执行文件所在的目录
- `root`： 当前脚本文件所在的目录
- `pwd`： 当前命令行所在的路径，与shell命令`pwd`等同

```js
printf("qkDir:%v , root: %v, pwd: %v\n", qkDir, root, pwd)
```

### 命令行参数相关
`cmdArgs`： 命令行参数

### HTTP相关
`mime`: 包含了POST请求常用的Content-Type:
```
mime.json => application/json
mime.form => application/x-www-form-urlencoded
mime.data => multipart/form-data
```

