# 从 Cirrus 迁移到 Wilbur 的指南

这里简要说明了已弃用的 `cirrus` 信令服务器与新的 `wilbur` 信令服务器之间的差异。

- 服务器配置可通过命令行参数（CLI options）或 `config.json` 文件中的相同参数进行设置
- 默认情况下，Web 服务功能是禁用的，需要通过指定 `--serve` 来启用
- `platform_scripts` 目录下的便捷脚本会自动加上 `--serve`，并尽量再现旧版 `cirrus.js` 的行为
- 使用便捷脚本时，前端将会构建到 `www` 目录下，而不是以前的 `Public`
- 消息现在使用 [Common](../Common/protobuf/signalling_messages.proto) 库中的 protobuf 定义
- 服务器基于 [Common](../Common) 库构建，该库可供开发者自行编写自定义应用
- 来自 `wilbur` 的日志现以结构化 JSON 形式输出，便于被外部工具读取和分析
- 默认情况下，不会在终端中回显收发的消息；可使用 `--console_messages` 参数控制此行为
- 如果你删除了 `config.json`，它不会被自动重新创建；若需要根据当前参数自动生成 `config.json`，可以使用 `--save`
