## 从 UE5 向玩家页面发送消息

您可以让 Unreal Engine 应用程序向所有连接的玩家 HTML 页面发送自定义事件，玩家页面的 JavaScript 环境可以对这些事件作出响应。这使得您可以根据游戏事件在网页 UI 中做出相应的改变。

设置步骤如下：

1. 在您的 Unreal Engine 应用程序中，每次您想向玩家页面发送事件时，您需要一个带有 **Pixel Streaming Input** 组件的 Actor。该组件可以访问 **Send Pixel Streaming Response** 节点。通过该节点指定一个自定义字符串参数，以向网页前端发送消息。

<p align="center">
    <img src="Resources/Images/pixelstreaming-send-game-event.png" alt="发送游戏事件">
</p>

2. 在您的 TypeScript 前端实现中，这些消息将被一个事件监听器接收。每当前端从 Unreal Engine 应用程序接收到自定义消息时，该事件将被触发。传递给 **Send Pixel Streaming Response** 节点的原始字符串参数将作为 `response` 参数传递给该函数。例如：

```typescript
	public myHandleResponseFunction(response: string) => void {
		Logger.Info(Logger.GetStackTrace(), "Response received!");
		switch (response) {
			case "MyCustomEvent":
				... // handle one type of event
			case "AnotherEvent":
				... // handle another event
		}
	}
```

3. 使用 `PixelStreaming` 对象提供的 `addResponseEventListener` 函数注册您的监听器函数，该对象位于 PixelStreaming/PixelStreaming.ts 中。您需要传递一个唯一的名称给您的事件监听器，以及您的函数。例如：

        addResponseEventListener("handle_responses", myHandleResponseFunction);

4. 如果您需要移除您的事件监听器，请调用 `removeResponseEventListener` 并传递相同的名称。例如：

        removeResponseEventListener("handle_responses");

**_提示:_**  
如果您需要传递更复杂的数据，可以将传递给 **Pixel Streaming Input -> Send Pixel Streaming Response** 节点的字符串格式化为 JSON。例如：

<p align="center">
    <img src="Resources/Images/pixelstreaming-send-game-event-json.png" alt="使用 JSON 发送 Pixel Streaming 响应">
</p>

然后，在您的响应事件处理函数中，使用 `JSON.parse(data)` 将字符串解码回 TypeScript 对象。

