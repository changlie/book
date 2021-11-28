# 文件操作

- [xml文件操作](#xml)  

## 文件操作函数

| 函数  | 别名 |	描述   |
|  ----  | ----  | ----  |
|  fbytes(path) | fbs(path) |  文件内容以`ByteArray`形式返回  |
|  fstr(path)      |  |  读取整个文本文件的内容  |
|  flines(path)) |  |  逐行读取整个文件，返回一个字符串数组   |
|  fjson(path)     |  |  读取整个json文件, 返回一个json对象  |
|  fout(path, content)     |  |  清空指定文件，并写入数据 |
|  fappend(path, content)  |  |  向指定文件以追加的方式写入数据  |
|  fsave(path, bytes) |  | 将`ByteArray`数据保存至文件 |
|  fappendBytes(path, bytes) |  | 将`ByteArray`数据追加至文件 |
|  fargs(path)  |  |  从参数文件中获取参数  |
|  fprops(path) |  | 读取配置文件, 返回一个json对象 |
|  fscan(path)  |  |  获取指定目录下所有文件的绝对路径  |
|  cp(src, dst)  |  |  文件复制  |


### 函数 fargs(path)
参数文件 `/home/xp/ws/test/inputFile` 内容为
```
name age salary
tom  9   1000
jerry 5  5000
```

参数文件 `/home/xp/ws/test/inputFile2` 内容为
```
chenlh.cn, 192.1.1.1
github.com, 192.168.0.1
```
对以上两个文件进行数据获取
```js

args = fargs("/home/xp/ws/test/inputFile")
println(args) // [["name", "age", "salary"], ["tom", "9", "1000"], ["jerry", "5", "5000"]]


args = fargs("/home/xp/ws/test/inputFile2")
println(args) // [["chenlh.cn", "192.1.1.1"], ["github.com", "192.168.0.1"]]

```

### 函数 fprops(path)
配置文件 `/home/xp/ws/test/aprops`
```
# dev mode: true or false
mode=

# service unique name
name=changlie server

port=502
```
配置文件读取
```js
props = fprops("/home/xp/ws/test/aprops")
println("config -> ", props) // config ->  {"name":"changlie server", "port":"502", "mode":""}

```












### xml

1. 写示例  

```js
doc = xml()
//doc.setHead("xml", `version="1.0" encoding="UTF-8"`)
doc.defHead()

root = doc.newElem("people")

p = root.newElem("person")
p.newAttr("type", "student")
p.newText("Joe")

p = root.newElem("person")
p.newAttr("type", "teacher")
p.newText("Lily")

p = root.newElem("person")
p.newAttr("type", "animal")
p.newCData("<cheator>>>")
echo("animal -> ", p.text())

doc.indent(2)
echo(doc.str())
```
```
animal ->  <cheator>>>
<?xml version="1.0" encoding="UTF-8"?>
<people>
  <person type="student">Joe</person>
  <person type="teacher">Lily</person>
  <person type="animal"><![CDATA[<cheator>>>]]></person>
</people>
```

2. 读示例  

```js
rawDoc = `
<bookstore xmlns:p="urn:schemas-books-com:prices">

  <book category="COOKING">
    <title lang="en">Everyday Italian</title>
    <author>Giada De Laurentiis</author>
    <year>2005</year>
    <p:price>30.00</p:price>
  </book>

  <book category="CHILDREN">
    <title lang="en">Harry Potter</title>
    <author>J K. Rowling</author>
    <year>2005</year>
    <p:price>29.99</p:price>
  </book>

  <book category="WEB">
    <title lang="en">XQuery Kick Start</title>
    <author>James McGovern</author>
    <author>Per Bothner</author>
    <author>Kurt Cagle</author>
    <author>James Linn</author>
    <author>Vaidyanathan Nagarajan</author>
    <year>2003</year>
    <p:price>49.99</p:price>
  </book>

  <book category="WEB" id="9527">
    <title lang="en">Learning XML</title>
    <author>Erik T. Ray</author>
    <year>2003</year>
    <p:price>39.95</p:price>
  </book>

</bookstore>
`

doc = xml().load(rawDoc)

root = doc.root()
echo("root tag -> ", root.name())

forv book : root.elems("book") {
    echo("book: ", book.elem("title").text())
    echo("category: ", book.attr("category"))
    echo("-------------")
}

// 查找
e = doc.find("//book[@category='WEB']/*")
echo(e.name(), e.text())
echo("======================")

forv e : doc.finds("//book[@category='CHILDREN']/*") {
    echo(e.name())
    echo("++++++++++++++")
}

echo("########################")
forv e : doc.finds("./bookstore/book[1]/*") {
    echof("%v > %v", e.name(), e.text())
}

echo("@@@@@@@@@@@@@")
forv e : doc.finds("./bookstore/book[p:price='49.99']/title") {
    echof("%v : %v", e.name(), e.text())
}
```
```
root tag ->  bookstore
book:  Everyday Italian
category:  COOKING
-------------
book:  Harry Potter
category:  CHILDREN
-------------
book:  XQuery Kick Start
category:  WEB
-------------
book:  Learning XML
category:  WEB
-------------
title XQuery Kick Start
======================
title
++++++++++++++
author
++++++++++++++
year
++++++++++++++
price
++++++++++++++
########################
title > Everyday Italian
author > Giada De Laurentiis
year > 2005
price > 30.00
@@@@@@@@@@@@@
title : XQuery Kick Start
```






