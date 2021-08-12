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