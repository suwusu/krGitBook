# div内文本自动换行

### 方法1
## html代码
```
<div>twrwwrwerwerwrwrwrwrwrwrwrwerwerwr</div>
```
## css代码
```
div{
    display: table;
    width: 200px;
    table-layout: fixed;
    word-wrap: break-word;
}
```


### 方法2
## html代码
```
<div>twrwwrwerwerwrwrwrwrwrwrwrwerwerwr</div>
```
## css代码
```
div{
    width: 100px;
    display:block;
    word-break: break-all;
    word-wrap: break-word;
}
```
### 相关属性

#### display

|属性值|描述|
|:-----|:-----|
|none|此元素不会被显示|
|block|此元素将显示为块级元素，此元素前后会带有换行符|
|inline|默认。此元素会被显示为内联元素，元素前后没有换行符|
|inline-block|行内块元素。(CSS2.1 新增的值)|
|list-item|此元素会作为列表显示|
|run-in|此元素会根据上下文作为块级元素或内联元素显示|
|table|此元素会作为块级表格来显示（类似 table），表格前后带有换行符|
|inline-table|此元素会作为内联表格来显示（类似 table），表格前后没有换行符|
|table-row-group|此元素会作为一个或多个行的分组来显示（类似 tbody）|
|table-header-group|此元素会作为一个或多个行的分组来显示（类似 thead）|
|table-footer-group|此元素会作为一个或多个行的分组来显示（类似 tfoot）|
|table-row|此元素会作为一个表格行显示（类似 tr）|
|table-column-group|此元素会作为一个或多个列的分组来显示（类似 colgroup）|
|table-column|此元素会作为一个单元格列显示（类似 col）|
|table-cell|此元素会作为一个表格单元格显示（类似 td 和 th）|
|table-caption|此元素会作为一个表格标题显示（类似 caption）|
|inherit|规定应该从父元素继承 display 属性的值|

### table-layout
|属性值|描述|
|:-----|:-----|
|automatic|默认。列宽度由单元格内容设定|
|fixed|列宽由表格宽度和列宽度设定|
|inherit|规定应该从父元素继承 table-layout 属性的值|

### word-wrap 属性允许长单词或URL地址换行到下一行（规定文本的换行规则）
|属性值|描述|
|:-----|:-----|
|normal|只在允许的断字点换行（浏览器保持默认处理）|
|break-word|在长单词或 URL 地址内部进行换行|

### word-break 属性规定自动换行的处理方法（规定非中日韩文本的换行规则）

|属性值|描述|
|:-----|:-----|
|normal|使用浏览器默认的换行规则|
|break-all|允许在单词内换行|
|keep-all|只能在半角空格或连字符处换行|
