## 布尔类型
布尔类型只有两种值：true, false。一般用于条件判断



Quick 的判空机制和js是一致的：  
变量值为false, null 或 相应类型默认值时, 条件判断会将它们等同于false,反之为true  

相应类型默认值: 
- Byte Array => null
- Number => 0
- Boolean => false
- String => ""
- JSON Array => null
- JSON Object => null
- 其他内置类型 => null