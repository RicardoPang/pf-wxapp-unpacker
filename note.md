wxml 视图展示内容 html 渲染引擎 ？？
wxss 视图样式 css 渲染引擎 ？？

js 逻辑、具体业务 ==> js ==> v8
setData

==> 微信 ==

Page(

)
setData
App(

)

小程序基本架构：
逻辑层 js ==> 业务、生命周期（Page、App）、事件逻辑的处理、数据的加载和处理  
 单独的线程 ==> ios/jscore 安卓/v8

    一个逻辑层 App1   many  Page   WAService.js

    1. Page()   App
    2. 通信
    3. 生命周期维护
    4. wx
    基础库

    WeixinJSBridge
            提供 线程直线的通信
            提供 native 线程之间的通信
        Foundation 基础模块


     wx 全局SDK
     Page
     App
     setData


    执行过程
    1. loading 基础库 WAService.js
    2. 加载所有页面pagejs (Page\App)
    3. 构建全局配置 JSON、Render？？

渲染层 wxml wxss 页面的基本结构 样式 webkit （iframe）单独的线程 div  
 html / WAWebview.js 1.事件处理 2.通信

        WeixinJSBridge
            提供 线程直线的通信
            提供 native 线程之间的通信
        Foundation 基础模块

        exparser 组件系统 webComponent
        ```js
            window.exparser.registerElement
        ```
        衔接 native原生组件 html组件融合
        https://developers.weixin.qq.com/miniprogram/dev/framework/custom-component/wxml-wxss.html  事件 ==>逻辑层

        __virtualDOM__ VNode ==》exparser diff


    3. 数据 ==> 页面
    4. web component \组件系统 \渲染逻辑


    执行过程： 构建渲染器 render

    render(data)

    执行过程:
    1. 加载默认配置、加载基础库、js（WXML、WXSS）
    2. WXSS js  ==> 动态计算css
    3. 改变路由
    4. 合并配置 默认、app配置、页面配置
    5. 构建渲染器 ==>通知基础库 渲染器ready
    5. 基础库 JsBridge() ==>Native ==> 逻辑层
    6. 基础库==>render (data)==>VNode===>组件系统 ==> 组件

2.0.4.wxvpkg ==>基础库

wcc Wechat WXML Compiler WXML (js)  
 $gwx ==>生成渲染器的方法 render
render(data)==> VNode

wcsc WeChat Stylesheet Compiler WXSS(rpx) ==> css  
 手机分辨率
./wcsc -js index.wxss >> wxss.js

1.  js 运行时 ==> 动态计算 DPR ==> 拼接 css ==>添加

    ```js
    var BASE_DEVICE_WIDTH = 750;
    var isIOS = navigator.userAgent.match('iPhone');
    var deviceWidth = window.screen.width || 375;
    var deviceDPR = window.devicePixelRatio || 2;
    var checkDeviceWidth =
      window.__checkDeviceWidth__ ||
      function () {
        var newDeviceWidth = window.screen.width || 375;
        var newDeviceDPR = window.devicePixelRatio || 2;
        var newDeviceHeight = window.screen.height || 375;
        if (
          window.screen.orientation &&
          /^landscape/.test(window.screen.orientation.type || '')
        )
          newDeviceWidth = newDeviceHeight;
        if (newDeviceWidth !== deviceWidth || newDeviceDPR !== deviceDPR) {
          deviceWidth = newDeviceWidth;
          deviceDPR = newDeviceDPR;
        }
      };
    ```

picker

微信开发者工具
双线程  
 document.getElementsByTagName('webview')[0].showDevTools(true,null)
js ==> iframe ==>
wxml wxss ===>iframe

native h5

小程序
小程序的底层架构
逻辑层
page app setData V8
视图层
render dom diff 组件 事件

wxml
wxss
js

为什么小程序也需要有框架?

编译时框架 => 上线之前就处理称为小程序可以认知的形态
wepy taro 主要的工作在编译阶段 babel

taro 类 react
vue 提前定好模板规则 => 编译阶段 模板规则 =>
缺点: 模板规则
优点:在线运行效率较快

把一种语言或者代码 => 转换成另一种代码的形态

运行时框架
mpvue uni-appremax magalo
