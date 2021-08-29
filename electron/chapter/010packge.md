# 打包

### electron-packager
[github地址](https://github.com/electron/electron-packager)

全局安装electron-packager
```
cnpm install -g electron-packager
```

设置镜像(不知有用没用)
```
export ELECTRON_MIRROR="https://cdn.npm.taobao.org/dist/electron/"
```

执行打包命令
```
electron-packager .
```


electron-packager 命令详解
```
electron-packager <sourcedir> <appname> --platform=<platform> --arch=<arch> [optional flags...]
```
- `--platform` 操作系统： "linux" | "win32" | "darwin" | "mas"
- `--arch` cpu架构： "ia32" | "x64" | "armv7l" | "arm64" | "mips64el"
- `--electron-version` `electron`版本  e.g. --electron-version=13.2.2

示例： 在linux下打包windows执行文件
第一步：安装 wine64
```
sudo apt install wine64 --fix-missing
```
第二步：打包electron应用
```
electron-packager . --electron-version=13.2.2 --platform=win32 --arch=x64
```

