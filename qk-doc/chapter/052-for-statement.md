# for 循环

### 示例
```js
println("demo1 ================")
for a = 0; a < 5; a++ {
    println("current value:", a)
}

println("demo2 ================")
arr = [1, false, true, 3.14, "changlie"]
for a = 0 ; a < arr.size(); a++ {
    println("current value:", arr[a])
}
```
### while
Quick的for循环与golang的很像。  
在Quick中，for可以像while语句一样使用：
```js
i = 0
for i<9 {
    println("i is", i)
    i++
}
```
输出
```
i is 0
i is 1
i is 2
i is 3
i is 4
```
### 死循环
死循环可以简写为如下方式：
```js
for {
    println("it's a dead loop")
}
```


