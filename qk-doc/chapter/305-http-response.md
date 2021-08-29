# HttpResponse

`HttpResponse` 是内置函数`httpGet(url[, headers])`, `httpPost(url, config)`
的返回值的数据类型

| 方法   |	别名   |	描述   |
|  ----  | ----  | ----  |
| showCookies() | showck() | 在控制台打印所有cookie信息 |
| cookies() |  | 返回所有cookie信息 |
| showHeaders() | showhs() | 在控制台打印所有响应头信息 |
| headers() | hs() | 返回所有响应头信息 |
| status() |  | 请求响应状态 |
| statusCode() | code() | 响应状态码 |
| save(path) |  | 保存响应体数据至指定文件 |
| string() | str() | 响应体数据以string形式返回 |
| bytes() |  | 响应体数据以字节数组形式返回 |
| pretty() |  | 响应体数据如果是json格式的话，可以使用这个方法将json美化输出至控制台 |
| json() |  | 响应体数据以json形式返回 |
