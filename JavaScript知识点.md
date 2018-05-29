### 上传文件的时候
上传文件的信息在触发的this对象上
this.files包含着所有上传的数组

### 创建图片渲染的引用
```
 var windowURL = window.URL || window.webkitURL;
 dataURL = windowURL.createObjectURL(fileObj.files[0])
 ```
 
 技巧：当时发现一种写法不行的时候，先检查下是否是哪个地方写错了
 ，还是无法改正，这个时候可以尝试着用另外的一种方式来重新写实现的方式。这个道理可以推广
 
 获取上传的图片
 
 fileObj值得是input时候的this对象
 ```
 if (fileObj && fileObj.files && fileObj.files[0]) {
        dataURL = windowURL.createObjectURL(fileObj.files[0]);
        imgObj.src=dataURL;
    } else {
        dataURL = fileObj.value;
        imgObj.style.filter = "progid:DXImageTransform.Microsoft.AlphaImageLoader(sizingMethod=scale)";
        imgObj.filters.item("DXImageTransform.Microsoft.AlphaImageLoader").src = dataURL;
    }
 ```
 
 
 ### 图片压缩的实现
 ```
 **
 * 将图片压缩后返回base64格式的数据
 * @param {*} image img元素
 * @param {*} requiredWidth 压缩后图片宽度
 * @param {*} requiredHeight 压缩后图片高度
 * @param {*} requiredQuality 图片质量1-100
 */
 
function compressImageTobase64(image,requiredWidth,requiredHeight,requiredQuality){
    var _quality = requiredQuality ? requiredQuality / 100 : 0.8;
    var canvas = document.createElement("canvas"),     
        ctx = canvas.getContext('2d');     
    var originWidth = image.naturalWidth,     
        originHeight = image.naturalHeight;     
    canvas.width = requiredWidth||originWidth;     
    canvas.height = requiredHeight||originHeight;     
    ctx.drawImage(image, 0, 0, originWidth, originHeight, 0, 0, requiredWidth||originWidth, requiredHeight||originHeight);
    var data = canvas.toDataURL("image/jpeg", requiredQuality);     
    return data;
}

```
HTML页面间跳转及参数传递
页面跳转的方式
HTML页面跳转：使用JS手动控制，或HTML链接自动实现
window.open(url, "", "width=600,height=400");
第二个参数：_self，在当前窗口打开窗口；_blank（默认值），在另外的新建窗口打开新窗口；
window.location.href="http://www.jb51.net";     //在同当前窗口中打开窗口
window.history.back(-1);    //返回上一页面
 <a href="http://www.baidu.net"  target="_blank">
 参数传递
 1. url传参：

第一个页面(a.html)：
```
var obj = a.value; //传给弹出页面参数
var url = 'jxb.html?obj='+obj;
url = encodeURI(url);
window.open(url, "", "width=600,height=400");
```
第二个页面(b.html)：
```
var url = decodeURI(window.location.href);
var argsIndex = url .split("?obj=");
var arg = argsIndex[1];
```
注:中文传输:可以在页面a用encodeURI 编码url  在b页面用decodeURI解码url

2. cookie传参：
```
function setCookie(cname,cvalue){
    document.cookie = cname + "=" + cvalue;
}
function getCookie(cname){
    var name = cname + "=";
    var ca = document.cookie;
}
```
3. localStorage对象传参：

a.html：
```
var div = doucment.getElementById('要获取字符串的DIV ID名');
localStorage.string = div.textContent;
```
b.html：
``
var div = doucment.getElementById('要写入的DIV ID名');
div.textContent = localStorage.string;
``
4. window.opener()

父页面：
```
<input type="text" name="textfield" id="textfield"/>
window.open("子页面.html");
```
子页面：
```
window.opener.document.getElementByIdx('textfield').value='123123123';
```

在页面中实现页面的查找，查找的实现，正则表达式


获取当前的时间具体信息代码
```
 var today = new Date();
             //分别取出年、月、日、时、分、秒
             var year = today.getFullYear();
             var month = today.getMonth()+1;
             var day = today.getDate();
             var hours = today.getHours();
             var minutes = today.getMinutes();
             var seconds = today.getSeconds();
             //如果是单个数，则前面补0
             month  = month<10  ? "0"+month : month;
             day  = day <10  ? "0"+day : day;
             hours  = hours<10  ? "0"+hours : hours;
             minutes = minutes<10 ? "0"+minutes : minutes;
             seconds = seconds<10 ? "0"+seconds : seconds;
			 
```			 
			 
HTML页面自动清理js、css文件的缓存（自动添加版本号）
```
<script type="text/javascript">  
document.write("<link rel='stylesheet' type='text/css' href='/css/layout.css?v="+new Date().getTime()+"'>");   
</script>  
```
文本框只读不能修改其中的内容
```
<!-- 方法2:readonly  文字不会变色，也是不可编辑的-->
<input type="text" name="input1" value="中国" readonly> 
<input type="text" name="input1" value="中国" readonly="true"> 
<!-- 方法3: disabled   此时文字会变成灰色，不可编辑。 -->
<input type="text" name="input1" value="中国" disabled="true">
```
另外可以创建一个div元素，该元素大小刚好可以完整覆盖住input表单，设置其z-index靠前，
使得无法接触到input表单