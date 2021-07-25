# 语法分析 Primary Expression
Primary Expression: 原始表达式。 常量值，变量，函数调用，数组元素等等都归类到Primary Expression

Primary Expression定义
```go 
type PrimaryExpr struct {
	t PrimaryExpressionType
	caller string // 调用者名称
	name string  // 变量名或者函数名称
	args []*Expression // 函数调用参数 / 数组索引
	res *Value  // 常量值
}
```

关键代码：
```go 
func parsePrimaryExpression(t *Token) *PrimaryExpr {
	v := tokenToValue(t)
	var res *PrimaryExpr
	if v != nil {
		primaryExprType := ConstPrimaryExpressionType
		if t.isObjLiteral() {
			primaryExprType = primaryExprType | ObjectPrimaryExpressionType
		}
		if t.isArrLiteral() {
			primaryExprType = primaryExprType | ArrayPrimaryExpressionType
		}
		res = &PrimaryExpr{res: v, t: primaryExprType}

	} else if t.isElement() {
		exprs := getArgExprsFromToken(t.ts)
		res = &PrimaryExpr{name: t.str, args: exprs, t: ElementPrimaryExpressionType}

	} else if t.isAttribute() {
		res = &PrimaryExpr{name: t.str, caller: t.caller, t: AttibutePrimaryExpressionType}

	} else if t.isFcall() {
		exprs := getArgExprsFromToken(t.ts)
		res = &PrimaryExpr{name: t.str, args: exprs, t: FunctionCallPrimaryExpressionType}

	} else if t.isMtcall() {
		exprs := getArgExprsFromToken(t.ts)
		res = &PrimaryExpr{name: t.str, caller:t.caller, args: exprs, t: MethodCallPrimaryExpressionType}

	} else {
		res = &PrimaryExpr{name: t.str, t: VarPrimaryExpressionType}
	}
	return res
}
```