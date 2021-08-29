# ServerResponse

`HttpResponse` 是 `HttpServer`服务函数第二个形参的数据类型，用于响应http请求。



| 方法   | 别名 |	描述   |
|  ----  | ----  | ----  |
| redirect(url) |  | 重定向 |
| txt(content) |  | 返回一个文本内容 |
| html(content) |  | 返回一个html |
| json(content) |  | 返回一个json |
| file(bytes) |  | 返回一个文件，通常用于文件文件预览 |
| fileForDownload(fileName, bytes) | dl(fileName, bytes) | 返回一个用于下载的文件 |
| setHeader(name, value) | seth(name, value) | 设置响应头 |
| setContentType(value) | setType(value) | 设置响应体的数据类型 |







