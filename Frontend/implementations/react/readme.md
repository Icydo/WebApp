## Pixel Streaming sample React application

一个使用Pixel Streaming库的React最小示例应用程序。

### 主要功能
- 一个最小的React应用程序，包含一个Pixel Streaming包装组件
  - 在包装组件挂载时启动Pixel Streaming会话
  - 在包装组件卸载时断开会话，例如在单页面应用中导航到其他视图时
  - 监听`playStreamRejected`事件，并在浏览器拒绝视频流自动播放时显示一个`Click to play`覆盖层

### 开发

要构建和运行React应用程序，请运行：

- `npm install`
- `npm run build-all`
- `npm run serve`
