# @epicgames-ps/lib-pixelstreamingsignalling

一个用于开发者实现 Pixel Streaming 应用信令功能的库。

---

## 构建（Building）

要构建 `Signalling` 模块，需要在 `Common` 和 `Signalling` 目录下分别执行以下命令：

```bash
npm install
npm run build-all
# 或 npm run build
```

此操作会在各自的目录下生成 `/dist` or `/build` output directory.

**Note:** 如果你只是想让一个信令服务器（signalling server）跑起来，请参考 ["Getting Started"](../README.md#getting-started)

### 库的构建方式 How this library is built
该 NPM 包支持：
- ES6 module usage
- CommonJS usage
- Type definitions
- Source maps

## Documentation

- [Protocol Notes](docs/Protocol.md)
- [Protocol Messages](../Common/docs/messages.md)

The API documentation is [here](docs/) and covers details of all exported components of the library.

