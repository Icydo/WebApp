# 在 UE 5.5 中发布的实验性 Pixel Streaming 2 插件

从 UE 5.5 开始，Epic Games 引入了一层，用于在内部更方便地维护 WebRTC。由于原版的 Pixel Streaming 插件直接使用 WebRTC，因此这一变更意味着我们必须引入一个新插件，以便为那些基于 PixelStreaming 插件开发自定义解决方案的开发者提供更好的过渡阶段。现阶段，原版 Pixel Streaming 插件和 Pixel Streaming 2 插件会同时随 Unreal Engine 一起提供，让用户有时间进行迁移。

我们已经编写了一份[迁移指南](/Docs/pixel-streaming-2-migration-guide.md)，以帮助所有使用该插件的许可用户平稳过渡，并重点介绍新旧插件之间的主要差异。

# 仓库健康检查与操作

| Health Checks |
|-|
| [![Libraries](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/healthcheck-libraries.yml/badge.svg?branch=master)](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/healthcheck-libraries.yml) |
| [![Platform Scripts](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/healthcheck-platform-scripts.yml/badge.svg?branch=master)](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/healthcheck-platform-scripts.yml) |
| [![Signalling Protocol](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/healthcheck-signalling-protocol.yml/badge.svg?branch=master)](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/healthcheck-signalling-protocol.yml) |
| [![Signalling Server Image](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/healthcheck-image-wilbur.yml/badge.svg?branch=master)](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/healthcheck-image-wilbur.yml) |
| [![SFU Docker Image](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/healthcheck-image-sfu.yml/badge.svg?branch=master)](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/healthcheck-image-sfu.yml) |
| [![Documentation Links](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/healthcheck-markdown-links.yml/badge.svg?branch=master)](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/healthcheck-markdown-links.yml) |

| Action | UE5.5 | UE5.4 | UE5.3 |
| -------|--|--|--|
| Common Lib | [![Publish common lib](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-common-library-to-npm.yml/badge.svg?branch=UE5.5)](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-common-library-to-npm.yml) | [![Publish common lib](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-common-library-to-npm.yml/badge.svg?branch=UE5.4)](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-common-library-to-npm.yml) | [![Publish common lib](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-common-library-to-npm.yml/badge.svg?branch=UE5.3)](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-common-library-to-npm.yml) |
| Signalling Lib | [![Publish signalling lib](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-signalling-library-to-npm.yml/badge.svg?branch=UE5.5)](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-signalling-library-to-npm.yml) | | |
| Publish Containers | [![Publish container images](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/container-images.yml/badge.svg)](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/container-images.yml) | | |
| Frontend lib | [![Publish frontend lib](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-library-to-npm.yml/badge.svg?branch=UE5.5)](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-library-to-npm.yml) | [![Publish frontend lib](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-library-to-npm.yml/badge.svg?branch=UE5.4)](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-library-to-npm.yml) | [![Publish frontend lib](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-library-to-npm.yml/badge.svg?branch=UE5.3)](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-library-to-npm.yml) |
| Frontend ui-lib | [![Publish ui-lib](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-ui-library-to-npm.yml/badge.svg?branch=UE5.5)](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-ui-library-to-npm.yml) | [![Publish ui-lib](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-ui-library-to-npm.yml/badge.svg?branch=UE5.4)](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-ui-library-to-npm.yml) | [![Publish ui-lib](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-ui-library-to-npm.yml/badge.svg?branch=UE5.3)](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-ui-library-to-npm.yml) |
| Release | [![Releases](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/create-gh-release.yml/badge.svg?branch=UE5.5)](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/create-gh-release.yml) | [![Releases](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/create-gh-release.yml/badge.svg?branch=UE5.4)](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/create-gh-release.yml) | [![Releases](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/create-gh-release.yml/badge.svg?branch=UE5.3)](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/create-gh-release.yml) |

# Pixel Streaming 服务器与前端的官方主页！
用于 Unreal Pixel Streaming（之前位于 `Samples/PixelStreaming/WebServers`）的前端和 Web 服务器元素现已合并到这个仓库，供所有人共同贡献。它们被称为 **Pixel Streaming Infrastructure**。

## Getting Started
要 **构建** 并 **运行** 一切所需，以便连接到 Pixel Streaming 插件，只需在 `PixelStreamingInfrastructure` 目录的根目录下执行以下命令：

**Windows**
```
.\SignallingWebServer\platform_scripts\cmd\start.bat
```

**Linux or Mac**
```
./SignallingWebServer/platform_scripts/bash/start.sh
```

如果你想在这个 monorepo 中的某个特定库内进行工作，那么可以 `cd` 到那个目录并运行：

`npm install`
`npm run build-all`

如果你想安装所有依赖项并清空已有的 `node_modules`，可以在仓库的根目录执行：

`npm install`


这是因为该 monorepo 使用 [NPM workspaces](https://docs.npmjs.com/cli/v7/using-npm/workspaces?v=true)。使用 NPM workspaces 意味着：

- monorepo 中的每个子工作区都没有自己的 `package-lock.json` 文件，而是只有一个集中在根目录的文件。
- 常见的依赖会提升（hoisted）到根目录的 `node_modules` 目录。
- 某些子工作区可能没有自己的 `node_modules`，因为它们的依赖都位于根目录的 `node_modules` 中。
- 当在 monorepo 内本地开发时，对子工作区的依赖会首先尝试通过本地 `symlink` 进行解决，而不是从 NPM 上下载已发布的包。例如，`pixelstreaming-frontend` 依赖 `pixelstreaming-common`，在此仓库中开发时，会首先尝试使用本地的 `./Common` 目录。

## Goals

本仓库的目标是：

- 加快 Pixel Streaming 服务器的发布频率（以更快应对浏览器的破坏性更新）。
- 鼓励 Unreal Engine 许可用户更轻松地对这些组件做出贡献。
- 提供更标准化的 Web 发布机制。
- 通过 MIT 许可证随心分发和修改此代码。

## Contributing

如果你想为我们的仓库贡献内容，请参阅我们的[贡献指南](CONTRIBUTING.md)。感谢你的时间和努力！

## Contents

Pixel Streaming Infrastructure 包含了所有运行 Pixel Streaming 应用所需的组件的参考实现。它们被拆分为各个项目，可以协同工作，也可与其他 WebRTC 技术搭配使用。这些实现包括：
- 一个名为 Cirrus 的信令 Web 服务器，位于 [`SignallingWebServer/`](SignallingWebServer/)。
- 一个 SFU（Selective Forwarding Unit），位于 [`SFU/`](SFU/)。
- 一个通用的前端库，位于 [`Common/`](Common/)。
- 若干前端项目，位于 [`Frontend/`](Frontend/)，包括：
  - [通信](Frontend/library/)和 [UI](Frontend/ui-library/) 的共享库
  - 使用不同技术（例如 TypeScript 或 React/JSX）的[不同实现](Frontend/implementations/)
  - 详情可参见 [/frontend](/Frontend/)。
- 用于验证信令协议实现的测试应用，位于 [`SS_Test/`](SS_Test/)。

## Releases
我们会在此仓库下发布多个不同的组件，主要包括：

- 信令服务器的容器镜像
- 前端的 NPM 包
- 本仓库源码的发布版本，其中也包含构建后的前端（压缩后的 js bundle）

### Container images

以下容器镜像由本仓库构建：

- [[Unofficial] pixel-streaming-signalling-server](https://hub.docker.com/r/pixelstreamingunofficial/pixel-streaming-signalling-server/tags)
- [[Unofficial] pixel-streaming-sfu](https://hub.docker.com/r/pixelstreamingunofficial/pixel-streaming-sfu/tags)

### NPM Packages
下面是一些“非官方”NPM 包（官方版本即将发布）：

| NPM Package | 5.5 | 5.4 | 5.3 |
|-------------|-----|-----|-----|
| Frontend lib | [lib-pixelstreamingfrontend-ue5.5](https://www.npmjs.com/package/@epicgames-ps/lib-pixelstreamingfrontend-ue5.5) | [lib-pixelstreamingfrontend-ue5.4](https://www.npmjs.com/package/@epicgames-ps/lib-pixelstreamingfrontend-ue5.4) | [lib-pixelstreamingfrontend-ue5.3](https://www.npmjs.com/package/@epicgames-ps/lib-pixelstreamingfrontend-ue5.3) |
| Frontend-ui lib | [lib-pixelstreamingfrontend-ui-ue5.5](https://www.npmjs.com/package/@epicgames-ps/lib-pixelstreamingfrontend-ui-ue5.5) | [lib-pixelstreamingfrontend-ui-ue5.4](https://www.npmjs.com/package/@epicgames-ps/lib-pixelstreamingfrontend-ui-ue5.4) | [lib-pixelstreamingfrontend-ui-ue5.3](https://www.npmjs.com/package/@epicgames-ps/lib-pixelstreamingfrontend-ui-ue5.3) |
| Signalling lib  | [lib-pixelstreamingsignalling-ue5.5](https://www.npmjs.com/package/@epicgames-ps/lib-pixelstreamingsignalling-ue5.5)  | `N/A` | `N/A` |
| Common lib  | [lib-pixelstreamingcommon-ue5.5](https://www.npmjs.com/package/@epicgames-ps/lib-pixelstreamingcommon-ue5.5)  | `N/A` | `N/A` |

### NPM getting started

```bash
#frontend (core lib)
npm i @epicgames-ps/lib-pixelstreamingfrontend-ue5.5
#frontend ui
npm i @epicgames-ps/lib-pixelstreamingfrontend-ui-ue5.5
```

## Documentation 
* [General Docs](/Docs/README.md)
* [Frontend Docs](/Frontend/README.md)
* [Signalling Server Docs](/SignallingWebServer/README.md)
* [SFU Docs](/SFU/README.md)

### Tagged source releases + built typescript frontend

[Github releases](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/releases)

## Versions

我们在不同的分支中维护了与不同版本的 Unreal Engine 兼容的服务器和前端。

:warning: 不同的 UE 版本之间可能会有破坏性变化 —— 请确保使用正确的版本。 :warning:

<ins>主要版本之间的更改，请参阅 changelog。</ins>

本仓库包含以下分支，对应不同的 Unreal Engine 版本：

| Branch | Status |
|--------|--------|
|[Master](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/tree/master)| Dev |
|[UE5.5](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/tree/UE5.5)| Current |
|[UE5.4](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/tree/UE5.4)| Supported |
|[UE5.3](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/tree/UE5.3)| End of life |
|[UE5.2](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/tree/UE5.2)| Unsupported |

| Legend | Meaning |
|---------|-----------|
| Dev | 这是我们的开发分支，与 ue5-main 配套——实验性。 |
|Pre-release| 该分支将与下一版 UE 搭配，我们会定期从 master 更新该分支。|
| Current | 受支持并与 最新发布 的 UE 版本对应。|
| Supported | 接受该版本的 bug 修复和问题反馈。|
| End of life | 当下一版 UE 发布后，此版本将不再获得支持。 |
| Unsupported | 我们将不会为此版本提供任何修复。 |

## Legal
© 2004-2024, Epic Games, Inc. Unreal and its logo are Epic’s trademarks or registered trademarks in the US and elsewhere. 
