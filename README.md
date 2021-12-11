# qiankun + antd pro(父子应用都用antd pro) menu 等样式的适配处理
- 背景：
  - 使用 qiankun 做微前端框架，父子应用都是基于antd pro v5框架
  - 父应用 layout 为 top，子应用 layout 为 side 
  - 子应用的 fixSiderbar 设置为true 从而固定住 menu
- 问题1：fixSiderbar 会导致子应用的 menu 遮盖住父应用的 title, 如图1所示
![图1](https://upload-images.jianshu.io/upload_images/5527118-e0854c502e8e59dc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  - 解决方案：将menu的背景去除，隐藏menu的头部
    - 在 src/global.less中设置，去除背景
      ```css
      .ant-pro-sider.ant-layout-sider.ant-pro-sider-fixed {
        background: none
      }
      ```
    - 在app.tsx设置layout (相关参数见[ antdpro文档]，隐藏menu头部(https://procomponents.ant.design/components/layout/#api))
      ```js
      menuHeaderRender: () => (
        <div style={{ opacity: 0 }} > title </div> 
      ),
      ```
- 问题2：页面底部会多出一部分导致有滚动条，如图2所示
![problem2.png](https://upload-images.jianshu.io/upload_images/5527118-40428eedda7e9209.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  - 解决方案：修改antlayout样式中min-height属性（100vh修改为 100px，其中vh表示1%可视窗口高度）
      ```css
      .ant-layout {
        min-height: 100px;
      }
      ```
- 结果：
![1.png](https://upload-images.jianshu.io/upload_images/5527118-8b64eb43aa518557.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 源码：https://github.com/Flappyboy/demo-antd_pro-qiankun
