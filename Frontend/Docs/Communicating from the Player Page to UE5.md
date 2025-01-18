## 从玩家页面与 UE5 通信

前端提供了三个函数，您可以在 HTML 播放器页面中调用这些函数，以允许用户从浏览器向 Unreal Engine 应用程序传递事件和命令：

*   `emitCommand` 允许以 JSON 对象的形式向游戏发送任意命令。
*   您可以使用 `emitConsoleCommand` 向 Unreal Engine 发送控制台命令。例如，`stat fps` 显示帧率。请参见 [下面的使用 emitCommand 函数](#using-the-emitcommand-function)。
*   `emitUIInteraction` 发送任意字符串或对象到游戏。使用此函数从您的玩家 UI 向游戏发送自定义命令，您可以在游戏逻辑中响应这些命令，以在应用程序中产生任何所需的效果。请参见 [下面的使用 emitUIInteraction 函数](#using-the-emituiinteraction-function)。

### 使用 emitCommand 函数

当您调用 `emitCommand` 函数时，您传递给它一个对象，该对象会被转换为 JSON 并发送到游戏。然后，您可以使用它来实现任何您需要的自定义功能。

#### 保留关键字

虽然您可以根据自己的需要自由组织命令，但如果对象包含以下保留关键字之一，它将由 PixelStreaming 模块解释：

*   `ConsoleCommand` - 使用此关键字在远程 Unreal Engine 应用程序上执行控制台命令。该关键字的值应为一个字符串，包含您要运行的命令及其需要的任何参数。例如：

```typescript
	let descriptor = {
		ConsoleCommand: 'stat fps'
	}
	emitCommand(descriptor);
```

**_注意:_**  
由于 Unreal Engine 控制台命令的强大功能，`emitConsoleCommand` 函数可能带来安全风险。为了使此功能正常工作，您还需要在启动 Unreal Engine 应用程序或通过 Unreal 编辑器的独立游戏选项启动时，在命令行中提供 `-AllowPixelStreamingCommands` 参数。

### 使用 emitConsoleCommand 函数

您还可以使用 `emitConsoleCommand` 以字符串的形式传递 Unreal Engine 控制台命令。与通过 `emitCommand` 传递命令类似，您必须在命令行中提供 `-AllowPixelStreamingCommands`，才能使这些命令生效。

### 使用 emitUIInteraction 函数

当您调用 `emitUIInteraction` 函数时，您可以传递一个字符串或对象。例如：

```typescript
	emitUIInteraction("MyCustomCommand");
```

or

```typescript
	const descriptor = {
		LoadLevel: "/Game/Maps/Level_2",
		PlayerCharacter: {
			Name: "Shinobi",
			Skin: "Dynasty",
		},
	};
	this.stream.emitUIInteraction(descriptor);
```

如果您传递一个对象，`emitUIInteraction` 函数会将其内部转换为 JSON 字符串。然后，它将结果字符串传回 Unreal Engine 应用程序中的 Pixel Streaming 插件，该插件会在输入控制器上引发一个事件。在您的游戏逻辑中，您可以绑定自己的自定义事件来处理这些输入，使用 **Pixel Streaming Input > Bind Event to On Input Event** 节点。例如：

<p align="center">
    <img src="Resources/Images/pixelstreaming-ui-interaction-event.png" alt="绑定事件到输入事件">
</p>

您只需要在游戏开始时绑定此事件。每次任何连接到您的 Unreal Engine 应用程序实例的玩家 HTML 页面调用 `emitUIInteraction` 函数时，您的自定义事件将自动触发，无论传递给 `emitUIInteraction` 的输入是什么。

您分配的自定义事件（例如，图中 **UI Interaction** 节点）具有一个名为 **Descriptor** 的输出，您可以使用它来检索 `emitUIInteraction` 函数发送到 Unreal Engine 应用程序的字符串。您可以使用该值来确定每次调用 `emitUIInteraction` 时，游戏代码需要如何响应。

例如，以下 Blueprint 测试输入给 `emitUIInteraction` 的字符串是否包含 "MyCustomCommand"，并调用一个自定义函数来处理该事件：

<p align="center">
    <img src="Resources/Images/pixelstreaming-ui-interaction-search-substring.png" alt="搜索子字符串">
</p>

如果您最初传递了一个 JavaScript 对象到 `emitUIInteraction`，您可以使用 **Pixel Streaming > Get Json String Value** 节点来检索该 JSON 对象中任何键的值。例如，以下 Blueprint 测试名为 LoadLevel 的键是否存在。如果存在，则调用一个自定义函数来处理该事件：

<p align="center">
    <img src="Resources/Images/pixelstreaming-ui-interaction-extract-json.png" alt="获取 JSON 字段值">
</p>

**_提示:_**  
如果您需要检索嵌套的键，请使用 TypeScript 中常见的点号表示法来表示您的键。例如，`PlayerCharacter.Name` 或 `PlayerCharacter.Skin`。


