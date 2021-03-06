# css3 内置宽高

> 转　[https://www.cnblogs.com/xaun/p/13673798.html](https://www.cnblogs.com/xaun/p/13673798.html)


### vh/vw 
- `vh`: 相对于视窗的高度, 视窗被均分为100单位的vh; 
- `vw`: 相对于视窗的宽度, 视窗被均分为100单位的vw;

- `vmax`: 相对于视窗的宽度或高度中较大的那个。其中最大的那个被均分为100单位的vmax; 
- `vmin`: 相对于视窗的宽度或高度中较小的那个。其中最小的那个被均分为100单位的vmin;   
视区所指为浏览器内部的可视区域大小，   
即`window.innerWidth`/`window.innerHeight`大小，不包含任务栏标题栏以及底部工具栏的浏览器区域大小。  

### calc
`calc`是英文单词calculate(计算)的缩写，是css3的一个新增的功能，用来指定元素的长度。比如说，你可以使用`calc()`给元素的`border`、`margin`、`pading`、`font-size`和`width`等属性设置动态值。为何说是动态值呢?因为我们使用的表达式来得到的值。不过`calc()`最大的好处就是用在流体布局上，可以通过`calc()`计算得到元素的宽度。

calc是 css3提供的一个在css文件中计算值的函数：  
- 用于动态计算长度值。
- 需要注意的是，运算符前后都需要保留一个空格，例如：width: calc(100% - 10px)；
- 任何长度值都可以使用calc()函数进行计算；
- calc()函数支持 “+”, “-“, “*”, “/” 运算；
- calc()函数使用标准的数学运算优先级规则；
```
calc(100vh - 10px)  表示整个浏览器窗口高度减去10px的大小
calc(100vw - 10px)  表示整个浏览器窗口宽度减去10px的大小
```


