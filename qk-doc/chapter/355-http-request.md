# HttpRequest

`HttpRequest` 是 `HttpServer`服务函数第一个形参的数据类型


| 方法   |	别名   |	描述   |
|  ----  | ----  | ----  |
| showHeaders() | showhs() | 在控制台打印所有请求头 |
| headers() |  | 返回所有请求头 |
| getHeaderVal(name) | h(name) | 获取请求头，如果有多个值返回第一个值 |
| getHeaderVals(name) | hs(name) | 获取请求的所有值 |
| args() |  | 返回所有参数不包括上传文件 |
| json() |  | 请求体数据以json形式返回 |
| body() |  | 请求体数据以string形式返回 |
| bodyBytes() |  | 请求体数据以`ByteArray`形式返回 |
| param(name) |  | 获取请求参数，如果有多个值返回第一个值 |
| params(name) |  |  获取请求参数所有值 |
| files() |  | 所有上传文件 |
| getFiles(formName) |  | 指定form name的所有文件 |
| getFile(formName) |  | 指定form name的文件，如果有多个返回第一个 |



### MultipartFile

`MultipartFile`是上传文件所使用的文件类型  
`HttpRequest`的方法 `files()`，`getFiles(formName)`，`getFile(formName)`返回值的主要类型

| 方法   |	描述   |
|  ----  | ----  |
| name() | 文件名称 |
| size() | 文件大小 |
| bytes() | 文件数据以`ByteArray`形式返回 |
| save(path) | 文件保存至指定位置 |












