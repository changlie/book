# Excel 操作

excel文件 实际是一堆xml文件的压缩包

Quick支持对老版xls的读操作，及最新版xlsx文件的读写操作
* [Excel - Xls](#xls-相关对象)
* [Excel - Xlsx](#xlsx-相关对象)

### xls 数据读取
`tab1.xls`文件内容如下：  
![illustration](img/xls-src.png)  
[源文件](static/tab1.xls)
```js
f = xls("d:/tab1.xls")
println("xlsSheetNumber:", f.sheetNumber())
sheet = f.sheet(0)
println("sheetName: ", sheet.name())
println("sheetRowNumber: ", sheet.rowNumber())
row = sheet.row(0)
if row {
    println("headers:")
    forv cell : row.cols() {
        cell && print(cell.str()+", ")
    }
}

println("\ndata:")
rows = sheet.rows()
forv row : rows {
    cells = row.cols()
    forv cell : cells {
        cell && print(cell.str()+", ")
    }
    println("\n=============================")
}
```
输出
```
xlsSheetNumber: 2
sheetName:  无名
sheetRowNumber:  4
headers:
name, age, sex, , , , qs, 
data:
zs, 9, m, , , zz, 
=============================
ls, 11, f, , yy, 
=============================
ww, 16, m, xx, 
=============================
```

### xlsx 读取
`tab2.xlsx`文件内容：
![illustraction](img/xlsx-src.png)  
[源文件](static/tab2.xlsx)
方式1：
```js
f = xlsx("d:/tab2.xlsx")
sheet = f.sheet(0)
forv row : sheet.cellVals() {
    printf("[%v] ", row.size())
    forv cell : row {
        print(cell+", ")
    }
    println("\n=====================")
}
```
输出
```
[6] name, age, sex, attr, , yyy, 
=====================
[7] zs, 9, m, a, , , 1, 
=====================
[8] ls, 11, f, ab, xxx, , , 22, 
=====================
[9] ww, 16, m, abc, , zzz, , , 333, 
=====================
```
方式2：
```js
f = xlsx("d:/tab2.xlsx")
sheet = f.sheet(0)
rows = sheet.rows()
for rows.next() {
    cells = rows.cols()
    println(cells, cells.type())
}
```
输出
```
["name", "age", "sex", "attr", "", "yyy"] JSONArray
["zs", "9", "m", "a", "", "", "1"] JSONArray
["ls", "11", "f", "ab", "xxx", "", "", "22"] JSONArray
["ww", "16", "m", "abc", "", "zzz", "", "", "333"] JSONArray
```

### xlsx 写数据
```js
headers = ["name", "sex", "age", "addr"]
data = [
{name:"jerry", sex:"F", age:9, addr:"America"},
{name:"tom", sex:"M", age:13, addr:"America"},
{name:"changlie", sex:"M", age:18, addr:"China"},
{name:"zhangsan", sex:"F", age:33, addr:"town"},
{name:"fish", sex:"F", age:2, addr:"The World"},
]

f = newXlsx()
sheet = f.sheet(0)
// 批量写数据
sheet.setData(headers, data)
// 修改一个单元的数据
// 修改横坐标为B，纵坐标为2的单元格的值为"boom!"
sheet.setCellValue("B2", "boom!")
f.saveAs("d:/test.xlsx")
println("write successfully")
```
写出的文件数据如下：  
![illustration](img/xlsx-res.png)


# Xls 相关对象

### Xls
调用xls(path)后返回的对象类型

| 方法   |	描述   |
|  ----  | ----  |
|  sheetNumber()  | 返回sheet的数量 |
|  sheet(index)  | 返回一个类型为[XlsSheet](#XlsSheet)的sheet对象 |


### XlsSheet

| 方法   |	描述   |
|  ----  | ----  |
|  name()  | sheet名称 |
|  rowNumber()  | 有数据的行的数量 |
|  row(index)  | 返回索引为index的行对象，类型为[XlsRow](#XlsRow) |
|  rows()  |  返回所有有数据的行对象（除了第一行），类型为[XlsRow](#XlsRow) 数组 |


### XlsRow

| 方法   |	描述   |
|  ----  | ----  |
|  cols()  | 返回当前行的所有单元对象，类型为[XlsCell](#XlsCell) 数组  |
|  col(index)  | 返回索引为index的单元对象，类型为[XlsCell](#XlsCell)  |


### XlsCell

| 方法   |	描述   |
|  ----  | ----  |
|  getInt()  | 单元的int类型值  |
|  getFloat()  |  单元的float类型值 |
|  str()  | 单元的string类型值  |
|  getType()  |  单元的数据类型 |


# Xlsx 相关对象

### Xlsx

内置函数 `xlsx(path)`, `newXlsx()`返回的对象类型

| 方法   |	描述   |
|  ----  | ----  |
| newSheet(name) | 新建一个sheet,并返回该对象，类型为[XlsxSheet](#XlsxSheet) |
| setActiveSheet(index) | 设置索引为index的对象为当前sheet(打开excel默认展示的sheet) |
| saveAs(path) | excel另存为 |
| save() | 保存excel修改 |
| sheet(index) | 返回索引为index的sheet, 类型为[XlsxSheet](#XlsxSheet) |

### XlsxSheet

| 方法   |	描述   |
|  ----  | ----  |
| setData(headers, data) | 批量赋值 |
| setCellValue(axis, value) | 给指定坐标(e.g. B2)的单元格赋值字符串 |
| rows() | 返回当前sheet的[XlsxRows](#XlsxRows)对象 |
| cellVals() | 获取所有含数据的单元格的值，类型为一个字符串二维数组 |
| cellVal(axis) | 获取指定坐标(e.g. B2)的单元格的字符串的值 |

### XlsxRows

| 方法   |	描述   |
|  ----  | ----  |
| next() | 下一行是否存在数据，若是指针移向下一行，并返回true |
| cols() | 返回当前行的所以单元格的数据(与`next()`结合使用), 数据为字符串类型 |
