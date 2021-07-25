# 词法分析

所谓词法分析就是把程序源拆分成一个个Token.  
出于解析器简便地实现的目的，我们词法分析加入了一部分语法分析的内容。  
所以Quick解析器的Token 由两种Token组成：原始Token, 复合Token.  
Token细分类型如下：
```
    -----  原始Token类型  -----
    Identifier  // 标识符
	Str // 字符串类型
	Int // 整数类型
	Float  // 浮点类型
	Symbol  // 符号

    -----  复合Token类型  -----
	Fcall  // 函数调用
	Fdef  // 函数 定义
	Mtcall // 方法调用
	Attribute // 对象属性
	ArrLiteral // 数组字面值
	ObjLiteral // 对象字面值
	Element // 元素，用于指示对象或数组的元素
	Complex // 用于标记复合类型token

	AddSelf // 自增一
	SubSelf // 自减一
```
> 复合Token 的形成属于语法分析。