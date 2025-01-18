## TypeScript Reference Frontend

这是我们与Pixel Streaming插件一起发布的前端。参考前端包含：

1. 基础的`lib-pixelstreamingfrontend`库。
2. 基于`lib-pixelstreamingfrontend`库的参考UI插件`lib-pixelstreamingfrontend-ui`。

使用这两个库可以提供一个功能完整（且可自定义）的Pixel Streaming体验。

该包也是一个很好的示例，展示了如何将前端库作为依赖项包含并打包/压缩最终的应用程序。

### 参考前端的主要功能
- 一个信息面板（屏幕右侧），提供一个UI，用于向用户显示实时统计信息。
- 一个设置面板（屏幕右侧），提供一个UI，展示[config.ts](/Frontend/library/src/Config/Config.ts)中所有的选项。
- 一组控件（屏幕左侧），用于最大化视频、打开设置面板、打开信息面板以及进入VR模式。
- 能够显示叠加层，向用户展示信息或错误，或者展示提示让用户进行交互。

### 构建参考前端
```
cd Frontend/implementations/typescript
npm install
npm run build-all
```

### 使用参考前端
使用上述命令构建参考前端后，它将被放置在`SignallingWebServer/www`目录。
```
# Serve the reference frontend
cd SignallingWebServer/platform_scripts/cmd
start.bat
# Navigate to http://localhost in your browser to see the reference frontend
```

***Note:* You can also run `start.bat --build` to build all the dependent libraries.
