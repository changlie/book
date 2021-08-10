## 基础语法

Quick语法以简单实用为主

- 变量无需声明即可使用
- 只支持函数的自定义
- if, for 等条件语句不需要加括号 


### 编码
强烈建议使用 UTF-8 编码，所有字符串都应是 unicode 字符串。

### 标识符
第一个字符必须是字母表中字母或下划线 `_`。  
标识符的其他的部分由字母、数字和下划线组成。  
标识符对大小写敏感。  

### 保留字
保留字即关键字，我们不能把它们用作任何标识符名称。
```
fn, this, 
for, foreach, fori, forv, if, switch,
retIf, return, break, continue, 
true, false, null
```

### 注释
```js
// 第一个注释
println("Hello, Quick!") // 第二个注释
/*  
 这是一个
 多行注释
 */
println("comments demo")
```