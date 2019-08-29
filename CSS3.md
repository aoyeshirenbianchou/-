# CSS3  
### 选择器
*{} 通配符选择器  
  
##### 子元素选择器：区别于后代选择器，只能选择直接后代  
父元素>子元素  
  
##### 相邻元素选择器：紧接在另一个元素后的元素，并且它们之间拥有同一个父元素  
元素+兄弟元素  
    
##### 通用兄弟选择器：选择某元素后面的所有兄弟元素，它们之间必须具有同一个父元素  
元素~所有后面的兄弟元素    
  
##### 群组选择器：元素，元素，元素 … …  
  
##### 属性选择器  
element[attribute]  
选择具有某种属性元素  
  
element[attribute=“value”]  
选择具有某种属性值的元素  

element[attribute~=“value”]  
选择含有某种属性值的元素  
  
element[attribute^=“value”]  
选择属性值中以value开头的元素例如（元素属性值为a12,a23,a34,a45的）  
  
element[attribute$=“value”]  
选择属性值中以value结尾的元素  
  
element[attribute*=“value”]  
选择属性值中包含value的元素  
  
element[attribute|=“value”]  
选择属性值为value(注意不是包含value嗷)或以value-开头的元素  
  
##### 伪类选择器  
##### 动态伪类  
锚定伪类 :link  :visited  
用户行为伪类 :hover  :active  :focus  
UI元素状态伪类  
:enabled  :disabled  :checked  
  
##### CSS3结构类(nth选择器)  
element:first-child   element:last-child    
:nth-child(n)  :nth-last-child(n)   
:only-child  
*注意：需要满足lement是它的父元素的第一个子元素，就选中。  
也就是说它应该满足①是第一个子元素②这个元素刚好是element  
*以上选择器都是同样原理  
*:nth-child(n)，n其实是一个简单表达式，取值从0开始计算，且在表达式中只能是“n”不能用其他字母代替。列如：它可以是:nth-child  (n+4)这个的意思就是从第四个开始选取。  
*:nth-child(odd)，:nth-child(even)  
  
:nth-of-type(n)    
:nth-first-of-type()  :nth-last-of-type()    
:first-of-type  :last-of-type  
:only-of-type  
*注意区别上面的“child”系列  
  
:empty选择没有子元素以及内容的元素  
  
##### 否定选择器  
:not(element/selector) 匹配非指定元素/选择器的每个元素  
  
##### 伪元素  
伪元素用于向某些选择器设置特殊效果  
语法格式  元素：：伪元素  
①element::first-line   
根据“first-line”伪元素中的样式对element元素的第一行文本进行格式化  
“first-line”伪元素只能用于块级元素  
②element::first-letter  
③element::before  
*::before伪元素总是第一个子元素；它是行级元素；内容通过content写入；可以进行CSS的各种操作。  
④element::after在元素内容后面插入新内容  
*常与content配合使用，多用于清除浮动。  
⑤element::selection 用于设置在浏览器中选中文本后的背景色和前景色  
  
### CSS权重  
行内样式(1000)>ID选择器(100)>类  
属性选择器和伪类选择器(10)>元素和伪元素(1)>*(0)  
CSS权重规则：  
包含更高权重选择器的一条规则拥有更高的权重；  
ID选择器的权重比属性选择器高，例如#IDvalue > [id=“IDvalue”]；  
带有上下文关系的选择器比单纯的元素选择器权重要高；  
  
#### 圆角  
border-radius它是一个复合属性，可以直接单独定义每一个角，如border-top-left-radius；单位可以是em/px/%等  
*启示：当div的长宽不一样时，border-radius值为50%就能做出椭圆形  
  
#### 盒阴影  
box-shadow设置一个或多个下拉阴影  
语法：box-shadow：h-shadow v-shadow blur spread color inset  
h-shadow和v-shadow的值都是偏移值，可以是负值（也就是往左/上边移动）；  
blur模糊值，spread是扩展值，inset就是把阴影加在div内部  
  
#### 边界图片  
border-image是一个复合属性  
语法：border-image：source slice width outset repeat  
slice：image切割，从边框向内切割多少。默认单位是px  
  
#### 背景图像  
①background-clip 指定背景图像绘制区域  
可选值：border-box、padding-box、content-box  
②background-origin 指定background-position的起始位置  
可选值：border-box、padding-box、content-box  
*注意区别clip与origin，一个是背景的裁剪绘制，一个是背景图片的起始位置  
③background-size 指定背景图像的大小，  
可选值：一对像素值、一对百分比值、（只有一个值时，第二个值默认为auto），cover（一边100%，另一边裁剪）、contain（保证整个图片的显示）  
④多个背景图片。  
允许添加多个背景图片，图片url地址靠前的在最前面层显示。  
⑤背景属性整合  
background：color position size repeat origin clip attachment(滚动) image  
  
#### 渐变  
##### 线性渐变  
语法：background：linear-gradient(direction,color1,color2,…)  
*默认从上到下，从左到右存在比较多的浏览器兼容的问题，需要对不同浏览器做不同的写法。标准写法如下：  
水平方向：  
background：linear-gradient(to enddirection,color1,color2,…)  
对角线方向：  
background：linear-gradient(to direction1 direction2,color1,color2,…)  
使用角度：  
background：linear-gradient(angel,color1,color2,…)  
*兼容性较好  
*angle指水平线和渐变线之间的角度(0~180deg)，顺时针方向开始计算为正。  
*控制渐变节点background：linear-gradient(angel,color1 0%,color2 30%,…，colorN 100%)；指的是控制从总长度的哪里开始渐变,以及到哪里结束。  
透明渐变：background：linear-gradient(angel,rgba()1,rgba()2,…)  
*使用不同的a值来控制渐变  
重复渐变  
background：repeating-linear-gradient(angel,color1 n%,color2 n%,…)  
  
##### 径向渐变  
background：radial-gradient(center,shape size,color1,color2,…)  
默认第一个参数为center，可以省略不写。  
*在径向渐变中的节点控制中的百分比指的是从渐变中心到边角距离的百分比  
设置形状、设置尺寸：（他们是一个参数）  
形状的可选值：circle/ellipse  
*如果元素宽高相同，不论形状参数的设置，都只会是圆形。  
尺寸可选值：closest-side/farthest-side/closest-coner/farthest-coner;  
设置中心点位置：一组值对  
重复渐变  
background：repeating-radial-gradient(center, color1,color2,…)  
  
老版本IE浏览器的渐变 … …   
  
#### 文本效果  
*本节存在较大兼容性问题。要注意  
文本阴影  
text-shadow：h-shadow v-shadow blur color  
text-outline：thickness blur color；  
  规定文本轮廓。  
*目前主流浏览器都不兼容。  
换行  
word-break:normal/break-all/keep-all  
规定自动换行。break-all切断单词换行，keep-all在半角符号处换行  
word-wrap:normal/break-word  
  规定长文本、url地址等会被浏览器认为是“长单词”的文本  
  
### 一些新属性  
#### text-align-last：auto/left/right/center/justify/start/end/initial/inherit  
规定如何对齐文本的最后一行。  
*兼容性：只有IE支持，其他要加前缀  
*该属性只有在text-align属性设置为justify时才生效  
text-overflow：clip/ellipsis/string  
  规定文本溢出包含元素时发生的事情  
  *(经尝试发现是要跟overflow:hidden;whitespace:nowrap;配合使用才行)  
  *elip修建掉；ellipsis修剪并加省略号(保留完整的字符)；  
*string，自定义省略号（该值只在火狐浏览器中生效）  
  
#### 字体效果  
@font-face{  
font-family：字体名称；  
src：source format；  
font-weight：（一般就是定义它是否加粗）  
style：（一般就是定义它是否倾斜）  
}  
  *字体格式。  
   TureType(.ttf)：是Windows和Mac的最常见字体，是一种写入式的字体(RAW)，因此它不支持网页优化。  
   OpenType(.otf)：内置在TrueType基础之上  
   web open font format(.woff)：是前两种格式的压缩版本，web字体中的最佳格式，支持元数据包的分离。但是在iOS移动端是不支持的。  
   Embedded open type(.eot)：IE专用  
   SVG(.svg)：基于SVG字体渲染的一种格式。IE、火狐都不支持。  
  
#### 兼容模板： 
```
@font-face{  
font-family:“myFont”；  
src：url(“”);  
sc：url(“”) format(“embedded-opentype”)，  
    url(“”) format(“woff”)，  
url(“”) format(“truetype”)，  
url(“”) format(“svg”)，  
}  
element{font-family:“myFont”；}
```
### transform 变换
`transform:rotate(angle)`  
旋转，数值单位deg，正值顺时针旋转，负值逆时针。  
rotateX()3D旋转绕X轴旋转  rotateY()绕Y轴旋转 rotateZ()  
rotate3d(x,y,z,angle)参数不允许省略。  
  
`transform:translate` 平移   
translateX  translateY  translateZ    
translate(X,Y)*省略第二个参数时默认为0  
translate3d(x,y,z)  
  
`transform:scale`   
缩放，缩放中心在水平以及竖直位置的中间，数值不需要单位。  
    scaleX  scaleY  scaleZ  
scale(X,Y)*第二个参数省略时为等比例缩放，数值不能为分数  
scale3d(x,y,z)*值不能省略  
  
`transform:skew`   
斜切扭曲 *正负值的倾斜方向有所不同  
    skewX  skewY  skew(X,Y)*只有一个值的时候默认第二个参数为0  
  
`transform-origin`  
设置transform转换基准点  
    transform-origin:x,y,z;  可以这样写transform-origin：left top;  
`transform-style`   
默认值为flat，需要显示3d效果时值需要设置为preserve-3d  
  
perspective指定目光与z=0平面的距离，使具有3d位置变换的元素产生透视效果，默认值为none，需要透视效果时则添加数值（需要单位）  
  
`perspective-origin`  
指定视点的位置。  
    语法perspective-origin:x y;  
默认值：perspective-origin：50% 50%；  
  
`backface-visibility`  
不可见部分是否显示为可见  
  
### transition 过渡  
transition允许CSS的属性值在一定的时间区间内平滑地过渡。这种效果可以在鼠标单击、获得焦点、被点击或对元素任何改变中触发，并圆滑地以动画效果改变CSS的属性值。  
transition：property duration timing-function delay；  
  
#### animation 动画  
* 所有移动端都不支持。chrome和Safari都需要加前缀-webkit-  

①animation-name 需要绑定到选择器的keyframe名称  

②animation-duration 规定完成动画的时间  

③animation-timing-function 速度曲线  

ease、linear、ease-in、ease-out、ease-in-out、step-start、step-end、steps(<integer>[, [ start | end ] ]?)、cubic-bezier(<number>, <number>, <number>, <number>) 
④animation-delay 开始前的延迟，  
允许负值，负值使动画马上开始，但跳过相应时间开始  

⑤animation-iteration-count 播放的次数  
取值为数值或infinite  
    
⑥animation-direction是否应该反向播放  
取值：normal、reverse、alternate、alternate-reverse、initial、inherit  
    
⑦animation-fill-mode规定动画在播放之前或播放之后，其动画效果是否可见  
取值：none、forwards、backward、both  
forwards：当动画完成后，保持最后一个属性值(留在最后一个关键帧)  
backwards：在动画显示之前，应用第一个关键帧属性值  
    
both：向前和向后填充模式都被应用  
⑧animation-play-state 规定动画运行或是暂停  
取值：paused、running  
  
animation复合属性  
animation：①②③④⑤⑥⑦⑧（①②必需，所以会优先判断）  
  
keyframes 规定动画的关键帧  
    @keyframes 动画名称{  
       动画持续时间的百分比{css样式}  
    }  
例如：
```
@keyframes name{  
0%{aaa:ddd;}  
20%{aaa:ddd;}  
… …  
100%{aaa:ddd;}  
}  
```
from相当于0%，to就是100%  

will-change 提前通知浏览器将要对什么元素进行什么样的动画操作  
取值：auto(跟普通情况一样)、scroll-position(将要改变的元素的滚动位置)、contents(将要改变的元素内容)、(直接指明将要改变的属性或者给定的名称)、(一些直接特征，例如top、margin等)  
*在will-change使用之后需要释放，可以通过改变它的属性值(auto)来实现。  
  
### columns 多列布局  
##### columns复合属性  
语法：columns：width || count;   
*可以只有一个参数，列数优先。  
  
##### column-width 每列宽度，用长度值来定义，不允许负值；  
取值：长度值、auto(根据列数自动分配)  
##### column-count 列数  
取值：列数、auto(根据列宽自动分配)；不允许负值  
*在容器宽度足够的情况下，count是优先于width的
  
##### column-gap 设置或检索列与列之间的空隙  
取值:长度值、normal(默认值，与字体大小一致)  
  
##### column-rule 复合属性  
语法：column-rule:边框宽度 样式 颜色；  
*当边框宽度大于列与列之间的间隙时，边框会被列遮盖  
column-rule-width 取值：长度值、thin、medium(默认值)、thik  
##### column-rule-style 取值：none、hidden、dotted、dashed、solid、double(双线轮廓)、groove(凹槽)、ridge(凸槽)、inset(凹边)、outset(3D凸边)  
##### column-rule-color：颜色值。  
    
##### column-span 是否横跨所有列    
取值：none/all（默认为none） *用于子元素    
    
##### column-fill检索或设置所有列的高度    
取值：auto、balance(以最高列为标准)；    
*目前所有浏览器都不支持    
    
##### column-break-before 之前是否断行另起新列    
取值：auto、always、avoid    
column-break-after 之后是否断行另起新列    
column-break-inside内部是否断行，取值有auto、avoid；    
    
### 用户界面    
##### appearance 设置或检索外观按照本地默认样式  
取值：none、button、button-bevel….有110个  
*所有主流浏览器都不支持；加前缀貌似可以？？  
  
##### outline 复合属性，规定对象外的线条轮廓  
*画在border外，不占布局空间，不影响尺寸  
语法：outline：宽度 样式 颜色  
outline-offset 规定线条轮廓的偏移值；取值：偏移值。  
  
##### nav-index 规定导航顺序  
取值：auto/数值。主流浏览器均不支持  
  
##### cursor鼠标指针的形状，取值很多，可以用自定义图片有代替(直接写图片地址)  
      
##### zoom 规定对象的缩放比列，取值normal、数值、百分比  
  
##### resize 规定对象区域是否允许用户缩放，调节尺寸大小  
取值：none、both、horizontal、vertical  
*对象的最小尺寸值为原定的尺寸  
*需要设置overflow属性，且属性值不能为visible  
  
##### ime-mode 规定是否允许用户激活输入法状态  
  
##### user-select 规定规定是否允许用户选中文本
取值：none、text、all、element  
  
##### pointer-event 规定在何时成为属性事件的target  
取值：auto、none、……(其他都是svg的内容)  
  
### CSS变量  
http://www.ruanyifeng.com/blog/2017/05/css-variables.html  

--name:xxxx 声明变量  
var(--name) 读取变量  
*var()函数可以有第二个参数，var(--name,xxx)，第二个参数不处理内部的逗号或空格，视为一个整体的参数。  
*同一个css变量可以在多个选择器内声明，读取的时候，优先级最高的声明生效  
*变量的声明有它自己的作用域，全局的变量通常放在 :root 根元素中。  
*兼容性处理可以写为  
   
  
##### BEM命名规范  
https://blog.csdn.net/chenmoquan/article/details/17095465  
block__element—modifile  
  
##### 移动端VS PC端  
①浏览器支持  
②  
③布局上可以采用更多的方式  
④性能  
- 网络环境的多变  
- 流量问题，图片配适和压缩问题  
⑤浏览器的性能、版本  
  
##### physical pixel物理像素  
device-independent pixel设备独立像素  
device pixelratio设备像素比  
PPI 像素密度  
物理像素* 设备像素比 = 设备独立像素  
   
***viewport、移动端新的度量单位  
  
### flex  
弹性布局。除此之外还有：block-layout、inline-layout、table-layout、position-layout、flexible-layout、grid-layout  
* flex布局需要有容器与项目。容器默认存在水平的主轴和垂直的交叉轴，主轴的开始位置(与边框的交叉点)叫做main start，结束位置叫main end；交叉轴的称为cross start和cross end  
* 项目默认沿主轴排列，单个项目占据的主轴空间叫mainsize交叉轴空间cross size  
  
#### 容器的属性  
##### flex-direction 规定主轴方向  
取值：row(默认值)、row-reverse、column(垂直从上到下)、column-reverse  

##### flex-wrap规定换行与否  
取值：nowrap(默认值，不换行)、wrap、wrap-reverse(换行，行序列倒序)  
flex-flow 复合属性，复合direction与wrap属性。  
  
##### justify-content 项目在主轴上的对齐方式  
取值：flex-start、flex-end、center、space-between、space-around  
  
##### align-content 容器内多行项目在交叉轴上的排列方式  
取值：flex-start、flex-end、center、stretch(多行填满整个交叉轴)、space-between、space-around  
  
##### align-items 项目在交叉轴上的对齐方式  
取值：flex-start、flex-end、center、baseline、stretch(当项目未设置高度时将占满容器高度)  

#### 项目的属性  
##### order 控制子元素出现在容器中的顺序  
取值：数值，可以为负，数值越小排列越靠前，默认为0  

##### flex-grow 剩余空间(除了内容以外的空间)进行分配  
取值：大于等于零的数  
*如果所有项目的该属性值都一样，则剩下的空间平均分配  
*如果值不一样则是根据值的比值来分配  
          
##### flex-shrink 当空间不足时的空间分配    
取值：数值，不能为负。    
*当值为0时，空间不足该项目部缩小    
*当容器具有flex-wrap属性时(会换行)则不存在空间不足的情况，该属性无效    
            
##### flex-basic 规定项目在分配多余空间之前，项目占主轴空间的大小    
取值：auto(默认值，项目内容占据的空间)、0、数值(基准宽度)    
伸缩项目分配空间=伸缩容器的空间-basic空间-元素设置的width(没有时    
元素内容所占的空间)  
  
#### flex 复合元素  
##### flex：flex-grow  flex-shrink  flex-basic；  
*默认值为0 1 auto  
*后两个值可选。(也就是说当只有一个值时，为第一个属性的值)  

##### *flex：none； = (0 0 auto)    flex：auto； = (1 1 auto)  
  
##### align-self   
允许单个项目与其他项目有不一样的对齐方式，可覆盖align-items的值  
取值：auto(默认，继承于父元素，没有父元素则等同于stretch)、flex-start、flex-end、center、baseline、stretch  
  
### media 响应式布局  
解决移动端屏幕尺寸不同的问题。  

但是：  
响应式布局为了兼容各种设备工作量会更大，代码累赘，需要加载的文件更大；  
他可能只是当前状况下的一种折中解决方案    
##### 响应式布局的写法@media mediatype and (media feature){CSS-code}  
* @media not/only mediatype and (media feature){CSS-code}  
* @media not/only mediatype and (feature1) and (feature2)…{CSS-code}  
* 媒体类型：all、print、screen(用于电脑、平板、智能机)、speech  
* 媒体特征：width、height、min-width、min-height……  
  
#### 单位  
px 绝对单位  
em 相对单位，基准点为字体大小(自身字体、父元素字体、浏览器默认)  
rem 相对单位，可以理解为root em根据根节点html的字体大小来计算  
vw 视窗宽度，1vw相当于视窗宽度的1%  
vh 视窗高度，1vw相当于视窗高度的1%  
vmin  vw和vh中较小的那个  
vmax  vw和vh中较大的那个

