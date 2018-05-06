1.http-equiv属性

    功能：模拟http协议文件头信息，当信息从服务器端传到客户端时，告诉浏览器如何正确的显示网页内容。

    http-equiv属性一般要与content属性配合使用。Content属性指定信息的详细参数。

(1)设置网页的字符集
<meta http-equiv="Content-Type" content="text/html;
charset=utf-8" />

(2)网页自动刷新
<meta http-equiv="refresh" content="2">   //每隔2秒钟，自动刷新网页一次
<meta http-equiv="refresh" content="2;url=http://www.ifeng.com">   //2秒钟后，跳转到凤凰网


2.name属性
       name属性主要用于设置网页的搜索关键字、版权信息、作者等。

(1)设置网页搜索关键字

<meta name="keywords" content="网站建设，企业网站建设，网站制作，网上商城，网站推广，域名注册，中企动力" />

(2)设置网页描述信息
<meta name="description" content="网站建设、网站制作专家中企动力，为您提供专业的展示型网站建设、营销型网站建设、独立商城系统网站建设、并提供一体化的企业邮箱”>


action：指定表单的处理程序，一般是PHP文件。
如果action为空，那么表单数据发到哪里去了？
结果：那么表单数据提交给了它自己来处理。
enctype：指定表单数据的编码方式(解密方式)。这个属性只能用在 method = “post” 的情况下。
application/x-www-form-urldecoded  //默认的加密方式
multipart/form-data  //如果你上传文件，该值必须它自己。