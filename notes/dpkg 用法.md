---
tags: [undefined]
title: dpkg 用法
created: '2022-02-15T09:45:56.481Z'
modified: '2022-02-15T09:47:41.236Z'
---

# dpkg 用法

dpkg 是Debian Package的简写，是为Debian 专门开发的套件管理系统，方便软件的安装、更新及移除。所有源自Debian的Linux发行版都使用dpkg，例如Ubuntu、Knoppix 等。
以下是一些 Dpkg 的普通用法：
1、dpkg -i <package.deb>
安装一个 Debian 软件包，如你手动下载的文件。
2、dpkg -c <package.deb>
列出 <package.deb> 的内容。
3、dpkg -I <package.deb>
从 <package.deb> 中提取包裹信息。
4、dpkg -r <package>
移除一个已安装的包裹。
5、dpkg -P <package>
完全清除一个已安装的包裹。和 remove 不同的是，remove 只是删掉数据和可执行文件，purge 另外还删除所有的配制文件。
6、dpkg -L <package>
列出 <package> 安装的所有文件清单。同时请看 dpkg -c 来检查一个 .deb 文件的内容。
7、dpkg -s <package>
显示已安装包裹的信息。同时请看 apt-cache 显示 Debian 存档中的包裹信息，以及 dpkg -I 来显示从一个 .deb 文件中提取的包裹信息。
8、dpkg-reconfigure <package>
