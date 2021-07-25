# 语法分析 Constant Value

在Quick中， 所有类型值都会存储在Value类型中, Value储存着所有值.   
所谓变量，其实就是map 中的一对键值对，key为变量名，值为一个Value实例。  
Value定义如下：
```go
const (
    IntValue ValueType = 1 << iota // 整型
    FloatValue // 浮点型
    BooleanValue // 布尔类型
    StringValue // 字符串
    AnyValue // 任意值
    ArrayValue // json 数组
    ObjectValue // json 对象
    NULLValue // 空值
)

type Value struct {
    t ValueType
    integer int
    decimal float64
    boolean bool
    str string
    any interface{}
    jsonArr JSONArray
    jsonObj JSONObject
}
```

Primary Expression只有常量值才会直接通过函数 `tokenToValue(t *Token) (v *Value)` 解析至Value.  
属性获取，变量值获取要等到程序执行实时计算相应值  
数组元素获取，函数调用，方法调用还需要把相关参数转成Expression, 待程序执行实时计算参数值，然后计算出数组元素获取，函数调用，方法调用的值  

`tokenToValue(t *Token) (v *Value)`相关代码
```go 
func tokenToValue(t *Token) (v *Value) {
	if t.isArrLiteral() {
		v := newJSONArray(t.ts)
		return newQkValue(v)
	}
	if t.isObjLiteral() {
		v := newJSONObject(t.ts)
		return newQkValue(v)
	}
	if t.isFloat() {
		f, err := strconv.ParseFloat(t.str, 64)
		assert(err != nil, "failed to parse float", t.String(), "line:", t.lineIndex)
		v = newQkValue(f)
		return
	}
	if t.isInt() {
		i, err := strconv.Atoi(t.str)
		assert(err != nil, "failed to parse int", t.String(), "line:", t.lineIndex)
		v = newQkValue(i)
		return
	}
	if t.isStr() {
		str := strings.Replace(t.str, "\\\\", "\\", -1)
		str = strings.Replace(str, "\\n", "\n", -1) // 对 \n 进行转义
		str = strings.Replace(str, "\\t", "\t", -1) // 对 \t 进行转义
		v = newQkValue(str)
		return
	}
	if t.isIdentifier() && (t.str == "true" || t.str == "false") {
		b, err := strconv.ParseBool(t.str)
		assert(err != nil, t.String(), "line:", t.lineIndex)
		v = newQkValue(b)
		return
	}
	return nil
}
```