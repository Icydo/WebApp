## 麦克风功能总结

在当前的状态下，Pixel Streaming中的麦克风功能旨在将流媒体的麦克风输入音频从Pixel Streaming传输到Unreal Engine。WebRTC音频流在引擎内未被暴露或进一步处理，因此任何自定义使用音频流的功能都需要用户进行大量修改。

## 在UE项目中启用Pixel Streaming麦克风输入

一旦您在项目中启用了Pixel Streaming插件，您需要将`Pixel Streaming Audio`组件添加到您的场景中。它可以附加到场景中的任何演员或资产，按照以下步骤操作：

- 选择场景中任何已启用的演员或资产；
- 单击其详细面板中的*添加*按钮；
- 在搜索栏中输入*Pixel Streaming Audio*并点击匹配的组件：

<p align="center">
    <img src="Resources\Images\add-pixel-streaming-to-actor.png" alt="添加组件到演员">
</p>

添加组件后，您可以调整其设置，并指定要监听的玩家或流媒体ID（如果需要）。默认配置将监听它能够听到的第一个对等节点，应该适用于大多数基本用例：

<p align="center">
    <img src="Resources\Images\settings-pixel-streaming-audio.png" alt="组件配置">
</p>	

UE端无需更多的设置，因此项目现在可以打包或独立使用。

## 在Pixel Streaming前端启用麦克风

启动Pixel Streaming并点击齿轮图标以打开流设置，在这里您可以启用麦克风切换。确保重新启动流以应用更改：

<p align="center">
    <img src="Resources\Images\mic-toggle.png" alt="组件配置">
</p>	

*注意：* 或者，您也可以通过在URL中添加`?UseMic=true`来启用麦克风。您仍然需要刷新页面才能使更改生效。

第一次进行此操作时，浏览器可能会请求您允许该页面使用麦克风，您需要允许。一些浏览器和防火墙可能会自动阻止它，因此您需要在浏览器设置中创建权限规则。

现在您准备好开始了！连接到流并对着麦克风说话。如果一切设置正确，您的麦克风输入将被传递到UE并通过Pixel Streaming播放，您将听到自己的声音。

*注意：* 如果没有在项目中设置`Pixel Streaming Audio`组件，上述步骤将无法生效。如果没有听到回放，请仔细检查项目中是否已添加相应组件。

## 进一步处理麦克风WebRTC流的技巧

如前所述，麦克风音频流在传递到UE后不会进一步处理。您可能希望以自定义方式使用它，例如，将其反馈给Pixel Streaming，以便您能听到其他玩家的声音，或者将其传递到另一个插件以创建语音聊天。以下是一些帮助您入门的技巧：

- 您可以选择使用语音聊天插件，其音频数据通过UE音频系统传递，这些数据将自动被Pixel Streaming拾取。
- 如果您希望将数据传递到其他地方，例如到您的自定义插件，您需要创建自己的音频接收器，更多信息请见[这里](https://github.com/EpicGames/UnrealEngine/blob/5ca9da84c694c6eee288c30a547fcaa1a40aed9b/Engine/Plugins/Media/PixelStreaming/Source/PixelStreaming/Public/IPixelStreamingStreamer.h#L220)。
- 您可以实现Pixel Streaming音频混音器，并将您的语音插件的音频接入其中。[这里](https://github.com/EpicGames/UnrealEngine/blob/release/Engine/Plugins/Media/PixelStreaming/Source/PixelStreaming/Private/AudioInputMixer.h)是一个很好的起点。
- 由于Chrome 47以来的*不安全来源*会阻止相机和麦克风访问，因此请确保在生产环境中使用HTTPS。在本地使用时，例如在开发期间，则不需要此要求。
