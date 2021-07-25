# 语法分析

将词法分析得来的Token进行语法分析，生成解析器可以执行的数据结构。  
相应的数据结构如下：
```
语句         表达式          原始表达式             常量值   
Statement -> expression -> primary expression -> constant value
```



