# 原生js操作css

> 转 [https://www.cnblogs.com/tugenhua0707/p/10004654.html](https://www.cnblogs.com/tugenhua0707/p/10004654.html)

js操纵css通常有三种方式：
1. 通过元素的属性`style`进行修改(对伪类无可奈何)
2. 通过`<style>`标签进行修改(相当强大)

### 通过元素的属性`style`修改css(对伪类无可奈何)
```js
divElem = document.getElementById("box")
divElem.style.width = '100px'
divElem.style.cssText ="border:5px solid black; width:400px; height:200px;"
divElem.style.opacity ="0.2"
```

### 通过现有`<style>`标签修改css
```js
// styleId: <style>标签id
// cssSelector: css选择器
// attrName: css属性名
// attrVal: css属性值
function modifyStyle(styleId, cssSelector, attrName, attrVal) {
    var styleElem = document.getElementById(styleId)
    if (!styleElem) {
        console.log(`styleElem ${styleId} is not found`)
        return 
    }
    var sheet = styleElem.sheet
    var cssRules = sheet.cssRules
    var cssRule
    for (var i=0; i<cssRules.length; i++) {
        if (cssRules[i].selectorText == cssSelector) {
            cssRule = cssRules[i]
            break
        }
    }
    if (!cssRule) {
        console.log(`cssSelector ${cssSelector} is not found`)
        return
    }

    cssRule.style[attrName] = attrVal
}
```

### 通过创建`<style>`标签添加css
```js
function createStyleSheet() {
    var style = document.createElement('style');
    style.appendChild(document.createTextNode(""));
    document.head.appendChild(style);

    var styleObj = {
        index: 0,
        raw: style.sheet
    }
    styleObj.addRule = function(cssRule) {
        this.raw.insertRule(cssRule, this.index)
        this.index++
    }
    return styleObj;
}
var stylesheet = createStyleSheet();
stylesheet.addRule(`.box {width:100px;height:100px;background:red}`);
```

