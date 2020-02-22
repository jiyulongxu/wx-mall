# 微信小程序电商平台

视频学习：[零基础玩转微信小程序](https://www.bilibili.com/video/av73342655?p=131)

跟着视频中老师敲了一遍，自己换了数据接口又折腾了一遍。

数据使用的是：[api工厂](https://www.it120.cc/) ，免费使用，有配套的[后台管理](https://admin.it120.cc/#/login?redirect=%2Fdashboard)，更详细的使用可以前去官网查看相关文档。

api工厂数据使用：

1. 前往后台管理注册账户信息并登录
2. 登录后台，左侧菜单 “工厂设置” --> “数据克隆” --> “将别人的数据克隆给我”
3. 对方商户ID填写 951
4. 点击 “立即克隆” ，然后退出后台重新登录，然后在左侧菜单的商城管理便可以看到相关数据



进入到后台管理后，在首页可以查看自己的域名，初始域名为一串字符串，这样不好看的同时用着也不顺畅，可以修改为自己喜欢的字符串。

![](https://s2.ax1x.com/2020/02/20/3mynld.png)

然后使用api工厂的域名拼接自己的子域名在加上接口地址，就可以访问数据了。

比如我的轮播图：https://api.it120.cc/kotoba/banner/list

在浏览器中就可以打开并返回数据。



测试数据来源与某位大佬的项目，更为强大的微信小程序商城：[wechat-app-mall](https://github.com/EastWorld/wechat-app-mall)，动手能力强的同学也可以自己手动修改编辑数据，这些在后台管理中都是可以做到的。



由于支付接口并不像其他接口一样可以随意调用，故支付并未完成，相应的订单页面也暂未完成，其他的就基本和视频中的项目基本一致了。



主要修改的地方在每个页面的js文件，比如首页，获取到的数据都是数组，那就只需要把接口地址改一下，然后重新赋值到data里面对应的数组，然后在wxml文件中修改一下数据字段名称； 比如之前接口的商品id对应的字段名称叫goods_id,但在这个接口中叫id,所以这些都是需要自己手动修改的，具体的对应名称可以在浏览器中输入接口地址查看，也可以在开工具中console.log打印出来查看。



<img src="https://s2.ax1x.com/2020/02/20/3myNlj.png" style="zoom: 50%;" />



<img src="https://s2.ax1x.com/2020/02/20/3my000.png" style="zoom: 50%;" />



改动较大的就是上面的首页和分类页面了，因为数据不一样，页面也要稍微的进行调整。



在商品详情页中，因为rich-text标签的体验不好，所以我选择了一个小程序的组件，wxParse,

简单易上手且强大，简单使用请查看这篇文章[微信小程序使用wxParse解析html](https://blog.csdn.net/Kotoba209_/article/details/104413748)。

以上就是完成接口数据的替换了，如想要在开发工具中校验合法域名，

<img src="https://s2.ax1x.com/2020/02/21/3m2bIP.png" style="zoom: 50%;" />

或者想要发布小程序的话，需要在微信开发者设置合法域名https://api.it120.cc，具体如下。

<img src="https://s2.ax1x.com/2020/02/21/3m2W8O.png" style="zoom: 50%;" />



### 更新一

1. 使用[apifm-wxapi](https://github.com/gooking/apifm-wxapi) 模块来请求数据，写法比原先的request方法更简洁，注释掉之前的request请求代码，可以直观的看到代码量的减少。这样优化可以使项目体积减少一点，[apifm-wxapi接口文档](https://github.com/gooking/apifm-wxapi/blob/master/instructions.md) 。

   apifm-使用方法：[使用 “apifm-wxapi” 快速开发小程序](https://blog.csdn.net/abccba9978/article/details/102861340) 。按照链接里的使用方法就可以请求到数据了，但是想要使用自己后台管理的数据需要在 app.js里定义一个 变量 来接收自己的域名

   `globalData: {
   ​    subDomain: "kotoba"
     }` 

   然后在app.js的onLaunch方法中初始化 `onLaunch: *function* (*options*) {
   ​    WXAPI.init(this.globalData.subDomain);
     },`， 具体信息在项目文件中都可以找着。

