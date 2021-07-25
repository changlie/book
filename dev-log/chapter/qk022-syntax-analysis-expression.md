# 语法分析 Expression
expression是Statement组成部分, 

上一步Statement分析，函数，各种Statement都解析出了ExpressionStatement   
ExpressionStatement 就是只包含一个expression的Statement  
然后, 我们继续解析Expression  

Expression我们分为三种类型：  
1. 一元表达式： 只包含一个Primary Expression（是Expression至Primary Expression的过渡）
2. 二元表达式： 包含操作符及两个Primary Expression
3. 多元表达式： 含多个Primary Expression及操作符

多元表达式最终转化成二元表达式处理

关键代码：
```go
func extractExpression(ts []Token) *Expression {
	var expr *Expression

	// 去括号
	ts = clearParentheses(ts)

	tlen := len(ts)

	if tlen%2 == 0 {
		runtimeExcption("error expression:", tokensString(ts))
	}

	if tlen < 1 {
		return expr
	}
	switch {
	case tlen == 1:
		return parseUnaryExpression(ts)

	case tlen == 3:
		expr = parseBinaryExpression(ts)

	default:
		// 处理多元表达式
		expr = parseMultivariateExpression(ts)
	}
	if expr == nil {
		runtimeExcption("parseExpressionStatement Exception:", tokensString(ts))
	} else {
		expr.raw = ts
	}
	return expr
}
```

通过递归与穷举法将多元表达式转化二元表达式， 关键代码如下：
```go
func parseMultivariateExpression(ts []Token) (expr *Expression) {
	var resVarToken *Token
	var multiExprTokens []Token
	if ts[1].assertSymbol("=") {
		resVarToken = &(ts[0])
		multiExprTokens = ts[2:]
	} else {
		multiExprTokens = ts
	}
	var exprTokensList [][]Token
	reduceTokensForExpression(resVarToken, multiExprTokens, &exprTokensList)
	//printExprTokens(exprTokensList)

	exprs := generateBinaryExprs(exprTokensList)
	if len(exprs) == 1 {
		// 只有一个表达式时,直接返回一个二元表达式
		return exprs[0]
	}

	finalExpr := getFinalExpr(exprs, resVarToken)

	expr = &Expression{
		t:         MultiExpression,
		list:      exprs,
		finalExpr: finalExpr,
	}
	return expr
}

// 分解多元表达式, 并把结果保存至exprTokensList *[][]Token
func reduceTokensForExpression(res *Token, ts []Token, exprTokensList *[][]Token) {
	var exprTokens []Token

	ts = clearParentheses(ts)

	size := len(ts)
	if size < 3 {
		runtimeExcption("reduceTokensForExpression Exception:", tokensString(ts))
	}

	// 处理括号是第一个token的情况
	if ts[0].assertSymbol("(") {
		leftTokens, nextIndex := extractTokensByParentheses(ts)
		tmpvarToken := getTmpVarToken()
		if !hasSymbol(leftTokens, "(") && len(leftTokens) == 3 {
			// e.g. (a + b) / 5
			// 左处理
			exprTokens = append(leftTokens, tmpvarToken)
			*exprTokensList = append(*exprTokensList, exprTokens)

			// 右处理
			nextTokens := insert(tmpvarToken, ts[nextIndex:])
			reduceTokensForExpression(res, nextTokens, exprTokensList)
			return
		} else {
			// e.g. (d + (f - c)) * e
			// 左处理
			reduceTokensForExpression(&tmpvarToken, leftTokens, exprTokensList)

			// 右处理
			nextTokens := insert(tmpvarToken, ts[nextIndex:])
			reduceTokensForExpression(res, nextTokens, exprTokensList)
			return
		}
	}

	for i := 0; i < size; i++ {
		tmpSize := len(exprTokens)
		token := ts[i]

		condBoundry := tmpSize == 2
		condFinish := condBoundry && i == size-1
		preCond1 := condBoundry && i < size-1
		// 处理根据运算符优先级, 左向归约的情况
		condShiftLeft1 := preCond1 && last(exprTokens).equal(next(ts, i))
		condShiftLeft2 := preCond1 && last(exprTokens).lower(next(ts, i))
		if condShiftLeft1 || condShiftLeft2 || condFinish {
			// e.g. c + 7
			// a = 23
			exprTokens = append(exprTokens, token)
			if !condFinish {
				// e.g. a + 9 + c
				tmpVarToken := getTmpVarToken()
				nextTokens := insert(tmpVarToken, ts[i+1:])
				exprTokens = append(exprTokens, tmpVarToken)
				reduceTokensForExpression(res, nextTokens, exprTokensList)
			}
			break
		}

		// 处理括号不是第一个token的情况
		condRightParentheses := preCond1 && token.assertSymbol("(")
		if condRightParentheses {
			rightTokens, nextIndex := extractTokensByParentheses(ts[i:])
			nextIndex = i + nextIndex // 转换回切片ts的相应索引
			if nextIndex < size-1 {
				// e.g. a + (9 * d) - 3; rightTokens -> 9 * d; 9 * d => tmpVarToken1
				// 因为括号圈的不是右边整个表达式, 故先求括号值, 再通过运算符优先级求值
				tmpVarToken1 := getTmpVarToken() // 括号内的中间临时值
				reduceTokensForExpression(&tmpVarToken1, rightTokens, exprTokensList)

				// 根据运算符优先级的不同, tmpVarToken2可能是左边表达式的或者右边表达式的中间临时值
				tmpVarToken2 := getTmpVarToken()

				nextToken := ts[nextIndex]
				if last(exprTokens).equal(&nextToken) || last(exprTokens).lower(&nextToken) {
					// e.g. d * tmp + c / 2
					// 左优先
					exprTokens = append(exprTokens, tmpVarToken1) // middle tmp result
					exprTokens = append(exprTokens, tmpVarToken2) // left expr result.

					nextTokens2 := insert(tmpVarToken2, ts[nextIndex:]) //
					reduceTokensForExpression(res, nextTokens2, exprTokensList)
				} else {
					// e.g. e + tmp * f
					// 右优先
					exprTokens = append(exprTokens, tmpVarToken2) // rigtht expr result.

					nextTokens3 := insert(tmpVarToken1, ts[nextIndex:])
					reduceTokensForExpression(&tmpVarToken2, nextTokens3, exprTokensList)
				}
				break
			}

			// e.g. a * (b + 3)
			// 因为括号圈的是右边整个表达式时
			tmpVarToken3 := getTmpVarToken()
			exprTokens = append(exprTokens, tmpVarToken3)

			nextTokens := ts[i:]
			reduceTokensForExpression(&tmpVarToken3, nextTokens, exprTokensList)
			break
		}

		// e.g. 
		// a + b * c
		// a * b - 3
		// 处理根据运算符优先级, 右向归约的情况
		condShiftRight1 := preCond1 && last(exprTokens).upper(next(ts, i))
		if condShiftRight1 {
			tmpVarToken := getTmpVarToken()
			nextTokens := ts[i:]
			exprTokens = append(exprTokens, tmpVarToken)
			reduceTokensForExpression(&tmpVarToken, nextTokens, exprTokensList)
			break
		}

		exprTokens = append(exprTokens, token)
	}

	if res != nil && len(exprTokens) == 3 {
		exprTokens = append(exprTokens, *res)
	}

	*exprTokensList = append(*exprTokensList, exprTokens)
}
```