# HTML（hypertext markup language）超文本标记语言  
***
*   它不是编程语言而是一种标记语言；
*   标记语言是一套标记标签；
*   html使用标记标签来描述网页。
*   Html标记标签通常被称为html标签，是由尖括号包围的关键词；
*   标记标签通常是成对出现，第一个标签是开始标签，第二个是结束标签。

## 特点：
1.  不需要编译，直接由浏览器执行  
2.  文本文件  
3.  必须使用html或htm为文件名后缀  
4.  对大小写不敏感  

## 基本结构
标签 元素 属性 注释  
```html  
<!doctype html> 
<html>  
<head>  
    <title>第一个网页</title>  
    <meta http-equiv="content type" content="text/html;charset=utf-8"/>
    <!--页面内容中有中文时，meta标签设置编码格式-->
</head>
<body bgcolor='yellow'>
    <hr/>
    <p>大家好，一起来学习html标记语言</p>
</body>
</html>
```
## 标签  
### 文字和段落标签  
文字斜体 ：<i> </i>  <em></em>  \*显示效果一样但是含义不同：i为倾斜，em为强调  
加粗：<b></b>  <strong></strong>  \*显示效果一样但是含义不同：b为加粗，strong为强调  
文字下标：<sub> 文字上标：<sup>  
特殊符号的输入需要查找书写符号实体  
`&nbsp;` 半角的不断行的空白格(与文字一致)  
`&ensp;` 半角的空格   
`&emsp; `全角的空格  
`<pre></pre>`预定义格式显示文本  
`<br>`换行  
`<hr>`水平线  
`<h1></h1>~<h6></h6>`从大到小6种标题  
align对齐属性 left right center justify : align=”center”
 

### 列表标签
#### 无序列表标签
```html
<ul>
<li>列表项</li>
<li>列表项</li>
</ul>
```
无序列表Type属性 disc、 square、 circle
#### 有序列表
```html
<ol>
<li>列表项</li>
<li>列表项</li>
</ol>
```
无序列表Type属性 1、a、A、i、I
#### 定义列表
`<dl>  <dt></dl> <dd> </dd> …<dt></dt>…</dl>`

### 在网页中插入图片
语法：`<img src=”” alt=”” …/>`  
属性：src（必写）图像地址   alt 图像的代替文字   height 图像高   width 图像宽  
*img是空标签，也就是它只包含属性，并没有闭合标签。要在页面上显示图像就需要使用源属性(src)，源属性的值是图像的url地址。  

#### Html的路径
绝对路径，完整的路径地址  
相对路径：  
1.图片与网页文件在同一目录下，`<img src=”name.jpg”/>`  
2.在上一级目录中`<img src=”../name.jpg”/>`  
3.在下一级目录中`<img src=”文件夹名称/name.jpg”/>`  
图像的宽、高可以用像素（px）作为单位也可以是百分比（图像占所包含它的容器的百分比）

### 超链接
`<a href=””> </a>`  href是链接地址，可以是内部链接也可以是外部链接。  
属性：href链接地址   target目标窗口——值：_self（当前窗口打开链接）  _blank（新窗口打开链接）  _top   _parent   title提示文字   name链接名字

#### 锚定位
1.定义锚的位置和锚名  
2.设置寻找锚的链接`<a href=”#锚名 ”></a>`    
\*锚标签内可以没有内容，即`<a name=”*** ”> </a>`  

#### 不同页面锚定位
1.定义锚的位置和锚名  
2.设置寻找锚的链接`<a href=”网页名称#锚名 ”></a>`  

超链接发送邮件：`<a href=”mailto:676410292@qq.com”>`  mailto加所要发送的邮箱地址。该操作会直接打开本地邮箱编辑器进行邮箱编辑。
超链接文件下载：`<a href=”文件地址”>`链接地址写为文件地址，文件需要压缩，不压缩会导致打开文件而不是下载。

### 表格
`<table></table>`表格标签  
`<tr></tr>`行标签  
`<th></th>`表头标签，居中加粗  
`<td></td>`单元格标签  
单元格标签跨行跨列属性：colspan（跨列） rowspan（跨行）   eg:`<td colspan=”2”>`   
\*注意要把对应的被合并的单元格去掉。  
`<caption></caption>`表格标题，居中显示  

带结构的表格,对表格进行结构划分  *3个结构顺序不影响表格展示顺序，即不影响表格布局。   
`<thead></thead>`  
`<tbody></tbody>`  
`<tfoot></tfoot>`  


表格嵌套：嵌入到<td>单元格内。*嵌入的表格注意要完整。  
表格网页布局：1、尽量减少使用表格嵌套  2、减少跨行跨列的使用  

### 表单
`<form></form>`  
表单元素：
文本域、单选框、复选框、按钮、列表 … …  通过`<input>`标签下type属性来确定表单元素。  
单选框radio
`<input type=”radio” name=”* * *（注意要保持该项目下所有选框的name一致）” value=”默认值，在这里也就是该选框所代表的的意义，要传送给服务器的内容” checked（起始状态，也就是默认选项）/>`  
复选框checkbox
`<input type=”checkbox” name=”* * *（选框的name不必须保持一致，但是为了方便服务器对提交内容的读取，还是最好保持一致）” value=”默认值” checked（起始状态）/>`  
按钮元素button、submit、reset.  `<input type=”button” value=”按钮上的显示” name=”名字”>`

下拉菜单和列表标签`<select></select>、<option></option>`  
Select标签属性：name、multiple（可选择多项）、size（显示的条目个数 ）*在添加了multiple和size属性之后下拉状态就不存在了，相对应的变成了列表形式。  
Option属性标签：value、selected（默认初始选项）   
Optgroup标签：选项分组。属性标签：label（标签）、 ` <optgroup label=”显示的组名称”>`  
Textarea标签：多行文本标签 
```
<select>
<option></option>
<option></option>
</select>
```

### 块级标签、行内标签
####显示特性：
块级元素：独占一行，可以设置宽高；  
行内元素：多个元素共占一行，不可以设置宽高，高度由内容撑开；  
行内块元素：结合的行内和块级的有点，不仅可以对宽高属性值生效，也可以多个标签存在一行显示；

* 行内标签：  
包含a、span、em、strong、b、i、u、label、br等  
a标签：主要用来链接一个其他的网页；  
span标签：主要用来对行内的文字进行一些样式以及其他的操作；  
em标签：一般用来对文字进行强调，使用斜体体现出来；  
strong标签：一般用来对文字进行强调，使用加粗字体体现出来；  
img标签：图片引用标签，其中 src属性中写入图片的地址；  
var标签：JavaScript中命名变量的标签。  
 
* 块标签：  
包含p、div、ul、ol、li、dl、dt、dd、h1~h6、form等  
p标签：段落标签，段落文字使用，默认格式：段尾进行换行；  
div标签：划分块的主要使用标签；  
ul标签：无序列表的主标签，后面的标号为圆点（黑色）；  
ol标签：有序列表的主标签，后面一般跟有序的1,2,3,4,5...；  
li标签：列表中的主体使用标签  
dl标签：自定义标签的主标签；  
dt标签：自定义标签的表头；  
dd标签：自定义标签的表头的解释（描述）信息；  
h1~h6：6级标题标签、字体的大小依次变小。  
 
* 行内块标签：img,input,textarea
特点：结合的行内和块级的有点，不仅可以对宽高属性值生效，还可以多个标签存在一行显示；

##### 标签可以通过设置display属性值来转换：
1.块级标签转换为行内标签：display:inline;  
2.行内标签转换为块级标签：display:block;  
3.转换为行内块标签：display：inline-block;  
 
##### 嵌套规则 
块标签可以套行标签，行标签不可以套块标签。  
P标签不要套块属性标签，可以套a，span，文本...  
嵌套的时候注意代码的缩进。
