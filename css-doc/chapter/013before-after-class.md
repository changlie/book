# 伪类　:before :after

> 转　[https://www.cnblogs.com/ys-ys/p/5092760.html](https://www.cnblogs.com/ys-ys/p/5092760.html)

<a href="demo/013before-after-class.html" target="_blank">查看示例</a>

1. `:before`是css中的一种伪元素，可用于在某个元素之前插入某些内容。
2. `:after`是css中的一种伪元素，可用于在某个元素之后插入某些内容。
3. 通过`p:before`／`p:after`创建出来的伪元素是`p`元素的子节点

```html
  <style>
    p:before{
        content: "H"  
    }
    p:after{
        content: "d"  
    }
  </style>
  <p>ello Worl</p>
```
最终显示结果为　`Hello World`

使用浏览器的审查功能，我们看到的内容是：
```html
<p>
  ::before
  "ello Worl"
  ::after
</p>
```
p标签内部的内容的前面会被插入一个:before伪元素，该伪元素内包含的内容是"H"；   
而在p标签内的内容后面会被插入一个:after伪元素，该元素包含的内容是"d"。




