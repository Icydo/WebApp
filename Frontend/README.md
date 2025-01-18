# Pixel Streaming 前端

**前端**指的是在网页浏览器中运行的 HTML、CSS、图片和 JavaScript/TypeScript 代码，它使浏览器能够连接到 Unreal Engine Pixel Streaming 应用并与其交互。前端库是开发者可以修改和扩展的基础，以适应他们的 Pixel Streaming 体验需求。

前端由以下两个包组成：

1. [lib-pixelstreamingfrontend](/Frontend/library/): Pixel Streaming 前端的核心库，提供 WebRTC、设置、输入和常规功能。
2. [lib-pixelstreamingfrontend-ui](/Frontend/ui-library/): 用户可选择在核心库之上应用或构建的 UI 库。
3. [reference-pixelstreamingfrontend](/Frontend/implementations/typescript/): Pixel Streaming 前端的参考实现（插件随附的实现）。

这些库作为 [NPM 包](/README.md#npm-packages) 发布，并支持作为 ES6 模块、CommonJS 使用，包含类型定义和源映射。

## 文档
- [设置面板](Docs/Settings%20Panel.md)
- [自定义播放器网页](Docs/Customizing%20the%20Player%20Webpage.md)
- [HTML 页面要求](Docs/HTML%20Page%20Requirements.md)
  - [播放器文件位置和 URL](Docs/HTML%20Page%20Requirements.md)
- [自定义播放器输入选项](Docs/Customizing%20Player%20Input%20Options.md)
  - [禁用用户输入](Docs/Customizing%20Player%20Input%20Options.md)
- [自定义播放器小部件样式](Docs/Customizing%20the%20Player%20Widget%20Style.md)
- [访问 Pixel Streaming 蓝图 API](Docs/Accessing%20the%20Pixel%20Streaming%20Blueprint%20API.md)
- [从播放器页面与 UE5 通信](Docs/Communicating%20from%20the%20Player%20Page%20to%20UE5.md)
  - [使用 emitCommand 函数](Docs/Communicating%20from%20the%20Player%20Page%20to%20UE5.md)
  - [使用 emitUIInteraction 函数](Docs/Communicating%20from%20the%20Player%20Page%20to%20UE5.md)
- [从 UE5 到播放器页面的通信](Docs/Communicating%20from%20UE5%20to%20the%20Player%20Page.md)
- [处理非活动连接的超时](Docs/Timing%20Out%20Inactive%20Connections.md)

## 将库集成到你的项目中
TypeScript 库作为 [NPM](https://www.npmjs.com/settings/epicgames-ps/packages) 包和 [UMD](https://github.com/umdjs/umd) 模块提供（通过 [unpkg](https://unpkg.com/) 获取），使你能够使用现代 Web 开发工具和工作流从 TypeScript 代码或普通 JavaScript 代码中轻松使用这些库。

## 从源代码使用

在开发自己的 Pixel Streaming 体验时，目的是从这个库开始并通过其公共 API 扩展它。我们在 [implementations/typescript](/Frontend/implementations/typescript) 中提供了一个示例工作流，它实现了前端库并展示了如何打包/压缩最终的应用 JavaScript。

## 贡献

如果库的某部分没有公开，并且你希望扩展它，请在自己的分支中进行更改并打开一个 PR 供我们考虑。

## 开发

⚠️ 仅 NodeJS LTS 18.17.0 被正式支持，某些新版本的 NodeJS **可能会破坏你的构建** ⚠️

### 本地开发的前置条件
- 在你的系统上安装 NodeJS LTS 18.17.0。
- 使用以下命令全局安装 npm: `npm install npm -g`（是的，这是必须的）

### 构建库

对库的更改发生在 [/library](/Frontend/library) 目录下，并且需要你在开发环境中安装 NodeJS。
安装 NodeJS 后：

- `cd library`
- `npm install`
- `npm run build-all`

### 构建 UI 库

用户界面库位于 [/ui-library](/Frontend/ui-library) 目录中。你可以使用它或提供自己的用户界面。构建步骤如下：
- 先按照上述步骤构建库
- `cd ui-library`
- `npm install`
- `npm run build-all`

### 构建默认 UI

默认用户界面位于 [/implementations/typescript](/Frontend/implementations/typescript) 中。构建步骤如下：

- 先按照上述步骤构建库和 UI 库
- `cd implementations/typescript`
- `npm install`
- `npm run build-all`

这将生成 `player.html` 和 `player.js` 文件，并存储在 `SignallingWebServer/Public` 目录中，这就是默认的 UI。

### 创建自己的 UI

我们推荐学习 [/ui-library](/Frontend/ui-library) 和 [player.ts](/Frontend/implementations/typescript/src/player.ts)/[player.html](/Frontend/implementations/typescript/src/player.html)，或者是位于 [implementations/react](/Frontend/implementations/react) 的示例 React 实现。然后，在复制并修改 [package.json](/Frontend/implementations/typescript/package.json) 和 `.ts` 文件后，放置到自己的 `implementation/your_implementation` 目录，过程类似：

- `cd implementation/your_implementation`
- `npm run build-all`

## 单元测试

[/library](/Frontend/library) 项目有单元测试，测试 Pixel Streaming 功能是否与模拟连接兼容。要手动运行测试，请执行以下步骤：

- `cd library`
- `npm install`
- `npm run test`

## 法律

版权所有 &copy; 2025，Epic Games。根据 MIT 许可证授权，详细信息请参见 [LICENSE](/LICENSE.md) 文件。
