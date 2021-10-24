# hoppinzq-jquery-zjax

#### 是什么？
zjax是基于JQuery的Ajax的拓展，是对原生ajax的二次封装。

#### 使用说明

1.  拉取代码，直接打开html即可。demo里上传文件的接口我是用本地后台的，你要测试文件上传监听进度，需要有一个接口。
2.  ```$.zjax({config})```
3.  ```$dom.zjax({$.extend(config,success:function(){//this.resporse,this.$dom})})```  
4.  ```$.zjaxChain({config}).zjaxChain({config}).zjaxChain({config}).runZjax()```

#### 特技

1.   支持缓存，通过配置storageCache为true来启动缓存，当启动缓存时，响应内容会被封装成url对象或base64码，第二次请求将直接请求缓存的url对象。
2.   支持请求锁定，通过配置lockRequest为true来锁定请求，可以配置锁定时间。被锁定的请求只要没接收到响应（无论成功还是失败抑或是意外终止），就不能重复发起请求，防止遮罩失效可以无限新增或者点赞等等。
3.   支持绑定ajax到dom元素上，通过$dom.zjax即可绑定，在响应里通过this.$dom来获取绑定的dom元素。通过zjax绑定dom元素，可以将ajax的响应直接赋值到下拉框，表格等。
4.   支持链式请求，通过zjax内置调度器，实现ajax循序执行，你不应该指望通过配置ajax的async:false来同步请求，因为ajax将会锁定浏览器并阻塞后面的脚本代码运行。
5.   支持代理URL，即配置额外的url，只有当响应404时，去请求其他的url。（这个是我为了在服务器跟本地测试而写的一个配置，有时候发布到服务器上忘改url了，或者图片上传到本地了）
6.   支持进度跟踪，通过配置isProcess为true来启动，可以监听文件上传的实时进度，上传速度，预计上传完成时间等等。
7.   支持绑定遮罩，通过配置isLoading为true来启动，将遮罩绑定在loadingDom的dom上，如果没有配置dom则会默认绑定在body上，如果将zjax绑定到dom上，则会在该dom上绑定遮罩。这其实是通过代理来实现的，在ajax要执行前，绑定或者启动遮罩；在ajax执行后，关闭遮罩。可以自己定制。
8.   支持自动阻塞请求，通过配置blockRequest为true来启动，如果用户频繁点击ajax请求，有两个问题：①、如果连续点击了5个ajax请求，前4个其实是无效的，趁早结束节省资源。 ②、最后一个发送的请求，响应未必是最后一个，有可能造成混乱。③、还有一个问题，有一个人进入首页，结果首页还没加载完就切换到tab2，然后又切换到tab3，由于没有发生路由跳转，主页跟tab2仍在请求，这时这些请求应该被关闭，防止tab3加载慢。zjax就可以帮你阻塞这些无用的请求，防止网页因无用的请求太卡或者加载混乱。
9.   支持轮询，通过配置roundUrl来启动，轮询启动会禁用遮罩，缓存，锁定跟阻塞。
10.  支持直接修改url使其进入ZQ网关，这个我估计你们应该用不到，ZQ网关url十分长，因为通过这个url后台可以知道前台要干什么事情，比如你后台是否要加密，请求从什么页面（友链或者广告）来的，是否让你后台缓存接口防止IP超频，自动分发到对应的服务等等，所以就把配置项拆出来了。


轮询，等功能。
2.   ajax返回值的缓存做的非常好
