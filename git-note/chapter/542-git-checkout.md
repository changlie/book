# git checkout

### git checkout
本地库有分支：master; 远程库有分支：master, dev  
```
git checkout dev
```
执行以上命令后，Git会在本地库创建一个dev分支，并把这个分支指向远程库的dev分支，同时本地库当前分支会切换至dev分支


### git checkout -b
本地库有分支：master; 远程库有分支：master.  
执行命令 `git checkout -b dev`, Git会在本地库创建一个dev, 但由于这个一个远程库没有的新分支，所以首次提交更改时需执行命令`git push -u origin dev`, 使得本地库的dev分支指向远程库的dev分支