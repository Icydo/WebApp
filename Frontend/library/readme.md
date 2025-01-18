## lib-pixelstreamingfrontend

Pixel Streaming体验的浏览器/客户端端核心库。**此库不包含UI。**

请参阅[lib-pixelstreamingfrontend-ui](/Frontend/implementations/typescript)了解如何在此库的基础上构建UI示例。

### 主要功能
- 创建一个WebSocket连接，与信令服务器进行通信。
- 创建一个WebRTC对等连接，显示Unreal Engine的视频和音频。
- 处理来自用户的输入并将其传输回Unreal Engine。
- 打开数据通道连接，发送和接收自定义数据（除了输入之外）。
- 可编程和通过URL指定的设置。

### 如何将其添加到项目中
npm install @epicgames-ps/lib-pixelstreamingfrontend-ue5.5

### 本库的构建方式
NPM包支持：
- ES6模块使用
- CommonJS使用
- 类型定义
- 源映射

**注意：** NPM包不包含压缩/打包输出，用户需要在自己的应用程序中进行此操作。
