# JQuery
* 方便处理HTML、事件、动画  
* 可以兼容浏览器  

##jquery选择器的性能优化  
1.量使用CSS中有的选择器  
2.避免过度约束  
3.尽量以ID开头  
4.让选择器的右边有更多特征  
5.避免使用全局选择器  
6.缓存选择器结果  

## JQ事件模型  
1.提供了统一的事件处理方法  
2.允许添加多个事件处理函数  
3.使用标准的事件名称(不带on)  
4.事件实例作为事件处理函数的第一个参数    
5.标准化事件实例最常用的属性  
6.提供了统一的事件取消和组织默认行为的方法  

##### 添加事件处理  
on(事件名称,[选择器][数据],事件处理函数)
$(“p”).on(“click”,null,null,function(event){console.log(“pclick);})  
$(“p”).on(“click”,function(event){console.log(“pclick);})  
  
##### 执行一次事件  
one(事件名称,[选择器][数据],事件处理函数)  
  
##### 统一方法和属性  
阻止冒泡stopPropagation()  
阻止默认行为preventDefault()  
阻止冒泡和默认行为return false  
  
冒泡就是向下查找再从最里层执行到触发层。  
  
event.target返回触发该事件的节点  
  
##### 类，对象，实例，属性，方法，事件，实例都是对象。  
属性描述对象或实例的特征，对象所含的变量就是对象的属性。  
事件是event对象，是对外部动作进行的响应。  
方法就是在对象上执行某个动作。  
  
##### triggerHandler相比trigger：  
1、不会触发浏览器默认事件  
2、不会产生事件冒泡  
3、只触发JQ对象集合中第一个元素的事件处理函数  
4、返回的是事件处理函数的返回值而不是JQ对象(也就是说不能使用链式语法)  
*trigger和triggerHandler事件是可以传入参数的，然后在事件出咯函数中接收这些参数。参数的传入应该是数组的形式。  
eg:`trigger(‘event’，[arg1,arg2,…])`  

##### 自定义事件  
on(“自定义事件名称”，执行函数)，trigger(‘自定义事件名称’)  

##### 事件命名空间
(相当于给事件名称加类，例如click.a.b的意思就是事件click添加了a这个类，a这个类里面又还包含b这个类。当需要触发a类click事件时写为trigger(“click.a”  )，同时，当触发a类click事件时他所包含的b类事件也会被触发)  

#### 定义一个对象方法：  
```
var object={say:function(){}}  
var EventsUtility={  
	addEvent:function(element,type,callback){  
		if(typeof addEventlistener!=="undefined")  
		{element.addEventListener(type,callback,false)}  
		else if(typeof attachEvent!=="undefined")  
		{element.attachEvent("on"+type,callback)}  
	    else{element["on"+type]=callback}  
	}  
}  
```
#### 使用插件  
http://plugins.jquery.com/  
向页面添加JQ：  
```
<head>  
<script type=“text/javascript” scr=“jquery.js”>  
</head>  
```
#### JQ版本的选择、下载，CDN的使用  
*production version用于实际网页中，被精简压缩  
*development version用于测试和开发  
jQuery.com下载。下载使用或者通过CDN使用。  
  
##### JQ库是一个JS函数库，JQ库包含以下特性：  
1.	HTML元素选取  
2.	HTML元素操作  
3.	CSS操作  
4.	HTML事件函数  
5.	JS特效和动画  
6.	HTML DOM遍历和修改  
7.	AJAX  
8.	Utilities  
  
##### 语法：  
$(selector).action()  
美元符号定义jQuery，选择符selector查询和查找HTML元素，action()执行对元素的操作。  
  
##### 文档就绪函数：文档加载完成之后运行jq代码  
$(document).ready(function(){  
---jquery function go here---  
})  
  
#### JQ选择器  
##### 一、元素选择器  
jQuery使用CSS选择器来选取HTML元素。  
$("p")选取<p>元素。  
$("p.intro")选取所有class="intro"的<p>元素。  
$("p#demo")选取所有id="demo"的<p>元素。  
##### 二、属性选择器  
jQuery 使用 XPath 表达式来选择带有给定属性的元素。  
$("[href]")选取所有带有href属性的元素。  
$("[href='#']")选取所有带有href值等于"#"的元素。  
$("[href!='#']")选取所有带有href值不等于"#"的元素。  
$("[href$='.jpg']")选取所有href值以".jpg"结尾的元素。  
  
##### jQuery CSS 选择器  
jQuery CSS选择器可用于改变HTML元素的CSS属性。  
$("p").css("background-color","red")  
  
###### css选择器  
(“*”)  
(“element”)  
(“#id”)  
(“.class”)  
(“selector1,selector2,selector3”)  
(“ancestor  descendant”)  
###### 属性选择器  
[属性]：  
[属性=‘值’]  
[属性*=‘值’]  
[属性~=‘值’]  
[属性$=‘值’]  
[属性!=‘值’]  
##### 筛选器  
###### 位置筛选器  
:even  匹配的索引为偶数的元素  
:odd  匹配的索引为奇数的元素  
:gt(index)  索引大于index的元素  
:lt(index)  索引小于index的元素  
:root  选取文档根元素，在html中根元素总是<html>  
设置 HTML 文档的背景颜色为黄色：$(“:root”).css(“background-color”,”yellow”);  
###### 子元素筛选器  
:eq(n)  
:fist-child  第一个子元素  
:last-child  最后一个子元素  
:nth-child(n)  所有父元素的子元素  
:first-of-type  相同元素名的所有第一个子元素  
:last-of-type  相同元素名的最后一个子元素  
:first  匹配的第一个元素  
:last  最后一个匹配的元素  
:has(selector)  至少含有一个筛选元素的所有元素  
:only-child  只为子元素的元素  
:parent  匹配元素的所有父元素  
###### 表单筛选器  
:button  
:checkbox  
:password  所有password类型元素  
:input  所有input、textarea、select和button元素  
:radio  所有radio类型的元素  
:reset  所有reset类型的元素  
:submit  所有提交类型的元素  
:checked  被检查或选中的元素  
:selected  所有被选中的元素  
###### 内容筛选器  
:empty  
:contains(text)   
:header  所有作为标题的元素，例如h1,h2  
:image  选取所有图像类型的元素  
:text  所有文本类型元素  
###### 其他筛选器  
:animated    
:disabled  
:enabled  
:visible  所有可见元素  
:hidden  所有被隐藏的元素  
:file  选取所有文件类型的元素  
:lang(language)  所有给定language的元素  
:not(selector)  所有不匹配的元素  
:target  选取由文档URL片段标识符指定的目标元素  

### JQ名称冲突  
jQuery使用$作为jQuery的简写方式，某些其他JS库中的函数(比如prototype)同样使用$符号，可以使用`noConflict()`的方法来解决问题  
`var name=jQuery.noConflict()`  
使用自己的名称来代替$符号。  
  
### jQuery HTML  
#### 内容的获取和设置  
text()设置或返回所选元素的文本内容  
html()设置或返回所选元素的内容(包括HTML标记)  
val()设置或返回表单字段的值  
  
#### 属性的获取和设置  
attr(“属性”，“值”)  
*允许同时设置多个属性：  
```
$(“#id”).attr({  
“href”:“http//www.abcd.com.cn”,  
“title”:“titleabcd”  
})  
```  
#### 添加新的HTML内容  
##### append()  
功能：在被选元素的结尾(仍然在内部)插入内容  
语法：$(selector).append(content)  
content规定要插入的内容，可以包含HTML标签  
*可添加多个内容，之间用逗号隔开  
相似功能：appendTo()  
  
##### prepend()  
功能：在被选元素的开头 (仍然在内部)插入内容  
语法：$(selector).prepend(content)  
content规定要插入的内容，可以包含HTML标签  
相似功能：prependTo()  
  
##### after()在被选元素之后插入内容（可包含HTML标签）  
##### before()在被选元素之前插入内容（可包含HTML标签）  
  
##### insertAfter()  
功能：在被选元素之后插入HTML标记或已有元素  
*如果该方法用于已有元素，这些元素会被从当前位置移动到被选元素之后  
语法：$(content).insertAfter(selector)  
*content规定要插入的内容，可以是选择器表达式，也可以是HTML标记  
eg：
```
$("button").click(function()  
{$("<span>Hello world!</span>").insertAfter("p");})  
```  
##### insertBefore()  
  
##### clone()  
功能：生成被选元素的副本，包含子节点、文本和属性  
语法：$(selector).clone(includeEvents)  
*includeEvents值为布尔值，规定是否复制元素的所有事件处理，默认不包含。  
  
#### 删除替换元素、内容  
##### remove()  
功能：移除被选元素，包括所有文本和子节点  
*不会把匹配的元素从JQ对象中删除，可以继续使用  
*但只保留本身，其他的事件、数据等都会被移除  
  
##### detach()  
功能：移除被选元素，包括所有文本和子节点  
*不会把匹配的元素从JQ对象中删除，可以继续使用  
*保留所有绑定的事件，附加的数据。这一点与remove()不同  
  
##### empty()  
功能：从被选元素中移除所有内容，包括文本和子节点  
  
##### replaceWith()  
功能：用指定的HTML内容或元素替换被选元素  
语法：$(selector).replaceWith(content)  
*content规定替换元素的内容。  
可以是HTML代码（<div></div>）;  
可以是新元素，如（document.createElement(“div)）  
可以是已存在的元素，如（$(“.div1”)）  
*已存在的元素不会被移动，只会被复制，并包裹被选元素  
  
##### replaceAll()  
功能：用指定的HTML内容或元素替换被选元素  
语法：$(content).replaceAll(selector)  
*同replaceWith  
  
#### 获取并设置CSS类  
##### addClass()  
功能：向被选元素添加一个或多个类  
*该方法不会移除已存在的class属性，只添加一个或多个class属性  
*添加多个时，使用空格分隔类名  
语法：$(selector).addClass(class)  
  
##### removeClass()  
功能：向被选元素移除一个或多个类  
*如果没有规定参数，则该方法将从被选元素中删除所有类  
  
##### toggleClass()  
功能：对设置或移除被选元素的一个或多个类进行切换。检查每个元素中指定的类，如果存在则删除，如果不存在就添加，实现切换效果  
*通过使用“switch”参数规定只删除或只添加  
语法：$(selector).toggleClass(class,switch)  
*switch值为布尔值，true为只添加，false为只移除  
  
##### hasClass()  
功能：检查被选元素是否包含指定的class  
语法：$(selector).hasClass(class)  
  
##### css()  
功能：返回或设置CSS属性  
语法：$(selector).css(“属性名”，“值”)  
设置多个：$(selector).css({  
“属性”:“值”，  
“属性”:“值”，  
… })  
  
#### HTML结构  
##### wrap()  
功能：把每一个符合匹配的元素放置在指定的HTML内容或元素中  
（连标签一起包裹；有几个匹配元素就有几个包裹）  
语法：$(selector).wrap(wrapper)  
*wrapper规定包裹被选元素的内容  
可以是HTML代码  
可以是新元素  
可以是已存在的元素  
*已存在的元素不会被移动，只会被复制，并包裹被选元素  
##### wrapAll()  把所有符合匹配的元素全部包裹在一个包裹中。  
##### wrapInner()  使用指定的HTML内容或元素，包裹每一个被选元素的内容  
(包裹在匹配的标签内)  
##### unwrap()  $(selector).unwrap()删除被选元素的父元素  
  
#### 元素和浏览器窗口的尺寸  
width() 设置或返回宽度（不包括内边距、边框或外边距）  
height() 设置或返回高度（不包括内边距、边框或外边距）  
innerWidth() 返回宽度（包括内边距）  
innerHeight() 返回高度（包括内边距）  
outerWidth() 返回宽度（包括内边距和边框）  
outerHeight() 返回高度（包括内边距和边框）  
  
### jQuery遍历  
遍历意为移动，用于根据其相对于其他元素的关系来查找或选取HTML元素。  
#### 祖先遍历——向上遍历DOM树  
##### parent()  
语法：parent(filter)  
功能：返回被选元素的直接父元素  
  
##### parents()  
语法：parent(filter)  
功能：返回被选元素的所有祖先元素，直到文档的根元素<html>  
  
##### parensUntil()  
功能：返回介于两个给定元素之间的所有祖先元素  
语法：$(selector).parentsUntil(selector/element，filter)  
*filter规定匹配元素的选择器表达式  
  
#### 后代遍历  
##### children()  
功能：返回被选元素的所有直接子元素  
  
##### find()  
功能：获得当前元素集合中每个元素的后代，通过选择器、jQ对象或元素来筛选。  
  
#### 同胞遍历  
siblings(selector)  返回所有同胞元素  
next(selector)  下一个同胞元素  
nextAll(selector)  随后的同胞元素  
nextUntil(selector)  之间的同胞元素  
prev(selector)    
prevAll(selector)  
prevUntil(selector)  
  
#### 过滤遍历  
first()  将匹配元素集合缩减为集合中的第一个元素  
last()  将匹配元素集合缩减为集合中的最后一个元素  
eq(index)  将匹配元素集缩减值指定 index 上的一个  
filter()  将匹配元素集合缩减为匹配指定选择器的元素  
not()  从匹配元素集合中删除元素  
  
#### 属性操作  
addClass()  
hasClass()  
removeClass()  
toggleClass()  
attr()  
removeAttr()



