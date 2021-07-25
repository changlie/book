# 控制语句
Quick 包含以下控制语句：
- if 条件控制语句
- for  一般循环
- foreach 索引，值遍历
- fori 索引遍历
- forv 值遍历
- break 中止整个循环／遍历
- continue 中止循环／遍历的当前轮的程序执行
- return 函数返回

#### 示例一
```js
arr = [1, false, true, 3.14, "changlie"]
println("### normal: ")
foreach i, item : arr {
    println("index:", i, "; item:", item)
}
println("### abnormal: ")
foreach i, item : arr {
    if i == 1 {
        println("index:", i, "; item:", item, " #continue")
        continue
    }
    if i == 3 {
        println("index:", i, "; item:", item, " #break")
        break
    }
    println("index:", i, "; item:", item)
}
```
输出
```
### normal: 
index: 0 ; item: 1
index: 1 ; item: false
index: 2 ; item: true
index: 3 ; item: 3.14
index: 4 ; item: changlie
### abnormal: 
index: 0 ; item: 1
index: 1 ; item: false  #continue
index: 2 ; item: true
index: 3 ; item: 3.14  #break

```


#### 示例二
```js
println("2 -> ", fprint(2))
println("===================")
println("4 -> ", fprint(4))

fprint(flag) {
    sum = 0
    for i=0; i<10; i++ {
        sum += i
        if flag == i {
            return sum
        }
    }
    return sum
}
```
输出
```
2 ->  3
===================
4 ->  10

```

#### 示例三
```js
println("ftest below -----------------")
ftest(3, false)
println("===================")
ftest(4, true)

ftest(flag, exit) {
    for i=0; i<20; i++ {

        if i%flag == 2 {
            println(i, " -> execute continue")
            continue
        }
        if exit && i == 4  {
            println(i, " -> execute return")
            return 0
        }
        if i > 9 {
            println(i, " -> execute break")
            break
        }
        println("row -> ", i)
    }
    println("func over!")
}
```
输出
```
ftest below -----------------
row ->  0
row ->  1
2  -> execute continue
row ->  3
row ->  4
5  -> execute continue
row ->  6
row ->  7
8  -> execute continue
row ->  9
10  -> execute break
func over!
===================
row ->  0
row ->  1
2  -> execute continue
row ->  3
4  -> execute return
```


#### 示例四
```js
println("doubleLoopTest below----------------")
doubleLoopTest(4, false)
println("=========================")
doubleLoopTest(4, true)

doubleLoopTest(num, flag) {
    for i=1; i<5; i++ {
        for j=1; j<12; j++ {
            if i*j == 9 {
                println(i, j, "-> continue")
                continue
            }
            if flag && j == 4 {
                println(i, j, "-> return 0")
                return 0
            }
            if j == num {
                println(i, j, "-> break")
                break
            }
            println(i, j, "-> normal")
        }
    }
    println("func over!")
}
```
输出
```
doubleLoopTest below----------------
1 1 -> normal
1 2 -> normal
1 3 -> normal
1 4 -> break
2 1 -> normal
2 2 -> normal
2 3 -> normal
2 4 -> break
3 1 -> normal
3 2 -> normal
3 3 -> continue
3 4 -> break
4 1 -> normal
4 2 -> normal
4 3 -> normal
4 4 -> break
func over!
=========================
1 1 -> normal
1 2 -> normal
1 3 -> normal
1 4 -> return 0

```