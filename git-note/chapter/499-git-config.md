# git config

参考  
[git config](https://www.cnblogs.com/fireporsche/p/9359130.html)

### 常用例子
1. 指定仓库忽略SSL证书验证
```
cd repositoryDir
env GIT_SSL_NO_VERIFY=true git clone https://<host_name>/<username>/project.git
git config http.sslVerify false
```
2. 忽略所有仓库SSL证书验证
```
git config --global http.sslVerify false
```

### 优先级
在git中，我们使用git config 命令用来配置git的配置文件，git配置级别主要有以下3类：

1. 仓库级别 local 【优先级最高】
2. 用户级别 global【优先级次之】
3. 系统级别 system【优先级最低】

### 配置文件相应位置
**git 仓库级别** 对应的配置文件是当前仓库下的.git/config 【windows: 在当前目录下.git目录默认是隐藏的，所以在文件管理器中我们要打开显示以藏文件】  

**git 用户级别** 对应的配置文件是用户宿主目录下的~/.gitconfig 【windows: C:\Users\usernamexxx】  

**git 系统级别** 对应的配置文件是git安装目录下的 /etc/gitconfig【windows: e.g.D:\Program Files\Git\mingw64\etc】

### 查看配置
1. git config --local -l 查看仓库配置【必须要进入到具体本地仓库的目录下】
2. git config --global -l 查看用户配置
3. git config --system -l 查看系统配置

