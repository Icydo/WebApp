# Pixel Streaming Infrastructure 更新日志

该更新日志汇总了 Unreal Engine 不同版本发布之间的提交记录。

请注意，本仓库内的每个 UE-X 分支/标签都对应一个特定的 Unreal Engine 版本。

---

## [UE 5.5（当前）](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/commits/UE5.5)

### 主要说明：Pixel Streaming 2 发布
- 通过 [PR #305](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/305)（@DenisTensorWorks 提交），添加了迁移指南和 Pixel Streaming 2 的发布说明

### 新增功能
- 通过 [PR #251](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/251)（@Belchy06 提交）添加了双向视频支持
- 通过 [PR #258](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/258)（@Belchy06 提交）在 SFU 中添加了 SVC（可分级视频编码）支持
- 通过 [PR #266](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/266)（@mcottontensor 提交）添加了 JS Streamer 和前端测试
- 通过 [PR #284](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/284)（@gingernaz 提交）为 Pixel Streaming 2 添加了 `DataChannel` 多路复用支持
- 通过 [PR #205](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/205)（@mcottontensor 提交）添加了一个 GitHub Action，用于运行软件版流推送测试以验证流能正常启动
- 通过 [PR #233](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/233)（@mcottontensor 提交）添加了针对 Linux 流测试的 GitHub Action
- 通过 [PR #160](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/160)（@mcottontensor 提交）移除了 matchmaker
- 通过 [PR #212](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/212)（@mcottontensor 提交）移除了浏览器“发送 offer”支持

### 改进
- 通过 [PR #90](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/90)（@mcottontensor 提交）更新了 GitHub Actions 构建脚本
- 通过 [PR #126](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/126)（@mcottontensor 提交）更新了平台脚本，使其在不需要构建时能跳过
- 通过 [PR #134](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/134)（@mcottontensor 提交）重构了 GH 工作流程
- 通过 [PR #151](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/151)（@mcottontensor 提交）进行了多项脚本更新
- 通过 [PR #152](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/152)（@mcottontensor 提交）添加了一个钩子，用于处理 `layerPreference` 消息并将其转发给 SFU
- 通过 [PR #152](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/152)（@mcottontensor 提交）为 `layerPreference message` 添加了测试
- 通过 [PR #198](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/198)（@mcottontensor 提交）添加了缺失的 WebSocket 关闭代码及原因
- 通过 [PR #199](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/199)（@mcottontensor 提交）使 URL 参数不再区分大小写
- 通过 [PR #210](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/210)（@mcottontensor 提交）简化了 Windows 下对 Node 的路径修改
- 通过 [PR #214](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/214)（@lukehb 提交）在 iPhone 上禁用显示全屏按钮
- 通过 [PR #218](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/218)（@mcottontensor 提交）更新了发布归档时排除的文件列表
- 通过 [PR #238](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/238)（@Belchy06 提交）为隐藏输入框设置默认行内样式
- 通过 [PR #240](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/240)（@lukehb 提交）将 `--no-save` 参数改为 `--save` 以避免覆盖 `config.json` 的混淆，并添加了默认 `config.json`
- 通过 [PR #244](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/244)（@lukehb 提交）添加了关于 streamer 断开连接的日志
- 通过 [PR #247](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/247)（@pr0g 提交）为 `AFKTimeout` 添加了可配置的倒计时值
- 通过 [PR #248](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/248)（@lukehb 提交）启用对 flexfec、ulpfec 以及其他非视频类视频编解码器的显示
- 通过 [PR #253](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/253)（@mcottontensor 提交）向 linter 规则中添加了 `prettier`
- 通过 [PR #261](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/261)（@mcottontensor 提交）为 `Common`、`Signalling`、`SignallingWebServer` 添加了 `prettier` 配置
- 通过 [PR #260](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/260)（@mcottontensor 提交）更新了 `keypress` 以使用助手函数来应对 `charCode` 弃用
- 通过 [PR #263](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/263)（@mcottontensor 提交）重构了 `Logger` 类
- 通过 [PR #275](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/275)（@mcottontensor 提交）重构了输入代码
- 通过 [PR #277](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/277)（@mcottontensor 提交）在 answer 消息中添加了最小和最大码率
- 通过 [PR #288](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/288)（@mcottontensor 提交）添加了为数值设置提供无最小值或无最大值的能力
- 通过 [PR #300](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/300)（@mcottontensor 提交）重新启用阻止未识别的 streamer 出现在 streamer 列表中的功能
- 通过 [PR #314](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/314)（@lukehb 提交）移除了 `uiless.html` 中对 signaling url 的冗余且固定的设置
- 通过 [PR #324](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/324)（@lukehb 提交）修复了在构建后的库中重复出现的源代码问题

### 文档
- 通过 [PR #124](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/124)（@mcottontensor 提交）为信令消息协议添加了文档
- 通过 [PR #129](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/129)（@lukehb 提交）更新了 RELEASING.md 中的分支链接

### Bug 修复
- 通过 [PR #114](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/114)（@mcottontensor 提交）更新了批处理脚本以正确处理带空格的路径，并更新了 peer connection 选项以正确传给信令服务器
- 通过 [PR #114](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/114)（@mcottontensor 提交）更新了信令服务器以正确将 peer connection options 添加到 config 消息
- 通过 [PR #122](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/122)（@lukehb 提交）修复了 Windows 平台脚本中的多个路径问题
- 通过 [PR #142](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/142)（@mcottontensor 提交）修复了脚本无法正确启动 TURN 服务器的问题
- 通过 [PR #148](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/148)（@mcottontensor 提交）修复了由于 `probator` track id 导致 SFU 在 Firefox 上无法正常工作的问题
- 通过 [PR #149](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/149)（@mcottontensor 提交）修复了在 Firefox 上 track 统计数据被设为零的问题
- 通过 [PR #167](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/167)（@richardFocus 提交）修复了动态玩家纵横比时可能出现 `NaN` 值的问题
- 通过 [PR #172](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/172)（@lukehb 提交）修复了 XR 立体视差以及不完整 XR 输入处理的问题
- 通过 [PR #177](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/177)（@lukehb 提交）恢复了从配置文件读取信令服务器配置和默认配置日志，并在 SSL 处理上添加了检查
- 通过 [PR #182](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/182)（@lukehb 提交）修复了配置文件和 CLI 参数的解析问题，确保 CLI 拥有优先级
- 通过 [PR #197](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/197)（@mcottontensor 提交）修复了流重启消息被遗漏或显示不正确的问题
- 通过 [PR #204](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/204)（@lukehb 提交）修复了在 Firefox 上 VPX 推流的问题
- 通过 [PR #213](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/213)（@lukehb 提交）修复了当导航栏出现时移动端 UI 无法正确缩放的问题
- 通过 [PR #235](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/235)（@rishi23root 提交）添加了缺失的 `track` 类型选项到 `RTCStatsTypePS`
- 通过 [PR #243](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/243)（@mcottontensor 提交）修复了对 `getUniqueLegacyId` 的无效引用
- 通过 [PR #271](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/271)（@mcottontensor 提交）修复了带虚拟摇杆的触摸问题
- 通过 [PR #282](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/282)（@Belchy06 提交）修复了 Pixel Streaming 2 中的演示统计按钮
- 通过 [PR #309](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/309)（@Belchy06 提交）修复了当 streamer 断开连接后 SFU 无法重新连接的问题
- 通过 [PR #323](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/323)（@lucastanger 提交）修复了 `TouchControllers` 函数重复添加同一事件监听器而不是移除的问题

### 安全
- 通过 [PR #144](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/144)（@dependabot 提交）在多个目录中更新了 npm_and_yarn 依赖
- 通过 [PR #147](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/147)（@dependabot 提交）在多个目录中更新了 npm_and_yarn 依赖
- 通过 [PR #154](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/154)（@dependabot 提交）在多个目录中更新了 npm_and_yarn 依赖
- 通过 [PR #262](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/262)（@dependabot 提交）在多个目录中更新了 npm_and_yarn 依赖
- 通过 [PR #279](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/279)（@dependabot 提交）在多个目录中更新了 npm_and_yarn 依赖
- 通过 [PR #283](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/283)（@dependabot 提交）在多个目录中更新了 npm_and_yarn 依赖
- 通过 [PR #285](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/285)（@dependabot 提交）在多个目录中更新了 npm_and_yarn 依赖
- 通过 [PR #302](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/302)（@dependabot 提交）在多个目录中更新了 npm_and_yarn 依赖
- 通过 [PR #303](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/303)（@dependabot 提交）在多个目录中更新了 npm_and_yarn 依赖
- 通过 [PR #267](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/267)（@dependabot 提交）在 `/Extras/JSStreamer` 中将 webpack 从 5.93.0 更新到 5.94.0
- 通过 [PR #237](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/237)（@Belchy06 提交）更新了 React 版本及其依赖

---

## [UE 5.4](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/commits/UE5.4)

### 新增功能
- 通过 [PR #452](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/452)（@Belchy06 提交）为非拉丁字符提供支持
- 通过 [PR #88](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/88)（@mcottontensor 提交）添加了隐藏 UI 的可选功能

### 改进
- 通过 [PR #362](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/362)（@mcottontensor 提交）将 NPM 库更新到了 5.4
- 通过 [PR #389](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/389)（@Belchy06 提交）更新了 SignallingWebServer 的平台脚本以支持 Mac
- 通过 [PR #397](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/397)（@timbotimbo 提交）在 `ui-library` 中公开了 JSS InsertionPoint
- 通过 [PR #409](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/409)（@bramford 提交）允许在无点击动作的情况下自动播放视频
- 通过 [PR #414](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/414)（@mcottontensor 提交）移除了认证功能
- 通过 [PR #416](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/416)（@mcottontensor 提交）修复了 Streamer 更换 ID 时出现的问题，并更新了 SFU 的多 streamer 行为
- 通过 [PR #419](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/419)（@mcottontensor 提交）重写了大量关于重连与断连处理的逻辑
- 通过 [PR #420](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/420)（@mcottontensor 提交）在浏览器中暴露了 pixelstreaming 接口
- 通过 [PR #425](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/425)（@mcottontensor 提交）在流启动时添加了码率协商
- 通过 [PR #431](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/431)（@mcottontensor 提交）为 SFU 添加了 Dockerfile
- 通过 [PR #434](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/434)（@evenstensberg 提交）删除了自动赋值属性
- 通过 [PR #441](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/441)（@alien299 提交）在 cirrus.js 中添加了更详细的错误消息，修复了 #184
- 通过 [PR #471](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/471)（@Belchy06 提交）对设置的显示顺序进行了重排序
- 通过 [PR #485](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/485)（@david-macpherson 提交）添加了 TCP+Relay 检测事件

### 文档
- 通过 [PR #361](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/361)（@MWillWallT 提交）将 Matchmaker 和 SFU 文档迁移至 Infra
- 通过 [PR #429](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/429)（@mcottontensor 提交）新增了文档
- 通过 [PR #448](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/448)（@alien299 提交）在 CONTRIBUTING.md 中添加了提交需验证签名的要求，解决了 #445
- 通过 [PR #474](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/474)（@DenisTensorWorks 提交）更新了版权/许可年份
- 通过 [PR #488](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/488)（@Ahhj93 提交）修复了 README 拼写错误

### Bug 修复
- 通过 [PR #25](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/25)（@david-macpherson 提交）修复了获取错误 ICE candidate pair 的问题
- 通过 [PR #86](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/86)（@zuvola 提交）为 probator 添加了 SDP
- 通过 [PR #372](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/372)（@Belchy06 提交）删除了 URL 带宽参数中的单位转换（URL 中已是 kbps）
- 通过 [PR #394](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/394)（@timbotimbo 提交）处理了 `statsPanel` 或 `settingsPanel` 未定义的情况
- 通过 [PR #406](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/406)（@mcottontensor 提交）为 matchmaker 在 Linux 环境下正常运行提供了修复
- 通过 [PR #427](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/427)（@mcottontensor 提交）修复了遗漏的函数重命名
- 通过 [PR #428](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/428)（@Belchy06 提交）更新了平台脚本，使 BASH_LOCATION 能在 Mac 上正常工作
- 通过 [PR #432](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/432)（@mcottontensor 提交）修复了当 streamer 晚于 ID 自报时留下的旧 streamer ID
- 通过 [PR #438](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/438)（@mcottontensor 提交）修复了在初始配置中对 StreamerId 的处理问题
- 通过 [PR #443](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/443)（@mcottontensor 提交）修复了一些信令服务器的小问题
- 通过 [PR #451](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/451)（@Belchy06 提交）修复了 `GamepadButtonReleased` 警告
- 通过 [PR #453](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/453)（@kroecks 提交）修复了 `build-all` 脚本依赖项问题
- 通过 [PR #472](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/472)（@Belchy06 提交）将 `NO_SUDO` 导出以使其在启动的进程中可用
- 通过 [PR #486](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/486)（@Belchy06 提交）修复了 iOS 上触摸事件无法正常工作的问题
- 通过 [PR #490](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/490)（@david-macpherson 提交）修复了 TCP Relay 事件多次触发的问题

### 安全
- 通过 [PR #37](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/37)（@dependabot 提交）将 `webpack-dev-middleware` 从 5.3.3 更新到 5.3.4（在 /Frontend/implementations/typescript）
- 通过 [PR #39](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/39)（@dependabot 提交）将 `webpack-dev-middleware` 从 5.3.3 更新到 5.3.4（在 /Frontend/implementations/react）
- 通过 [PR #41](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/41)（@dependabot 提交）将 `follow-redirects` 从 1.15.4 更新到 1.15.6（在 /Frontend/implementations/typescript）
- 通过 [PR #43](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/43)（@dependabot 提交）将 `follow-redirects` 从 1.15.4 更新到 1.15.6（在 /Frontend/implementations/react）
- 通过 [PR #65](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/65)（@dependabot 提交）将 `express` 从 4.18.2 更新到 4.19.2（在 /SignallingWebServer）
- 通过 [PR #70](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/70)（@dependabot 提交）将 `express` 从 4.18.2 更新到 4.19.2（在 /Matchmaker）
- 通过 [PR #73](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/73)（@dependabot 提交）将 `express` 从 4.18.2 更新到 4.19.2（在 /Frontend/implementations/typescript）
- 通过 [PR #79](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pull/79)（@dependabot 提交）将 `express` 从 4.18.2 更新到 4.19.2（在 /Frontend/implementations/react）
- 通过 [PR #380](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/380)（@dependabot 提交）将 `postcss` 从 8.4.21 更新到 8.4.31（在 /Frontend/implementations/typescript）
- 通过 [PR #386](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/386)（@dependabot 提交）将 `postcss` 从 8.4.21 更新到 8.4.31（在 /Frontend/implementations/react）
- 通过 [PR #388](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/388)（@dependabot 提交）将 `@babel/traverse` 从 7.21.3 更新到 7.23.2（在 /Frontend/library）
- 通过 [PR #465](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/465)（@dependabot 提交）将 `follow-redirects` 从 1.15.2 更新到 1.15.4（在 /Frontend/implementations/typescript）
- 通过 [PR #464](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/464)（@dependabot 提交）将 `follow-redirects` 从 1.15.2 更新到 1.15.4（在 /Frontend/implementations/react）

---

## [UE 5.3](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/commits/UE5.3)

### 新增功能
- 通过 [PR #336](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/336)（@Belchy06 提交）使协议结构现在可包含字符串
- 通过 [PR #358](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/358)（@mcottontensor 提交）添加了前端 peer 当有新的 streamer 可用时自动连接的功能

### 改进
- 通过 [PR #262](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/262)（@lukehb 提交）将 5.2 升级到 5.3，包括库、文档、日志消息、构建流水线等
- 通过 [PR #273](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/273)（@jibranabsarulislam 提交）在 create、reconnect、update 事件（以及相关测试）中增加了相关功能
- 通过 [PR #304](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/304)（@Belchy06 提交）添加了针对 PR 和 Issue 管理的 GitHub Action
- 通过 [PR #305](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/305)（@Belchy06 提交）更新了 stale.yml
- 通过 [PR #306](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/306)（@Belchy06 提交）更新了 stale 工作流程，可自动关闭过期的 issue 和 PR
- 通过 [PR #303](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/303)（@Belchy06 提交）在统计面板中显示玩家数量
- 通过 [PR #177](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/177)（@gunsha 提交）将 `implementations/EpicGames` 重命名为 `implementations/typescript`（修正 #166）
- 通过 [PR #337](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/337)（@Belchy06 提交）重构了 SignallingWebServer，使之只用一个 dockerfile
- 通过 [PR #340](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/340)（@Belchy06 提交）更新了 LatencyTest 处理器以接受输入数据
- 通过 [PR #352](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/352)（@DenisTensorWorks 提交）在仓库中添加了贡献指南 `CONTRIBUTING.md`
- 通过 [PR #211](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/211)（@kasp1 提交）为 matchmaker queue 提供了一个更易定制的新界面
- 通过 [PR #357](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/357)（@Belchy06 提交）在 CONTRIBUTING.md 中添加了 backport 规则

### 文档
- 通过 [PR #271](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/271)（@mcottontensor 提交）添加了信令消息参考文档
- 通过 [PR #288](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/288)（@mcottontensor 提交）更新了 SignallingProtocol.md

### Bug 修复
- 通过 [PR #285](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/285)（@mcottontensor 提交）修复了在页面刷新后自动重连仍会执行的问题
- 通过 [PR #274](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/274)（@Belchy06 提交）修复了当设置面板打开时 iOS 触摸失效的问题
- 通过 [PR #310](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/310)（@Belchy06 提交）修复了 Firefox 控制台错误 `TypeError: this.preferredCodec.split is not a function`
- 通过 [PR #316](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/316)（@StomyPX 提交）修复了触摸事件相对父级矩形的绝对定位问题
- 通过 [PR #332](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/332)（@StomyPX 提交）修复了向 SDP 注入新参数以在 Chrome 中恢复立体声的问题
- 通过 [PR #333](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/333)（@StomyPX 提交）修复了 matchmaker 要求进行操作系统认证而不是报 EACCESS 的问题
- 通过 [PR #354](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/354)（@StomyPX 提交）修复了在右键菜单事件触发时需要阻止发送 mouse up 的问题

### 安全
- 通过 [PR #290](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/290)（@dependabot 提交）在 /Frontend/library 中将 `tough-cookie` 从 4.1.2 更新到 4.1.3
- 通过 [PR #320](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/320)（@dependabot 提交）在 /Frontend/library 中将 `word-wrap` 从 1.2.3 更新到 1.2.4
- 通过 [PR #327](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/327)（@dependabot 提交）在 /Frontend/ui-library 中将 `word-wrap` 从 1.2.3 更新到 1.2.5
- 通过 [PR #321](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/321)（@StomyPX 提交）将 Node.js 升级到了最新 LTS 版本

---

## [UE 5.2](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/commits/UE5.2)

### 新增功能
- 通过 [PR #159](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/159)（@hmuurine 提交）添加了一个最简化的 React 示例
- 通过 [PR #158](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/158)（@lukehb 提交）为 Pixel Streaming Demo 示例项目添加了新的前端
- 通过 [PR #74](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/74)（@mcottontensor 提交）添加了对多 streamer 的支持
- 通过 [PR #68](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/68)（@StomyPX 提交）在 `InitialSettings` 消息中添加了对 `DefaultToHover` 配置选项的解析
- 通过 [PR #75](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/75)（@Belchy06 提交）在浏览器有意图发送 offer 时向信令服务器提供指示
- 通过 [PR #85](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/85)（@Belchy06 提交）为基于 WebXR 的体验添加了实验性支持

### 文档
- 通过 [PR #254](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/254)（@MWillWallT 提交）新增了通用文档页面/目录和新的安全页面
- 通过 [PR #248](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/248)（@mcottontensor 提交）在 README 中说明了容器镜像需要加入 Epic 的 Github 组织
- 通过 [PR #224](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/224)（@lukehb 提交）更新了 platform_scripts/readme.md 来解释不同脚本
- 通过 [PR #223](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/223)（@DenisTensorWorks 提交）改进了信令服务器的文档
- 通过 [PR #228](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/228)（@DenisTensorWorks 提交）为 UE5.2 添加了麦克风功能的文档
- 通过 [PR #208](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/208)（@DenisTensorWorks 提交）添加了麦克风功能文档
- 通过 [PR #254](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/254)（@MWillWallT 提交）在通用文档页面/目录和安全页面中添加了新的文档
- 通过 [PR #135](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/135)（@MWillWallT 提交）添加了设置面板文档
- 通过 [PR #90](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/90)（@MWillWallT 提交）添加了定制 Pixel Streaming Player 页面的文档
- 通过 [PR #223](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/223)（@DenisTensorWorks 提交）更新了信令服务器文档
- 通过 [PR #224](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/224)（@lukehb 提交）更新了前端文档，添加了关于 settings 和 TURN 的说明
- 通过 [PR #228](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/228)（@DenisTensorWorks 提交）添加了麦克风功能文档
- 通过 [PR #248](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/248)（@mcottontensor 提交）在 README 中说明容器镜像需要 Epic 的 Github 组织身份
- 通过 [PR #152](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/152)（@StomyPX 提交）更新了前端文档，将部分官方 UE 文档中的内容迁移到本仓库
- 通过 [PR #122](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/122)（@Belchy06 提交）更新了文档，移除了失效链接

### 改进
- 通过 [PR #265](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/265)（@lukehb 提交）在 readme.md 上添加了以 GitHub 徽章形式呈现的仓库健康状态
- 通过 [PR #266](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/266)（@Belchy06 提交）重新启用了在 iOS 和 iPadOS 上的全屏
- 通过 [PR #253](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/253)（@StomyPX 提交）将转发日志颜色改为青色，并在缺失 playerId 时添加了警告
- 通过 [PR #232](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/232)（@chasse20 提交）在聚合统计中添加了 “media-playout” 以防止日志刷屏
- 通过 [PR #238](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/238)（@devrajgadhvi 提交）在演示前端中添加了 `stat PixelStreamingGraphs`
- 通过 [PR #240](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/240)（@StomyPX 提交）在日志中添加了缺失 playerId 的警告（重复提及，可能是合并冲突导致）
- 通过 [PR #134](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/134)（@Belchy06 提交）在获取初始应用设置后强制 URL 参数
- 通过 [PR #149](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/149)（@marcinbiegun 提交）通过 Cirrus 配置支持传递 HTTPS 证书位置
- 通过 [PR #156](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/156)（@hmuurine 提交）为 library 添加了单元测试
- 通过 [PR #63](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/63)（@lukehb 提交）将前端的 JavaScript 转换为 TypeScript 并进行重构
- 通过 [PR #59](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/59)（@Senseme 提交）清理了无用代码，使代码风格更统一
- 通过 [PR #88](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/88)（@Belchy06 提交）改进了多 streamer 的使用体验
- 通过 [PR #91](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/91)（@mcottontensor 提交）在转发消息时移除了 player id
- 通过 [PR #94](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/94)（@Belchy06 提交）在检测到多个 streamer 时增加了提示
- 通过 [PR #102](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/102)（@lukehb 提交）为 webpack 添加了开发(dev)和生产(prod)配置
- 通过 [PR #103](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/103)（@lukehb 提交）添加了 GitHub Actions，用于创建前端库的 NPM 包并为仓库生成 release
- 通过 [PR #106](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/106)（@Belchy06 提交）美化了安装脚本
- 通过 [PR #229](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/229)（@devrajgadhvi 提交）在演示前端中添加了 `stat PixelStreamingGraphs`（重复提及）
- 通过 [PR #253](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/253)（@StomyPX 提交）修改了日志转发颜色并在缺失 playerId 时添加警告（重复提及）
- 通过 [PR #209](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/209)（@Belchy06 提交）允许继承 `webrtcPlayerController` 和 `webXrController`
- 通过 [PR #195](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/195)（@Belchy06 提交）更改了重连流程，以请求 streamer 消息列表并在多次尝试失败后放弃
- 通过 [PR #193](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/193)（@kass-kass 提交）为 UI 配置类型添加了导出
- 通过 [PR #161](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/161)（@kass-kass 提交）添加了可选地禁用前端某些元素的功能
- 通过 [PR #179](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/179)（@Belchy06 提交）添加了在使用 SFU 时按需切换 peer 层（分辨率层）的能力
- 通过 [PR #132](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/132)（@hmuurine 提交）改进了前端 API，用于支持与 UE 的交互
- 通过 [PR #136](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/136)（@hmuurine 提交）在前端中添加了启用/禁用用户输入设备的功能
- 通过 [PR #124](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/124)（@lukehb 提交）公开了 `websocketController` 和 `webXRController` 到公共 API
- 通过 [PR #125](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/125)（@lukehb 提交）添加了 XR 事件：`xrSessionStarted`, `xrSessionEnded`, `xrFrame`
- 通过 [PR #110](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/110)（@hmuurine 提交）让 UI 从前端库中解耦
- 通过 [PR #39](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/39)（@Mirmidion 提交）把日志路径从硬编码改为可参数传递

### Bug 修复
- 通过 [PR #247](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/247)（@mcottontensor 提交）修复了由于定时器调用异常而导致的视口重设大小不稳定问题
- 通过 [PR #246](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/246)（@mcottontensor 提交）修复了 URL 中设置的鼠标悬停模式在刷新后被覆盖的问题
- 通过 [PR #245](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/245)（@mcottontensor 提交）修复了 matchmaker 在信令服务器使用 https 时仍将用户导向 http 的问题
- 通过 [PR #215](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/215)（@Belchy06 提交）修复了当 afk 超时触发时仍会继续尝试重连的问题
- 通过 [PR #137](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/137)（@mcottontensor 提交）修复了使用 SFU 时 datachannel 无法工作的问题
- 通过 [PR #129](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/129)（@StomyPX 提交）修复了 SFU 中发生的 datachannel/stream id 冲突问题，改用 mediasoup 内部的 stream ids
- 通过 [PR #165](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/165)（@Belchy06 提交）修复了多个 peer 的 controller 索引会冲突的问题
- 通过 [PR #180](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/180)（@Belchy06 提交）修复了使用 5.2 前端连接到 5.1 应用时会崩溃的问题
- 通过 [PR #172](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/172)（@Belchy06 提交）修复了当 SFU 断开时，sfu player 仍尝试订阅的问题
- 通过 [PR #185](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/185)（@lukehb 提交）修复了压力测试器会留下一些孤立的 Pixel Streaming 连接的问题
- 通过 [PR #215](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/215)（@Belchy06 提交）修复了当 afk 超时触发时仍然尝试重连的问题（重复提及）
- 通过 [PR #247](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/247)（@mcottontensor 提交）修复了视口缩放不稳定的问题（重复提及）
- 通过 [PR #232](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/232)（@chasse20 提交）修复了在聚合统计中缺少 “media-playout” 导致的日志刷屏问题
- 通过 [PR #246](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/246)（@mcottontensor 提交）修复了刷新后鼠标悬停模式被覆盖的问题（重复提及）
- 通过 [PR #245](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/245)（@mcottontensor 提交）修复了使用 https 时 matchmaker 错误地将用户导向 http 的问题（重复提及）
- 通过 [PR #96](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/96)（@StomyPX 提交）修复了由于大小写问题导致 Linux 上无法构建前端库
- 通过 [PR #95](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/95) 和 [PR #97](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/97)（@Belchy06 提交）修复了 SFU peer 的 datachannel 未被创建的问题
- 通过 [PR #93](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/93)（@Belchy06 提交）修复了在 navigator 上没有 xr 对象时出现的浏览器崩溃
- 通过 [PR #83](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/83)（@Belchy06 提交）修复了如果应用未启动时未带 `-PixelStreamingNegotiateCodecs`，首选编解码器选择器会导致流无法正常启动的问题
- 通过 [PR #84](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/84)（@lukehb 提交）在添加首选编解码器后，修复了对浏览器支持的其他编解码器的加载（与 #83 相关）
- 通过 [PR #77](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/77) 和 [PR #78](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/78)（@Belchy06 和 @lukehb 提交）修复了麦克风输入延迟的问题
- 通过 [PR #44](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/44)（@mcianni 提交）修复了语法错误
- 通过 [PR #48](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/48)（@lukehb 提交）在 KeyboardEvent.keyCode 被弃用的情况下，改用 KeyboardEvent.code + 映射
- 通过 [PR #49](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/49)（@lukehb 提交）修复了在移除重复属性时对属性取反的错误
- 通过 [PR #55](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/55)（@Belchy06 提交）修复了当使用身份验证时指向错误登录页路径的问题
- 通过 [PR #60](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/60)（@StomyPX 提交）修复了在 offer 中对 “defaultToHover” 字段的处理
- 通过 [PR #141](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/141)（@hmuurine 提交）修复了使用新前端时 Pixel Streaming 会话会彻底断开的情况
- 通过 [PR #144](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/144)（@lukehb 提交）修复了在卸载输入时未完全注销的问题
- 通过 [PR #168](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/168)（@hmuurine 提交）修复了在较旧版本 NodeJS 上前端无法工作的问题，主要由于 ts-jest 和 jest
- 通过 [PR #118](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/118) 和 [PR #117](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/117)（@lukehb 和 @hmuurine 提交）修复了 webpack 将前端库二次打包到最终生成包的问题（#117）
- 通过 [PR #123](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/123)（@Belchy06 提交）修复了 cirrus Dockerfile 导致无法正常工作的信令服务器问题

### 安全
- 通过 [PR #220](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/220)（@mcottontensor 提交）在多个方面进行了安全更新
- 通过 [PR #196](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/196)（@gingernaz 提交）在默认 turn 服务器配置上做了安全更新
- 通过 [PR #69](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/69)（@dependabot 提交）将 `qs` 和 `express` 在 /SignallingWebServer 中进行升级
- 通过 [PR #70](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/70)（@dependabot 提交）将 `qs` 和 `express` 在 /Matchmaker 中进行升级
- 通过 [PR #71](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/71)（@dependabot 提交）将 `passport` 从 0.4.1 更新到 0.6.0（在 /SignallingWebServer）
- 通过 [PR #72](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/72)（@dependabot 提交）在 /Matchmaker 中升级了 `engine.io` 和 `socket.io`
- 通过 [PR #244](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/244)（@dependabot 提交）将 `socket.io-parser` 从 4.2.2 更新到 4.2.4（在 /Matchmaker）
- 修复了在解码 Socket 数据包时的校验不足（@iot-defcon / CVE-2022-25896）由 [PR #35](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/35)（@mik-patient）合并
- 通过 [PR #153](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/153) 和 [PR #155](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/155)（@dependabot 提交）将 /Frontend/library、/Frontend/ui-library 以及 /Frontend/implementations/EpicGames 中的 webpack 从 5.75.0 升级到 5.76.0
- 通过 [PR #163](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/163)（@mcottontensor 提交）修复了多项安全警告
- 通过 [PR #187](https://github.com/EpicGames/PixelStreamingInfrastructure/pull/187)（@lukehb 提交）将所有 package.json 都迁移到 `@epicgames-ps` 作用域以避免包冲突

---

## [UE 5.1](https://github.com/EpicGames/PixelStreamingInfrastructure/commits/UE5.1)

### Bug 修复
- `3b1b84` 修复了收到 freeze frames 时出现的黑屏闪烁问题
- `853625` 修复了 CSS 未展示 AFK 叠层的问题
- `c897e1` 修复了在 iOS 等没有 `pointerlock` 的平台上出现的错误

### 新增功能
- `980208` 添加了对鼠标双击的处理
- `6b8f31` 将延迟显示 freeze frame 的时间改为可配置选项
- `fe5c4c` 为 5.1 信令服务器容器添加了 Dockerfile

---

## [UE 5.0](https://github.com/EpicGames/PixelStreamingInfrastructure/commits/UE5.0)

### Bug 修复
- `3d641a` 修复了多次切换 `MatchViewportWidth` 失效的问题
- `ca6644` 修复了无法发送手柄按键信息的问题
- `bb4063` 修复了循环中缺失 `let` 声明的问题
- `b59bfb` 修复了 `removeResponseEventListener` 使用 remove 而不是 delete 的问题
- `4fee8a` 修复了 `unquantizeAndDenormalizeUnsigned` 未正确初始化的问题
- `42fa91` 迁移到标准化的 `onwheel` 浏览器事件

### 新增功能
- `b23cba` 为信令服务器添加了 `MaxPlayerCount` 配置选项，用于限制参与者人数（默认 -1 表示无限制）
- `e46c4d` 添加了对以二进制方式发送的 WebSocket 消息的支持
- `616f07` 添加了 `offerToReceive` 开关/标志，用于表示浏览器是否应生成 SDP offer
- `845ab1` 添加了对 “input protocol” 的处理能力，该协议规范了 UE 端通过 datachannel 发送的消息。如此一来，前端无需额外处理即可支持自定义 datachannel 消息（当然，如果用户想对消息做任何处理，仍需要自行绑定处理器）。
- `1c1fe0` 添加了在前端请求关键帧的能力

---

## [UE 4.27（生命周期结束）](https://github.com/EpicGames/PixelStreamingInfrastructure/commits/UE4.27)

回退移植了 5.0 的前端以支持 4.27：
- 移除了 SFU 支持，因为 4.27 不支持
- 忽略 `playerConnected` 消息，因为 4.27 不支持
- 强制前端生成 WebRTC offer，因为 4.27 期望这样

---

## [UE 4.26（不受支持）](https://github.com/EpicGames/PixelStreamingInfrastructure/commits/UE4.26)

回退移植了 5.0 的前端以支持 4.26：
- 移除了 SFU 支持，因为 4.26 不支持
- 忽略 `playerConnected` 消息，因为 4.26 不支持
- 强制前端生成 WebRTC offer，因为 4.26 期望这样
- 移除了 Linux 脚本，因为 4.26 不支持 Linux Pixel Streaming
- 强制从 SDP 中移除 `extmap-allow-mixed`，因为 4.26 所使用的 WebRTC 版本并不支持

---

## 旧版本
在 UE 4.26 之前的版本不在此记录范围内，因为本仓库从未支持过那些版本。
