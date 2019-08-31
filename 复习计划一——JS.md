# 复习计划一——JS  
  
## 目录  
* 函数、对象、实例、原型  
* 原型链  
* 执行上下文 EC (execution context)  
* 闭包  
* script引入方式  
* 对象的拷贝  
* instanceof  
* 继承  
* 复用  
* 数据类型  
* 模块化  
* dom事件  
* call、apply、bind  
* 节流与防抖  
* Ajax  
* 数组  
* 字符串  
* ES6、ES7  
* AST抽象语法树  
* babel编译原理  
* 函数柯里化  
  
## 1. 函数、对象、实例、原型  
* ##### 函数独立存在，函数可以用来创建对象。  
* ##### 对象是函数的实例，对象的方法是对象的属性，本质是函数，对象需要被创建；  
  
*    ##### 创建对象的方法：  
1、字面量的声明方式；  
2、构造函数的方式；如new Object() ;注意Object是函数；  
3、工厂模式；本质上还是构造函数，在函数内部构造函数，通过调用函数的方式来构造对象  
4、构造方法的方式；本质上也是构造函数，只不过使用的构造函数是定义的函数模板  
  
*	##### 在使用new 的时候发生了什么  
1、创建一个对象{}  
2、给对象添加`__proto__`属性，`__proto__`是一个对象，值为构造器的prototype  
3、将构造函数的作用域赋值给新对象（即this指向这个新对象）  
4、执行构造函数中的代码（为这个新对象添加属性）  
5、返回这个对象  
  
*	##### prototype：实例的原型  
包含constructor和__proto__两个部分constructor指向原型所在的函数本身；  
`__proto__`指向构造器的原型函数具有prototype，对象具有`__proto__`。  
  
*	##### 总结：  
① 函数调用还是函数，具有prototype，prototype包含constructor和`__proto__`；  
② 函数构造成为实例对象，对象具有`__proto__`属性，指向构造器原型。  
  
## 2. 原型链  
*	##### 原型链由原型对象组成。  

*	##### 每个原型对象都包含一个`__proto__`属性，指向创建该对象的构造函数原型，`__proto__`将对象链接起来组成了原型链。是一个用来实现继承和共享属性的有限对象链。  

*	##### 属性查找机制  
当查找对象属性时，如果实例对象自身不存在该属性，则沿着原型链往上一级查找，直至顶级原型对象（Object.prototype）,否则输出undefined；  

*	##### 属性修改机制  
修改原型属性会造成所有继承于该对象的实例的属性发生改变。  

*	##### instanceof  
`object instanceof constructor` 返回值为布尔型；  
object .`__proto__=== constructor.prototype.constructor `则返回 true  
  
## 3. 执行上下文 EC (execution context)  
*	##### 执行环境的类型：  
全局级执行上下文，默认的代码运行环境，引擎最先进入的环境  
函数级执行上下文  
eval执行上下文  
  
*	##### 执行环境的三个部分：  
1、VO（variable object）变量对象：一个抽象的概念，可以当成是一个对象，包含当前执行上下文的所有变量和函数声明。  
2、在不同的执行上下文中，它有不同的具体表现，例如在全局执行上下文中，VO就等于window；在函数执行上下文中，由于要保存函数形参、局部变量、自身函数对象引用变量、参数、this，所以新创建了一个AO(active object)活动对象来保存，而此时，VO的具体实现就是AO。  
3、作用域链：作用域链就是将有嵌套层次关系的执行上下文的VO拼接起来。  
4、this指向  
*	##### 代码执行过程  
1、创建全局执行上下文（创建作用域链、变量、函数和参数，求this值）  
2、全局执行上下文自上而下执行（变量赋值，函数引用，解释/执行其他代码）  
3、遇到函数时，函数执行上下文被推到执行栈顶层（当前EC放在顶层），函数执行上下文被激活，执行函数中的代码，执行完成后移除执行栈，全局执行上下文重新推到顶层。  
  
## 4. 闭包    
*	##### GC（garbageCollection）垃圾回收机制    
a/标记清除 b/引用计数 c/标记整理 d/复制算法    
JS引擎的GC方案是标记清除，即：遍历所有对象，标记可达对象，回收已不可访问对象。GC的缺陷：GC时，会停止响应其他操作。  
  
*	##### 闭包是什么  
闭包属于一种特殊的作用域，称为静态作用域。  
闭包可以理解为：在一个作用域已经被销毁的情况下，仍有其他变量保存着可以访问到这个作用域的作用域链，因此可以继续访问到该作用域的变量对象。  
  
*	##### 闭包产生的问题：  
多个子函数的[[scope]]都是同时指向父级，是完全共享的。  
因此当父级的变量对象被修改时，所有子函数都受到影响。  
  
*	##### 解决:  
① 变量可以通过 函数参数的形式 传入，避免使用默认的[[scope]]向上查找  
② 使用setTimeout包裹，通过第三个参数传入  
③ 使用 块级作用域，让变量成为自己上下文的属性，避免共享  
  
## 5. script引入方式  
*	html 静态`<script>`引入  
*	js 动态插入`<script>` （创建script元素，添加src属性）  
*	`<script defer>`: 延迟加载，立即下载，元素解析完成后执行  
*	`<script async>`: 异步加载，立即下载，不妨碍页面其他操作，执行时会阻塞元素渲染 （延迟加载和异步加载都只适用于外部脚本）  
  
## 6. 对象的拷贝  
*	##### 基本类型&引用类型  
ECMAScript中的数据类型可以分为两种：基本类型和引用类型  
基本数据类型按值访问，可操作保存在变量中的实际的值，指的是简单的数据段。  
引用类型指，当复制保存着对象的某个变量时，操作的是对象的引用，但在为对象添加属性时，操作的是实际的对象，引用类型指可能为多个值构成的对象。  
基本数据类型有这五种：Undefined、Null、String、Number、Boolean。  
引用类型有这几种：object、Array、RegExp、Date、Function；  
特殊的基本包装类型(String、Number、Boolean)以及单体内置对象(Global、Math)。  
  
*	##### 不同类型的存储方式  
基本类型值在内存中占据固定大小，保存在栈内存中；  
引用类型值是对象，保存在堆内存中，并且在栈内存中存储对象的变量标识符以及对象在堆内存中的存储地址。  
  
*	##### 不同类型的复制方式  
基本类型：复制变量值，创建值的副本，将副本赋值给新变量；  
引用类型：复制的是指针，也就是对象在栈内存中的引用地址，最终两个变量都会指向同一个对象。  
浅拷贝：仅仅是复制了引用，彼此间的操作会互相影响  
深拷贝：在堆中重新分配内存，创建新的地址，相同的值，互不影响  
/* 深浅拷贝的概念是针对于引用类型的。   
/* 拷贝也是继承的一种  
  
*	##### 实现深拷贝的方式：  
1、 JSON.stringify()把js对象转换为字符串，然后JSON.parse()把JSON字符串反序列化为一个js对象。   
`JSON.parse(JSON.stringify(obj))`；  
但是当对象具有循环引用的对象时会报错，当有值为函数、undefined或symbol时，无法拷贝。  
2、 利用递归来实现对对象或数组的深拷贝。思路：对属性中所有引用类型的值进行遍历，直到是基本类型为止，拷贝基本类型值。  
实例：  
```  
```  
3、 实现第一层深拷贝，作为整体的深拷贝  
①Object.assign(trget,sorce) * Object.assign({},obj) 返回拷贝的新对象  
②扩展运算符  
  
## 7. 继承  
*	##### 继承的几种方式  
①原型链继承：让新实例的原型等于父类的实例。  
②借用构造函数：使用call()和apply()在子类函数中做了父类函数的自执行。  
③组合  
<table><tr><td bgcolor=red>待补充。</td></tr></table>  
  
## 8. 复用  
函数封装；继承；复制（拷贝）；借用（call、apply）  
<table><tr><td bgcolor=red>貌似涉及很多设计模式。分类依据不清晰。之后再看。</td></tr></table>  
  
## 9. 数据类型	  
*	##### 简单数据类型：string、number、boolean、undefined、null、symbol  
*	##### 复杂数据类型：object。  
*   
string字符串由双引号或单引号包裹表示；  
number中有一个特殊的类型NaN，NaN与任何值都不相等，数据类型是number；  
boolean值为true或false；  
undefined声明了一个变量但没有赋值，一般情况下变量不会特别赋值为undefined，但是如果出现诸如name=undefined的情况，它的变量类型也还是会自动识别为undefined；  
null用来初始化变量值，undefined值派生自null，所以undefined==null；Symbol类型的数据永远不相等，即便在创建时传入了相同的值。  
  
*	##### 数据类型判断  
typeof运算符可以返回string、number、boolean、undefined四种原始数据类型，复杂数据类型返回function、object；  
对象、数组、null等均返回为object；  
函数返回为function；  
Array、RegExp、Date等对象类型的判断都可以用constructor来判断。形如arr.constructor==Array ?  
  
*	##### 类型转换  
###### 隐式转换：  
隐式转换涉及三种转换:转为原始值、转为数字、转为字符串  
`-`  `*`  `/`  `%` 全都转换成数值后计算  
`+`  ：  
数字 + 字符串 =字符串  
数字 + 对象 –> 优先调用对象的valueOf，然后再toString  
数字+Boolean/null  –> 数字  
数字 + undefined  –> NaN  
*   
Number()强制转换，可用于任何数据类型；  
parseInt()提取字符串开头的数字。返回整数或NaN。  
parseFloat()解析字符串返回浮点数。返回整数或NaN。  
a .toString()；  String（a）;  
  
## 10. 模块化   
###### 参看 https://yq.aliyun.com/articles/700551  
  
*	##### 无模块化：  
为了提高项目代码的可读性、可扩展性拆分成多个JS文件。但多个JS文件之间的相互依赖关系难以维护，每个模块都是暴露在全局的。  
  
*	##### commonJS规范（同步加载模块）(运行在node环境中)  
在commonJS中，一个文件就是一个模块，拥有单独的作用域。  
普通方式定义的变量、函数、对象都属于该模块内。  
通过require来加载模块。  
通过exports和module.exports来暴露模块中的内容。（为了方便node为每个模块提供一个exports变量，其指向module.exports; exports，相当于在模块头部添加了var  exports=module .exports可以添加方法但不能赋值。）
模块可以多次加载，但只会在第一次加载的时候运行一次，然后运行结果就被缓存了，再次加载直接读取缓存结果；模块的加载顺序是同步加载的。  

*	##### ES6模块化  
ES Module 是语言层面的模块化方案，由 ES 2015 提出，其规范与 CommonJS 比之 ，导出的值都可以看成是一个具备多个属性或者方法的对象，可以实现互相兼容；但写法上 ES Module 更简洁，与 Python 接近；  
•	ES Module 会对静态代码分析，即在代码编译时进行模块的加载，在运行时之前就已经确定了依赖关系（可解决循环引用的问题）；  
•	ES Module 关键字：import export 以及独有的 default 关键字，确定默认的导出值；  
•	ES Module 中导出的值是一个 只读的值的引用 ，无论基础类型和复杂类型，而在 CommonJS 中 require 的是值的拷贝，其中复杂类型是值的浅拷贝；  
  
*	##### AMD规范（非同步加载模块）CMD规范（非同步加载模块）  
由于Node.js 主要用于服务器编程，模块文件一般都已经存储于本地硬盘，不用考虑非同步加载的方式，所以commonJS规范比较适用，但是浏览器端环境复杂，需要从服务器端加载模块，就必须采用非同步模式。浏览器端一般采用AMD规范。  
模块化开发在现代开发中已是必不可少的一部分，它大大提高了项目的可维护、可拓展和可协作性。通常，我们在浏览器中使用 ES6 的模块化支持，在 Node 中使用 commonjs 的模块化支持。  

*	##### 分类:  
•	es6: import / export  
•	commonjs: require / module.exports / exports  
•	amd: require / defined  
•	require与import的区别  
•	require支持 动态导入，import不支持，正在提案 (babel 下可支持)  
•	require是 同步 导入，import属于 异步 导入  
•	require是 值拷贝，导出值变化不会影响导入值；import指向 内存地址，导入值会随导出值而变化  
  
## 11. dom事件  
*	##### dom级别  
•	dom0级(从来没有成为过规范)/dom1/dom2/dom3  
•	对应的dom0级事件/dom2级事件/dom3级事件（1级并没有事件标准）  

*   
0级事件（HTML属性）：将函数值赋值给一个事件处理属性，通过给事件处理属性赋值null来解绑，缺点是结构跟事件强耦合。  
*   
2级事件（DOM元素属性）：定义了addEventListener和removeEventListener两个方法，用来允许给一个事件添加多个处理函数；addEventListener(事件，处理函数，是否在捕获时期执行处理函数)。<table><tr><td bgcolor=#ddd>IE8以下不支持，需要attachEvent和detachEvent实现</td></tr></table>
*     
3级事件：在二级的基础上添加了更多的事件类型（UI事件，如load、scroll；焦点事件，如blur、focus；鼠标事件，如dbclick、mouseup；滚轮事件，如mousewheel；文本事件，如textInput；键盘事件，如keydown、keypress；合成事件，输入法编辑器输入字符时触发，如compositionstart；变动事件，当底层DOM结构发生变化时触发，如DOMsubtreeModified）

*	##### dom事件流程  
事件捕获与事件冒泡：事件的传递是先捕获，后冒泡，点击inner后，发生从最外层到target的事件捕捉，  
（例如里层、外层节点都绑定了click事件，在事件冒泡阶段，里层节点被点击之后会继续触发外层节点点击事件；否则相反。）  
  
*	##### Event对象  
•	事件对象是与某一特定事件香瓜且包含该事件详细信息的对象。  
•	Event接口表示在DOM中发生的任何事件；  
•	一些是用户生成的，一些是其他API生成的。  
•	事件本身包含所有事件通用的属性和方法。  
•	当事件发生时，event对象就会被创建，并依次传递给事件监听器。  
•	在处理函数中，将event对象作为第一个参数，可以访问到DOMEvent接口。  
•   event对象方法  
stopPropagation():  
用于阻止事件进一步传播（当前层阻止则当前层仍会冒泡，下一层不会）/* IE8以下不支持，需要attachEvent和detachEvent实现  
preventDefault():  
用于取消事件的默认操作。比如a链接的跳转行为，  
/* 在IE9之前的浏览器中需要设置returnValue属性为false来实现  
/* 目前草案中还添加了一个新的stopImmediatePropagation  
• event对象属性  
属性非常多。常用的：  
type属性可以获取事件发生的类型；  
target获取事件的目标对象；  
鼠标事件属性(例如screenX，获取鼠标基于屏幕的x轴坐标)；  
键盘事件属性(例如keyCode获取按下键盘的建码值)；  
以及表单事件属性、window事件属性等等。  
  
* ##### 事件委托  
将事件监听器添加到父元素上，以此来避免对多个子节点逐一添加事件监听。  
具体方法：（以点击为例）把子元素需要执行的事件处理绑定到父元素上，当子元素被点击，触发click事件，通过事件冒泡，触发了父元素的click事件，父元素上的事件处理判断点击的元素是否符合需要执行的条件，然后执行。  
• 优势：    
a/减少事件注册，节省内存。    
b/减少dom节点更新操作 /* 例如动态新增的li元素不用新绑定事件，删除li时不需要进行元素与处理函数的解绑。    
• 缺点：    
a/事件委托基于事件冒泡机制，对于onfocus和onblur事件不支持    
b/层级过多冒泡过程可能会被阻止（建议就近委托）只要冒泡过程中遇到stopPropagation等或者事件不支持冒泡委托就会失败。    
* ##### 自定义事件    
这些事件不是浏览器本身的事件，通常称为合成事件。    
###### 创建自定义事件：    
1、使用Event构造函数创建：new Event(selfEvent)      
2、需要添加自定义数据时，使用new CustomEvent(“selfEvent”，{‘detail’：somedetail})    
触发自定义事件：使用dispatchEvent()触发。/* IE8以下使用fireEvent    
    
## 12. 节流与防抖    

   节流（throttle）和防抖（debounce）用来减少事件处理函数的调用频率。    
    
* ##### 防抖debounce  
当持续触发事件时，一定时间段内没有再次触发事件，事件处理函数就执行一次，如果设定的时间来到之前有一次出发了事件，就重新开始延时。  
实现原理：在事件处理函数中返回一个函数(事件发生就会触发函数执行)，在函数中先清除timeout，再添加timeout，以此来实现防抖。（因为当停止持续触发时，timeout才不会被清除，才会生效，然后才能在一定时间后执行timeout里的函数）。  
实例：  

```  
//防抖  
function debounce(fn,wait){  
  var timeout=null;  
  return function(){    
    if(timeout!==null){clearTimeout(timeout)};    
    timeout=setTimeout(fn,wait);    
  }    
}    
    
//事件处理函数    
function handle(){    
  console.log(Math.random())    
}    
    
//滚动事件（需要防抖的事件）    
window.addEventListener("scroll",debounce(handle,1000))    
```    
  
* ##### 节流throttle  
当持续触发事件时，保证一定时间段内只调用一次事件处理函数。  
实现方式： 
##### 1、时间戳。  
当持续触发事件时，记录每一次触发时的时间，与上一次执行事件处理函数时的时间作比较，大于设定的节流时间时再执行事件处理。  
实例：  

```  
//节流  
function throttle(fn,wait){  
  var pre=Date.now();  
  return function(e){  
    var context=this,  
      now=Date.now();  
    if(now-pre>=wait){  
      fn.apply(context,e)  
    }  
  }  
}  
  
//事件处理函数  
function handle(){  
  console.log(Math.random())  
}  
  
//滚动事件（需要防抖的事件）  
window.addEventListener("scroll",throttle(handle,1000))  
```  
*   
##### 2、定时器  
设置定时器，直到一定时间定时器执行并被清除后再次添加定时器。  
实例：  

```  
function throttle(fn,wait){  
  var timer=null;  
  return function(e){  
    var context=this;  
    if(!timer){  
      timer=setTimeout(function(){  
        fn.apply(context,e)  
      })  
    }  
  }  
}  
  
//事件处理函数  
function handle(){  
  console.log(Math.random())  
}  
  
//滚动事件（需要防抖的事件）  
window.addEventListener("scroll",throttle(handle,1000))  
```  
  
## 13. Ajax（Asynchronous JavaScript And XML）  
Ajax=异步的JavaScript和XML。  
Ajax是一种无需重新加载整个网页的情况下，能够更新部分网页的技术。  
  
* ##### 1、创建XMLHttpRequest对象  
XMLHttpRequest对象是Ajax的基础。  
使用new XMLHttpRequest()的方法创建对象。  
/* 老版本的 Internet Explorer （IE5 和 IE6）使用 ActiveX 对象  
  
* ##### 2、发送请求  
使用XMLHttpRequest对象的open()和send()方法向服务器发送请求。  
<font color=#aaa>open（请求的类型get/post，文件在服务器上的位置，是否同步）；</font>  
<font color=#aaa>send（string），仅用于post请求。</font>  
与post相比，get更简单也更快捷，大部分情况下适用。然而当需要向服务器发送大量数据时(post没有数据量限制)，无法使用缓存文件时（更新服务器上的文件或数据库），发送包含未知字符的用户输入时，post比get更稳定也更可靠。  
实例：  
```  
xhr.open(method , url , async)  
xhr. setRequestHeader(头的名称，头的值)：向请求添加HTTP头，*使用post时需要添加这一项。  
xhr.send(string)  
```  
* ##### 3、取得响应  
使用XMLHttpRequest对象的responseText和responseXML来获取响应  
*   responseText：如果来自服务器的响应并非XML就使用responseText属性，否则使用responseXML 这两个属性中包含了服务器返回的内容。  
*   onreadystatechange事件  
当请求被发送到服务器时，需要执行一些基于响应的任务。每当readystate改变时，就会触发onreadystatechange事件，readyState属性反映客户端一个Ajax请求的过程状态。status属性反映服务器对请求的反馈。  readyState共有5种状态：0（还未调用send方法）1（已调用send正在发送请求）2（send方法执行完成）3（正在解析响应内容）4（响应内容解析完成可以在客户端调用了）   status状态码一般可以分为5类，以1—5开头的三位数字来表示不同的响应状态。例如200就表示响应成功。404未找到网页  
  
## 14. 数组Array  
* ##### 对象属性：constructor、prototype、length  
  
* ##### 对象方法：  
###### • 增：  
push()向末尾添加一个或多个元素，返回新的数组  
unshift()向数组开头添加一个或多个元素，返回新的数组  
###### • 删：  
pop()删除并返回数组最后一项；  
shift()删除并返回数组的第一项；  
splice(索引序号，删除个数，插入项1，插入项1 …)增删改  
###### • 拼接：  
concat(arr1，arr2 …)连接两个或更多的数组  
###### • 字符串：  
join()指定分隔符，数组转字符串  
toString()数组转换为字符串  
###### • 排序：  
reverse()颠倒数组中元素顺序；  
sort()排序,sort()比较的是字符串；sort可以接收一个函数作为参数，函数返回值小于等于0时，项目位置不变，大于0时交换位置。例如：arr.sort(function(a,b){return a-b})，就是数组按升序排列。  
###### • 选取：  
slice(start , end)返回指定一个或多个元素，不会对原数组产生改变。start必需，如果是负数则从尾部开始选取，，经实验貌似不必需；end省略时从开头选取到结尾。  
###### • 值：  
valueOf()  
返回数组对象的原始值  
###### • 查找：  
indexOf(要查找的项目，开始查找的位置)，返回值为数字，为项目在数组中第一次出现的位置。没有查找到返回-1。注意查找值的标准是===  
lastIndexOf()  
  
## 15. ES6、ES7  
* ##### let、const  
块级声明，在块的作用域外无法访问  
特点：a/不会被提升 b/不可重复声明 c/不绑定全局作用域  
const声明的常量值不能被修改。/* 如果声明的是引用类型，其值就有可能被修改，但不同于重新赋值   
  
* ##### 解构赋值  
一种JS表达式  
可以用来赋值 /交换变量 /数组与字符串相互转换 /数组字符串对象的拼接 /设置默认值 /提取乱序传入对象参数 等等。  
  
* ##### 扩展  
###### 字符串扩展：  
模板字符串 ` $ { } `  例如 ` 字符串直接与变量 $ { data } 拼接 `  
填充字符串padStart() padEnd() padLength()  
重复字符串 repeat(重复次数)  
检测是否以str开头/结尾/存在startWith()/endWith()/includes()  
forEach(callback [ , thisArg ]) 遍历arr中的每一项，并对每一项执行callback  
Unicode表示法，形如\u{1f436}，以保证超出四位的字符能够正确解析  
###### 数值扩展  
isNaN() , isFinite() ,isSafeInteger()  
parseINt与parseFloat方法从window对象上转移到了Number对象上  
0o打头八进制，0b打头二进制  
幂运算 /** ，从左往右计算  
###### 数组扩展  
var set=new Set（arr）;会对数组进行去重，得到一个数组项组成的对象，然后可以继续通过[…set]来转换成数组  
…很多新方法，感觉重要的：  
find（function(value , index ,arr),thisValue）返回数组中符合条件的第一个元素，没有的话返回undefined； findIndex()返回索引。  
filter（function(value , index ,arr) ,thisValue）创建一个新数组，新数组中的元素是array中符合条件的所有元素;  
array.map(function(value, index, arr),thisValue)返回一个新数组，新数组元素是原始数组元素调用函数处理之后的值，按原始数组顺序处理  
forEach(function(value, index, arr),thisValue)调用数组每个元素，并将元素传递给回调函数，无法跳出或终止forEach语句，除非抛出异常  
参数解释：  
function是回调函数，回调函数接收三个参数：  
value：数组中正在处理的当前元素  
index：可选，数组中正在处理的当前元素索引  
arr：可选，map方法被调用的数组  
thisValue：执行回调函数时的this值  
reduce(function(返回值，正在处理的值，正在处理的值的索引，调用reduced的数组)，第一次调用回调函数的初始值)；  
###### 对象扩展  
###### •	简洁表达式  
①对象属性名可以省略（直接匹配同名属性）  
②形如name:function(){}可以直接写成name(){};  
###### •	属性名表达式  
可以使用表达式来表示属性名，形如：obj{[${variable}string]：value} 、obj{[“aaa”+”bbb”]:999}  
###### •	扩展运算符合并、浅拷贝对象  
Object.keys(obj)、Object.values(obj)、Object.entries(obj)分别返回obj的key/value/[key:value]组成的数组  
例如： for（let [k,v]  of  Object .entries(obj)）{console .log (k , v)}；  
###### •	super访问和调用对象父对象上的方法和父对象  
###### •	箭头函数。  
箭头函数没有arguments形参，this指向函数运行的环境  
#### promise  
参看：http://www.qiutianaimeili.com/html/page/2019/03/8rfqp1yeul5.html一个题  
promise用于表示一个异步操作的最终状态（成功或失败）及该操作的结果值。  
一个promise有三种状态：pending初始状态，fulfilled，rejected  
new Promise( function(resolve, reject) {...} 这是executor )  
executor是带有resolve、reject两个参数的函数，Promise构造函数执行时立即调用executor函数，resolve和reject两个函数作为参数传递给executor（executor函数在Promise返回实例对象前被调用）。executor内部通常会执行一些异步操作，一旦异步操作执行完毕（也可能失败），就调用resolve或者reject。当resolve和reject函数被调用时，分别将promise的状态改为fulfilled完成状态或rejected失败状态。如果executor内部抛出一个错误，那么该promise状态为reject，executor的返回值将被忽略。  
#### class  
声明创建一个基于原型继承的具有给定名称的类。  
###### •	定义类：  
类声明  class 类名{ }  
类表达式  var 标识符 = class{ }  
类是一种特殊的函数，它不存在变量提升。只能先定义才能被访问；  
###### •	原型方法  
constructor方法是一个特殊的方法，这种方法用于创建和初始化一个由class创建的对象。  
在constructor中可以使用super关键字来调用父类的构造函数  
###### •	静态方法  
static 关键字用来定义一个类的一个静态方法。调用静态方法不需要实例化该类，但不能通过一个类实例调用静态方法。静态方法通常用于为一个应用程序创建工具函数。  
###### •	extends创建子类  
  
## 16. AST抽象语法树    
*   ##### 一般来说，程序中的一段源代码在执行之前会经历以下三个步骤    
###### •	1、分词，词法分析    
这个过程将由字符组成的字符串分解成有意义的代码块，这些代码块被称为词法单元。例如var a = 4 会被分解成 vra 、 a 、 = 、 4 。    
###### •	2、解析，语法分析    
这个过程将词法单元流（数组）转换成一个由元素逐级嵌套所组成的代表了程序语法结构的树，这个数就是 抽象语法树Abstract Syntax Tree。    
###### •	3、代码生成  
将AST转换成可执行代码的过程称为代码生成。简单来说就是将var a=4的AST转化成一组机器指令，用来创建一个叫a的变量，并将值储存在a中。  
/* 例如webpack、eslint等前端工具的核心都是通过抽象语法树的概念来实现对代码的检查分析和转换的。  

*   ##### 抽象语法树  
抽象语法树，或者语法树，抽象出了编程语言的源代码结构。利用抽象语法树可以做代码语法检查、代码混淆压缩、代码转换等等。  
  
## 17. babel编译原理  
*   Babel是一个JavaScript编译器。主要用于将 ECMAScript 2015+ 版本的代码转换为向后兼容的 JavaScript 语法，以便能够运行在当前和旧版本的浏览器或其他环境中。  
*   babylon将ES6/ES7代码解析成AST  
*   babel-traverse 对 AST 进行遍历转译，得到新的 AST  
*   新 AST 通过 babel-generator 转换成 ES5  
  
## 18. 函数柯里化  
*   参看：https://www.jianshu.com/p/2975c25e4d71  
  
*   柯里化是指：把接收多个参数的函数变换成接收单一参数的函数，并返回接收其他参数且返回结果的函数技术。  

*   实例：  
```  
function a(){    
	//定义了一个数组，用来储存参数(第一次执行时的参数)    
  var args=Array.prototype.slice.call(arguments);    
	//声明了一个函数，当函数调用时向args里添加参数，并且返回它函数本身(可以继续调用)    
  var inner=function(){    
    args.push(...arguments);    
    return inner;    
  }    
	//对每一个接收到的参数进行操作(此处是进行了累加操作)    
  inner.toString=function(){    
    return  args.reduce(function(accumulator,item){    
      return  accumulator+item+",";    
    },"五班的同学有：")    
  }    
	//在整个大函数被调用的时候就返回添加参数的函数，使之可以连续调用。    
  return  inner;    
}    
console.log(a("小当")("老当")("益壮") )  
```