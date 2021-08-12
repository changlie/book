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

