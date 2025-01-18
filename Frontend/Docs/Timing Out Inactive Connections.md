## 超时断开非活动连接

在某些 Pixel Streaming 部署中，您可能希望自动断开一段时间内未活动的用户连接。例如，如果您有有限的 Unreal Engine 应用程序池，并且这些应用程序的访问受匹配服务器控制，您可能需要丢弃长期未活动的连接，以确保有可用的应用程序实例来处理新的连接请求。

您可以配置 Pixel Streaming 实现来检测用户是否处于离开键盘（AFK）状态——即当用户在可自定义的时间间隔内未与播放器小部件进行交互时。AFK 系统会向用户发出警告：

<p align="center">
    <img src="Resources\Images\afk-warning.png" alt="AFK 超时警告">
</p>

如果用户继续不回应，AFK 系统将在最终断开会话前再等待 10 秒。

任何用户与播放器面板的交互都会重置 AFK 计时器。这包括鼠标移动和拖动、鼠标按钮按下、键盘按键、移动设备上的触摸事件以及您通过 `emitCommand` 和 `emitUIInteraction` 函数设置的自定义交互。

要使用 AFK 系统，请在用于创建 [`PixelStreaming`](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/blob/master/Frontend/library/src/PixelStreaming/PixelStreaming.ts) 流的 [`Config`](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/blob/master/Frontend/library/src/Config/Config.ts) 对象中设置以下属性。

| 属性 | 默认值 | 描述 |
| --- | --- | --- |
| `Flags.AFKDetection` | `false` | 决定是否启用 AFK 系统来检查用户交互。 |
| `NumericParameters.AFKTimeoutSecs` | `120` | 设置用户离开键盘后，播放器小部件中显示警告覆盖层前的最大时间间隔，单位为秒。 |
| `NumericParameters.AFKCountdown` | `10` | 设置在用户未及时响应时，流被终止前的倒计时持续时间，单位为秒。 |

例如，要启用 AFK 检测并设置为在五分钟后生效，您可以在实现中执行以下操作：

```typescript
const config = new Config({ useUrlParams: true });
config.setFlagEnabled(Flags.AFKDetection, true);
config.setNumericSetting(NumericParameters.AFKTimeoutSecs, 300);
config.setNumericSetting(NumericParameters.AFKCountdown, 60);

const stream = new PixelStreaming(config);
```

**_Tip:_**
如果您想自定义覆盖层的内容，可以替换 [`AFKOverlay`](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/blob/master/Frontend/ui-library/src/Overlay/AFKOverlay.ts) 类。然后 您还需要扩展 [`Application`](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/blob/master/Frontend/ui-library/src/Application/Application.ts) 类才能使用新的覆盖层。
