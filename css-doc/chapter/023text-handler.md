# 文本处理

### css文字超出显示省略号
单行：
```css
div {
    white-space:nowrap;
    overflow:hidden;
    text-overflow:ellipsis;
}
```
多行：
```css
div {
    word-break: break-all;
    text-overflow: ellipsis;
    overflow: hidden;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
}
```

### 文字垂直居中

一、行高（line-height）法
如果要垂直居中的只有一行或几个文字，那它的制作最为简单，只要让文字的行高和容器的高度相同即可，比如：
```css
p { height:30px; line-height:30px; width:100px; overflow:hidden; }
```
这段代码可以达到让文字在段落中垂直居中的效果。

二、内边距（padding）法
另一种方法和行高法很相似，它同样适合一行或几行文字垂直居中，原理就是利用padding将内容垂直居中，比如：
```css
p { padding:20px 0; }
```
这段代码的效果和line-height法差不多。