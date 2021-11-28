# http client

* [Http Response](#httpresponse)


### GET 请求
```js
resp = httpGet("http://localhost:12345/hello?from=qk")
printf("status: %v|%v \n", resp.status(), resp.statusCode())
println(resp.string())
```
添加请求头
```js
resp = httpGet("http://localhost:12345/hello", {
    auth: "rxstXXXX"
})
printf("status: %v|%v \n", resp.status(), resp.statusCode())
println(resp.string())
```

### POST 请求

Quick专门为POST请求内置了一变量`mime`, 其包含了POST常用的Content-Type:
```
mime.json => application/json
mime.form => application/x-www-form-urlencoded
mime.data => multipart/form-data
```

- xhr 传json对象 (Content-Type: application/json)

```js
url = "http://localhost:12345/hello?from=qk"
resp = httpPost(url, {type:mime.json,
    headers:{trace:"witch"}, // 添加头信息
    body:{
        name:"changlie",
        age:18,
        addr:"中国"
    }
})
```

- form表单默认方式 (Content-Type: application/x-www-form-urlencoded)

```js
resp = httpPost(url, {type:mime.form,
    headers:{trace:"witch"}, // 添加头信息
    body:{
        name:"changlie",
        age:18,
        addr:"中国"
    }
})
```     


- 文件上传 (Content-Type: multipart/form-data)

```js
descBytes = fbytes("README.md")
versionBytes = fbytes("version.go")

url = "http://localhost:12345/hello?from=qk"
resp = httpPost(url, {type:mime.data,
    headers:{trace:"witch"},
    body:{
        name:"changlie",
        age:18,
        addr:"中国",
        files: [ // 存放上传文件信息列表的key名必须为files
            // field: 指表单字段名
            {field: "uploadFile", name: "demo.txt", path:"test.txt"},
            // path: 指待上传的文件路径
            {name: "qk.txt", path:"main.go"},
            // data: 指待上传的文件二进制数据
            {name: "desc.txt", data:descBytes},
            // name: 指文件名
            {field: "uploadFile", name: "version.txt", data:versionBytes},
        ]
    }
})
printf("status: %v|%v \n", resp.status(), resp.statusCode())
println(resp.string())
```


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





