# Pixel Streaming Selective Forwarding Unit

SFU（Selective Forwarding Unit）是一种允许将单个流分发给大量客户端的机制。这样做的好处是，当客户端直接连接到推流端（Streamer）时，需要为每个客户端分配相应资源来进行流的编码，资源在同时连接的用户一多时就会耗尽。而使用 SFU 可以在无需重新编码的情况下，利用 simulcast 接收来自 Streamer 的多路流，并基于远端客户端（Player）的可用网络和设备资源来选择性转发特定码率的流。

---

## 配置（Configuration）

SFU 的所有配置都在一个 `config.js` 文件中完成。

| 名称 | 类型 | 默认值 | 描述 |
| --- | --- | --- | --- |
| signallingURL | String | 'http://localhost:8889' | 指向要连接的信令服务器（signalling server）的 URL。 |
| SFUId | String | 'SFU' | 本 Peer 的名称，Streamer 列表中会显示该名称。需要从该 SFU 接收流的 peers 应该订阅此 ID。 |
| subscribeStreamerId | String | 'DefaultStreamer' | SFU 应该订阅并转推的 Streamer 的名称。 |
| retrySubscribeDelaySecs | Number | 10 | 如果订阅指定的 Streamer 失败，等待多少秒再尝试。 |
| mediasoup | Object | | 与 mediasoup 相关的配置，详见下文。 |

### Mediasoup 相关配置

| 名称 | 类型 | 默认值 | 描述 |
| --- | --- | --- | --- |
| worker | Object | | 与 worker 相关的配置，见下文。 |
| router | Object | | 与 router 相关的配置，见下文。 |
| webRtcTransport | Object | | 与 WebRTC transport 相关的配置，见下文。 |

#### worker 相关配置

| 名称 | 类型 | 默认值 | 描述 |
| --- | --- | --- | --- |
| rtcMinPort | Number | 40000 | ICE、DTLS、RTP 等使用的最小端口号。 |
| rtcMaxPort | Number | 49999 | ICE、DTLS、RTP 等使用的最大端口号。 |
| logLevel | String | 'debug' | worker 的日志级别，详见 [Mediasoup 文档](https://mediasoup.org/documentation/v3/mediasoup/api/#WorkerLogLevel)。 |
| logTags | Array<WorkerLogTag> | | 在日志中包含的标记，详见 [Mediasoup 文档](https://mediasoup.org/documentation/v3/mediasoup/api/#WorkerLogTag)。 |

#### router 相关配置

| 名称 | 类型 | 默认值 | 描述 |
| --- | --- | --- | --- |
| mediaCodecs | Array<RtpCodecCapability> | | 要支持的编解码器列表，详见 [Mediasoup 文档](https://mediasoup.org/documentation/v3/mediasoup/rtp-parameters-and-capabilities/#RtpCodecCapability)。 |

#### WebRTC transport 相关配置

| 名称 | 类型 | 默认值 | 描述 |
| --- | --- | --- | --- |
| listenIps | Array<TransportListenIp\|String> | | 按优先顺序指定监听的 IP 地址列表（第一个为首选）。详见 [Mediasoup 文档](https://mediasoup.org/documentation/v3/mediasoup/api/#TransportListenIp)。 |
| initialAvailableOutgoingBitrate | Number | | 初始可用的发送比特率（bps）。 |

---

## 运行（Running）

在 [platform_scripts](platform_scripts/) 文件夹中提供了若干适用于 Windows 和 Linux 的脚本。这些脚本适用于常见场景，可轻松启动服务器。同时也可用作自定义环境配置的参考。

---

## 从 UE 推流（Streaming from UE）

若要充分利用 SFU 的能力，推荐做法是让单个 Streamer 使用 simulcast 将多路流推给 SFU，然后让各客户端（Player）订阅从 SFU 推送的流。

可以在启动 UE 应用时加入以下参数：

`-SimulcastParameters="1.0,5000000,20000000,2.0,1000000,5000000,4.0,50000,1000000"`

该参数会告诉 Pixel Streaming 插件启用 3 路 simulcast 流，每一路均会缩放一半的分辨率。参数的取值顺序依次为：  

`scale_down_factor,min_bitrate,max_bitrate,...repeating for each stream`

SFU 接收到这 3 路流后，会根据每个客户端的连接质量来选择推送最合适的流给它们。

---

## 在 Docker 中运行（Running the Docker image）

Docker 镜像需要知道要连接的信令服务器地址。你需要将 `SIGNALLING_URL` 环境变量设置为指向你的信令服务器的 URL，该 URL 指向已配置好的 SFU 端口（默认 8889）。

另外还需要使用 Docker 的 `host` 网络驱动，因为 SFU 会收集并上报自己的可用端口以进行数据交互。例如：

```bash
docker run -e SIGNALLING_URL=ws://192.168.1.10:8889 --network="host" ghcr.io/epicgames/pixel-streaming-sfu:5.4
