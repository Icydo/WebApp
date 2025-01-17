## 什么是 SFU？

SFU（Selective Forwarding Unit，选择性转发单元）是一种服务器，负责在参与者之间智能地路由媒体流。在 Pixel Streaming 中，SFU 的作用是接收来自 Unreal Engine 应用程序的流数据，并将其分发给各接收端（通常是 Web 浏览器），并可根据各接收端的网络状况有选择地发送数据，以适应其实际带宽和网络环境。

当使用 SFU 时，Pixel Streaming 会采用 simulcast（多码率同时广播）策略来适配流带宽。在该策略中，Unreal 会生成多路不同分辨率的流，SFU 再根据各接收端的网络条件选择向其发送合适质量的流。

> **注意：** 目前 Pixel Streaming 的 SFU 功能尚处于实验阶段（experimental）。

![SFUSetup](images/SFUDiagram.PNG)

---

## 何时使用 SFU

SFU 可以实现多对多或一对多的推流，而不必让所有客户端都以点对点方式直接连接到 Pixel Streaming 应用。如果你的 Pixel Streaming 应用需要同时向多个客户端提供流，并且这些客户端的网络状况参差不齐，需要使用不同的质量（例如较低的码率、分辨率或帧率），那么使用 SFU 往往是合适的选择。

---

## SFU 配置（Configuration）

在 `Samples/PixelStreaming/WebServers/SFU` 目录中的 `config.js` 文件中可以对 SFU 进行配置。

默认情况下，SFU 配置了两档质量：一个是完整分辨率，另一个是半分辨率。该配置可以通过启动 Unreal 时设置 `-SimulcastParameters=` 来进行调整（详情请参阅 [Pixel Streaming 参考](https://docs.unrealengine.com/5.3/en-US/unreal-engine-pixel-streaming-reference/)）。

> **注意：** 如果你同时启用超过三路的 simulcast 流，某些消费级 GPU 所提供的 H.264 硬件编码器可能会有最多三路编码会话的限制。

---

## 创建一个 SFU 分层切换功能

为了方便测试 SFU 的层级（layer）切换功能，我们在蓝图（Blueprint）中添加了一些简单的节点，可在游戏中强制切换到不同的流层。

![SFULayerBP](images/SFULayerBP.PNG)

将以上逻辑添加到关卡蓝图（Level Blueprint）中后，作为已连接的客户端，你可以使用设置的按键来强制切换 SFU 输出的不同流层。

> **注意：** SFU 本身会根据客户端的连接质量在各层之间自动切换，因此在实际部署中无需使用此蓝图。

以下为三档示例层之间切换后的效果：

- ![Layer1](images/Layer1.PNG) Layer 1  
- ![Layer2](images/Layer2.PNG) Layer 2  
- ![Layer3](images/Layer3.PNG) Layer 3  
