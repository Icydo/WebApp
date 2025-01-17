# 欢迎阅读 Pixel Streaming 贡献指南

首先，感谢你为 Pixel Streaming 付出的时间和贡献！

我们很自豪也很高兴能够与如此热情的社区共同努力，不断帮助我们改进 Pixel Streaming。🎉

如果你对如何在 GitHub 上做贡献还不熟悉，建议先阅读[官方文档](https://docs.github.com/get-started)，以了解仓库结构、fork、分支、提交（commit）、Issue、PR 等的相关信息。

### 行为准则

请时刻保持耐心、礼貌和专业。任何形式的垃圾信息、滥用或歧视都将被禁止。

---

## 入门

### 创建 Issue

如果你在使用过程中遇到了 Bug，或有关于文档或基础设施方面的建议，或者想提出某个新功能的想法（可应用于各种使用场景），你可以通过创建一个新的 Issue 来与我们沟通。

1. 首先，在 [这里](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/issues?q=is%3Aissue+) 或在 [旧仓库](https://github.com/EpicGames/PixelStreamingInfrastructure/issues?q=is%3Aissue+is%3Aclosed) 中搜索所有已打开和已关闭的 Issue——你要提的问题可能之前已经被讨论或解决过。
2. 如果确定该 Issue 不存在，则可在 [这里](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/issues/new/choose) 打开一个新的 Issue，选择 “Bug” 或 “Feature Request”（功能需求）。
3. 尽量在模板中填写更多信息；如重现步骤、崩溃堆栈、截图等。提供更多信息有助于我们更快地定位和解决问题。
4. 关注你所创建的 Issue 状态；我们的开发者或其他用户可能会请求你提供更多信息。如果在 30 天内你没有回复，Issue 将被自动关闭。
5. 在等待问题解决的过程中请保持耐心；我们会根据内部优先级来处理 Issue，一些优先级较低的功能（即使我们非常想去实现）可能会排在更紧迫的问题之后，因此某些 Issue 可能需要更长时间才能解决。

---

### 创建 Pull Request (PR)

如果你对所遇到的问题或其他已存在的 Issue 有解决方案，可以通过创建 Pull Request 来提交你的修改。

1. Fork 此仓库，并在你的 Fork 中基于 `main` 分支创建新分支。
2. 在这个分支里进行你的修改，并确保你的提交（commit）已验证签名（Verified）。合并需要签名的提交！请参考[GitHub 签名文档](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification)。
3. 尽可能多地进行测试。当你认为已经准备就绪后，整理好你的工作并提交更新。
4. 创建一个[新的 Pull Request](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/pulls)，如果有对应的 Issue，请务必关联它。并尽量在 PR 中提供更多信息：描述你的修改解决了什么问题，提到你所做的任何测试，附上相关文档或截图等。
5. 如果你的 PR 提供了新功能，我们强烈建议你附带相关文档，并详细说明你所做的测试。没有这些信息的 PR 可能需要很长时间才能被评估，因为我们需要自行做测试来验证。
6. 如果你的 PR 一切就绪，我们会将其合并。太棒了！非常感谢你的时间与付出！🎉
7. 请关注你的 PR——我们的开发者通常会对其进行审查，并留下评论；他们可能会要求一些小的代码更改或调整，以统一风格或提出一般性问题。我们无法合并 PR 的原因也会在评论中说明。
8. 如果我们在提出更多信息或更改请求后 30 天内没有收到回复，该 PR 将自动关闭。在这种情况下，我们可能会自己开一个新的 PR，重用你提出的修改，并补充任何在原 PR 中缺失的内容。
9. 如果你的 PR 修复了之前[仍受支持 UE 分支](https://github.com/EpicGamesExt/PixelStreamingInfrastructure#versions)中的问题，可以添加 `auto-backport` 和相应的 `auto-backport-to-UEX.X` 标签。每个你想合并回去的分支都需要一个对应的 `auto-backport-to-UEX.X` 标签。需要注意的是，如果要合并到之前的分支所需的改动量很大，并且需要很多测试和兼容性检查，我们可能会根据价值和成本衡量决定不合并到该分支。

---

### 其他贡献方式

- 关注我们仓库中已存在的 Issue 和 PR；在讨论中补充任何有价值的信息，例如更多的重现步骤、在不同环境下的重现结果，或对问题原因及解决方法的建议。
- 处理[带有 “good first issue” 标签](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/issues?q=is%3Aopen+is%3Aissue+label%3A%22good+first+issue%22)的 Issue。我们特意标注了这些 Issue，期待社区能帮助解决。
- 为当前未记录的功能撰写文档。最好先新开一个 Issue，让我们的开发者可以给你一些指导。
- 编写更多单元测试，提高代码覆盖率。
- 为尚未在公共 API 中记录的函数提供文档。
- 使用其他 Web 框架（如 Angular、Vue 等）编写新的前端实现。
- 在不同的引擎版本上执行测试，尤其是预览版，然后根据发现的 Bug 创建 Issue。

---

## 编码规范

- 应优先使用 TypeScript 而非 JavaScript。
- 所有 TypeScript 代码都应遵守[这些 lint 规则](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/blob/master/Frontend/library/.eslintrc.js)。
- 命名应使用美式英语拼写。
- 所有公共函数/API 都应提供注释。
- 代码格式应符合[此处的空白和缩进规则](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/blob/master/Frontend/library/.prettierrc.json)。
- 所有新功能在提交时都应带有相应的单元测试和文档。
- `if` 语句中应尽量采用提前返回（early return）以减少嵌套层级。
- 函数行数不应超过约 20 行。
- 对较长的函数应添加注释。
- 在可读性和语法糖之间，更倾向可读性（verbosity）。
- 尽量只导出最小的公共 API，以便后续迭代和支持。
- 函数内部不应超过三层嵌套。

---

## 文档风格

所有文档应使用美式英语书写，并保证语法和拼写正确。请尽量以合理的方式排版文本，使用标题、列表、项目符号等。

文档应拆分到各自独立的 `.md` 文件中，理想情况下，每个顶层目录下都有一个 `readme.md` 文件来说明该组件的用途。当合适时，可以在仓库中对应的索引页中加入链接，引导用户找到这些文档。

---

## 法律声明

© 2004-2025，Epic Games, Inc. “Unreal” 及其徽标是 Epic 在美国及其他地区的商标或注册商标。
