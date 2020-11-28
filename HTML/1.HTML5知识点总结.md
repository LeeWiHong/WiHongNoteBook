为了更有效的学习知识点，需要对所有学习过的知识点进行总结，才不会遗忘

-------

### 1.html5字符集问题
在大部分的浏览器中直接输出中文会有乱码产生，根本原因是编码问题，因此需要在html的头部加上
`<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>页面标题</title>
</head>
<body>
<h1>我的第一个标题</h1>
<p>我的第一个段落。</p>
</body>
</html>`

-------

### 2.HTML标签
#### 基础标签

`h1>to<h6>`标题

`<h1>h1号标题</h1>`
`<h2>h2号标题</h2>`
`<h3>h3号标题</h3>`
`<h4>h4号标题</h4>`
`<h5>h5号标题</h5>`
`<h6>h6号标题</h6>`
只有六级标题，而且是字体从上往下越来越小

-------

`<p>`段落

`<p>这是一个段落</p>`
`<p>这是另外一个段落</p>`
两个段落实例

-------

`<a>`链接

`<a href="https://www.baidu.com">百度一下你就知道</a>`
通常a标签都是用来做链接用，可以再href中指定链接的地址

-------

`<img>`图像

`<img src="../ImageSource/logo.jpg" width="254" height="92">`
图片的宽度和高度可以不在这里指定，在css中指定也可以

-------

`<title>`标题

`<title>会员登录</title>`
定义一个文档的标题，通常title是放在html文档的首部

-------

`<br>`换行

br标签是一个空标签，因此他并没有结束标签，他只是插入一个简单的换行符

-------

`<hr>`水平线

hr标签主要用来分割html页面中的内容或者定义一个变化，他在页面中显示为一条水平线，他跟br标签一样也是一个空标签，没有结束标签，在h5中已经没有align(对齐)、noshade(呈现纯色)、size(高度)、width(宽度)这些属性，但这些属性在h4中是被定义成可用的

-------

#### 格式
`<abbr>`定义一个缩写

用来表示一个缩写词或者首字母缩略词
`The<abbr title="World Health Organization">WHO</abbr> was founded in 1948.`<br>在页面显示的效果如下
![](https://ws3.sinaimg.cn/large/006tNc79gy1fj1jvgcfvej30r8084ab4.jpg)

-------

`<address>`定义文档作者/所有者的联系信息

`<address>
    Written by <a href="mailto:gzlwhong101@gmail.com">LeeWiHong</a>.<br>
    Visit us at:<br>
    https://www.github.com/kavinkily<br>
    guangzhou<br>
    China
</address>`
如果元素位于body元素内部，则他表示该文档所有者的联系信息；如果元素位于article元素内部，则他表示该文章所有者的联系方式，元素内的文本通常为斜体，不建议使用address来描述邮政地址，除非这些信息是联系信息的组成部分，通常的做法address被包含在footer元素的其他信息中

-------

`<b>`定义粗体文字

`<p>这是一个普通的文本- <b>这是一个加粗文本</b>。</p>`

`<bdo>`定义文本的方向

``<p>该段落文字从左到右显示。</p> ``
`<p><bdo dir="rtl">该段落文字从右到左显示。</bdo></p>`
该标签的属性值为ltr以及rtl这两个值是必须的，规定`<bdo>`元素内的文本方向,ltr是left to right的缩写，rtl是right to left的缩写

-------

`<blockquote>`定义块引用

`<blockquote cite="http://www.worldwildlife.org/who/index.html">
For 50 years, WWF has been protecting the future of nature. The world's leading conservation organization, WWF works in 100 countries and is supported by 1.2 million members in the United States and close to 5 million globally.
</blockquote>`
这里定义一个摘自另外一个源的块引用，浏览器通常会对blockquote元素进行缩进，如果标记是不需要段落分隔的短引用建议是用p，在他的属性中cite的值是必须要有的，他规定了引用的来源。

-------

`<cite>`定义引用

`<cite>`定义作品(比如书籍、歌曲、电影、电视节目、绘画、雕塑等等)的标题，需要注意的是人名不属于作品的标题
`<p><cite>The Scream</cite> by Edward Munch. Painted in 1893.</p>`
效果如下图所示
![](https://ws2.sinaimg.cn/large/006tKfTcgy1fj1livasiqj30mo0j676q.jpg)

-------

`<em>`、`<strong>`、`<dfn>`、`<code>`、`<samp>`、`<kbd>`、`<var>`、`<i>`、`<mark>`、`<s>`、`<sub>`、`<sup>`等短语标签的使用

`<em>强调文本</em>`<br>
`<strong>加粗文本</strong>`<br>
`<dfn>定义项目</dfn>`<br>
`<code>一段电脑代码</code>`<br>
`<samp>计算机样本</samp>`<br>
`<kbd>键盘输入</kbd>`<br>
`<var>变量</var>`<br>
`<i>斜体文本</i>`<br>
`<mark>mark文本高亮</mark>`<br>
`<s>定义删除文本</s>`<br>
`<small>定义small小号文本</small>`<br>
`<p>正常文本<sub>定义下标问题</sub><sup>定义上标文本</sup></p>`<br>
`<u>定义的下划线文本</u>`<br>

效果如图所示
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fj1tz2j8bsj30wy0k4tal.jpg)

-------

`<del>`定义被删除文本、`<ins>`定义插入的文本

`<p>My favorite color is <del>blue</del> <ins>red</ins>!</p>`
效果如图所示
![](https://ws3.sinaimg.cn/large/006tKfTcgy1fj1lua2dw3j30hc08gt91.jpg)

-------

`<meter>`定义度量衡

meter标签仅可用于已知最大和最小值得度量，比如磁盘使用情况，查询结果的相关性等，但他并不能用来做为进度条,如果想使用进度条的话需要使用`<progress>`标签，IE浏览器并不支持meter标签
meter标签使用如下
`<meter value="2" min="0" max="10">2 out of 10</meter><br>
<meter value="0.6">60%</meter>`
效果如下
![](https://ws3.sinaimg.cn/large/006tKfTcgy1fj1qwzur3kj31fc0iy427.jpg)

-------

`<progress>`定义运行中的任务进度

progress就是用来表示进度条的，一般需要通过与JavaScript一起使用来显示任务的进度
![](https://ws3.sinaimg.cn/large/006tKfTcgy1fj1rb4ecw8j31kw0kfadp.jpg)

-------

#### 表单
`<form>`用于创建供用户输入的html表单

![](https://ws1.sinaimg.cn/large/006tKfTcgy1fj1rv6tls8j31kw0m5n2q.jpg)
在form表单中可以包含一个或者多个表单元素，在form表单中的属性值包括如下的

| 属性 | 值 | 描述 |
| --- | --- | --- |
| accept | MIME_type | html5不支持，规定服务器接收到的文件类型，文件是通过文件上传提交的 |
| accept_charset | character_set | 规定服务器可处理的表单数据字符集 |
| action | url | 规定当提交表单时向何处发送表单数据 |
| autocomplete | on/off | 规定是否启用表单的自动完成功能 |
| enctype | application/x-www-form-urlencoded multipart/form-data text/plain | 固定在向服务器发送表单数据之前如何对其进行编码,适用于method=“post”的情况 |
| method | get/post | 规定用于发送表单数据的http方法 |
| name | text | 规定表单的名称 |
| novalidate | novalidate | 如果使用该属性，则提交表单时不进行验证 |
| target | _blank/_self/_parent/_top | 规定在何处打开action url |

-------

`<input>`规定用户可以再其中输入数据的字段

input元素在form元素中使用，用来声明允许用户输入数据的input控件，输入字段可通过多种方式改变，取决于type属性，input属性值包括以下

| 属性 | 值 | 描述 |
| --- | --- | --- |
| accept | audio/video/image/MMIE_type | 规定通过文件上传来提交的文件的类型,只针对type=“file" |
| align | 定义对齐方式left/right/top/middle/bottom | html5已经废弃，不赞成使用，规定图像输入的对齐方式，只针对type=“image" |
| alt | text | 定义图像输入的替代文本,当图片显示不全时显示文本,只针对type=“image" |
| autocomplete | on/off | autocomplete属性规定imput元素输入字段是否应该启用自动完成功能 |
| autofocus | autofocus | 属性规定当页面加载时，input元素应该自动获得焦点 |
| checked | checked | checked属性规定在页面加载时应该被预先选定的input元素，只针对type=“checkbox”或者是type=“radio" |
| disabled | disabled | disabled属性规定应该禁用的input元素 |
| form | form_id | form属性规定input元素所属的一个或多个表单 |
| formaction | url | 属性规定当表单提交时处理输入控件的文件的url,只针对type=“submit”和type=“image" |
| formenctype | application/x-www-form-urlencoded multipart/form-data text/plain | 属性规定当表单数据提交到服务器时如何编码,只适合type=“submit”和type=”image" |
| formmethod | get/post | 定义发送表单数据到action URL的http方法，只适合type=“submit”和type=“image" |
| formnovalidate | formnovalidate | formnovalidate属性覆盖form元素的novalidate属性 |
| height | pixels | 规定input元素的高度,只针对type=“image" |
| list | datalist_id | 属性引用datalist元素，之中包含input元素的预定义选项 |
| max | number/date | 属性规定input元素的最大值 |
| maxlength | number | 属性规定input元素中允许的最大字符数 |
| min | number/date | 属性规定input元素的最小值 |
| multiple | multiple | 属性规定允许用户输入到input元素的多个值 |
| name | text | name属性规定input元素的名称 |
| pattern | regexp | pattern属性规定用于验证input元素的值得正则表达式 |
| placeholder | text | placeholder属性规定可描述input字段的展位文字 |
| readonly | readonly | readonly规定输入字段是只读的 |
| required | required | 属性规定必须在提交表单之前填写的输入字段 |
| size | number | size属性规定以字符数统计的input元素的可见宽度 |
| src | url | src属性规定显示为提交按钮的图形的url只针对type=“image" |
| step | number | step属性规定input元素的合法数字间隔 |
| type | button<br> checkbox<br> color<br> date<br> datetime<br> datetime-local<br> email<br> file<br> hidden<br> image<br> month<br> number<br> password<br> radio<br> range<br> reset<br> search<br> submit<br> tel<br> text<br> time<br> url<br> week | type属性规定要显示的input元素的类型 |
| value | text | 指定input元素value的值 |
| width | pixels | width属性规定input元素的宽度，只针对type=“image" |

-------

`<textarea>`定义多行的文本输入控件

文本区域中可以容纳无限数量的文本，其中的文本默认字体是等宽字体通常是courier，可以通过cols和rows属性来规定textarea的尺寸大小，不过更好的方法是使用css的height和width属性，其属性有如下

| 属性 | 值 | 描述 |
| --- | --- | --- |
| autofocus | autofocus | 规定当页面加载时，文本区域自动获得焦点 |
| cols | number | 规定文本区域内可见的列数 |
| rows | number | 规定文本区域内可见的行数 |
| disabled | disabled | 规定禁用文本区域 |
| form | form_id | 定义文本区域所属的一个或多个表单 |
| maxlength | number | 规定文本区域允许的最大字符数 |
| name | text | 规定文本区域的名称 |
| placeholder | text | 规定一个简短的提示，文本区域内的站位符 |
| readonly | readonly | 规定文本区域为只读 |
| required | required | 规定文本区域是必须的 |
| wrap | hard/soft | 规定当提交表单时，文本区域中的文本该怎么样换行 |

应用效果如下图
![](https://ws2.sinaimg.cn/large/006tKfTcgy1fj1uratjhvj31g20k2wh1.jpg)

-------

`<button>`定义一个按钮

在button内部可以放置内容比如文本和图像，这是该元素和input创建的按钮之间的不同之处，需要始终为button元素规定type属性，不同的浏览器对button元素的type属性使用不同的默认值，button属性值如下表所示

| 属性 | 值 | 描述 |
| --- | --- | --- |
| autofocus | autofocus | 规定当页面加载时按钮应当自动的获得焦点 |
| disabled | disabled | 规定应该禁用该按钮 |
| form | form_id | 规定按钮属于一个或多个表单 |
| formaction | url | 规定当提交表单时向何处发送表单数据，覆盖form元素的action属性，该属性与type=“submit"配合使用 |
| formenctype | application/x-www-form-urlencoded<br>multipart/form-data<br>text/plain | 规定在想服务器发送表单数据之前如何对其进行编码，覆盖form元素的enctype属性，该属性与type=“submit”配合使用 |
| formmethod | get<br>post | 规定用户发送表单数据的http方法，覆盖form元素的method属性该属性与type=“submit”配合使用 |
| formnovalidate | formnovalidate | 如果使用该属性，则提交表单时不进行验证，覆盖form元素的novalidate属性，该属性与type=“submit"配合使用 |
| formtarget | _blank<br>_self<br>_parent<br>_top<br>framename | 规定在何处打开actionurl，覆盖form元素的target属性，该属性与type=“submit”配合使用 |
| name | name | 规定按钮的名称 |
| type | button<br>reset<br>submit | 规定按钮的类型 |
| value | text | 规定按钮的初始值，可由脚本进行修改 |

使用效果图如下
![](https://ws3.sinaimg.cn/large/006tKfTcgy1fj2qzpn8vfj31e20mqq5z.jpg)

-------

`<select>``<option>`、`<optgroup>`用来创建下拉列表与下拉选项

用于创建列表中的可用选项比如城市地址选择等等,optgroup用来定义选项列表中相关选项的组合
属性值如下表所示

| 属性 | 值 | 描述 |
| --- | --- | --- |
| autofucus | autofocus | 规定在页面加载时下拉列表自动获得焦点 |
| disabled | disabled | 当该属性为true时，会禁用下拉列表 |
| form | form_id | 定义select字段所属的一个或多个表单 |
| multiple | multiple | 当该属性为true时可选择多个选项 |
| name | name | 定义下拉列表的名称 |
| required | required | 规定用户在提交表单前必须定义一个下拉列表的选项 |
| size | number | 规定下拉列表中可见选项的数目 |

控件使用效果如下图所示
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fj2rtiw2y4j31800oiq6j.jpg)

使用optgroup的使用效果如下
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fj2x0geqqxj31bg0ts0xh.jpg)

-------

`<label>`用于定义input元素的标注

label不会向用户呈现任何特殊效果，不过如果在label元素内点击文本，就会触发此空间，也就是说当用户选择该标签时，浏览器就会自动将焦点转到和相关标签相关的控件表单上去，label标签的for属性应当与相关元素的id属性相同，用for属性可以把label绑定到另外一个元素，需要把for属性设置的值设置为相关元素的id属性的值
使用效果如下
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fj2x63ftiyj31eu0r20xa.jpg)

-------

`<fieldset>`、`<legend>`定义围绕表单中元素的边框以及边框的标题

fieldset标签可以将表单内的相关元素分组，并会在相关表单元素周围绘制边框，而legend为fieldset的定义标题，其属性值有如下

| 属性 | 值 | 描述 |
| --- | --- | --- |
| disabled | disabled | 规定该组中的相关表单元素应该被禁用 |
| form | form_id | 规定fieldset所属的一个或多个表单 |
| name | text | 规定fieldset的名称 |

使用效果如下图所示
![](https://ws2.sinaimg.cn/large/006tKfTcgy1fj2xdft4pjj31kw0mmq7c.jpg)

-------

`<datalist>`规定了input元素可能的选项列表

datalist被用来为input元素提供自动完成的特性，用户能在一个下拉列表里面的选项是预先定义好的，将做为用户的输入数据，需要使用input的list属性绑定datalist元素
使用效果如下图所示
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fj2xha9024j31kw0o043t.jpg)

-------

#### 框架
`<iframe>`框架

标记一个内联框架，一个内联框架被用来在当前html文档中嵌入另外一个文档，可以使用css为iframe包括滚动条定义样式
属性值如下表所示

| 属性 | 值 | 描述 |
| --- | --- | --- |
| align | left<br>right<br>top<br>middle<br>bottom | h5不支持，规定如何根据周围的元素来对齐iframe |
| frameborder | 1<br>0 | h5不支持,规定是否显示iframe周围的框架 |
| height | pixels | 规定iframe的高度 |
| longdesc | url | h5不支持,规定一个页面该页面包含了有关iframe的较长描述 |
| marginheight | pixels | h5不支持,规定了iframe的顶部和底部的边距 |
| marginwidth | pixels | h5不支持,规定了iframe的左侧和右侧的边距 |
| name | name | 规定iframe的名称 |
| sandbox | ""<br>allow-forms<br>allow-same-orgin<br>allow-scripts<br>allow-top-navigation | 对iframe的内容定义一系列额外的限制 |
| scrolling | yes<br>no<br>auto | h5不支持,规定是否在iframe中显示滚动条 |
| seamless | seamless | 规定iframe看起来像是父文档的一部分 |
| src | url | 规定iframe中显示的文档的url |
| srcdoc | html_code | 规定页面中的html内容显示在iframe中 |
| width | pexels | 规定iframe的宽度 |

使用效果如下图所示
![](https://ws2.sinaimg.cn/large/006tKfTcgy1fj2xx5znpcj31kw0krwhl.jpg)

-------

#### 图像
`<img>`定义图片

定义页面中的图片，有两个必要的属性src和alt，图片并不会插入htm页面中，而是链接到html页面上，img标签的作用是为被引用的图像创建占位符,通过a标签中嵌套img标签给图像添加到另一个文档的连接
属性列表如下

| 属性 | 值 | 描述 |
| --- | --- | --- |
| align | top<br>bottom<br>middle<br>left<br>righ | h5不支持，规定如何根据周围的文本来排列图像|
| alt | text | 规定图像的替代文本 |
| border | pixels | h5不支持，规定图像周围的边框 |
| crossorigin | anonoymous<br>use-credentials | 设置图像的跨域属性 |
| height | pixels | 规定图像的高度 |
| width | pexels | 规定图像的宽度 |
| hspace | pesels | h5不支持，h4已废弃，固定图像左侧和右侧的空白 |
| ismap | ismap | 将图像规定为服务器端图像映射 |
| longdesc | url | h5不支持，h4已废弃，指向包含长的图像描述文档的url |
| src | url | 规定显示图像的url |
| usemap | mapname | 将图像定义为客户端图像映射 |
| vspace | pixels | h5不支持，h4已废弃，规定图像顶部和底部的空白 |

使用效果如下图所示
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fj2zuu1neuj31fy0igmzo.jpg)

-------

`<map>`定义图像映射

用于客户端图像映射，图像映射指带有可点击区域的一幅图像，在img中的usemap属性可引用map中的id或name属性，所以应同时向map添加id和name属性，跟area不同的是area永远嵌套在map元素内部，area元素可定义图像映射中的区域
使用效果如下图所示
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fj300p2sz5j31ek0qon2q.jpg)

-------

`<area>`定义图像地图内部的区域

area定义图像映射内部的区域，该元素始终嵌套在map标签内部，imag标签中的usemap属性与map元素中的name相关联，以创建图像与映射之间的关系
area相关的属性如下表所示

| 属性 | 值 | 描述 |
| --- | --- | --- |
| alt | text | 规定区域的替代文本，如果使用href属性，则该属性是必须的 |
| coords | coordinates | 规定区域的坐标 |
| href | url | 规定区域的目标url |
| hreflang | language_code | 规定目标url的语言 |
| media | media query | 规定目标URL是为何种媒介优化的默认all |
| nohref | value | h5不支持，规定没有相关链接的区域 |
| rel | alternate<br>author<br>bookmark<br>help<br>license<br>next<br>nofollow<br>noreferrer<br>prefetch<br>perv<br>search<br>tag<br> | 规定当前文档与目标URL之间的关系 |
| shape | default<br>rect<br>circle<br>poly | 规定区域的形状 |
| target | _blank<br>_parent<br>_self<br>_top<br>framename | 规定在何处打开目标URL |
| type | MIME_type | 规定目标URL的MIME类型 |

-------

`<canvas>`绘制图形图像

canvas主要通过脚本来绘制图形图像，所有支持canvas的属性如下图

| 属性 | 值 | 描述 |
| --- | --- | --- |
| height | pixels | 规定画布的高度 |
| width | pixels | 规定画布的宽度 |
使用效果如下图所示
![](https://ws3.sinaimg.cn/large/006tNc79gy1fj7c3ksq0kj31dy0oo0wj.jpg)

-------

#### Audio/Video音视频
`<Audio>`定义声音，比如音乐或者其他音频流

目前audio支持的3种文件格式为MP3、WAV、Ogg，而在IE8或者更早版本的IE不支持audio
audio三者格式支持表如下图所示

| 浏览器 | MP3 | WAV | Ogg |
| --- | --- | --- | --- |
| Chrome | yes | no | no |
| Firefox | yes | yes | yes |
| Safari | yes | yes | no |
| opera | yes | yes | yes |

在audio中支持的属性如下表所示

| 属性 | 值 | 描述 |
| --- | --- | --- |
| autoplay | autoplay | 如果出现该属性，则音频在就绪后马上播放 |
| controls | controls | 如果出现该属性，则向用户显示音频控件(比如播放/暂停按钮) |
| loop | loop | 如果出现该属性，则当音频结束时重新开始播放 |
| muted | muted | 如果出现该属性，则音频输出为静音 |
| preload | auto<br>metadata<br>none | 规定当网页加载时，音频是否默认被加载以及如何被加载 |
| src | URL | 规定音频文件的URL |

关于audio的使用效果如下图所示
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fj7dys6updj31kw0mead1.jpg)

-------

`<source>`媒体元素

用于定义媒体资源，允许规定两个视频/音频文件供浏览器根据他对媒体类型或者编解码器的支持进行选择
其包括的属性值如下图所示

| 属性 | 值 | 描述 |
| --- | --- | --- |
| media | media_query | 规定媒体资源的类型，供浏览器决定是否下载 |
| src | URL | 规定媒体文件的URL |
| type | MIME_type | 规定媒体资源的MIME类型 |

其使用效果如下所示
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fj7e5di8lvj31ko0mkdjc.jpg)

-------

`<video>`定义视频
video用户电影片段或者是其他视频流，目前支持的三种格式MP4、WebM、Ogg如下表所示

| 浏览器 | MP4 | WebM | Ogg |
| --- | --- | --- | --- |
| IE | yes | no | no |
| Chrome | yes | yes | yes |
| Firefox | yes | yes | yes |
| Safari | yes | no | no |
| opera | yes | yes | yes |
MP4 = MPEG4文件使用h264视频编码解码器和AAC音频编码解码器
WebM= WebM文件使用VP8视频编码解码器和Vorbis音频编码解码器
Ogg = Ogg 文件使用Theora视频编码解码器和Vorbis音频编码解码器

video支持的可选属性如下表所示

| 属性 | 值 | 描述 |
| --- | --- | --- |
| autoplay | autoplay | 如果出现该属性，则视频在就绪后马上播放 |
| controls | controls | 如果出现该属性，则向用户显示控件，比如播放按钮 |
| loop | loop | 如果出现该属性，则当媒介文件完成播放后再次开始播放 |
| muted | muted | 如果出现该属性，则视频的音频输出为静音 |
| preload | auto<br>metadata<br>none | 如果出现该属性，则视频在页面加载时进行加载，并预备播放，如果使用autoplay则忽略该属性 |
| poster | URL | 规定视频正在下载时显示的图像，知道用户点击播放按钮 |
| src | URL | 要播放的视频的URL |
| height | pixels | 设置视频播放器的高度 |
| width | pixels | 设置视频播放器的宽度 |

video使用效果如下图所示
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fj7j0dyxtnj31kq0m6q7p.jpg)

-------
























































































