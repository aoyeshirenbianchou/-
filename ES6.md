# ES6  
## 1. let & const  
块级声明，在块的作用域外无法访问。  
  
特性：  
* 不会被提升  
* 重复声明会报错  
* 不绑定全局作用域    
  
const用于声明常量，其值被设定之后不能再被修改。（但如果声明的常量是引用类型时，其值就可以被修改，*但是不同于重新赋值。可以使用）  
  
## 2. 解构赋值  
解构赋值语法是一种JavaScript表达式，用来将数组中的值或对象中的属性取出来区分为不同变量。  
  
### a/数组的结构赋值  
匹配规则/扩展运算符/默认值/交换变量/接收多个函数返回值  
  
#### 匹配规则  
```  
const arr=[1,2,3,4];  
let [a,b,c,d]=arr; //abcd分别赋值为1234  
let [ , , ,e]=arr; //e赋值为4  
```  
#### 扩展运算符  
```  
let [ , ...f]=arr;//f赋值为数组[2,3,4]  
let [ , ...f,g]=arr;//这种情况会造成g无法匹配而报错  
let [a,b,c,d,e  ]=arr;//这种情况则造成e赋值为undefined    
  
const arr1=[1,2,3];  
const arr2=["a","b"];  
let arr=[...arr1,...arr2];  
//获得了arr=[1,2,3,"a","b"];  
```  
#### 默认值  
```  
const arr=[1,undefined,undefined,null];  
const [a,b,c=2,d,e,f=3]=arr;  
//a匹配赋值为1  
//b匹配赋值为un  defined  
//c匹配为undefined，赋值为默认值2  
//d匹配赋值为null  
//e匹配不到，赋值为undefined  
//f匹配为undefined,赋值为默认值  
```  
#### 交换变量  
```  
let a=1;  
let b=2;  
[a,b]=[b,a]  
```  
### b/对象的解构赋值  
与数组的解构赋值不同的是，对象是无序的，它不需要各项目的一一对应，但是对象的解构赋值是通过的属性名来赋值的。  
#### 匹配规则  
```  
const studen  t={  
    name:"r",  
	gender:"female",  
	edEX:[  
		{pri:"TQ",dur:"6y",gra:"12"},  
		{pri:"ML",dur:"3y",gra:"15"},  
		{pri:"QJ",dur:"3y",gra:"18"}  
	]  
}  
const {gender}=student;  
//gender被赋值为female  
const {eduEX:[,,{dur:junior}]}=student;  
//jinior赋值  为3y  
//第一个冒号是保持结构一致  
//第二个冒号是匹配dur,匹配结果赋值给junior  
```  
#### 扩展运算  
```  
const obj1={  
	a:"aaa",  
	b:"bbb",  
	c:"ccc"  
},obj2={  
	d:"ddd",  
	e:"eee  "  
};  
const obj={...obj1,...obj2,...{f:"fff"}}  
  
```  
#### 对已经声明的变量进行结构赋值  
```  
let age;  
const obj={  
	name:"xm",  
	age:22  
};  
({age}=obj)  ;  
//对已经声明的变量进行赋值时，  
//{}会被当成一个块级作用域  
//解决的办法是添加括号  
```  
#### 默认值  
与数组相同当匹配不到或是匹配为undefined时则赋值为默认值  
应用场景：  
* 提取对象属性  
* 使用对象传入乱序函数参数   
* 获取多个函数反返回值  
  
### c/字符串的解构赋值  
字符串的每一个字符按照位置作为数组的每一项进行复制  
#### 匹配规则  
```  
const str="my name is r";  
const [a,b,c,...others]=str;  
//a赋值为"m"  
//b赋值为"y"  
//c赋值为" " (空格)  
//others赋值为一个由剩下的字符串组成的数组  
const spl=[...str];  
const [...spl]=str;  
//两个spl均会被赋值为由str字符串组成的数组  
```  
#### 提取属性  
```  
const str="my name is r";  
const {length,split}=str;  
console.log(length);  
//提取到字符串长度  
console.log(split.call(str,""));  
//提取到字符串方法，然后使用call调用  
```  
  
### d/数值与布尔值的解构赋值  
会把数值、布尔值（其实字符串也是）转换成一个临时包装对象，在完成赋值之后销毁，所以才能够进行提取属性等操作。  
  
### e/函数参数的解构赋值  
  
## 3. ES6扩展  

### a/字符串扩展  
#### 模板字符串  
```  
`字符串中直接拼接${data1},  
也可以拼接里面再拼接${`比如${data2}`}`  
```  
#### 部分新方法  
① padStart（ “padLength”[，“padString”]）  
  padEnd（ “padLength”[，“padString”]）  
*padLength：把当前字符串填充到目标长度；padString：用以填充的str  
*填充到字符创开头或填充到结尾  
  
② repeat（count）重复当前str  
  
③ startsWith（“str”）检测是否以str开头  
endsWith（“str”）检测是否以str结尾  
  
④ includes（“str”）检测字符串里面是否存在字符串str  
  
⑤ arr.forEach（callback[,thisArg]）  
遍历arr中的每一项，并对每一项执行回调函数。for-of。  
  
#### Unicode表示法  
在js解析中，\u代表开始解析字符，但是通常只能解析0000-ffff的Unicode，所以会拆分成四位-四位的形式来解析。例如“\u1f436”就会被拆成1f43和6来解析。所以可以写成“\u{1f436}”这样的形式以保证正确的解析；  
  
str.codePointAt（index）获取字符串中对应索引字符的Unicode；  
  
str.at（index）获取字符串中对应索引字符；（存在很大兼容问题）  
  
### b/数值扩展  
##### 新的进制表示法：  
0o打头表示八进制；0b打头表示二进制  
parseINt与parseFloat方法从window对象上转移到了Number对象上  
isNaN()判断是否是非数字、isFinite()判断数字是否有限、isSafeInteger()数字是否处在JS能够精确表达的范围之内* (-253-1)~ (253-1)范围  
  
##### 幂运算 `**`   
幂运算默认计算顺序是从右往左的（例如`2**3*4`是先计算`3**4`然后再`**2`）  
  
### c/数组扩展  
#### 结合扩展运算符来使用。  
`var set=new Set（[arg1，arg2，… argN]）`  
会对参数进行去重，得到一个数组项组成的对象。可以通过[…set]来转换成数组。  
  
#### 新的方法  
##### Array.from(object, mapFunction, thisValue)  
object	必需，要转换为数组的对象。  
mapFunction	可选，数组中每个元素要调用的函数。  
thisValue	可选，映射函数(mapFunction)中的 this 对象。  
*obj必须具有length属性，用于指定数组的长度。如果没有length属性，那么转换后的数组是一个空数组；obj的属性名必须为数值型或字符串型的数字。  
    
##### Array.of(arg1, arg2,… argN)     
返回一个由参数组成的数组  
  
##### array.fill(arg, startIndex, endIndex)   
使用arg参数填充从起始到结束索引的数组项，（用以设置数组初始值，如果数组中本来就有值会被填充值覆盖）  
  
##### array.includes() 检测是否具有某个数组项  
具有keys()/value()/entries()方法，获得索引、数组项、索引和数组项  
  
##### array.find(function(value, index, arr),thisValue)  
返回通过测试的数组的第一个元素的值，没有的话返回undefined  
  
##### array.filter(function(value, index, arr),thisValue)  
创建一个新数组，新数组中的元素是array中符合条件的所有元素;  
  
##### array.map(function(value, index, arr),thisValue)  
返回一个新数组，新数组中的元素为原始数组元素调用函数处理后的值，map()方法按照原始数组元素顺序依次处理元素  
  
##### array.forEach(function(value, index, arr),thisValue)  
用于调用数组每个元素，并将元素传递给回调函数（注意没有办法跳出或终止forEach语句，除非抛出异常）  
  
#### 总结：  

| 方法 | 使用 |  
| --- | --- |  
|find | 主要用来返回数组中符合条件的第一个元素（没有的话，返回undefined） |  
|filter | 主要用来筛选数组中符合条件的所有元素，并且放在一个新数组中，如果没有，返回一个空数组 |  
|map | 主要用来对数组中的元素调用函数进行处理，并且把处理结果放在一个新数组中返回（如果没有返回值，新数组中的每一个元素都为undefined） |  
|forEach | 用于对数组中的每一个元素执行一次回调函数，但它没有返回值（或者说它的返回值为undefined，即便我们在回调函数中写了return语句，返回值依然为undefined） |  
|findIndex | 跟find类似，但返回的是索引（*在查找NaN的时候indexOf就不行，该方法就可以） |  
  
  
### d/对象扩展  
#### 简洁表达式  
* 对象属性名可以省略，会直接匹配同名变量然后赋值为同名属性。  
* 对象方法形如key:function(){};可以直接写为key(){};  
  
#### 属性名表达式  
可以在对象中使用表达式来表达属性名，形如：  
`[${data}andStr]:value`  
`['aa'+'bb']:value`  
  
#### 扩展运算符  
##### Object.is(arg1,arg2)检测arg1是否与arg2相同  
*比如Object.is(NaN,NaN)就会得到返回值true  
  
##### Object.assign(obj1,obj2…,objn) 合并对象，浅拷贝类型    
    
##### Object.keys(obj)、Object.values(obj)、Object.entries(obj)    
分别返回obj的key/value/[key:value]组成的数组    
    
##### _proto_    
`Obj.setProtoTypeOf(obj, protoObj)`    
`Obj.getProtoTypeOf(obj)`    
    
##### super  *只能使用在对象方法的简介表达中    
  
### e/函数扩展  
#### 函数默认值：  
function fun(a,b=99){}  b就获得了默认值99；  
一个例子：function fun({a,b=99}={}){} *参数为需要解构赋值的对象  
  
#### 扩展运算符（剩余参数）  
之前使用arguments来接收所有参数形成一个类数组对象；ES6使用…args来聚合所有参数，形如function fun(a, b, …args){}  
  
#### 箭头函数 =>  
`const add=(a,b)=>{ a+b }`  
add(1,2)接收1,2两个参数，返回1+2。  
箭头函数是没有arguments形参的；  
箭头函数this的指向；  
  
### f/正则扩展  
##### u修饰符：  
Unicode模式（用以正确处理大于\uffff的Unicode字符）  
ES6 新增了使用大括号表示Unicode字符，这种表示法在正则表达式中必须加上 u 修饰符，才能识别当中的大括号，否则会被解读为量词。  
（更多影响参看 https://blog.csdn.net/ww430430/article/details/78403536）  

##### y修饰符：粘连修饰符
y 修饰符的作用与 g 修饰符类似，也是全局匹配，后一次匹配都从上一次匹配成功的下一个位置开始。不同之处在于，g 修饰符只要剩余位置中存在匹配就可，而 y 修饰符确保匹配必须从剩余的第一个位置开始  

* reduce 的使用
数组方法 reduce 用来迭代一个数组，并且把它累积到一个值中。
使用 reduce 方法时，你要传入一个回调函数，这个回调函数的参数是一个累加器，参数的第一项是上一次累加return的结果，第二个餐参数是遍历到的每一个数组项。


## 4. Promise
promise提供一种解决方案，即A调用B，B返回一个承诺给A，然后A就可以在写计划的时候这么写：当B返回结果成功时，A执行S1方案，当B返回结果失败时，A执行S2方案。这样就可以做到更好的风险控制，流程控制。  

promise可能有三个状态：等待（pending）已完成（fulfilled）已拒绝（rejected），一个promise状态只能从等待转到完成或拒绝，不能逆向转换，同时，完成和拒绝状态不能相互转换。    
  
promise新建后立即执行，then方法指定的回调函数将在当前脚本所有同步任务执行完之后执行。    
  
## 5. Class  
在JS语言中，生成实例对象的传统方式就是通过构造函数。在ES6中，提供了class这个概念，作为对象的模板，通过class关键字可以定义类。  
  
### a/定义类  
```  
class Car{  
	constructor(color,brand,speed){  
		this.color=color;  
		this.brand=brand;  
		this.speed=speed;  
	}  
	speedup(){  
		speed+=10;  
	}  
}  
//定义了一个Car类  
//constructor是类默认方法，通过new生成实例对象时自动调用该方法  
//在定义了speedup方法  
//this指向实例化后生成的对象  
//类的所有方法都定义在prototype上  
```  
  
### b/constructor方法  
constructor方法是类的默认方法，通过new 命令生成对象实例时，自动调用该方法，一个类必须有constructor方法，如果没有显示定义，一个空的constructor方法会被默认  添加；constructor方法默认返回实例对象（即this）,完全可以指定返回另外一个对象  
  
### c/静态属性和静态方法  
静态方法：类相当于实例的原型，所有在类中定义的方法都会被实例继承。如果在一个方法前加上“static”关键字，就表示该方法不会被实例继承。而只能直接通过类来调用。  
  
*如果静态方法中存在this，则this指向类而不是实例。  
  
*静态方法可以与非静态方法同名。  
  
静态属性：直接在类中使用  类名.属性  来定义静态属性。  
  
### d/类表达式  
```  
const Person=class P{  
	constructor(){  
	P.a=1;//P只能在类里访问到  
	console.log(P===Person);//打印结果为true  
	}  
}  
new Person();  
```  
```  
const Person=class P{  
	constructor(){...}  
}() //类似于匿名函数自执行    
```    
    
### e/get和set方法    
```  
const obj={  
	a:111,  
	b:222,  
	get valA(){  
		console.log("正在访问a值");  
		return this.a;  
	},  
	set valB(val){  
		console.log("正在访问b值");  
		this.b=val;  
	}  
}  
obj.valB=666;  
//当set规定的属性valB属性值发生改变时，执行set操作  
//此处等价于val赋值为666  
obj.valA;  
//当get规定的属性被访问时，执行get操作  
//getter是不能有任何形式的参数的  
```  
### f/name 属性返回类的名称  
### g/new.target   
### h/super   
##### 作为父类构造函数，在子类中调用  
##### 作为对象调用父类的方法
