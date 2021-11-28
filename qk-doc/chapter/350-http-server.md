# http server

* [Http Request](#httprequest)
* [Server Response](#serverresponse)

### HttpServer

`HttpServer`是内置函数`httpServer(post)`的返回値类型

| 方法   |	描述   |
|  ----  | ----  |
| get(path, func) | 定义一个get 服务 |
| post(path, func) | 定义一个post 服务 |
| startup() | 启动http服务 |


### get 服务
```js
server = httpServer(8888)

server.get("/hi", $ req, resp {
    resp.txt("Hello World!")
})

server.startup()
```


### post 服务
```js
server = httpServer(8888)

server.post("/newUser", $ req, resp {
    // 打印参数
    req.args().pretty()

    resp.json({"result":"ok"})
})

server.startup()

```


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