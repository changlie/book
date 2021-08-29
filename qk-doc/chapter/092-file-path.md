# 内置根路径变量

为了快速定位到我们想操作的文件， `Quick`内置了几个变量`qkDir`, `root`, `pwd`, 用于表示一些常用的路径

```js
printf("qkDir:%v , root: %v, pwd: %v\n", qkDir, root, pwd)
```

### qkDir
qk执行文件所在的目录

### root
当前脚本文件所在的目录

### pwd
当前命令行所在的路径，与`pwd`等同
