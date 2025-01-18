## 推荐阅读
我们建议首先查看[示例实现](/Frontend/implementations/typescript/src)，以便评估如何构建新的播放器页面并将其与您的Unreal Engine应用程序集成。此外，如果您已经克隆了Pixel Streaming基础设施仓库并进行了上游更改，您可以分叉该仓库并发起拉取请求。

## 使用默认播放器网页
Pixel Streaming信令和Web服务器提供了一个示例播放器页面，该页面已设置为从您的Unreal Engine应用程序流媒体内容，并将鼠标、键盘和触摸事件发送回应用程序。如果默认播放器页面符合您的需求，您可以直接使用它。

## 自定义播放器网页
通过一些创意和对Web技术（如TypeScript、HTML和CSS）的了解，您可以完全控制播放器页面，创建自己的自定义UI以远程交互Unreal Engine内容。您可以触发和响应游戏事件，发出控制Unreal Engine行为的控制台命令等。

Pixel Streaming基础设施已经提供了一些[示例实现](/Frontend/implementations/)，可以用作参考，了解播放器网页本身是如何构建的。主要是，它们使用`library`包中的`Stream`类进行WebRTC通信，并使用`ui-library`包中的`Application`类进行UI处理。

当创建一个[`Application`](/Frontend/ui-library/src/Application/Application.ts)实例时，播放器的UI HTML会被创建。所有构成播放器页面基础的UI都附加到该对象的`rootElement`上。这个元素可以附加到页面上进行显示（在示例实现中，它直接附加到body本身）。

### 禁用或提供外部UI元素
默认情况下，`Application`会自动创建一些元素，用于显示和控制流媒体，例如：
 - 全屏按钮
 - 设置按钮+面板
 - 状态按钮+面板
 - 视频QP指示器
 - XR按钮

然而，对于许多应用程序来说，禁用某些元素可能会更有利。例如，面向最终用户的网页流可能需要禁止更改设置，如端点地址，或者通过不显示技术性信息来简化用户体验。在其他情况下，可能希望使用自定义HTML/CSS样式化播放器网页，并使用该页面上的元素来控制流媒体。

对于这种用例，可以更改创建`Application`时使用的初始配置对象，以自定义UI元素的创建方式。这个配置对象被称为`UIOptions`，它可以包含前述元素的任何组合设置，这些设置存储在以下参数中：`settingsPanelConfig`、`statsPanelConfig`、`fullScreenControlsConfig`、`xrControlsConfig`和`videoQpIndicatorConfig`。

例如，要创建一个没有设置面板或按钮的应用程序UI，并使用外部HTML按钮来切换流的全屏状态：
```ts
// Import needed types
import { Config, PixelStreaming } from '@epicgames-ps/lib-pixelstreamingfrontend-ue5.2';
import { Application, UIOptions, PanelConfiguration, UIElementCreationMode } from '@epicgames-ps/lib-pixelstreamingfrontend-ui-ue5.2'

// Create a stream and UI
const stream = new PixelStreaming(new Config({ useUrlParams: true }));
const application = new Application({
	stream: stream,
	onColorModeChanged: (isLightMode) => PixelStreamingApplicationStyles.setColorMode(isLightMode),
	settingsPanelConfig: { 
		isEnabled : false,
		visibilityButtonConfig : { creationMode : UIElementCreationMode.Disable }
	},
	fullScreenControlsConfig: {
		creationMode: UIElementCreationMode.UseCustomElement,
		customElement: document.getElementById('myCustomFullscreenButton')
	}
});
```

`PixelStreaming`对象还可以通过其事件监听器与自定义UI直接交互。例如，当视频量化参数（可用于衡量视频流的质量）发生变化时，可以执行以下操作（接着上面的内容）：
```ts
stream.addEventListener('videoEncoderAvgQP', (qp: number) => {
	/* Code to change any visuals needed based on the QP parameter */
})
```

### 自定义叠加层

进一步的自定义也可以通过[`Overlays`](/Frontend/ui-library/src/Overlay)来完成。顾名思义，这些叠加层会在满足特定条件时覆盖在播放器页面上，例如当玩家[离开](/Frontend/ui-library/src/AFKOverlay.ts)键盘时。可以查看[`Application`](/Frontend/ui-library/src/Application/Application.ts)源代码，了解这些条件是什么，以及如何添加新的叠加层。

### 自定义样式

有关如何更改播放器及其组件小部件CSS样式的概述，请参见[自定义播放器小部件样式](/Frontend/Docs/Customizing%20the%20Player%20Widget%20Style.md)。

## 对基础Pixel Streaming UI库的更改

此外，还可以对`ui-library`项目进行更深层次的更改和扩展，该项目作为前端UI实现的基础。任何有用的更改都可以通过拉取请求合并到主库中。
