## 访问 Pixel Streaming Blueprint API

运行在 Unreal Engine 内的 Pixel Streaming 插件暴露了一个 Blueprint API，您可以在游戏逻辑中使用它来处理由玩家 HTML 页面发送的自定义 UI 事件，并从 Unreal Engine 向玩家页面发送事件。

要访问这个 Blueprint API，请将 **PixelStreamingInputComponent** 添加到您关卡中的一个 Actor。您的应用程序中的 **PlayerController** 是一个安全的选择。您可以通过在 Blueprint 菜单中点击 **Add Component** 并从下拉菜单中选择 **Pixel Streaming Input** 组件来完成这一操作。

<p align="center">
    <img src="Resources\Images\pixelstreaming-add-component.jpg" alt="添加 Pixel Streaming 组件">
</p>

**_注意:_** 在 UE 4.27 之前，PixelStreamingInput 组件在加载 Pixel Streaming 插件时会自动添加。这存在一些问题，现在要求用户按照上述方式手动将其添加到项目中。
