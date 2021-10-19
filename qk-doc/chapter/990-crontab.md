# 任务调度

### delay/interval
```js
println("start at", now())
delay(${
    println("延迟两秒执行", now())
}, 2000)


interval(${
    println("每1.5秒执行一次", now())
}, 1500)
```


### crontab示例

```js
cron("* * * * *", ${
    println("每秒执行一次", now())
})

cron("3/4 * * * *", ${
    println("每4秒执行一次，3秒后开始执行", now())
})
```

### crontab相关知识

##### 中文版
###### cron 表达式代表了一个时间集合，使用 6 个空格分隔的字段表示。

字段名 |	是否必须 |	允许的值 |	允许的特定字符
----------   | ---------- | --------------  | --------------------------
秒(Seconds) |	是 |	0-59 |  * / , –
分(Minutes) |	是 |	0-59 |  * / , –
时(Hours) |	是 |	0-23 |  * / , –
日(Day of month) |	是 |	1-31 | * / , – ?
月(Month) |	是 |	1-12 or JAN-DEC | * / , –
星期(Day of week) |	否 |	0-6 or SUM-SAT | * / , – ?

注：  
```
1）月(Month)和星期(Day of week)字段的值不区分大小写，如：SUN、Sun 和 sun 是一样的。
2）星期(Day of week)字段如果没提供，相当于是 *
```

###### 特殊字符说明   
1）星号(*)
表示 cron 表达式能匹配该字段的所有值。如在第5个字段使用星号(month)，表示每个月

2）斜线(/)
表示增长间隔，如第1个字段(minutes) 值是 3-59/15，表示每小时的第3分钟开始执行一次，之后每隔 15 分钟执行一次（即 3、18、33、48 这些时间点执行），这里也可以表示为：3/15

3）逗号(,)
用于枚举值，如第6个字段值是 MON,WED,FRI，表示 星期一、三、五 执行

4）连字号(-)
表示一个范围，如第3个字段的值为 9-17 表示 9am 到 5pm 直接每个小时（包括9和17）

5）问号(?)
只用于 日(Day of month) 和 星期(Day of week)，表示不指定值，可以用于代替 *

##### 英文版
CRON Expression Format ¶

A cron expression represents a set of times, using 6 space-separated fields.

Field name   | Mandatory? | Allowed values  | Allowed special characters
----------   | ---------- | --------------  | --------------------------
Seconds      | Yes        | 0-59            | * / , -
Minutes      | Yes        | 0-59            | * / , -
Hours        | Yes        | 0-23            | * / , -
Day of month | Yes        | 1-31            | * / , - ?
Month        | Yes        | 1-12 or JAN-DEC | * / , -
Day of week  | Yes        | 0-6 or SUN-SAT  | * / , - ?

Note: Month and Day-of-week field values are case insensitive. "SUN", "Sun", and "sun" are equally accepted.
Special Characters ¶

Asterisk ( * )

The asterisk indicates that the cron expression will match for all values of the field; e.g., using an asterisk in the 5th field (month) would indicate every month.

Slash ( / )

Slashes are used to describe increments of ranges. For example 3-59/15 in the 1st field (minutes) would indicate the 3rd minute of the hour and every 15 minutes thereafter. The form "*\/..." is equivalent to the form "first-last/...", that is, an increment over the largest possible range of the field. The form "N/..." is accepted as meaning "N-MAX/...", that is, starting at N, use the increment until the end of that specific range. It does not wrap around.

Comma ( , )

Commas are used to separate items of a list. For example, using "MON,WED,FRI" in the 5th field (day of week) would mean Mondays, Wednesdays and Fridays.

Hyphen ( - )

Hyphens are used to define ranges. For example, 9-17 would indicate every hour between 9am and 5pm inclusive.

Question mark ( ? )

Question mark may be used instead of '*' for leaving either day-of-month or day-of-week blank. 
