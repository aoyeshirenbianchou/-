# JavaScript
* Javascript是一种基于对象和事件驱动的客户端脚本语言。  
* 完整的JavaScript是由ECMAScritp(语法)和Browser Object(DOM、BOM)(特性)组成的。DOM提供访问和操作网页内容的方式，BOM提供与浏览器交互的接口和方法。
* <script></script>标签，可以嵌入在head中也可以写在body中。也可以在head标签中嵌入外部script：<script src=””></script>。
***
//单行注释  
/**/多行注释  
；作为结束语句  
ECMAScript中的一切（变量、函数名和操作符）都区分大小写  

### 标识符：  
变量、函数、属性的名字，或函数的参数  
标识符的命名规则：  
1、由字母、数字、下划线_或美元符$号组成  
2、不能以数字开头  
3、不能使用关键字、保留字等作为标识符  

### 变量  
ECMAScript的变量是松散类型（可以用来保存任何类型的数据，每个变量仅仅是一个用来保存值的占位符而已）   
#### 声明与赋值   
变量的声明要使用var操作符    
语法：var空格 变量名 

var name_01=”XXX”或者 var name_01; name=”XXX”  
一次可以声明多个变量以及赋值，之间用逗号隔开：  
var name _01=”XXX”,age=18,sex=”man”,address;  
*还没有赋值的变量就不用赋值    
*省略var声明的变量是全局变量    
*当我们需要存储一个值的时候就需要使用变量    

### 数据类型  
在ECMAScript中有5种简单数据类型也称基本数据类型：undefined、null、Boolean、number、string，（ECMAScript6新增了symbol数据类型）以及1种复杂数据类型：object。  
  
** undefined **：声明了一个变量，但是没有赋值，这个变量类型就是undefined  
*一般情况下变量不会特别赋值为undefined，但是如果出现诸如name=undefined的情况，它的变量类型也还是会自动识别为undefined  
  
** null **：声明一个变量，但是暂时还不知道要给它赋的值，是一个空对象指针。用null来初始化这个变量的值。例如：name=null或者name=””  
*如果定义变量准备在将来用于保存对象，那么最好将它初试化为null而不是其他值。  
*undefined值是派生自null值的，所以undefined==null的返回结果是true。也就是说undefined和null的值是相等的。  
  
**number **：表示整数和浮点数  
*在number中有一个特殊的类型NaN即Not a Number是一个特殊的数值。表示本来应该反馈一个数值，但是没办法反馈程一个数值，所以反馈NaN。但是它的数据类型仍然是number。
*因此，任何涉及NaN的操作，反馈结果都是NaN  
*NaN与任何值都不相等，包括NaN本身，但NaN的数据类型是number  
  
** String **：表示由零或多个16位Unicode字符组成的字序列，即字符串。字符串可以由双引号或单引号表示。  
*字符串需要用引号包裹。  
    
##### Typeof：检测变量类型  
语法：typeof 空格 变量 或 typeof(变量)  
返回值：字符串类型，可能的值有：undefined、Boolean、number、string、object、function  
例如：console.log(typeof  name_01)，或者console.log(typeof(name_01))，则在控制台中打印出变量name_01的类型。  
  
##### console.log：在控制台中打印  
语法：console.log(XXX)  
返回值：在控制台中打印  
  
##### IsNaN:检测变量是不是一个“非数值”  
语法：isNaN(n)  
反馈值：Boolean（Boolean只有两个值：true和false）  
*isNaN()对接收的数值会先尝试转换为数值，再检验是否为非数值。  
*null和undefined并不是NaN。
  
### 数值转换  
Number()将非数值强制转换成数值  
*可以用于任何数据类型  
  
##### parseInt()解析一个字符串并返回一个整数。  
忽略字符串前面的空格，直至找到第一个非空格字符；也就是将以数字开头的字符串中的数字提取出来。  
例如：var  leftvalue=“18px”; someone=“abc18”    
paseInt(leftvalue)反馈18       paseInt(someone)反馈NaN  
*parseInt()转换空字符返回NaN  
*语法parseInt(string,radix)  
string:必需，要被解析的字符串  
radix:可选，表示要解析的数字的基数。值介于2~36之间。省略该参数或值为0，则以10为基础来解析。  
*如果小于2或大于36，则返回NaN.  
*如果字符串以“0x”或“0X”开头，将以16为基数进行解析。  
例如parseInt(“0xf”)返回的值不会是0，而是十六进制下的数字f转换返回相等的十进制下的数字，或者parseInt(15,16)的结果，也是15。  
  
##### ParseFloat():解析一个字符串并返回一个浮点数。应该是以数字开头，直到数字末端。  
*只返回第一个数字  
*开头和结尾的空格是被允许的  
*如果字符串的一个字符不能被转换成数字则返回NaN  
*如果字符串中包含有效的十六进制格式，parseInt(0xf)，则返回十进制下同等的数字，而parseFloat(0xf)则只会返回0
  
##### String()与toString()   
语法：对象.toString()或String()  
例如：  
var a=1234  
b=a.toString  
typeof(String(a))   //返回string  
typeof(b)    //返回string  
  
##### Boolean  
语法：Boolean()  
*除0与NaN之外的所有数字转换为布尔型都为true  
*除空之外的所有字符转换为布尔型都为true  
*null和undefined转换为布尔型为false  
  
##### 表达式：将同类型的数据（如常亮、变量、函数等），用运算符号按一定的规则连接起来的、有意义的式子称为表达式。  
  
alert(“”)弹出警示对话款  
  
prompt(“”)输入框  
例如：var age=prompt(“请输入您的年龄”)；
用户输入的值为age的值，引号里的字符串为需要显示的提示语  
  
string.length获取string字符串的长度，返回值是数字。  
  
new Date().getDay()获取星期，返回值：number(0~6)  
  
document.write(“给输入框添加的提示文字”)  
*不论用户输入了什么，type均为string  
  
### 操作符  
操作符的分类：算数操作符、逻辑操作符、赋值操作符、比较操作符、三元操作符  
  
算数操作符  
+、-、*、/、%、++a、a++、- -a、a- -  
递增：++a与a++       
++a先自身加1，然后再参与运算  
a++先参与运算，然后自身再加1  
即：var A=10,B=10,C=++A-B++;  
console.log(A);    //11  
console.log(B);    //11  
console.log(C);    //11-10=1  
*“+”运算，如果是相加的是两个数字，则运行加法运算，如果相加的不是两个数字，比如5+“5”，就是数字加字符串5，则运行拼接运算，结果为55.  
  
##### 赋值操作符  
=  
a=5  
a=a+5  
等同于a+=5  
  
##### 比较操作符  
\>、<、>=、<=、==、===、!=、!==  
`==`：相等，只比较值是否相等  
`===`：全等，比较值也比较数据类型  
`!=`：不相等，比较值是否不相等  
`!==`：不全等，比较值与数据类型是否不全等  
返回值：boolean  
  
##### 三元操作符  
语法：条件？执行代码1：执行代码2  
*可替代简单的if语句，如果天健成立，执行代码1，否则执行代码2     
例如：  
var   
score=85;  
result=(score>=60)？“及格”：“不及格”；  
  
##### 逻辑操作符  
&&：与，只要有一个条件不成立，返回false  
1、可以操作任意类型数据，不一定是布尔型。  
2、如果第一个操作数经过隐式类型转换后为true，则返回最后一个操作。  
3、如果第一个操作数经过隐式类型转换后为false，则返回第一个操作。  
4、如果有一个操作数是null，则返回null。  
5、如果有一个操作数是NaN,则返回NaN.  
6、如果有一个操作数是undefined，则返回undefined。  
  
||：或，只要有一个条件成立就返回true（完全是boolean的时候）  
1、从第一个条件开始往下验证，直到第一个条件成立就返回第一个操作  
2、在所有条件都不成立的情况下，返回最后一个null或NaN或undefined。  
  
！：非，boolean结果，条件成立则返回为false，条件不成立则返回true  
！！：非非：对非求反

#### JS条件语句：分支语句、循环语句  
##### 分支语句：  
if(条件){操作1；操作2；}  
else if{操作3；操作4；}  
else if{操作5；操作4；}  
……  
else{操作6；操作7；}  
  
##### switch语句：  
switch(要判断的东西)  
{  
case 情况1：操作或表达;  
break；  
case 情况2：操作或表达;  
break；  
……  
default:statement  
}  
*如果不添加break语句，则自条件成立开始，操作会一直被执行，直到遇到break或一直执行到结束。  
eg:switch语句在浏览器输出星期  
```
var week=new Date().getDate(),  
weekstr=“”；  
switch(week)  
{  
case 0:  
weekstr=“日”;  
break；  
case 1：  
weekstr=“一”;  
break；  
case 2:  
weekstr=“二”;  
break；  
case 3：  
weekstr=“三”;  
break；  
case 4:  
weekstr=“四”;  
break；  
case 5：  
weekstr=“五”;  
break；  
default:  
weekstr=“六”；  
}  
document.write(“今天是星期”+weekstr)  
```

##### 循环语句：for、for-in、while、do…while  
for语句  
语法：for(语句1；语句2；语句3)  
{被执行的代码块}  
语句1：在循环(代码块)开始前执行  
语句2：定义运行循环(代码块)的条件  
语句3：在循环(代码块)已被执行之后执行  
eg:  
for(var i=1;i<=100;i++)  
{document.write(i+“<br/>”)}  
语句1，i=1  →  语句2，1<=100  →  执行{}的内容，输出1  →  执行语句3，i++得到2  →  i=2  …  
  
##### for循环嵌套  
*外层为假时内层不执行  
*先执行外层再执行内层，直至内层条件为假时再返回外层去执行  
  
##### while循环  
语法while(条件){执行操作}  
*并不只是当条件成立就执行，更是条件成立就循环执行，直到条件不成立。所以一定要注意不要写成死循环  
  
##### do while循环  
do{需要执行的操作}while(条件)  
*先执行操作再判断条件， 这种语法的循环操作至少会被执行一次  
  
##### break结束循环，此后的操作都不再执行  
continue结束本次循环，本次循环后面的操作不再执行，开始下一次循环  
  
#### 函数  
* 通过函数可以封装任意多条语句，放在任何地方，在任何时间调用执行  
* 函数使用function声明，后跟一组参数以及函数体  
* 
##### 语法  
function 函数名([参数1，参数2，…参数3]){操作}  
*[]以及[]里的内容为函数的参数，不是必须的，不属于语法  
函数的调用：函数名()，参数一一对应，函数可以反复调用。  
return返回函数值标识符  
  
##### argument  
1、argument对象与数组类似，管理传递进函数的参数。并不是array实例  
2、[]语法访问它的 每一个元素  
3、length属性确定传递参数的个数  
例如  
function fun(){}   这个函数并没有设置参数接收  
fun(5,6,7)   但在函数调用的时候却传入了参数  
*这个时候，这些参数就是被argument对象管理的。通过argument.length可以获取参数个数；通过argument[]可以索引到相应序号参数(索引是从0开始的正整数，argument[0]也就是接收到的第一个参数)  
*在非严格模式下，通过对argument[]赋值，可以修改参数值，但严格模式下不行。  
  
  
### JavaScript中的内置对象  
Array、String、Math、Date  
  
#### 数组Array  
用来存储数据的，可以是任意类型  
##### 创建数组：  
##### 1、使用Array构造函数  
语法new Array()  
*()小括号说明：  
(1)预先知道数组要保存的项目数量，可以在括号中写项目数量  
(2)向Array构造函数中传递数组应包含的项  
a   b   c   
2、使用数组字面量表示法  
由一对包含数组项的方括号[]表示，多个数组项之间以逗号隔开  
  
array.length获取数组array长度  
*通过设置length可以从数组的末尾移除项或者向数组中添加新的项  
*数组的长度总是比索引多一  
  
##### 数组的方法：  
##### push  
语法array.push(新元素1，新元素2，…)  
功能：把新的元素顺序添加到array数组的尾部  
返回值：添加元素后的新数组  
##### unshift  
语法：array.unshift(新元素1，新元素2，…)  
功能：把新的参数顺序添加到数组的开头  
返回值：添加后的新数组  
##### pop  
语法：array.pop()  
功能：删除数组的最后一个元素  
返回值：被删除的元素  
##### shift  
语法：array.shift()  
功能：删除数组的第一个元素  
返回值：被删除的元素  
##### join  
语法：array.join(“分隔符”)  
功能：用于把数组中的所有元素放入一个字符串，括号里放入分隔符，作为数组项  
之间的分隔符，默认情况下的分隔符为逗号“，”    *分隔符可以为空或者空格。  
返回值：string  
例如：array(1,2,3,4,5)  
var A=array.join(“-”)  
document.write(A)  
打印出1-2-3-4-5  
##### reverse  
语法：array.reverse()  
功能：用于颠倒数组中元素的顺序。  
返回值：颠倒后的数组  
例如：var str=[“a”,“b”,“c”,“d”];  
var newstr=str.reverse().join(“”)  
console.log(newstr)  
控制台输出dcba  
  
##### sort  
语法：array.sort(sortby)  
功能：对数组的元素进行排序  
返回值：数组  
\*  
1.  即使数组中的每一项都是数值，sort()方法比较的也是字符串  
2.  sort()方法可以接受一个比较函数作为参数  
3.  默认情况下，sort()方法比较的是字符串，排序方式是按每一个数组项的第一个  
字符数字大小或者字母顺序  
数组数字按升序排列array.sort(function(a,b){return a-b})   
数组数字按降序排列array.sort(function(a,b){return b-a })此时排的是数字大小  
  
##### concat  
语法：array.concat(array1,array2,…)  
功能：用于连接两个或多个数组  
返回值：新的数组  
例如：var arr1=[1,2,3,3],  
arr2=[“a”，“b”，“c”],  
arr3;  
arr3=arr1.concat(arr2,[“d”,4,5,6]);  
则，输出arr3为arr1+arr2+[…],即[1,2,3,4, “a”，“b”，“c”, “d”,4,5,6]  
  
##### slice()  
语法：array.slice(start,end)
功能：从已有的数组中返回固定的元素  
参数：start，必需，规定从何处开始选取，如果该参数是负数，则从尾部开始选取。  
end，可选，从哪里结束，是数组片段结束处的数组下标，省略时为开始到结束  
  
##### splice  
删除数组项、插入数组项、替换数组项  
删除  
语法：array.splice(索引序号，个数)  
功能：删除从索引序号开始处的零个或多个元素  
返回值：被删除的元素  
*当个数省略时，删除开始之后的所有项  
插入  
语法：array.splice(索引序号，0，插入项1，插插入项2…)  
功能：从索引序号之后（删除0个项），插入项  
返回值：被删除的元素  
  
##### 替换  
语法：array.splice(索引序号，个数，插入项1，插插入项2…)  
返回值：被删除的元素  
  
indexOf（html5新增的功能）  
语法：array.indexOf(searcvalue，startIndex)  
功能：从起点位置开始向后查找。没有起点位置则默认从数组开头向后查找。  
searcvalue：必需，要查找的项  
startIndex：可选，起点位置的索引  
返回值：number，查找项在数组中第一次出现的位置，没有查到的情况下返回-1  
lastIndexOf  
    功能：从末尾开始查找  
*注意查找值的时候是===  
  
  
#### string对象方法  
##### charAt  
string.charAt(索引)  
功能：返回string中index位置的字符  
charCodeAt  
##### string.charCodeAt(索引)  
功能：返回string中index位置字符的字符编码  
*在ECMAS5中可以使用stringobject[]来获取指定字符，但是在IE7以及更早的版本中是不支持的，所以还是需要用这个方法  
*在索引号大于字符串长度时，返回空，而不是undefined  
##### indexOf  
语法：stringobject.indexOf(“要搜索的字符串)  
功能：从一个字符串中搜索给定子字符，返回子字符串的位置，没有找到返回-1  
##### lastIndexOf  
语法：stringobject。indexOf(“要搜索的字符串)  
功能：从结尾处开始检索  
##### slice  
string.slie(start，end)  
功能：截取字符串  
*start：必需，  
end：可选，end本身不在截取范围之内，省略时截取至字符串末尾  
当参数出现负数时，相当于字符串长度加上这个负数  
##### substring  
语法，功能与slice一样，而不同之处是：  
1、当参数为负数时，自动将参数转换为0.  
2、substring会自动将较小的数字作为起始位置  
##### substr  
语法：stringobject.substr(start，len)  
*start：必需  
len：可选，省略时截取至字符串的末尾  
当start为负数会将字符串长度加上这个负值  
当len为负时，返回空字符串  
##### split  
语法：stringobject.split(separator)  
功能：把一个字符串以分隔符作为标记，分割成字符串数组  
返回值：array  
*如果把空字符串“”当成分隔符，则会把字符串中的每一个字符都分割开  
##### replace  
语法:stringobject.replace(regexp/substr,replacement)  
功能：在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的子串。  
参数：regexp:必需，规定子字符串或要替换的模式的RegExp对象  
replacement：必需，要换的字符串值  
var c="我们是共产主义接班人";  
document.write("<br>"+c.replace("共产主义","社会主义"));  
上述例子只替换第一个；  
var c="我们是共产主义接班人是未来共产主义社会的栋梁";  
document.write("<br>"+c.replace(/共产主义/g,"社会主义"));  
全局标志，全部替换。  
*只替换第一个  
##### toUpperCase()  
##### toLowerCase()  
语法：stringobject.toUpperCase()  
功能：把整个stringobject字符串全部转换为大/小写  
  
#### Math对象  
##### Math.min()  
语法：Math.min(num1,num2…)  
功能：求一组数中的最小值  
返回值：number  
例：min=Math.min(1,2,3,4,5,6)  
    返回min==1  
    *在这一组数中，只要出现一个非数字，就返回NaN  
##### Math.max()  
##### Math.ceil()  
语法：Math.ceil(num)  
功能：向上取整，即返回大于num的最小整数  
##### Math.floor()  
向下取整，返回小于num的最大整数  
##### Math.round()  
将数值四舍五入为最接近的整数  
##### Math.abs()  
返回绝对值  
##### Math.random()  
功能：返回一个大于等于0，小于1的一个随机数  
  
#### Date()日期对象  
##### 语法：new Date()  
*在没有参数的情况下返回当前时间  
   
*星期返回结果是0~6，月份返回的是0~11，Time返回的是从1970年1月1日00:00:00开始到现在时间的毫秒数。  
例如：var today=new Date(),  
year=today.getFullYear();  
  
##### 设置时间的方法  
   
get获取时间，set需要传入参数，设置时间  
例如：
var today=new Date();  
today.setMonth(8)  
onsole.log(today.getMonth())将在控制台中打印出8，也就是9月。  
*setMonth()具有容错的能力，当参数值大于11时，将使用参数对12取余，输出取余结果，同时，年份也会随之改变  
  
计算50天后是星期几  
today.setDate(today.getDate()+50);  
console.log(today.getDay());  
创建一个Date对象，参数按照年、月、日、时、分、秒来设置。  
例如：var year=today.getFullYear(),month=today.getMonth(),day=today.getDate();  
var setT=new Date(year,month+30,day),这样设置30个月之后的日期  


