# HTML5  
1.  HTML5是最新的HTML标准  
2.  是专门为承载丰富的web内容而设计的，并且无需额外插件  
3.  拥有新的语义、图形及多媒体元素  
4.  它所提供的新元素和新API简化了web应用程序的搭建  
5.  它是跨平台的，被设计为在不同类型的硬件（PC、手机、电视等）之上运行  

* 所有现代浏览器都支持HTML5，所有浏览器不论新旧，都会把未识别元素当做行内元素来处理。HTML5定义了8个新的语义HTML元素，都是块级元素（所以，可以为它们统一设置display：block，以确保新标签在老式浏览器中的正确行为——  
header，section，footer，aside，nav、main，article，figure{display：block；}）  
* 但是在IE8之前的浏览器里面，不允许对未知的元素添加样式。解决办法：“the shiv”，它实际上就是在文档加载之前先教浏览器认识所有的标签元素。  
  
#### 文本格式化标签  
`<b>`粗体文字  
`<small>`小号文字  
`<em>`着重文字  
`<i>`斜体文字   
`<strong>`加重语气   
`<sub>`下标  
`<sup>`上标   
`<ins>`插入文字  
`<del>`删除文字  
  
#### DTD文档类型定义; 作用是定义 XML 文档的合法构建模块。  
    
## 新增元素    
### 结构标签(块级元素)：有意义的div  
<article> <header> <nav> <section> <aside> <hgroup> <footer> <>  
<figure>标记定义一组媒体内容以及他们的标题  
<figcaption>定义figure元素的标题  
<dialog>定义一个对话框  
  
### 多媒体标签  
*多媒体标签的出现意味着富媒体的发展以及支持不使用插件的情况下即可以操作多媒体文件，极大地提高了用户体验。  
<audio>定义一个音频  
几个主要属性：src音频位置、autoplay=“autoplay”自动播放、loop=“-1”无限重播、controls=“controls”显示音频控件；  
可以在标签内添加提示文字，在不支持该标签的浏览器中会显示出提示文字。  
```  
<source>  
    <audio>
        <source></source>
    </audio> 
</source> 
```
用在audio或者video标签里，应对音频格式不兼容问题  
主要属性：src、type=“audio/mpeg”规定类型与转码器  

####   `<video>`  
#### 几个主要属性：  
`src` 音频位置、  
`autoplay=“autoplay”` 自动播放（在chrome浏览器下不会自动播放）、  
`loop=“-1”` 无限重播、  
`controls=“controls”` 显示音频控件、  
`poster=“图片文件地址”` 视频封面、  
`muted` 默认静音播放（在chrome浏览器中，当该属性与autoplay同时存在时autoplay属性就会生效）、  
`width`，`height`同时设置时只会改变播放窗口大小，视频本身还是会居中播放；  
* 这个标签支持的视频格式有：mp4 , webm, ogv
* 各浏览器对该标签以及视频格式的支持效果是不同的。兼容问题可以在标签开始和结束内添加文字提示，在浏览器不兼容时，会显示提示文字，否则正常显示视频。  

#### video API事件  
`play()`控制视频让其播放  
`pause()`让其暂停  
`duration()` 返回视频总长度，以秒的形式返回  
`currentTime()` 返回当前播放时间，也可以设置当前播放时间（通过这个事件可以设置快进功能例如：element.currentTime=element.currentTime+3单位为秒）  
`src()` 返回、设置（element.src=“地址”）当前视频来源  
`volume()` 设置、返回视频音量，设置音量的默认值为0~1 *可以结合input type=“range”来设置音量控件  
`controls()` 设置控件的有无element.controls=true  
`muted` 设置element.muted=true设置静音，但是在video标签属性中不会添加这一属性。*相比较的，controls的设置会使video标签中增加controls属性。  
`networkState` 返回状态码0未初始化1视频已选取好资源，但是未使用网络2浏览器正在下载视频资源3未找到视频资源，在网页刚被打开的时候视频资源也不会立即被找到  
`currentSrc` 返回视频地址，必须是在视频被可以被加载的时候返回，不能被赋值。  
`ended` 返回视频是否已经播放结束了  
`loop` 返回音视频是否循环播放  
`playbackRate` 设置或返回视频播放速度，默认是1
`readyState`  返回视频就绪状态。0没有视频1有数据，但是马上就快要没有了（就是加载了一部分，但是没有加载完，没网了）2当前数据可用，但是已经没有数据来播放下一帧的内容了3数据正在缓冲，当前及至少下一帧是可用的了4视频已经开始播放  
`timeupdate` 视频是否已经开始播放  
`seeked` 视频播放位置发生改变时onseeked（当用户对视频进度进行操作时）  
`seeking` （当用户开始触发进度条时）onseeking触发频率高于seeked  
`volumechanged` 当音量发生改变时,onvolumechanged  
`requestFullscreen` 视频全屏播放。它必须在用户事件中调用  
  mozRequestFullScreen   
  webkitRequestFullscreen   
*moz火狐内核，ms IE内核，webkit webkit内核，常见的有谷歌和苹果浏览器  
load()重新加载视频    
canplay当视频已经加载好可以开始播放了    
    
### 其他标签    
`<canvas>`    
画布，定义图片  
  
`<embed>`  
定义外部的、可交互的内容或插件。  
  
web应用标签 *有兼容问题  
`<meter>`  
状态标签(实时状态显示：气压、气温)  
几个主要属性：  
value，min，max，low，high，optimum  
  
`<progress>`  
状态标签(任务过程：安装、加载)  

`<datalist>`  
列表标签，为input标记定义一个下拉列表，配合option  
```
<input placeholder=“请选择” list=“datalist的id”>  
<datalist id=“listname”>  
      <option></option>  
<option></option>  
… …  
</datalist>  
```  
`<details>`  
列表标签，标记定义一个元素的详细内容（默认收起状态，有一个open属性控制起始状态的收起或展开 open=“open/close”）配合summary（控制该收起项的标题，类似于placeholder的作用）使用  
   
##### 注释标签  
`<ruby>` 标记定义注释或音标  
`<rt>` 定义对ruby的注释内容文本  
`<rp>` 告诉不支持ruby元素的浏览器如何显示注释文本  
`<p>`云南方言我们来<ruby>夼<rp>(</rp><rt>kuang</rt><rp>)</rp></ruby>一个话题<p>  
  
`<mark>`  定义有标记的文本(黄色选中状态)  
  
`<output>`  定义一些输出类型，计算表单结果配合oninput事件  
  
##### 删除了一些纯表现类的，影响结构的，容易产生混淆的标签  
  
##### 重定义标签  
显示不变，只是表达的含义进行了重新定义  
`<b>` 内联元素，粗体，没有表示重要的意思  
`<i>` 内联元素，斜体，没有表示重要  
`<dd>` 可以与detail以及figure使用，定义包含文本。dialog也可以  
`dt>` 汇总细节，可与detail、figure、dialog一起使用  
`<hr>` 表示主题结束，不只是水平线  
`<menu>` 重新定义为用户界面的菜单，配合command或者menuitem使用  
`<small>` 表示小字体，例如打印注释或者法律条款  
`<strong>` 表示重要但不强调。（也就是不加粗）  
  
##### 新标签的意义：
①语义化，提升了网页的质量和语义，减少了class和id属性的调用  
②对搜索引擎的友好  
  
##### 注意：li标签里的内容是最不利于被搜索引擎搜索到的。

### HTML5属性变化  
#### input的新增类型  
##### type值的新增值：
email、url、tel（以上三个属性值在pc端显示效果没有什么特别的，但在移动端会在使得键盘的布局出现相应的变化）  
number（在pc端会出现增加减少的数字加减按钮，以及只能输入数字以及运算符，在移动端同时也会使得输入键盘产生相应布局变化） 

data pichers input类型，主要显示效果的区别在移动端；  
也是type值的新增值：date设置年月日、month设置月年、week设置该年的第几周和年、time设置小时和分钟、datetimeUTC时间基本不用、datetime-local设置本地时间以及日月年。  

range、search、color主要显示效果在PC端  
`<input type=“range” min=“” max=“”>` 显示滑块  
search显示搜索框，输入完成之后带有清空“×”按钮  
color显示色块，能够调用色盘  

#### 新增属性  
#####autocomplete属性，  
可以用在form标签以及以下类型的input标签：  
text，search，url，telephone，email，password，datepickers,range,color  
在填写过一次之后，有自动完成的功能，它有两个可选值on/off。  
*注意：需要在标签后添加name属性，否则无效  
autofocus   
规定在页面加载时，域自动获得焦点。值为autofocus适用于所有input标签的类型  
  
##### multiple  
规定输入域中可选择多个值。  
适用于以下类型的input标签：email和file  
  
##### placeholder  
提供一种提示，提示期望的输入值。  
适用的type类型有：text、search、url、tel、email、password  
  
##### required  
规定必须在提交前填写输入域（不能为空）值为required  
适用的type类型有：text、search、url、tel、email、password、date pichers、number、chechbox、radio、file  
  
#### HTML框架  
通过使用框架，可以在同一个浏览器中显示不止一个页面  
http://www.w3school.com.cn/html/html_frames.asp  
  
<base>元素  
放在head标签内，为页面上所有连接规定默认地址或默认目标(target)  
```
<head>  
<base href=“http://xxxxx.com/”/>  
<base target= “_blank”/>  
</head>  
```
