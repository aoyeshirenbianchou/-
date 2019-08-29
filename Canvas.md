# CANVAS  
html5的canvas元素使用JavaScript在网页上绘制图像  

应用场景：动画、h5游戏、图表  
  
## canvas坐标体系  
#### 画布大小  
canvas默认大小：300*150  
通过HTML和JavaScript设置的width、height是画布的大小  
通过CSS设置的是画布缩放后的大小  
坐标系原点在左上角，右下为正方向  
创建canvas元素  
```
<canvas id="myCanvas" width="200" height="100"></canvas>  
```
#### 通过 JavaScript 来绘制  
*canvas元素本身没有绘图能力。所有绘制工作必须在JavaScript 内完成  
JavaScript使用id来获取到canvas元素  
var c=document.getElementById("myCanvas");  
#### 然后创建context对象  
var cxt=c.getContext("2d");  
*getContext("2d") 对象是内建的 HTML5 对象，拥有多种绘制路径、矩形、圆形、字符以及添加图像的方法  
  
#### 路径  
###### moveTo(x,y)   
把路径移动到画布指定点  
###### lineTo(x,y)   
路径目标位置  
###### arc(x，y，r，startangle，endangle，counterclockwise[true逆/false顺])  
使用arc创建圆形时，起始角设置为0，结束角设置为2*Math.PI  
###### arcTo(x1，y1，x2，y2，r)  
在画布上创建介于两个切线之间的弧  
*貌似x1y1和x2y2两点应该要横坐标相同或者纵坐标相同  
###### quadraticCurveTo(cpx，cpy，x，y)  
通过一个控制点来画曲线  
###### bezierCurveTo(cp1x，cp1y，cp2x，cp2y，x，y)  
通过两个控制点来画曲线  
###### clip() 从原画布中剪切任意形状和尺寸(剪切保留的是该方法之前的部分)  
###### beginPath()用来开始一条新的路径(但是画布环境依旧保存)  
###### stroke()绘制出路径  
###### fill()  
*填充路径，默认颜色是黑色。(使用fillStyle属性来填充另一种颜色)  
*如果路径未关闭，该方法会从路径结束点到开始点之间添加一条线  
closePath() 创建从当前点到开始点的路径  
  
#### 矩形  
rect(x，y，width，height) 创建矩形  
fillrect(x，y，width，height) 创建并填充(黑色)矩形  
strokeRect(x，y，width，height) 创建并绘制(黑色)出矩形   
clearRect(x，y，width，height) 清空指定矩形(x,y)内的指定像素(width，height)  
  
#### 文本  
font属性，包含粗细、字号、字体等信息。  
textAlign属性，设置或返回文本内容的当前对齐方式  
*可选值start、end、center、left、right  
*相当于规定设置文本位置的原点  
textBaseline 属性，设置或返回文本基线  
*可选值top、hanging、middle、bottom等  
*基线均是以em框来说的  
  
###### fillText(text，x，y，maxWidth) 绘制出“被填充的”文本  
*x，y为相对画布，开始绘制文本的坐标  
*允许的最大文本宽度  
strokeText(text，x，y，maxWidth) 绘制出无填充的文本  
measureText(text) 返回一个包含指定字体宽度的对象  
获得文本宽度measureText(text).width  
  
#### 线条样式  
lineCap()  
lineJoin()  
lineWidth()  
miterLimit()  
  
#### 颜色样式阴影  
fillstyle 规定用于填充的颜色、渐变或模式  
strokeStyle 规定用于描边的颜色、渐变或模式  
shadowColor  shadowBlur  shadowOffsetX  shadowOffsetY 阴影相关  
createLinearGradient(x0，y0，x1，y1)  
*创建线性渐变，可用于填充矩形圆形线条文本等。  
*使用该对象作为strokeStyle或fillStyle的属性值  
*使用addColorStop()方法规定不同的颜色及渐变位置。  
createRadialGradient(x0，y0，r0，x1，y1，r1)  
*创建放射状渐变(*可以制作灯光效果)  
addColorStop(stop，color)  
*stop是0~1之间的值；多次使用该方法添加多个渐变颜色  
createPattern(image，repeat/repeat-x/repeat-y/no-repeat)  
*在指定方向内重复指定的元素，元素可以是图片、视频或其他canvas元素  
  
#### 转换  
scale(width，height)  
rotate(angle)  
translate(x，y)  
transform()  setTransform()  矩阵相关  
  
drawImage() 向画布上绘制图像、画布、或视频  
drawImage(img，x，y) 定位图像  
drawImage(img，x，y，width，height) 定位图像，规定图像宽高；  
  
drawImage(img，sx，sy，swidth，sheight，x，y，width，height)剪切定位  
*在JS中var img=new Image([width]，[height])； img.src=“”；相当于给浏览器缓存了一张图片；  
  
###### save() 保存当前环境状态  
###### restore() 返回到之前的环境
