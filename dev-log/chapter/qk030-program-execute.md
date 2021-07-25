# 程序执行

程序执行就是让语句分析出来的数据结构运行起来。

其中，有比较重要的两点：
1. return, continue, break的实现
2. 变量的传递

Expression是最小的执行单元， Primary Expression是最小的表示单元

### 变量
变量栈
```go
// 变量栈
type VariableStack struct {
	list []Variables
}

func newVariableStack() *VariableStack {
	varStack := &VariableStack{}
	return varStack
}

func (stack *VariableStack) push() {
	vars := newVariables()
	stack.list = append(stack.list, vars)
}

func (stack *VariableStack) pop() {
	size := len(stack.list)
	if size<1 {
		return
	}
	stack.list = stack.list[:size-1]
}

func (stack *VariableStack) searchVariable(name string) *Value {
	for i:=len(stack.list)-1; i>=0; i-- {
		vars := stack.list[i]
		res := vars.get(name)
		if res != nil {
			return res
		}
	}
	runtimeExcption("variable", name, "is undefined")
	return nil
}

func (stack *VariableStack) addLocalVariable(name string, val *Value) {
	size := len(stack.list)
	if size<1 {
		runtimeExcption("stack is empty!")
	}

	stack.list[size-1].add(name, val)
}
```
变量池
```go
// 变量池
type Variables map[string]*Value

func newVariables() Variables {
	return make(map[string]*Value)
}

func (vs Variables) isEmpty() bool {
	return vs == nil || len(vs) < 1
}

func (vs Variables) add(name string, v *Value) {
	vs[name] = v
}

func (vs Variables) get(name string) *Value {
	if vs.isEmpty() {
		return nil
	}
	res, ok := vs[name]
	if ok {
		return res
	}
	return nil
}
```
变量传递
```go
func Interpret() {
	stack := newVariableStack()
	stack.push() // 执行方法前，向变量栈(list)添加的一个变量池(map)
	executeFunctionStatementList(mainFunc.block, stack)
}
// 执行函数
func executeFunctionStatementList(stmts []*Statement, stack *VariableStack) *Value {
	defer stack.pop() // 函数执行结束后， 删除变量栈(list)最新添加的变量池(map)

	executeStatementList(stmts, stack, StmtListTypeFunc)
	res := stack.searchVariable(funcResultName)
	return res
}
```

### return, continue, break的实现相关代码
```go
func executeStatementList(stmts []*Statement, stack *VariableStack, t StmtListType) *StatementResult {
	if t == StmtListTypeFunc {
		stack.addLocalVariable(funcResultName, NULL)
	}
	var res *StatementResult
	for _, stmt := range stmts {
		res = executeStatement(stmt, stack)
		if res == nil {
			println("executeStatement return error", tokensString(stmt.raw))
			break
		}

		if res.isContinue() {
			if t == StmtListTypeFor {
				res.t = StatementNormal
			}
			break
		} else if res.isReturn() || res.isBreak() {
			break
		}

	}
	// 修复空语句异常
	if res == nil {
		res = newStatementResult(StatementNormal, NULL)
	}
	return res
}

func executeForStatement(stmt *Statement, stack *VariableStack) (res *StatementResult) {
	if stmt.preExpr != nil {
		executeExpression(stmt.preExpr, stack)
	}
	var flag bool
	if stmt.condExpr != nil {
		flag = evalBoolExpression(stmt.condExpr, stack)
	}
	for flag {

		res = executeStatementList(stmt.block, stack, StmtListTypeFor)


		if res.isBreak() {
			res.t = StatementNormal
			return
		} else if res.isReturn() {
			return
		}

		if stmt.postExpr != nil {
			executeExpression(stmt.postExpr, stack)
		}
		if stmt.condExpr != nil {
			flag = evalBoolExpression(stmt.condExpr, stack)
		}
	}
	return res
}

func executeForeachStatement(stmt *Statement, stack *VariableStack) (res *StatementResult) {
	fpi := stmt.fpi
	varVal := stack.searchVariable(fpi.iterator)
	itr := toIterator(varVal)
	if itr == nil {
		runtimeExcption(fpi.iterator, "is not iterator!")
		return
	}

	indexs := itr.indexs()
	for _, index := range indexs {

		if !stmt.isForItemStatement() {
			i := newQkValue(index)
			stack.addLocalVariable(fpi.indexName, i)
		}
		if !stmt.isForIndexStatement() {
			item := itr.getItem(index)
			stack.addLocalVariable(fpi.itemName, item)
		}

		res = executeStatementList(stmt.block, stack, StmtListTypeFor)

		if res.isBreak() {
			res.t = StatementNormal
			return
		} else if res.isReturn() {
			return
		}
	}
	return res
}

```
