## 自定义播放器小部件样式

前端应用程序的CSS样式通过[`PixelStreamingApplicationStyle`](/Frontend/ui-library/src/Styles/PixelStreamingApplicationStyles.ts)对象在页面加载时应用，然后使用`PixelStreamingApplicationStyle.applyStyleSheet`方法将其应用到页面。在创建并将应用程序对象添加到页面之前，必须在实现中调用此方法。

与其修改或扩展`PixelStreamingApplicationStyle`类，不如将一个包含所需CSS选项的对象传递给构造函数，并为浅色模式和深色模式分别提供不同的基础色调调色板（默认样式广泛使用）。可以通过使用`setColorMode`方法选择浅色模式或深色模式，或通过调用`applyPalette`并传递自定义的`ColorPalette`来进一步自定义基础色调调色板。

该系统将覆盖实现HTML页面中任何现有的CSS，因此建议使用此方法，以实现与前端基础设施的最干净的互操作性。