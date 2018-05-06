1.为ul设置颜色时无法显示
  1，为ul显式设置高度
  2，使用如下写法
  ul::after {
            content: '';
            display: block;
            clear: both;
        }
3，在结束的</ul>前面加个清除浮动的属性 <ul>        <div style="clear:both"></div>



					
vertical-align  该属性定义行内元素的基线相对于该元素所在行的基线的垂直对齐。允许指定负长度值和百分比值。这会使元素降低而不是升高。在表单元格中，这个属性会设置单元格框中的单元格内容的对齐方式.
根据描述：该元素只能使用与行内的元素，且该该行中至少有两个行内元素。不能使用与块级元素。
一般的用于设置行内元素中图片的对其方式
设置的是行内元素在其父元素中的对其方式

baseline	默认。元素放置在父元素的基线上。
sub	垂直对齐文本的下标。
super	垂直对齐文本的上标
top	把元素的顶端与行中最高元素的顶端对齐
text-top	把元素的顶端与父元素字体的顶端对齐
middle	把此元素放置在父元素的中部。
bottom	把元素的顶端与行中最低的元素的顶端对齐。
text-bottom	把元素的底端与父元素字体的底端对齐。
length	
					
					
rem相对的是HTML根元素，主要实现的地方是在移动端，随者屏幕尺寸分辨率的变化，
当用户浏览网页时，根据屏幕的尺寸，来向用户展示更适合用户的文字、图片、按钮大小。
	


假设我们的网页需要适配的iPhone4（320px），iPhone6(375px)，iPhone6 Plus(414px)。我们的需求是，当用户浏览网页时，根据屏幕的尺寸，来向用户展示更适合用户的文字、图片、按钮大小。（1）iPhone4的时候，希望网页的内容文字大小12px=12*（320/320）px，按钮的大小是240px。（2）Iphone6的时候，虚妄网页的内容文字大小14px=12*（375/320）px，按钮的大小是280px，等比缩放。（3）Iphone6 Plus的时候，虚妄网页的内容文字大小15.5px=12*（414/320）px，按钮的大小是310px，等比缩放。以前的做法在rem概念没引入前我们的做法是，以最小的屏幕（iPhone）做一版数据出来，然后通过js去控制viewport 的 initial-scale （网页缩放比例）。如：iPhone4下：<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0 />
那么对应的到了iPhone6需要调整缩放比例   initial-scale=375/320 =1.18<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.18 />
同理到了iPhone6 Plus对应的应该是 initial-scale=414/320 =1.30<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=3.0 />
早期【天猫】移动端也是用用这样的方法实现的。能满足我们的需求。缺点是：这样做会使得，因为initial-scale越来越大，相当于拉伸网页，而使得在大屏幕的移动端设备下，文字、图片会变模糊。rem做法现在【天猫】的做法就是用rem来做。rem（font size of the root element）是指相对于根元素的字体大小的单位（可以联想一下em）。也就是比如我定义：html{ font-size:14px}
那么如引用.test-box font-size/width/height 设为2rem的话就相当于 2*14px。也就是.test-box{
        font-size:2rem;
       /*font-size:28px;*/
       /*2*14px/
}
我们可以理解为，一旦根节点html 定义的 font-size 变化，
那么整个网页中运用到 rem的也会变化。
iPhone4下html节点font-size
<html data-dpr="2" style="font-size: 64px; width: 100%; height: 100%; overflow: hidden;">
iPhone6下html节点font-size
<html data-dpr="2" style="font-size: 75px; width: 100%; height: 100%; overflow: hidden;">
iPhone6 Plus下html节点font-size
<html data-dpr="2" style="font-size: 82.8px; width: 100%; height: 100%; overflow: hidden;">

链接：https://www.zhihu.com/question/21504656/answer/85135845


filter用于给元素设置滤镜，

在ie下都是不支持的直接去显示本地图片，
用ie提供的css渲染吧。

AlphaImageLoader：在元素的背景和内容之间插入一张图片，并提供对此图片的剪切和改变尺寸的操作。如果载入的是PNG(Portable Network Graphics)格式，则0%-100%的透明度也被提供。

语法格式：filter : progid:DXImageTransform.Microsoft.AlphaImageLoader ( enabled=bEnabled , sizingMethod=sSize , src=sURL )

enabled：可选项，布尔值(Boolean)。设置或检索滤镜是否激活。 true：默认值。滤镜激活。 false：滤镜被禁止。
sizingMethod：可选项。字符串(String)。设置或检索滤镜作用的对象的图片在对象容器边界内的显示方式。
1）crop：剪切图片以适应对象尺寸。
2）image：默认值。增大或减小对象的尺寸边界以适应图片的尺寸。 
3）scale：缩放图片以适应对象的尺寸边界。
src：必选项。字符串(String)。使用绝对或相对 url 地址指定背景图像。假如忽略此参数，滤镜将不会作用。


 imgObj.style.filter = "progid:DXImageTransform.Microsoft.AlphaImageLoader(sizingMethod=scale)";
        imgObj.filters.item("DXImageTransform.Microsoft.AlphaImageLoader").src = dataURL;
    }
}

node.css({"filter":"progid:DXImageTransform.Microsoft.AlphaImageLoader(sizingMethod=scale)"});  
            node[0].filters.item("DXImageTransform.Microsoft.AlphaImageLoader").src = path;  


关于在ie下的透明度问题,如下:

语法格式:filter:Alpha(Opacity=opacity,　FinishOpacity=finishopacity，Style=style,　StartX=startX，StartY=startY，FinishX=finishX，FinishY=finishY)

[javascript] view plain copy
filter:Alpha(Opacity="50",FinishOpacity="100",Style="3");  




opacity:值0-100,0表示完全透明，100表示完全不透明， 这个玩过ps 的朋友应该都蝗

FinishOpacity: 表示结束处的透明度.

style: 1 ，2， 3 ;1 表示线行，2表示圆形，中心发散，3 表示星形中心发散。

在标准浏览器下：直接opacity:0.5 就可以了。


img默认是个行内元素，比如在img的前面或后面放一些文字，这些文字会与图片排在同一行。因此，当图片的前后存在一些空格或回车换行符时，它们会与图片一起成为同一块行内元素，从而会造成外面的div被撑得比你想象的尺寸要大一些，比如：
<div>
<img src="..."/>
</div>
而如果是这样就不会：
<div><img src="..."/></div>
如果给img的css添加display:block属性，它就会变成块级元素（它会独占一行），其前后的空格、回车等也会被自动忽略，这样外面的div的尺寸就会保持与img一致。

为图像指定 height 和 width 属性是一个好习惯。如果设置了这些属性，就可以在页面加载时为图像预留空间。如果没有这些属性，浏览器就无法了解图像的尺寸，也就无法为图像保留合适的空间，因此当图像加载时，页面的布局就会发生变化

为多个元素指定CSS样式时，逗号前面是一部分，逗号后面是一部分。.front,.back img 你认为的是front和back类的中的img元素，实际上对应的时front类和back类中的img元素。

		
		
在编写CSS的时候，注意编写的顺序，其顺序与html文档中出现的顺序一致，在编写内部元素的css属性时候，尽量使用层级选择器，这样会非常方便的识别出他们的层次关系，特别的上层position：relative布局
下层采用position：absolut布局，这样能看清楚其对应的关系


flex的布局的实现


点击文件下载链接后实现文件下载；
使用<a>标签来完成  <a href="/user/test/xxxx.txt" download="文件名.txt">点击下载</a> 
这样当用户打开浏览器点击链接的时候就会直接下载文件。

但是有个情况，比如txt,png,jpg等这些浏览器支持直接打开的文件是不会执行下载任务的，而是会直接打开文件，这个时候就需要给a标签添加一个属性“download”;

使用按钮进行监听
一是window.open()

var $eleBtn1 = $("#btn1");  
        var $eleBtn2 = $("#btn2");  
        //已知一个下载文件的后端接口：https://codeload.github.com/douban/douban-client/legacy.zip/master  
        //方法一：window.open()  
        $eleBtn1.click(function(){  
            window.open("https://codeload.github.com/douban/douban-client/legacy.zip/master");  
        });  
二是表单提交，借助表单的action属性来实现

//方法二：通过form  
        $eleBtn2.click(function(){  
            var $eleForm = $("<form method='get'></form>");  
            $eleForm.attr("action","https://codeload.github.com/douban/douban-client/legacy.zip/master");  
            $(document.body).append($eleForm);  
            //提交表单，实现下载  
            $eleForm.submit();  
        }); 
		
		
meta  
提供关于网页的元数据，位于头部head中，由一些键值对的数据构成

1. charset  (字符集)

　　 说明：规定 HTML 文档的字符编码。

　　 用法： <meta charset="UTF-8">  

2.  viewport (视区)

　　 说明：是用户网页的可视区域。 大家都知道移动设备的屏幕一般都比PC小很多，webkit浏览器会将一个较大的“虚拟”窗口映射到移动设备的屏幕上，默认的虚拟窗口为980像素宽（目前大部分网站的标准宽度），然后按一定的比例（3：1或2：1）进行缩放。

　　　　 　也就是说当我们加载一个普通网页的时候，webkit会先以980像素的浏览器标准加载网页，然后再缩小为490像素的宽度。注意这个缩小是一个全局缩小，也就是页面上的所有元素都会缩小。

　　 用法：

<meta id="viewport" name="viewport" content="width=device-width; initial-scale=1.0; maximum-scale=1; user-scalable=no;">
　　　　　　(1)  width

　　　　　　　　width 控制 viewport 的大小，一般为了自适应设置为device-width

　　　　　　(2) initial-scale

　　　　　　　  initial-scale：初始缩放比例，也即是当页面第一次 load 的时候缩放比例。

 　　　　　  (3) maximum-scale

　　　　　　　  maximum-scale 最大缩放。即允许的最大缩放程度。这也是一个浮点值，用以指出页面大小与屏幕大小相比的最大乘数。

　　　　　　(4)  minimum-scale

　　　　　　　　minimum-scale：允许用户缩放到的最小比例。和 maximum-scale 用法类似。

　　　　　　(5)  user-scalable

　　　　　　　　user-scalable 用户调整缩放。即用户是否能改变页面缩放程度。如果设置为yes则是允许用户对其进行改变，反之为no。

3. keywords (关键字)

　　说明：为搜索引擎提供的关键字列表。各关键词间用英文逗号“,”隔开。指定搜索引擎用来提高搜索质量的关键词。

　　用法：<Meta name="Keywords" Content="关键词1,关键词2，关键词3,关键词4,……">

4. description (描述、简介)
 

　　　说明：Description用来告诉搜索引擎你的网站主要内容。
 

　　　用法：<Meta name="Description" Content="你网页的简述">

5. format-detection (格式检测)　　

　　　说明：format-detection 是用来检测html里的一些格式的。

　　　用法：关于meta的format-detection属性主要是有以下几个设置：　　　 
 

　meta name="format-detection" content="telephone=no"
　　　　meta name="format-detection" content="email=no"
　　　　meta name="format-detection" content="adress=no"
　　　　也可以连写：meta name="format-detection" content="telephone=no,email=no,adress=no"　　

　　　　　　（1）telephone
 

　　　　你明明写的一串数字没加链接样式，而iPhone会自动把你这个文字加链接样式、并且点击这个数字还会自动拨号！想去掉这个拨号链接该如何操作呢？这时我们的meta又该大显神通了，代码如下：

　　　　telephone=no就禁止了把数字转化为拨号链接！
　　　　telephone=yes就开启了把数字转化为拨号链接，要开启转化功能，这个meta就不用写了,在默认是情况下就是开启！

　　　　（2）email

　　　　告诉设备不识别邮箱，点击之后不自动发送

　　　　email=no禁止作为邮箱地址！
　　　　email=yes就开启了把文字默认为邮箱地址，这个meta就不用写了,在默认是情况下就是开启！

　　　　（3）adress

　　　　adress=no禁止跳转至地图！
　　　　adress=yes就开启了点击地址直接跳转至地图的功能,在默认是情况下就是开启！

6. apple-touch-fullscreen

　　说明：添加到主屏幕后，全屏显示。

　　用法：<meta name="apple-touch-fullscreen" content="yes">

7.  apple-mobile-web-app-capable

　　说明： 作用就是删除默认的苹果工具栏和菜单栏。content有两个值”yes”和”no”,当我们需要显示工具栏和菜单栏时，这个行meta就不用加了，默认就是显示。

　　用法：<meta name="apple-mobile-web-app-capable" content="yes" />

8.  App-Config

　　说明：保留历史记录以及动画效果

　　用法：<meta name="App-Config" content="fullscreen=yes,useHistoryState=yes,transition=yes"/>

9. msapplication-tap-highlight

　  说明：点击无高光(高亮)

　用法：<meta name="msapplication-tap-highlight" content="no">
		
	如果图片想等比例缩放，只需要指定width或height其中一个。
Align属性只能让文本居中，不能让图片单独居中。
Align可以实现“图文混排”效果。align = “left | right”
要想让图片实现居中效果，可以给图片增加一个<div>元素