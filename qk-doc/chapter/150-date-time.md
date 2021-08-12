# 日期时间

### 获取当前时间毫秒值
```js
println(timestamp()) // 1628643356690
```

### 获取当前时间纳秒值
```js
println(nanosecond()) // 1628643387685050100
```

### DateTime
1. 日期格式字符串转DateTime
```js
println(parseDate("2017/05/12", "y/M/d").string()) // 2017-05-12 00:00:00
```

2. 毫秒值转DateTime
```js
println(newDate(1118643356690).string()) // 2005-06-13 14:15:56
```

3. 纳秒值转DateTime
```js
println(newDate1(1238643387685050123).string()) // 2009-04-02 11:36:27
```

4. 当前时间的DateTime对象
```js
dt = now()
// 日期格式化
println(dt.format("y/M/d h:m:s.S")) // 2021/08/11 17:02:01.837
// 年
println(dt.year()) // 2021
// 月
println(dt.month()) // 8
// 日
println(dt.day()) // 11
// 时
println(dt.hour()) // 17
// 分
println(dt.minute()) // 2
// 秒
println(dt.second()) // 1
```


### DateTime方法
| 方法  |	描述   |
|  ----  | ----  |
|  format(fmt) |  日期格式化， y(年), M(月), d(日), h(时), m(分), s(秒), S(毫秒) |
| ms() | 毫秒值 |
| ns() | 纳秒值 |
| year() | 年 |
| month() | 月,[1, 12] |
| day() | 日,[1, 30] |
| hour() | 时,[0, 23] |
| minute() | 分,[0, 59] |
| second() | 秒,[0, 59] |
