## 自定义滚动条

> 参考：　[https://www.cnblogs.com/ranyonsue/p/9487599.html](https://www.cnblogs.com/ranyonsue/p/9487599.html)  
[https://www.jianshu.com/p/c2addb233acd](https://www.jianshu.com/p/c2addb233acd)


主要通过`:-webkit-scrollbar`, `:-webkit-scrollbar-thumb`, `:-webkit-scrollbar-track`三个伪类实现  
兼容性：　chrome

1. `:-webkit-scrollbar` 滚动条整体样式
2. `:-webkit-scrollbar-thumb` 滚动条里面小方块
3. `:-webkit-scrollbar-track` 滚动条里面轨道

<a href="demo／016custom-scroll-bar.html" target="_blank">查看示例</a>

关键代码
```html

<div class="test test-5">
    <div class="scrollbar"></div>
</div>

<style>
    .test-5::-webkit-scrollbar {
        /*滚动条整体样式*/
        width : 10px;  /*高宽分别对应横竖滚动条的尺寸*/
        height: 1px;
    }
    .test-5::-webkit-scrollbar-thumb {
        /*滚动条里面小方块*/
        border-radius   : 10px;
        background-color: skyblue;
        background-image: -webkit-linear-gradient(
            45deg,
            rgba(255, 255, 255, 0.2) 25%,
            transparent 25%,
            transparent 50%,
            rgba(255, 255, 255, 0.2) 50%,
            rgba(255, 255, 255, 0.2) 75%,
            transparent 75%,
            transparent
        );
    }
    .test-5::-webkit-scrollbar-track {
        /*滚动条里面轨道*/
        box-shadow   : inset 0 0 5px rgba(0, 0, 0, 0.2);
        background   : #ededed;
        border-radius: 10px;
    }
    .scrollbar {
        background-color: cadetblue;
        width: 100px;
        height: 500px;
    }
    .test {
        background-color: yellow;
        width: 250px;
        height: 200px;
        overflow: scroll; 
        margin: 50px auto;
    }
</style>



```