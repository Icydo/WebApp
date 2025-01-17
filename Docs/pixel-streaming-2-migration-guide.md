# 迁移到 Pixel Streaming 2

## 为什么选择 Pixel Streaming 2？

从 UE 5.5 开始，我们在内部引入了一层，使得 Epic 更容易维护 WebRTC，因为它被用于引擎及其外围的许多部分。由于最初的 Pixel Streaming 插件直接使用 WebRTC，因此过渡到使用这层新抽象意味着插件的许多部分必须进行适配或重写。

为了给那些基于原版 PixelStreaming 插件开发自定义解决方案的开发者提供更好的过渡，我们决定引入一个新的插件。目前，原版的 Pixel Streaming 插件与 Pixel Streaming 2 插件将同时随 Unreal Engine 一起提供，为用户提供一段迁移时间。

## 谁会受到影响？

所有使用 Pixel Streaming 插件并准备迁移到新的 Pixel Streaming 2 插件的用户都应阅读本迁移指南。

## 有哪些影响？

在创建新的 Pixel Streaming 2 插件时，我们的主要目标之一是尽量减少对现有 Pixel Streaming 用户的影响。为此，我们保留了与 Pixel Streaming 相同的使用流程、步骤和启动参数。不过，新插件中仍有一些 Blueprint 节点、C++ 公共 API 和功能的变化，需要用户在迁移时注意。对于使用 C++ API 的用户来说，最明显的变化是所有的 WebRTC 类型都被移除。

## 兼容性

Pixel Streaming 2 与现有的 Pixel Streaming 基础设施完全兼容。与往常一样，我们建议你使用与自己的 Unreal Engine 版本相对应的 Pixel Streaming 基础设施分支。也就是说，对于 Unreal Engine 5.5 版本的 Pixel Streaming 2，你应该使用 Pixel Streaming Infrastructure 仓库的 UE5.5 分支。

## 会具体破坏哪些内容？

### Blueprints

所有 Blueprint 节点将会有一个 Pixel Streaming 2（PS2）版本，需要手动重新创建并重新连接（由于插件名称整体更改，无法使用重定向器）。

**迁移措施**

- 所需操作在本文件的相应章节中列出。

**删除内容**

- `SetPlayerLayerPreference` 和 `StreamerSetPlayerLayerPreference` 已被移除，建议使用前端设置替代。

### 公共 API 使用

#### `IPixelStreamingAudioConsumer.h`

重命名为 `IPixelStreaming2AudioConsumer.h`。无其他更改。

#### `IPixelStreamingAudioInput.h`

重命名为 `IPixelStreaming2AudioProducer.h`。无其他更改。

#### `IPixelStreamingAudioSink.h`

重命名为 `IPixelStreaming2AudioSink.h`。`IPixelStreamingAudioSink` 中的 `bool HasAudioConsumers` 方法被移除。用户无需与该方法交互，仍可使用现存的 `AddAudioConsumer` 和 `RemoveAudioConsumer` 方法。

#### `IPixelStreamingModule.h`

重命名为 `IPixelStreaming2Module.h`。以下方法已被移除，它们仅对 CVar 功能进行包装。如需以编程方式设置 PS2 编解码器，请使用引擎的 `IConsoleManager` 及其相关方法：
- `SetCodec`
- `GetCodec`

以下方法已被移除，因为外部视频源只是对其他插件的一个临时“hack”：
- `SetExternalVideoSourceFPS`
- `SetExternalVideoSourceCoupleFramerate`
- `SetExternalVideoSourceInput`
- `CreateExternalVideoSource`
- `ReleaseExternalVideoSource`
- `CreateVideoEncoderFactory`

以下方法被移除，因为 `InputComponent` 的 C++ 接口已移至模块内部：
- `AddInputComponent`
- `RemoveInputComponent`
- `GetInputComponents`

以下方法已新增：
- `CreateVideoProducer`
- `CreateAudioProducer`

#### `IPixelStreamingSignallingConnection.h`

已被完全移除，无替代品。在新插件中信令不再需要用户直接操作。

#### `IPixelStreamingSignallingConnectionObserver.h`

已被完全移除，无替代品。在新插件中信令不再需要用户直接操作。

#### `IPixelStreamingStats.h`

重命名为 `IPixelStreaming2Stats.h`。无其他更改。

#### `IPixelStreamingStreamer.h`

重命名为 `IPixelStreaming2Streamer.h`。此外，以下方法被移除：
- `SetTargetViewport`
- `GetTargetViewport`
- `SetTargetWindow`
- `GetTargetWindow`
- `SetTargetScreenRect`
- `GetTargetScreenRect`

使用上述方法的用户应改为先调用 `GetInputHandler`，然后直接在输入处理器上调用相应的方法。

- `OnInputReceived` 委托已被移除。依赖此功能的用户应改为在流端的输入处理器上注册消息处理器。
- `SendPlayerMessage` 重命名为 `SendAllPlayerMessage` 并且类型发生变化。类型从 `uint8` 变为 `FString`，用于表示要发送的消息的字符串标识符，例如 `"Command"`。
- `SendPlayerMessage` 是一个新方法（尽管与之前的方法同名），它可向某个特定的 `PlayerId` 发送消息。
- `SetInputHandler` 已被移除，建议用户使用同一个输入处理器并注册自定义消息处理器。

以下方法被移除，因为信令接口在 PS2 插件中不再暴露：
- `GetSignallingConnection`
- `SetSignallingConnection`
- `GetSignallingConnectionObserver`

- `SetPlayerLayerPreference` 被移除，建议使用前端设置替代。
- `SetInputHandlerType` 被移除，因为它只是输入处理器方法的一个代理。用户应从 streamer 获取输入处理器，然后在处理器上调用 `SetInputType`。
- `CreateAudioInput` 被移除，应使用 Pixel Streaming 模块的 `CreateAudioProducer`。
- `RemoveAudioInput` 被移除，因为音频输入的生命周期现由系统自动管理。

以下方法已被重命名：
- `SetVideoInput` 替换为 `SetVideoProducer`。
- `GetVideoInput` 替换为 `GetVideoProducer`。

以下方法已新增：
- `GetPeerVideoSink`
- `GetUnwatchedVideoSink`

#### `PixelStreamingAudioComponent.h`

该头文件暴露了两种类型：`FWebRTCSoundGenerator` 和 `UPixelStreamingEpicRtcAudioComponent`。两者现在都在 C++ 中被设为私有。此头文件的目的仅是将 Pixel Streaming 音频组件暴露给蓝图使用，这仍然通过将其设为私有来实现。如果用户需要在 C++ 中访问这些功能，必须在自己的项目中创建自定义类型来模仿这些类。不过，这并不复杂，因为所有必需的类型仍然是公共的。

#### `PixelStreamingBufferBuilder.h`

已被完全移除，无替代品。它纯粹用于 datachannel，而 datachannel 在 Pixel Streaming 2 中已成为内部类型。若用户以前使用该功能，可以在自己的代码中轻松复制其逻辑，因为所需类型都是常见的 UE 类型，仍可使用。

#### `PixelStreamingCodec.h`

已被完全移除，无替代品；改为使用 `Plugins\Experimental\AVCodecs\AVCodecsCore\Source\AVCodecsCore\Public\Video\VideoConfig.h` 中的 `EVideoCodec`。

#### `PixelStreamingDataChannel.h`

已被完全移除，无替代品。若要发送消息，请使用 `IPixelStreaming2Streamer` 中的 `SendAllPlayerMessage` 和 `SendPlayerMessage` 方法。若以前依赖 `OnMessageReceived` 委托，请改为在流端的输入处理器上注册消息处理器。若依赖 `OnOpen` 与 `OnClosed`，可使用 `UPixelStreaming2Delegates` 中的 `OnDataTrack(Open/Closed)` 与 `OnDataTrack(Open/Closed)Native`，但需要注意这些委托并不暴露 track 本身，仅用于跟踪 data track 的生命周期。

#### `PixelStreamingDelegates.h`

重命名为 `PixelStreaming2Delegates.h`。以下委托已被移除：
- `OnQualityControllerChangedNative`，因为在 PS2 中已经不再提供“流共享”的概念。若需要支持同时对大量客户端进行推流，可考虑使用 PixelStreamingInfra 提供的 SFU（Selective Forwarding Unit）。

以下委托被替换：
- 修正了 `OnFallbackToSoftwareEncodering(/Native)` 中单词拼写为 `OnFallbackToSoftwareEncoding(/Native)`。
- `OnDataChannelOpen/Closed(/Native)` 重命名为 `OnDataTrackOpen/Closed(/Native)`。
- `OnConnectedToSignallingServer` 调整为广播一个 `FString` 参数表示连接到信令服务器的 streamer ID。
- `OnConnectedToSignallingServerNative` 调整为广播一个 `FString` 参数表示连接到信令服务器的 streamer ID。
- `OnDisconnectedFromSignallingServer` 调整为广播一个 `FString` 参数表示连接到信令服务器的 streamer ID。
- `OnDisconnectedFromSignallingServerNative` 调整为广播一个 `FString` 参数表示连接到信令服务器的 streamer ID。

以下委托已新增：
- 新增了针对 VideoTracks 和 AudioTracks 打开/关闭的 C++ 委托。

其他信息：
- 所有 C++ 委托都移动为线程安全。
- 静态布尔量 `bIsExiting` 被移除，用户可使用全局 UE 函数 `IsEngineExitRequested()` 来跟踪引擎退出状态。
- 移除了 `CreateInstance` 方法并将 `GetPixelStreamingEpicRtcDelegates` 重命名为 `Get`。用户可通过 `UPixelStreamingEpicRtcDelegates::Get()` 获取到代表委托对象的单例指针。

#### `PixelStreamingInputComponent.h`

已被完全移除，无替代品。此组件用于在 Blueprint 中发送和接收 datachannel 消息。该功能仍在 Blueprint 中暴露，但在 C++ 中对该类型的交互仅限于插件内部。若需要在 C++ 中发送和接收 datachannel 消息，请使用已在多个引擎版本中暴露的 `PixelStreamingInputHandler.h`。

#### `PixelStreamingPeerConnection.h`

已被完全移除，无替代品。此文件完全使用了 WebRTC 类型，而在 PS2 中已不再引用这些类型。

#### `PixelStreamingPlayerConfig.h`

已被完全移除，无替代品。此类型之前用于处理 `PlayerConnected` 等信令消息。在 Pixel Streaming 2 中，所有信令逻辑都转为内部实现，因此不再需要此头文件中的类型。

#### `PixelStreamingPlayerId.h`

已被完全移除，无替代品。它实际上是 `FString` 的一个 typedef。所有使用 `PixelStreamingPlayerId` 的地方都可以直接替换为 `FString`。

#### `PixelStreamingSessionDescriptonObserver.h`

已被完全移除，无替代品。此类在以前用于监听 WebRTC 会话生命周期的变化，现在完全由内部处理。

#### `PixelStreamingSettings.h`

已被完全移除，无替代品。它包含以下三个方法：

1. `GetSimulcastParameters`
2. `GetCaptureUseFence`
3. `GetVPXUseCompute`

方法 (1) 和 (2) 可通过 CVar、ini 设置或插件设置进行查询，(3) 已被完全移除。该选项用于与 VPX 计算着色器相关的代码路径，但在性能方面无实质提升。

#### `PixelStreamingSignallingConnection.h`

已被完全移除，无替代品，因为信令现完全在插件内部进行处理。

#### `PixelStreamingStatNames.h`

重命名为 `PixelStreaming2StatNames.h`。`QualityController` 统计被移除，因为 Pixel Streaming 2 不再使用 qualityController（见后续“流共享”相关说明）。

#### `PixelStreamingUtils.h`

重命名为 `PixelStreaming2Utils.h`.

#### `PixelStreamingEpicRtcTrace.h`

已被完全移除，无替代品。该头文件仅用于 Pixel Streaming 及其相关模块的内部。如需使用此追踪定义，可使用 `UE_TRACE_CHANNEL_EXTERN` 自行创建。

#### 下列 `PixelStreamingVideoInput` 系列头文件

- `PixelStreamingVideoInput.h`
- `PixelStreamingVideoInputBackBuffer.h`
- `PixelStreamingVideoInputI420.h`
- `PixelStreamingVideoInputNV12.h`
- `PixelStreamingVideoInputPIEViewport.h`
- `PixelStreamingVideoInputRenderTarget.h`
- `PixelStreamingVideoInputRHI.h`

这些头文件已移为内部，并被 `IPixelStreaming2VideoProducer.h` 替代作为公共 API。用户现在可以使用 Pixel Streaming 模块的 `CreateVideoProducer` 方法，以及 streamer 的 `SetVideoProducer` 方法，在 PixelStreaming2 中使用自定义的视频输入。

#### `PixelStreamingVideoSink.h`

已被移除，替代为 `IPixelStreaming2VideoSink.h`。用户需要创建一个实现 `IPixelStreaming2VideoConsumer`（来自 `IPixelStreaming2VideoConsumer.h`）的自定义类。之后，可从 streamer 的 `GetVideoSink` 方法获取到一个 video sink，并通过 `AddVideoConsumer` 将自定义 consumer 指针添加进去。

#### `PixelStreamingWebRTCIncludes.h`

已被完全移除，无替代品，因为不再对外暴露 WebRTC，而使用了 EpicRtc。

---

### PixelStreamingEditor

#### `IPixelStreamingEditorModule.h`

重命名为 `IPixelStreaming2EditorModule.h`。此外，`bool UseExternalSignallingServer` 和 `void UseExternalSignallingServer(bool bUseExternalSignallingServer)` 方法被移除，应改为从对应的 ini / cvar 设置中查询此信息。

#### `PixelStreamingEditorUtils.h`

此头文件已被移除。它包含三个方法：

1. `ToString(EStreamType)`
2. `ToString(EWindowType)`
3. `HashWindow`

以上方法都是无用代码，已被完全删除。`EStreamType` 枚举现移动到 `PixelStreaming2CoreEnums.h` 并重命名为 `EPixelStreaming2EditorStreamTypes`。

#### `PixelStreamingStyle.h`

此头文件已改为内部，功能仅在 Editor Streaming 模块内部使用，因此被迁移到该模块中。

#### `PixelStreamingVideoBackBufferComposited.h`

此头文件已改为内部，仅用于 Editor Streaming 模块内部。

#### `PixelStreamingVideoViewport.h`

此头文件已改为内部，仅用于 Editor Streaming 模块内部。

---

### PixelStreamingHMD

#### `IPixelStreamingHMDModule.h`

重命名为 `IPixelStreaming2HMDModule.h`。此外，`GetPixelStreamingHMD` 现在返回的是新接口类型。

#### `PixelStreamingHMD.h`

此头文件被 `IPixelStreaming2HMD.h` 替代。用户可像以前一样使用以下两个公开函数：

1. `SetTransform`
2. `SetEyeViews`

#### `PixelStreamingHMDEnums.h`

重命名为 `PixelStreaming2HMDEnums.h`。

---

### PixelStreamingServers

#### `PixelStreamingServers.h`

以下方法已被移除：
1. `MakeCirrusServer`
2. `MakeLegacySignallingServer`

随着这些方法的移除，想在 UE 内直接启动信令服务器的用户只剩最后一个函数可用，此函数会启动一个嵌入式 C++ 信令服务器，同时仍会提供 PixelStreamingInfra 前端页面。

`EndPoint` 中的枚举类型被移除 `Signalling_Matchmaker`。

---

### PixelStreamingInput

#### `EditorPixelStreamingSettings.h`

此头文件的目的是暴露一些可在 Unreal Editor 插件 UI 中设置的插件配置项。这些功能现在已改为内部实现；不过，你仍可以通过插件 UI 或者 ini、CVar 方式去修改这些设置。

#### `IPixelStreamingInputHandler`

- `OnSendMessage`

该成员从多播委托变为一个事件，因为只有 Pixel Streaming 内部代码可以向此事件广播。不过，你仍可以绑定该事件，以便对输入处理器发送到 datachannel 的消息进行自定义处理（例如游戏手柄 ID 消息、文本框输入消息）。

#### `IPixelStreamingInputModule`

- `OnProtocolUpdated`

该成员委托被移动到新的 `IPixelStreamingDataProtocol` 接口，可通过 `IPixelStreamingInputHandler::GetFromStreamerProtocol()` 和 `IPixelStreamingInputHandler::GetToStreamerProtocol()` 获取。功能与以前相同，只是现在每个 streamer 都有自己独立的协议（分别为 `ToStreamer` 与 `FromStreamer` protocol），因此每个 protocol 都有自己的 `OnProtocolUpdated` 委托。

#### `PixelStreamingInputConversion.h`

此头文件仅由 PixelStreaming Input 模块使用，因此已改为私有。如果你之前使用过其中的映射，可以在项目中自行创建对应映射。所需类型都在公共范围内，可继续使用。

#### `PixelStreamingEnums.h`

增加了 `EPixelSreamingToStreamerMessage` 的 `FString` 和 `EPixelSreamingFromStreamerMessage` 的 `FString`。它们实际上被当作枚举来使用。

#### `PixelStreamingInputMessage.h`

已被完全移除。现在有个新的头文件 `IPixelStreaming2InputMessage.h`，用于暴露这些消息的接口。

#### `PixelStreamingInputProtocol.h`

此头文件已被移除。原本在此头文件中的两个静态协议被替换为 `IPixelStreaming2InputHandler::GetToStreamerProtocol` 和 `IPixelStreaming2InputHandler::GetFromStreamerProtocol`。

#### `PixelStreamingInputProtocolMap.h`

此头文件以前用于添加自定义数据通道消息，现在已改为内部实现。若要创建并添加自定义 Input Message，请使用 `IPixelStreaming2DataProtocol` 中的 `Add()` 方法，一旦添加成功，会返回刚添加的新消息对象。

---

### 流共享（Stream sharing）

“流共享”指以前可以在一个视频流中进行编码并发送给多个客户端（不论带宽或连接质量如何），并由一个“quality controlling”客户端来决定关键帧、带宽、重传等。这个“功能”已被移除，因为它有许多关于卡顿和卡帧的问题。更好的解决方案是在每个客户端上使用一个编码会话（新默认方案）或使用 PixelStreamingInfra 中的 SFU（Selective Forwarding Unit）。

**迁移措施**
- 如果你以前依赖“流共享”功能来支持多个观众共同观看一个流，请改用 SFU 作为替代。可在此文档中了解 SFU 的功能及使用方式：
  https://dev.epicgames.com/documentation/en-us/unreal-engine/hosting-and-networking-guide-for-pixel-streaming-in-unreal-engine#whatisthesfu

---

### 设置变化

Pixel Streaming 设置已被重构，可从 ini、控制台或命令行进行设置。一些设置的默认值有所变动，一些旧设置被废弃。现在你可以在 `ProjectSettings->Plugins->PixelStreaming2` 中查看所有可修改的设置及其默认值。优先级顺序为：ini < 命令行 < 控制台。

**迁移措施**

**控制台（命令行）设置更改**：

- `-PixelStreamingDisableLatencyTester` - 现在默认设置为 `true`，直到相关功能被重构并将统计重新加入。
- `-PixelStreamingSignalingKeepAliveInterval` - 新增！指示在信令 websocket 连接上多长时间（秒）发送一次 keep-alive 消息。
- `-PixelStreamingUseMediaCapture` - 现在默认启用 (`true`)。它的捕获时间性能与不使用 fencing 相似，但更安全，可避免撕裂、损坏或帧乱序，并且相比旧的 `CaptureUseFence` 性能更好。然而，它在 AWS g4dn 上会额外增加约 10% 的 CPU 使用（经我们测试）。
- `-PixelStreamingID` - 现在可以通过命令行设置。
- `-PixelStreamingSendPlayerIdAsInteger` - 已被废弃。不再使用整数 ID，字符串 ID 才是我们未来的方案。
- `-PixelStreamingVPXUseCompute` - 已被移除，因为在测试中未发现此设置能带来明显的性能提升。
- `-PixelStreamingIP` - 弃用警告：请使用 `PixelStreamingSignallingURL`。
- `-PixelStreamingPort` - 弃用警告：请使用 `PixelStreamingSignallingURL`。
- `-PixelStreamingURL` - 弃用警告：请使用 `PixelStreamingSignallingURL`。
- `-PixelStreamingSignallingURL` - 如果上面所述的 ip+port 或 url 都未设置，则必须使用此参数，否则 Pixel Streaming 2 将不会连接到任何信令服务器。
- `-PixelStreamingExperimentalAudioInput` - 已被移除，现在默认始终启用。
- `-PixelStreamingSuppressICECandidateErrors` - 已被移除，仅在一些不稳定测试中才有用，现在这些测试已被修复。
- `-PixelStreamingFastPan` - 已被移除，多个 UE 版本以来都没有任何代码路径在使用。
- `-PixelStreamingEncoderMinQuality` - 替代了 `-PixelStreamingEncoderMaxQP` 来设置编码质量下限。更改原因是使用 “MaxQP” 表示质量下限很难理解，而且原先 [1-51] 的取值范围仅适用于 H.264。新的范围为 [0 - 100]，其中 0 代表最低质量、100 代表最高质量，能适用于 VPX、AV1 等其他在 Pixel Streaming 中支持的编解码器（它们有完全不同的 QP 范围）。
- `-PixelStreamingEncoderMaxQuality` - 替代了 `-PixelStreamingEncoderMinQP` 来设置编码质量上限。更改原因同上，使用 “MinQP” 表示质量上限让人迷惑。新的取值范围 [0 - 100] 也能同时适配 VPX、AV1 等编解码器。
- `-PixelStreamingEncoderPreset` - 已被 `-PixelStreamingEncoderQualityPreset` 和 `-PixelStreamingEncoderLatencyMode` 所取代，以便更好地配置编码质量和延迟。
- `-PixelStreamingEncoderQualityPreset` - 用于设置编码的多个选项，以在质量和比特率之间进行平衡。
- `-PixelStreamingEncoderLatencyMode` - 新设置，用来配置编码多个方面并平衡延迟和质量。需要注意，如果选择较低延迟模式但质量预设较高，实际观感质量会比默认情况更低。
- `-PixelStreamingEncoderIntraRefreshPeriodFrames` - 已被移除，因为它与 `-PixelStreamingEncoderKeyframeInterval` 功能重复。
- `-PixelStreamingEncoderRateControl` - 已被移除，因为目前在 Pixel Streaming 中主要使用且测试充分的是 `CBR` 模式。
- `-PixelStreamingEnableFillerData` - 已被移除，并未找到真正的使用场景。
- `-PixelStreamingEncoderMultipass` - 已被移除；低延迟模式会自动禁用多遍编码，所以这个设置冗余。
- `-PixelStreamingEncoderIntraRefreshPeriodFrames` - 已被移除，这些设置过于针对 NVENC，且适用性不广。
- `-PixelStreamingEncoderIntraRefreshCountFrames` - 同上，已被移除。
- `-PixelStreamingDegradationPreference` - 已被移除并固定为 `MAINTAIN_FRAMERATE`，因为 Pixel Streaming 流程中许多环节都假定 WebRTC 以这种模式工作。
- `-PixelStreamingEncoderKeyframeInterval` - 默认值现在是 `-1`，这意味着不会发送周期性关键帧。关键帧只会在连接的客户端需要时发送，从而降低带宽占用。此功能在以前主要为已移除的“流共享”服务。
- `-SimulcastParameters` - 已由 `-PixelStreamingEncoderEnableSimulcast` 和 `-PixelStreamingEncoderScalabilityMode` 替代。
- `-PixelStreamingEncoderScalabilityMode` - 指定编码的 “scalability mode”，其可取值可参考：https://www.w3.org/TR/webrtc-svc/#scalabilitymodes 。
- `-PixelStreamingWebRTCMaxBitrate` - 默认值从 100mb/s 降至 40mb/s，因为在真实网络环境中 100mb/s 往往会导致拥塞。
- `-PixelStreamingWebRTCLowQpThreshold` - 已被移除，这是一个内部 WebRTC 设置，未正确暴露。
- `-PixelStreamingWebRTCHighQpThreshold` - 已被移除，这是一个内部 WebRTC 设置，未正确暴露。
- `-PixelStreamingWebRTCUseLegacyAudioDevice` - 已被移除，因为 LegacyAudioDevice 已被弃用。

---

## PixelStreamingPlayer（Engine/Plugins/Experimental/PixelStreamingPlayer）

在 Pixel Streaming 2 中，Pixel Streaming 播放器功能不再是独立插件，而是与 Pixel Streaming 2 插件合并。

#### `PixelStreamingMediaTexture.h`

已被完全移除，无替代品。此组件用于更新在 PS2 中接收的视频帧到材质。此功能仍在蓝图中暴露，但在 C++ 中对这个类型的交互已改为插件内部。如果需要在 C++ 中显示 PS2 接收的视频帧，应实现 `IPixelStreaming2VideoConsumer` 并将其添加到 `IPixelStreaming2VideoSink`。

#### `PixelStreamingPeerComponent.h`

已被完全移除，无替代品。此组件用于在引擎中接收 PixelStreaming 流。该功能仍在蓝图中暴露，但在 C++ 中对该类型的交互已改为仅限插件内部。如果需要在引擎中接收流，则应自己实现一个类似此类功能的自定义 peer。

#### `PixelStreamingSignallingComponent.h`

已被完全移除，无替代品。在新插件中信令对用户是透明的，无需用户直接操作。

#### `PixelStreamingWebRTCWrappers.h`

已被完全移除，无替代品，因为不再对外暴露 WebRTC。

---

### Blueprints

实现 `UPixelStreamingEpicRtcPeer` 组件的大部分 Blueprint 节点已被移除。现在的基本步骤如下：

1. 启用 Pixel Streaming2 插件。
2. 新建一个 Blueprint Class（例如 Actor），并随意命名保存。
3. 打开该 Blueprint Class，添加 Pixel Streaming Peer Component。
4. 将该组件拖到事件图中，从该组件拖线创建一个 `Connect` 节点。将 `BeginPlay` 事件的输出连接到新建 `Connect` 节点的输入，并在 URL 里输入类似于 `"ws://localhost:80"`。
5. 右键点击“组件”面板中的 Pixel Streaming Peer Component，添加 “OnStreamerList” 事件到事件图。
6. 具体如何处理要订阅哪个 streamer 由你决定。这里的示例是仅订阅第一个可用的 streamer。方法是：将 Pixel Streaming Peer Component 拖到事件图，从其拖线创建一个 “Subscribe” 节点，将 “OnStreamerList” 的输出连接到 “Subscribe” 的执行输入，从 “OnStreamerList” 的 “Streamer List” 输出上拖线，创建一个“Get (a ref)”（索引为 0），将其输出连接到 “Subscribe” 的 “Streamer Id” 输入。
7. 左键点击“组件”面板中的 Pixel Streaming Peer Component，在 “Details” 窗口中，找到 “Pixel Streaming Video Consumer”，下拉选择 “Pixel Streaming Media Texture”，根据需要命名或保存。
8. 当出现提示时，选择并保存 Video Output Media Asset。
9. 将你的 Blueprint Actor 拖到场景中。创建一个简单的平面对象，并对其进行合适地调整大小来作为显示平面。
10. 直接从内容浏览器将你的 Pixel Streaming Media Texture 拖到场景中的平面上，这会自动创建一个材质并将其应用到该平面上。
11. 在这个项目之外启动一个本地的 Pixel Streaming 流（外部进程），如启动 Signalling server 并使用相关 Pixel Streaming 启动参数运行应用。
12. 运行场景后，你应能在关卡中的平面对象上看到来自外部 Pixel Streaming 的视频！

<p align="center">
    <img src="Resources\Images\pixelstreamingplayerblueprint.png" alt="Pixel Streaming Player Blueprint">
</p>
