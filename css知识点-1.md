#### 为ul设置颜色时无法显示
  1，为ul显式设置高度
  2，使用如下写法
  ```
  ul::after {
            content: '';
            display: block;
            clear: both;
        }
		```
3,在结束的</ul>前面加个清除浮动的属性 <ul> 
```
       <div style="clear:both"></div>
	   ```
					
### vertical-align 
该属性定义行内元素的基线相对于该元素所在行的基线的垂直对齐。允许指定负长度值和百分比值。
这会使元素降低而不是升高。在表单元格中，这个属性会设置单元格框中的单元格内容的对齐方式.
根据描述：该元素只能使用与行内的元素，且该该行中至少有两个行内元素。不能使用与块级元素。
一般的用于设置行内元素中图片的对其方式
设置的是行内元素在其父元素中的对其方式

* baseline	    默认。元素放置在父元素的基线上。
* sub	        垂直对齐文本的下标。
* super	        垂直对齐文本的上标
* top	        把元素的顶端与行中最高元素的顶端对齐
* text-top	    把元素的顶端与父元素字体的顶端对齐
* middle	    把此元素放置在父元素的中部。
* bottom	    把元素的顶端与行中最低的元素的顶端对齐。
* text-bottom	把元素的底端与父元素字体的底端对齐。
* length	

### rem元素							
rem相对的是HTML根元素，主要实现的地方是在移动端，随者屏幕尺寸分辨率的变化，
当用户浏览网页时，根据屏幕的尺寸，来向用户展示更适合用户的文字、图片、按钮大小。
	
假设我们的网页需要适配的iPhone4（320px），iPhone6(375px)，iPhone6 Plus(414px)。
我们的需求是，当用户浏览网页时，根据屏幕的尺寸，来向用户展示更适合用户的文字、图片、按钮大小。
（1）iPhone4的时候，希望网页的内容文字大小12px=12*（320/320）px，按钮的大小是240px。
（2）Iphone6的时候，虚妄网页的内容文字大小14px=12*（375/320）px，按钮的大小是280px，等比缩放。
（3）Iphone6 Plus的时候，虚妄网页的内容文字大小15.5px=12*（414/320）px，按钮的大小是310px，等比缩放。
以前的做法在rem概念没引入前我们的做法是，以最小的屏幕（iPhone）做一版数据出来，然后通过js去控制viewport 
的 initial-scale （网页缩放比例）。如：iPhone4下：
```
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0 />
```
那么对应的到了iPhone6需要调整缩放比例initial-scale=375/320 =1.18
```
   <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.18 />
   ```
同理到了iPhone6 Plus对应的应该是 initial-scale=414/320 =1.30
```
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=3.0 />
```
缺点是：这样做会使得，因为initial-scale越来越大，相当于拉伸网页，
而使得在大屏幕的移动端设备下，文字、图片会变模糊。
rem做法现在【天猫】的做法就是用rem来做。rem（font size of the root element）是指相对于根元素的字体大小
的单位（可以联想一下em）。也就是比如我定义：html{ font-size:14px}
那么如引用.test-box font-size/width/height 设为2rem的话就相当于 2*14px。也就是
```
.test-box{
        font-size:2rem;
       /*font-size:28px;*/
       /*2*14px/
}
```
我们可以理解为，一旦根节点html 定义的 font-size 变化，
那么整个网页中运用到 rem的也会变化。
iPhone4下html节点font-size
```
<html data-dpr="2" style="font-size: 64px; width: 100%; height: 100%; overflow: hidden;">
```
iPhone6下html节点font-size
```
<html data-dpr="2" style="font-size: 75px; width: 100%; height: 100%; overflow: hidden;">
```
iPhone6 Plus下html节点font-size
```
<html data-dpr="2" style="font-size: 82.8px; width: 100%; height: 100%; overflow: hidden;">
```

链接：https://www.zhihu.com/question/21504656/answer/85135845


### filter用于给元素设置滤镜，
在ie下都是不支持的直接去显示本地图片，
用ie提供的css渲染吧。
AlphaImageLoader：在元素的背景和内容之间插入一张图片，并提供对此图片的剪切和改变尺寸的操作。
如果载入的是PNG(Portable Network Graphics)格式，则0%-100%的透明度也被提供。

语法格式：````
filter : progid:DXImageTransform.Microsoft.AlphaImageLoader ( enabled=bEnabled , sizingMethod=sSize , src=sURL )
```

enabled：可选项，布尔值(Boolean)。设置或检索滤镜是否激活。 true：默认值。滤镜激活。 false：滤镜被禁止。
sizingMethod：可选项。字符串(String)。设置或检索滤镜作用的对象的图片在对象容器边界内的显示方式。
1）crop：剪切图片以适应对象尺寸。
2）image：默认值。增大或减小对象的尺寸边界以适应图片的尺寸。 
3）scale：缩放图片以适应对象的尺寸边界。
src：必选项。字符串(String)。使用绝对或相对 url 地址指定背景图像。假如忽略此参数，滤镜将不会作用。

```
 imgObj.style.filter = "progid:DXImageTransform.Microsoft.AlphaImageLoader(sizingMethod=scale)";
        imgObj.filters.item("DXImageTransform.Microsoft.AlphaImageLoader").src = dataURL;
    }
}

node.css({"filter":"progid:DXImageTransform.Microsoft.AlphaImageLoader(sizingMethod=scale)"});  
            node[0].filters.item("DXImageTransform.Microsoft.AlphaImageLoader").src = path;  

```
关于在ie下的透明度问题,如下:

语法格式:
```
filter:Alpha(Opacity=opacity,　FinishOpacity=finishopacity，Style=style,　StartX=startX，StartY=startY，FinishX=finishX，FinishY=finishY)

[javascript] view plain copy
filter:Alpha(Opacity="50",FinishOpacity="100",Style="3");  
```

opacity:值0-100,0表示完全透明，100表示完全不透明， 这个玩过ps 的朋友应该都蝗
FinishOpacity: 表示结束处的透明度.
style: 1 ，2， 3 ;1 表示线行，2表示圆形，中心发散，3 表示星形中心发散。
在标准浏览器下：直接opacity:0.5 就可以了。

img默认是个行内元素，比如在img的前面或后面放一些文字，这些文字会与图片排在同一行。
因此，当图片的前后存在一些空格或回车换行符时，它们会与图片一起成为同一块行内元素，
从而会造成外面的div被撑得比你想象的尺寸要大一些，比如：
```
<div>
<img src="..."/>
</div>
```
而如果是这样就不会：
``
<div><img src="..."/></div>
```
如果给img的css添加display:block属性，它就会变成块级元素（它会独占一行），其前后的空格、
回车等也会被自动忽略，这样外面的div的尺寸就会保持与img一致。

为图像指定 height 和 width 属性是一个好习惯。如果设置了这些属性，就可以在页面加载时为图像预留空间。
如果没有这些属性，浏览器就无法了解图像的尺寸，
也就无法为图像保留合适的空间，因此当图像加载时，页面的布局就会发生变化

为多个元素指定CSS样式时，逗号前面是一部分，逗号后面是一部分。.front,.back img
 你认为的是front和back类的中的img元素，实际上对应的时front类和back类中的img元素。

		
		
在编写CSS的时候，注意编写的顺序，其顺序与html文档中出现的顺序一致，在编写内部元素的css属性时候，
尽量使用层级选择器，这样会非常方便的识别出他们的层次关系，特别的上层position：relative布局
下层采用position：absolut布局，这样能看清楚其对应的关系


### flex的布局的实现

###URL 带有后面跟有锚名称 #，
指向文档内某个具体的元素。这个被链接的元素就是目标元素(target element)。

:target 选择器可用于选取当前活动的目标元素。


使用transform中的scale进行屏幕的缩放设置，
```
let screenMatch = () => {
            document.body.style.setProperty('visibility', 'hidden')
            let page = document.getElementById("page");
            let _scale = window.outerWidth/750;
            
            page.style.setProperty("transformOrigin", "0 0");
            page.style.setProperty("transform", "scale("+ _scale + ")");
            //兼容ios8
            page.style.setProperty("-webkit-transform-origin", "0 0");
            page.style.setProperty("-webkit-transfrom", "scale("+ _scale + ")");
            setTimeout(() => {
  
                page.style.setProperty("transformOrigin", "0 0");
                page.style.setProperty("transform", "scale("+ _scale + ")");
                //兼容ios8
                page.style.setProperty("-webkit-transform-origin", "0 0");
                page.style.setProperty("-webkit-transfrom", "scale("+ _scale + ")");
                document.body.style.setProperty('visibility', 'visible')
            }, 100);

        }
        screenMatch();
        window.onresize = screenMatch;
		```
上述代码中id为page的是整个页面元素开始的跟节点，body下的第一个元素。
这里body/html要设置min-height:100%;height:100%;
该缩放的实现比较有限，缩放的比例过大，或过小都会导致模糊或看不清楚

canvas中绘制图形的时候，必须在canvas的内联元素中指定高度和宽度heith、width

判断页面当前的状态
```
var hiddenProperty = 'hidden' in document ? 'hidden' :    
    'webkitHidden' in document ? 'webkitHidden' :    
    'mozHidden' in document ? 'mozHidden' :    
    null;
var visibilityChangeEvent = hiddenProperty.replace(/hidden/i, 'visibilitychange');
var onVisibilityChange = function(){
    if (document[hiddenProperty]) {    
        console.log('页面非激活');
    }else{
        console.log('页面激活')
    }
}
document.addEventListener(visibilityChangeEvent, onVisibilityChange);

```
添加水印
```
<canvas id="myCanvas" width="1000" height="500" >
Your browser does not support the HTML5 canvas tag.
</canvas>


var img = new Image();   
img.src = './img/demo.jpg';

img.onload=function(){
       var canvas=document.getElementById("myCanvas");
       var ctx=canvas.getContext("2d");
       ctx.drawImage(img,0,0);
}

 ctx.font="20px microsoft yahei";
   ctx.fillStyle = "rgba(255,255,255,0.5)";
   ctx.fillText("my images",100,100);
  ``` 
   
绘制跨域的图片
```
 <canvas width="600" height="300" id="canvas"></canvas>
    <img id="image" alt="">
    <script>
        var canvas = document.getElementById('canvas');
        var ctx = canvas.getContext('2d');
        var image = new Image();
        image.setAttribute('crossorigin', 'anonymous');
        image.onload = function() {
            ctx.drawImage(image, 0, 0);
            document.getElementById('image').src = canvas.toDataURL('image/png');
        };
        image.src = 'https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=3497300994,2503543630&fm=27&gp=0.jpg';
    </script>
	
	```
	CSS中要想实现元素的翻转效果，比较简单，例如我们希望某一张图片水平镜像翻转，只需要一行CSS就可以了：
```
img {
    transform: scaleX(-1);
}
```
或者：
```
img {
    transform: scale(-1, 1);
	}
	```