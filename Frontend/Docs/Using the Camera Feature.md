## 相机功能概述

在当前状态下，Pixel Streaming中的相机功能旨在将玩家的视频输入音频从Pixel Streaming传递到Unreal Engine。WebRTC视频流通过`IPixelStreamingVideoSink`和`IPixelStreamingVideoConsumer`的组合暴露出来。

希望在`UPixelStreamingVideoComponent`所完成的基础上，处理接收到的视频的渲染（或保存）的用户，必须通过创建`IPixelStreamingVideoConsumer`的实现来处理这些内容，然后将其消费者注册到流媒体中。示例代码如下所示：

```c++
class FMyVideoConsumer : public IPixelStreamingVideoConsumer
{
public:
    virtual void ConsumeFrame(FTextureRHIRef Frame) override
    {
        // TODO: Handle the texture
    }

	virtual void OnConsumerAdded() override
    {
        UE_LOG(LogTemp, Display, TEXT("New consumer added!"));
    }

	virtual void OnConsumerRemoved() override
    {
        UE_LOG(LogTemp, Display, TEXT("Existing consumer removed!"));
    }
}

IPixelStreamingModule& Module = IPixelStreamingModule::Get();

TSharedPtr<IPixelStreamingStreamer> Streamer = Module.FindStreamer(Module.GetDefaultStreamerID());
if(!Streamer)
{
    return;
}

IPixelStreamingEpicRtcVideoSink* VideoSink = Streamer->GetUnwatchedVideoSink();
if(!VideoSink)
{
    return;
}

VideoSink->AddVideoConsumer(new FMyVideoConsumer()); 
```

## 在UE项目中启用Pixel Streaming视频输入

一旦您在项目中启用了Pixel Streaming插件，您需要将`Pixel Streaming Video`组件添加到您的场景中。它可以附加到场景中的任何演员或资产，按照以下步骤操作：

- 选择场景中任何启用的演员或资产；
- 点击其详细面板中的*添加*按钮；
- 在搜索栏中输入*Pixel Streaming Video*并点击匹配的组件：

<!-- <p align="center">
    <img src="Resources\Images\add-pixel-streaming-video-to-actor.png" alt="Add video component to actor">
</p> -->

一旦组件添加完成，您可以调整其设置，并指定要观看的播放器或流媒体ID（如果需要）。默认配置将观看它能看到的第一个对等端，适用于大多数基本用例：

<!-- <p align="center">
    <img src="Resources\Images\settings-pixel-streaming-video.png" alt="Video Component configuration">
</p>	 -->

在Blueprint中选择`PixelStreamingVideo`组件。在详细信息窗口的Pixel Streaming Video Component下，您应该能看到`Pixel Streaming Video Consumer`。选择下拉菜单并选择`Pixel Streaming Media Texture`。命名并保存相应的设置。

在场景中创建一个简单的平面对象，并调整其大小和形状以适合显示。

将您保存的`PixelStreamingMediaTexture`从内容浏览器直接拖放到场景中的平面上。这将自动创建一个材质并应用到该对象上。

UE端不再需要更多的设置，项目现在可以打包或单独使用。

## 在Pixel Streaming前端启用相机

启动Pixel Streaming并点击齿轮图标打开流媒体设置，在此您可以启用相机切换。确保重新启动流以应用更改：

<!-- <p align="center">
    <img src="Resources\Images\camera-toggle.png" alt="Component configuration">
</p>	 -->

*注意：* 或者，您也可以通过在URL中添加`?UseCamera=true`来启用相机。您仍然需要刷新页面以使更改生效。

首次操作时，浏览器可能会请求您允许该页面使用相机，您需要允许它。某些浏览器和防火墙可能会自动阻止该请求，因此您需要在浏览器设置中创建权限规则。

准备就绪！连接到流媒体。如果一切设置正确，您的相机输入将传递到UE并通过Pixel Streaming回放给您，这样您就能看到自己。

*注意：* 如果没有在项目中设置`Pixel Streaming Video`组件，以上步骤将无法工作。如果没有看到任何回放，请仔细检查项目中是否包含了适当的组件。
