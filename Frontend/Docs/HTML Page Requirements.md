## HTML页面要求

最终出现在页面上的大部分HTML实际上是由Pixel Streaming应用程序本身引入的。多个示例HTML页面在[示例实现](/Frontend/implementations/typescript/src)中提供，您可以看到基础页面非常简洁，唯一的作用是为应用程序提供一个附加空间，并将其填充。唯一的具体要求是确保被附加的元素占据足够的空间，以便视口在屏幕上可见。在示例实现中，这只是一个设置为填充屏幕且不滚动的`<body>`标签。

```html
<!-- Copyright Epic Games, Inc. All Rights Reserved. -->
<!DOCTYPE html>
<html style="width: 100%; height: 100%">

<head>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
</head>

<!-- Pixel Streaming播放器填充其父元素的100%，但`body`元素的高度默认为0px，除非被内容填充。因此，我们明确强制`body`的高度为视口的100%。 -->
<body style="width: 100vw; height: 100vh; min-height: -webkit-fill-available; font-family: 'Montserrat'; margin: 0px">

</body>

</html>
```

正如在[示例实现](/Frontend/implementations/typescript/src/player.ts)中所见，您必须指定Pixel Streaming视口要附加到页面上的哪个元素。在示例实现中，通常是在`document.body.onload`事件监听器中完成此操作，在这种情况下，它被附加到DOM中的`document.body`元素，从而使其填充整个页面。

[//]: # (这一步尚未完成)
### 播放器文件位置和URL

您有几种选择来放置自定义HTML播放器页面，以及客户端浏览器如何访问它。

* 您可以创建一个新的实现页面，并将其放置在[`/Frontend/implementations/typescript/src/`](/Frontend/implementations/typescript/src)中，和示例实现一起。这必须包含一个基础的`.html`页面和您的应用程序入口点的`.ts`源文件。然后，您可以通过将`html`文件名附加到运行信令服务器的计算机的IP地址或主机名来访问该页面。例如，示例的`stresstest`页面可以通过在本地运行的基础设施访问，URL为`http:/127.0.0.1/stresstest.html`。
* 您可以自定义信令和Web服务器的`HomepageFile`参数，并设置自定义HTML播放器页面的文件路径，相对于[Frontend实现源文件夹](/Frontend/implementations/src)。然后，当访问运行信令和Web服务器的计算机的IP地址或主机名时，就可以访问该页面。
* 您还可以使用信令和Web服务器的**AdditionalRoutes**参数来自定义URL路径与计算机本地文件夹之间的映射。

### 构建前端
启动基础设施信令服务器时，前端应该会自动构建。如果没有，您可以运行[`setup_frontend`](/SignallingWebServer/platform_scripts/)脚本来进行构建。如果之后对本地副本的前端进行了更改，您需要再次运行该脚本，并添加`--build`参数以强制重新构建。

