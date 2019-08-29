# SVG  
SVG嵌入HTML  
`<embed>`  
使用embed标签将svg文件以媒体形式插入html  
```
<embed src=“”width=“”height=“”type=“image/svg+xml”pluginspage=http://www.adobe.com/svg/viewer/install//>  
```
  
`<object>`  
使用object标签将svg文件以媒体对象形式插入html  
```
<object data=“”width=“”height=“”type=“image/svg+xml”codebase=http://www.adobe.com/svg/viewer/install//>  
```   
  
`<iframe>`  
使用iframe标签，将svg文件以网页文件的形式插入html  
```
<iframe src=“”width=“”height=“”/>
```  
  
*以上方式均是以整体网页嵌套的方式，将svg文件链接到html中。  
  
`<img>` 以图片形式插入。  

`<svg>`  
直接使用svg标签插入，成为html结构的一部分  
```
<svg viewBox=“”xmlns=“http://www.w3.org/2000/svg”>  
```
*貌似还有version=“”、xmlns:xlink=“”这些属性要写  
  
#### viewport   
svg可见区域的大小  
`<svg  width=“” height=“”></svg>`  
*各种单位可用，默认单位是px，单位可不写。  
  
#### viewBox  
视区盒子，viewBox=“x，y，width，height”  
viewbox在svg坐标内的x、y坐标，宽度和高度  
  
#### preserveAspectRatio  
形体比例保持，让viewBox保持一定的宽高  
preserveAspectRatio=[defer]<align><meet/slice>  
*defer是可选参数，仅在image元素应用上生效。  
*align属性值可以是： (xMin  xMid  xMax) (yMin  yMid  yMax)之间可以两两任意组合，  
例如xMinyMin ；(在viewBox中x方向有三条参考线，分别是从上到下xMin  xMid  xMax；y方向从左到右同理。)  
*meet/slice；meet：保持宽高比将viewBox缩放为适合vieport的最大尺寸  
 slice：保持宽高比，缩放为最大尺寸，并将超出viewport的部分剪裁掉  
 none：不保持宽高比，缩放为整个viewport的尺寸  
  
在svg中，坐标系统的原点是左上角，向下为y轴正方向，向右为X轴正方向。  
  
### SVG transform 属性  
例如 
```
<rect x=“”y=“”width=“”height=“”transform=“translate(100)”>
```  
*与csstransform基本变换类型一致，但在svg中转换的中心是坐标原点(相当于画布左上角)，所以会自带偏移，且不支持3D变换。  
  
##### transform=“translate(<x> [y])”  
*y是可选值，默认为0。  
*参数之间可以逗号也可以空格进行分隔。  
*参数中不能包含单位。  
  
##### transform=“rotate(<angle>[<cx><cy>])”  
*可选值代表无单位的旋转中心，默认为坐标原点  
*svg的transform声明的转换中心是不会保留的。  
transform=“rotate(45 100 50)”等同于transform=“translate(-100 -50)rotate(45)translate(-100 -50)”也就是先平移过去旋转再移回来，中心不会保留  
  
##### transform=“scale(<x>[<y>])”  
*y是可选值，如果省略，等于x  
*缩放中心依然是svg原点，所以会导致位置移动  
  
##### transform=“skewX(<angle>)”  
##### transform=“skewY(<angle>)”  
*连续多次斜切跟一次斜切的结果是不一样的。  
  
*在svg2中，svg已被引入到CSS3变换规范中。  
  
### SVG形状  
##### `<rect>`矩形  
```
<rect  x=“”y=“”rx=“”ry=“”width=“”height=“”/>
```
*x、y：在box的位置；rx、ry：圆角半径；width、height矩形长宽  
  
##### `<circle>`圆形  
```
<circle cx=“圆心X”cy=“圆心Y”r=“半径”>  
  
<ellipse>椭圆  
<ellipse cx=“中心”cy=“中心”rx=“x方向半径”ry=“y方向半径”/>
```
  
##### `<line>`线  
```
<line x1=“”y1=“”x2=“”y2=“”/>
```
*x1、y1：起点位置，x2、y2：终点位置  
  
##### `<polyline>`折线   
```
<polyline  points=“x1 y1,x2 y2,x3 y3 … xn yn”/>
```
polyline是一组连接在一起的直线，points点集数列。  
  
##### `<polygon>`多边形  
```
<polyline  points=“x1 y1,x2 y2,x3 y3 … xn yn”/>
```
*与折线不同的是它会自动在最后一个点处回到第一个点，形成闭合的多边形  
  
##### `<path>`路径  
1.path元素的形状是通过属性d定义的，属性d是一个点集数列，以及它的绘制命令，是一个“命令+参数”的序列  
2.每个命令都用一个关键字母表示，大写字母表示绝对定位，小写相对定位  
3.属性d不需要标明单位  
例如：`<path d=“M x y L x y H x y V x y Z”/>`  
4.命令  
M x y ：moveto命令，将画笔移动到(x,y)位置  
L X Y ：lineto命令，从当前点到(x,y)点画一条直线  
H x ：绘制水平线到x位置；  
V Y ：绘制垂直线到Y位置；  
Z / z：闭合路径，不区分大小写；  
C x1 y1 ，x2 y2 ，x y ：三次贝赛尔曲线  
x y 表示曲终点； x1 y1 、x2 y2分别表示起点和终点的控制点  
Q x1 y1 ，x y ：二次贝赛尔曲线  
x y 表示曲终点； x1 y1表示控制点(同时控制起点和终点)  
T x y ：快捷建立连续曲线，根据前一个贝塞尔曲线的控制点对称出一个新的控制点；如果单独使用则会出现直线效果  
A rx ry , x-axis-rotation , large-arc-flag , sweep-flag , x y ：弧形  
rx、ry 椭圆的x半径和y半径；  
x-axis-rotation 椭圆的旋转角度，默认deg单位，正方向为顺时针  
large-arc-flag 两个可选值0、1；0为小弧度，1为大弧度  
sweep-flag 两个可选值0、1；0为起点逆时针到终点，1为顺时针；  
  
### SVG文本  
EM框概念  
 
##### 字体属性：  
font-family、font-style、font-weight、font-variant、font-stretch、font-size、font-size-adjust、kerning、letter-spacing、word-spacing、text-decoration  
##### 文本位置：  
`<text x=“” y=“”> </text>`；  
*位置原点baseline上x为0的位置算起  
<text x=“x1x2 x3 …” y=“y1 y2 y3 …”> </text>  
*为每一个字符设置位置，没有单独设置的默认跟随前一个字符。  
##### 文本的偏移：  
`<text x=“”y=“”dx=“”dy=“”> </text>`；  
`<text x=“”y=“”dx=“x1 x2 x3 …”dy=“y1 y2 y3 …”> </text>`；  
##### 文本的旋转：rotate=“”属性，不写单位，每一个字符的旋转。  
##### 文本的长度：textLength=“”属性，字符以及间距所占的长度，不写单位  
##### 文字的宽度：lengthAdjust=“”属性，值为spacing/Glyphs，默认spacing，当文本具有长度时，控制拉伸的是字符还是间隙，值为Glyphs时，拉伸字符。  
  
`<tspan>`  
用来标记大段文本的子部分，它必须是text元素或其他tspan元素的子元素  
  
`<textPath>`  
使用xlink:href属性把字符对齐到路径。  
例如： 
```
<path id=“”d=“M 10 10，Q 100 100，80 290”>  
<text>  
<textPath xlink:href=“#pathID”>  
```
文字内容  
< textPath />  
<text/>  
  
### SVG填充和边框  
fill设置对象内部颜色  
stroke设置线条颜色  
stroke-width 描边的宽度  
stroke-linecap 控制边框形状。值为butt/square/round；  
butt：直边结束线段  
square：直边帽子，超出大小由stroke-width决定  
round：边框终点是圆角，圆角半径由stroke-width决定  
stroke-linejoin 控制两条描边线段之间的链接方式，值为miter/bevel/round;  
miter：默认值，连接处形成尖角  
bevel：连接处形成斜接  
round：圆角连接，实现平滑效果  
stroke-dasharray 虚线描边  
`<rect stroke-dasharray=“n1，n2，n3，…”/>`   
一组用逗号分割的数字组成的数列；  
数字交替表示填色段/空白段/填色段/空白段的长度。  
  
*也可以使用CSS，以及外链CSS ：`<?xml-stylesheet type=“text/css”href=“style.css”?>`   
  
### SVG滤镜  
`<clipPath>` 框选/剪切  
```
<defs>  
<clipPath id=“name”>  
<rect x=“” y=“”width=“”height=“”/>  
</clipPath>  
</defs>  
<circle cx=“”cy=“”r=“”clip-path=“url(#name)”/>  
```

`<linearGradient>` 线性渐变  
*在defs内定义，然后在形状元素的属性中使用id调用； 
```
<linearGradient id=“”x1=“”y1=“”x2=“”y2=“”>  
<stop offset=“0%”stop-color=“”/>  
… …  
<stop offset=“100%”stop-color=“”/>  
< /linearGradient >  
```
*x1 y1，x2 y2定义线性渐变起止位置。  
  
`<radialGradient>` 径向渐变  
```
<radialGradient id=“”cx=“”cy=“”r=“”fx=“”fy=“”/>  
<stop offset=“0%”stop-color=“”/>  
… …  
<stop offset=“100%”stop-color=“”/>  
< /radialGradient >  
```
*cx cy 定义fx fy定义 r定义  
  
`<mask>` 遮罩  
  
`<image>` 嵌入光栅图像  
```
<image xlink:href=“URL”x=“”y=“”width=“”height=“”/>  
```
*当x y width height没有设置时，默认为0；  
*width height为0时将不会呈现这个图像  
  
### SVG动画  
*svg动画全部基于SMIL(synchronized multimedia integration language)同步多媒体集成语言；  
*它与CSS3的不同一点是能够沿着运动路径运动  
  
`<set>`   
设置，在特定时间之后修改某个属性值  
```
<set attributeName=“”attributeType=“XML”to=“”begin=“”/>  
```
  
`<animate>`   
实现属性动画过度效果(但是每次只能控制一个属性，所以可以组合多个动画)  
```
<animate attributeName=“”from=“”to=“”begin=“”dur=“”/>  
```
  
`<animateTransform>`  
实现transform变换动画效果  
```
<animateTransform attributeName=“transform”type=“scale/translate …”from=“”to=“”begin=“”dur=“”/>  
```
  
`<animateMotion>`  
让svg图形沿着特定的path路径运动  
```
<animateMotion path=“”dur=“”[rotate=“auto”]使形状跟随路径>  
```
  
#### SVG animation参数  
##### attributeName=“”  
要变化的元素属性名称，可以是元素属性，也可以是CSS属性  
  
##### attributeType=“CSS/XML/auto”  
表示属性值的类型，元素属性就为XML，CSS属性就为CSS，默认auto时优先判断CSS  
  
from=“”动画起始值  
to=“”动画结束值(值是绝对的)  
by=“”相对变化值(值是相对的)  
values=“”用逗号分隔的一个或多个值，表示动画的多个关键帧  
begin，end  
dur=“”持续时间；值为：数值/indefinite  
  
*calcMode、keyTime、keySplines  
*控制动画播放速率曲线。取值discrete、linear、paced、spline  
  
repeatCount=“”执行次数  
repeatDur=“”重复动画的总时长  
fill=“remove/freeze”动画‘封面封底’填充方式  
remove：默认值，动画结束后直接回到开始的状态  
freeze：动画结束后保持动画结束的状态  
accumulate=“sum”  
动画结束时候的位置作为下次动画的起始位置。  
  
##### 动画的播放与暂停(svg动画全部暂停或播放)  
svg.pauseAnimation()  
svg.unpauseAnimation()
