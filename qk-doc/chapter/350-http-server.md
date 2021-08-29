# http server


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
