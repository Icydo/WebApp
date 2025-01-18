## 配置库行为

前端库通过 [Config](/Frontend/library/src/Config/Config.ts) 类公开了多个配置选项。这些选项的值可以被修改，以调整前端的一些内置行为。

以下是可用于自定义输入的前端库配置选项：

|       属性        | 默认值  | 描述 |
|         ---       |   ---  |     ---     |
|   HoveringMouseMode  |  false  | 决定是否在玩家与小部件交互时，视频元素捕获并锁定鼠标。当启用时，鼠标光标悬停在播放器小部件上而不与其交互。为了将鼠标移动传递到 Unreal Engine 应用程序的输入控制器，用户需要点击并按住鼠标左键。否则，点击播放器小部件会导致其捕获并锁定鼠标光标。任何进一步的鼠标移动将立即传递给 Unreal Engine 应用程序的输入控制器。这通常允许用户通过简单地拖动鼠标来移动和旋转相机。要释放光标的控制，用户可以按 **Esc** 键。 |
|  SuppressBrowserKeys  |   true  | 启用此设置时，播放器小部件会拦截功能键（**F1** 到 **F12**）和 **Tab** 键，并将这些按键事件传递给 Unreal Engine 应用程序，而不是允许浏览器正常处理它们。例如，启用此设置时，按 **F5** 将不会刷新浏览器中的播放器页面。相反，该事件会传递给 Unreal Engine 应用程序，并执行其通常的功能，即切换视图以可视化着色器复杂度。 |
| FakeMouseWithTouches  |  false  | 启用此选项后，当用户在具有触摸屏的设备（如智能手机或平板电脑）上查看流时，此设置会将单指触摸事件解释为 Unreal Engine 应用程序中的鼠标点击和拖动事件。启用此设置可以让移动设备上的用户部分控制 Unreal Engine 应用程序，即使应用程序的输入控制器并未专门处理触摸输入事件。 |
|   UseMic  |  false  | 指示是否应创建带有麦克风音轨的流，并将其发送到 UE 应用程序。可以使用 [`UPixelStreamingAudioComponent`](https://docs.unrealengine.com/5.0/en-US/API/Plugins/PixelStreaming/UPixelStreamingAudioComponent/) 来监听该麦克风音轨。如果启用此标志，将创建麦克风音轨（如果浏览器设置允许）并主动发送音频。为了节省带宽或实现其他功能，可以通过调用 `PixelStreaming` 的 `muteMicrophone` 来静音麦克风音轨，并稍后通过 `unmuteMicrophone` 重新启用它。如果创建 `PixelStreaming` 对象时没有启用此标志，可以稍后通过调用 `unmuteMicrophone(true)` 启用它，这将使用 `forceEnable` 参数添加音轨并触发完整重新连接（这是一个较重的操作，需要一些时间）。 |
|   UseCamera  |  false  | 指示是否应创建带有视频音轨的流，并将其发送到 UE 应用程序。可以使用 `UPixelStreamingVideoComponent` 来监听该视频音轨。如果启用此标志，将创建摄像头视频音轨（如果浏览器设置允许）并主动发送视频。为了节省带宽或实现其他功能，可以通过调用 `PixelStreaming` 的 `muteCamera` 来静音视频音轨，并稍后通过 `unmuteCamera` 重新启用它。如果创建 `PixelStreaming` 对象时没有启用此标志，可以稍后通过调用 `unmuteCamera(true)` 启用它，这将使用 `forceEnable` 参数添加视频音轨并触发完整重新连接（这是一个较重的操作，需要一些时间）。 |

在创建前端实现时，这些选项可以通过创建 [`PixelStreaming`](/Frontend/library/src/PixelStreaming/PixelStreaming.ts) 流所需的 [`Config`](/Frontend/library/src/Config/Config.ts) 对象来访问。只需在初始化流对象之前设置您需要的值即可。

```typescript
	const config = new Config({ useUrlParams: true });
	config.setFlagEnabled(Flags.HoveringMouseMode, true);
	config.setFlagEnabled(Flags.FakeMouseWithTouches, true);

	const stream = new PixelStreaming(config);
```

### 禁用用户输入

可以完全禁用一种或多种输入设备的用户输入。此操作由以下输入标志控制，默认情况下所有标志都启用。

*   **MouseInput**  - 允许鼠标输入事件。
*   **KeyboardInput**  - 允许键盘输入事件。
*   **TouchInput**  - 允许移动设备和平板电脑上的触摸事件。
*   **GamepadInput**  - 允许游戏手柄控制器的输入事件。
*   **XRControllerInput**  - 允许来自 XR 控制器的输入事件，用于增强现实（AR）和虚拟现实（VR）设置。

例如，您可以在 `Config` 对象中将所有这些标志设置为 `false`，以完全阻止用户输入。
```typescript
	const config = new Config({ useUrlParams: true });
	config.setFlagEnabled(Flags.MouseInput, false);
	config.setFlagEnabled(Flags.KeyboardInput, false);
	config.setFlagEnabled(Flags.TouchInput, false);
	config.setFlagEnabled(Flags.GamepadInput, false);
	config.setFlagEnabled(Flags.XRControllerInput, false);

	const stream = new PixelStreaming(config);
```

