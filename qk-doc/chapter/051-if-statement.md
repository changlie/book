# if语句
示例一：
```js
animal = "cat"
if animal == "cat" {
    println("this animal is cat!")
}

ifTest1(x) {
    if x {
        println("x is true")
    } else {
        println("x is false")
    }
}
ifTest1(true)
ifTest1(false)
```

示例二：
```js
ifTest(a) {
    if a>1 && a<100 {
        println("a greater than 1.")
    } elif a==0 || a==1 {
        println("elif test...")
    } elif a == 100 {
        println("Good job!")
    } else {
        println("a < 0 and a > 100")
    }
}

ifTest(1)
ifTest(-1)
ifTest(99)
ifTest(100)
```