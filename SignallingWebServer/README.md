# Wilbur

这是 `cirrus` 的直接替代版本。

Wilbur 是一个位于 `streamers` 和其他 peers 之间的小型中间应用。它负责处理初始连接协商，以及部分小规模的往返控制消息，同时也充当一个简单的 Web 服务器，用于提供 [Frontend](/Frontend/README.md) Web 应用。

和旧版 `cirrus` 在行为上的差异见[这里](from_cirrus.md)。

---

## 构建（Building）
本项目使用 `npm` 和 `tsc` 进行构建。然而，最简单的方法是运行：
```
.\SignallingWebServer\platform_scripts\cmd\start.bat --dev
```

这将安装并构建所有所需组件。

---

## 手动构建

如果你想自行手动构建（或使用其它配置进行构建），可以在以下目录分别执行：
```bash
npm install
npm run build
# 或 npm run build-dev
```

依次在 `/common`, `/Signalling`, 和 `/SignallingWebServer` 目录下运行（顺序非常重要）。

这些命令会将构建结果输出到各自的 build 或 dist 目录中。

运行（Running）
构建好服务器后，你可以通过 node 或 npm start 脚本来运行它。
```
npm start -- [arguments]
```
or
```
node build/index.js [arguments]
```
执行 `npm start -- --help` or `node build/index.js --help` 将显示可用的配置选项：
```
用法：node build/index.js [options]

一个用于 Unreal Engine Pixel Streaming 应用的基础信令服务器。

可选项（Options）：
  -V, --version                     输出版本号
  --log_folder <path>               设置日志文件的存储路径。（默认: "logs"）
  --log_level_console <level>       设置控制台日志的级别。（可选: "debug", "info", "warning", "error"，默认: "info"）
  --log_level_file <level>          设置日志文件的级别。（可选: "debug", "info", "warning", "error"，默认: "info"）
  --console_messages [detail]       在控制台显示接收和发送的信令消息。（可选: "basic", "verbose", "formatted"，若仅加此选项则为 "basic"）
  --streamer_port <port>            设置用于 Streamer（推流端）连接的侦听端口。（默认: "8888"）
  --player_port <port>              设置用于 Player（播放端）连接的侦听端口。（默认: "80"）
  --sfu_port <port>                 设置用于 SFU（Selective Forwarding Unit）连接的侦听端口。（默认: "8889"）
  --serve                           在 player_port 上启动 Web 服务器。（默认: false）
  --http_root <path>                设置 Web 服务器的根路径。（默认: "www"）
  --homepage <filename>             指定在 Web 服务器上提供的默认主页文件名。（默认: "player.html"）
  --https                           在 https_port 上启用 Web 服务器及 SSL。（默认: false）
  --https_port <port>               设置 HTTPS 服务器的侦听端口。（默认: 443）
  --ssl_key_path <path>             设置 SSL 密钥文件的路径。（默认: "certificates/client-key.pem"）
  --ssl_cert_path <path>            设置 SSL 证书文件的路径。（默认: "certificates/client-cert.pem"）
  --https_redirect                  启用对 HTTP 连接的重定向至 HTTPS。如果不设置此项，Web 服务器只在 https_port 上侦听。  
                                    注：Player 的 WebSockets 仍会侦听在 player_port。（默认: false）
  --rest_api                        启用可通过 <server_url>/api/api-definition 访问的 REST API 接口。（默认: false）
  --peer_options <json-string>      在配置信息（config message）的 peerConnectionOptions 中添加额外的 JSON 数据。
  --log_config                      启动时打印程序配置。（默认: false）
  --stdin                           允许在运行时通过标准输入（stdin）交互。（默认: false）
  --no_config                       跳过读取配置文件，仅使用命令行参数。（默认: false）
  --config_file <path>              指定配置文件的路径。（默认: "config.json"）
  --save                            解析完命令行参数后，将相关参数保存进 config.json。（默认: false）
  -h, --help                        显示此帮助文本。

```
也可以在 `config.json` （默认为 config.json，可通过 --config_file 指定） 中使用 JSON 格式来描述这些 CLI 配置选项。例如：
```
{
	"log_folder": "logs",
	"log_level_console": "info",
	"log_level_file": "info",
	"streamer_port": "8888",
	"player_port": "80",
	"sfu_port": "8889",
	"serve": true,
	"http_root": "www",
	"homepage": "player.html",
	"log_config": false,
	"stdin": false
}
```
给定这些选项，如果想让服务器的行为尽可能接近旧的 cirrus，可以执行：
```
npm start -- --console_messages --https_redirect verbose --serve --log_config --http_root Public --homepage player.html
```
注意这里使用 `Public` 作为 http root 假设你的前端位于该目录，沿用旧脚本的目录布局。而新的便捷脚本 (`platform_scripts` 目录下) 现在会将构建后的前端放在 `www` 目录中。

## 开发 Development
该实现基于 [Signalling](../Signalling) 库，它以库的形式提供用于开发信令应用的功能。更多信息参见该库的 [documentation](../Signalling/docs) .

### 自签名证书 Self-signed certificates
在开发中，可能需要使用自签名证书（例如某些功能如 XR、麦克风等需要 HTTPS 才能正常工作）。可按照以下步骤生成自签名证书：

1. 进入 `SignallingWebServer` 目录.
2. 创建一个名为 `certificates` 的子目录.
3. 打开 Git Bash 或你喜欢的 shell。
4. Run `openssl req -x509 -newkey rsa:4096 -keyout client-key.pem -out client-cert.pem -sha256 -nodes`
5. 确保你的 `config.json` 文件包含以下内容：

```json
"ssl_key_path": "certificates/client-key.pem",
"ssl_cert_path": "certificates/client-cert.pem",
```

## 更多文档 Further Documentation
- [Protocol Messages](../Common/docs/messages.md)
- [Protocol Negotiation](../Signalling/docs/Protocol.md)

