# 异步编程

Quick的异步是用Go的协程实现的  

Quick的异步编程通过调用内部函数`async(func)`，并传入一个需要异步执行的函数即可。  

### 示例一：异步执行一个函数
```js
start = timestamp()

async(${
    println("it's in async")
    sleep(1500)
})

println("cost: ", timestamp() - start, "ms")
```
输出
```
cost:  0 ms
it's in async
```
我们可以发现用时统计是最先输出的，并且用时为0ms，说明的确是异步的


### 示例二： 异步执行一个函数并获取其返回值
`async()`被调用后会返回一个函数，执行这个函数，即可获取异步返回值，但同时会造成阻塞，
直到子协程执行结束。   
我们先不调用`async()`返回的函数，看看运行结果
```js
start = timestamp()

res = async(${
    println("it's in async")
    sleep(1500)
    return 998
})

// println("async result:", res())

println("cost: ", timestamp() - start, "ms")
```
输出
```
cost:  0 ms
it's in async
```
我们发现和示例一的结果是一样的，然后我们再调用`async()`返回的函数，看看运行结果
```js
start = timestamp()

res = async(${
    println("it's in async")
    sleep(1500)
    return 998
})

println("async result:", res())

println("cost: ", timestamp() - start, "ms")
```
输出
```
it's in async
async result: 998
cost:  1501 ms
```
结果是: 用时统计是最后执行的，并且用时1.5s