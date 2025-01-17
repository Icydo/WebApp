# 发布版本（Cutting releases）

在本仓库中，有多项内容可以发布：

- 信令服务器（Signalling Server）容器镜像
- `/library` 目录下的 NPM 包
- `/ui-library` 目录下的 NPM 包
- 整个仓库以及构建后的前端，以 Github release `.zip`/`.tar.gz` 归档文件的形式发布

---

## `/Common` NPM 包
1. 切换到目标分支（例如 5.5）。
2. 将需要的更改合并或直接在 `/Common` 目录中进行修改。
3. 根据所做的更改，遵照 [semver](https://semver.org/) 规范，在 [`package.json`](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/blob/master/Common/package.json#L3) 文件中更新版本号。
4. 提交对 `package.json` 文件的更改。
5. 这会自动触发 [此操作](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-common-library-to-npm.yml)，并执行构建和推送到 NPM 的流程。

---

## `/Signalling` NPM 包
1. 切换到目标分支（例如 5.5）。
2. 将需要的更改合并或直接在 `/Signalling` 目录中进行修改。
3. 根据所做的更改，遵照 [semver](https://semver.org/) 规范，在 [`package.json`](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/blob/master/Signalling/package.json) 文件中更新版本号。
4. **可选操作：** 如果 `/Common` 库版本被更新了，可以在 `package.json` 中一并更新其版本号。
5. 提交对 `package.json` （以及可能的 `package-lock.json`）的更改。
6. 这会自动触发 [此操作](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-signalling-library-to-npm.yml)，并执行构建和推送到 NPM 的流程。

---

## `/library` NPM 包
1. 切换到目标分支（例如 5.5）。
2. 将需要的更改合并或直接在 `/library` 目录中进行修改。
3. 根据所做的更改，遵照 [semver](https://semver.org/) 规范，在 [`package.json`](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/blob/master/Frontend/library/package.json) 文件中更新版本号。
4. 提交对 `package.json` 文件的更改。
5. 这会自动触发 [此操作](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-library-to-npm.yml)，并执行构建和推送到 NPM 的流程。

---

## `ui-library` NPM 包
1. 切换到目标分支（例如 5.5）。
2. 将需要的更改合并或直接在 `/ui-library` 目录中进行修改。
3. 根据所做的更改，遵照 [semver](https://semver.org/) 规范，在 [`package.json`](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/blob/master/Frontend/ui-library/package.json#L3) 文件中更新版本号。
4. **可选操作：** 如果 `/Common` 库版本被更新，请在 `package.json` 中同步更新（[示例](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/blob/master/Frontend/ui-library/package.json#L19)）。
5. **可选操作：** 如果 `frontend` 库版本被更新，请在 `package.json` 中同步更新（[示例1](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/blob/master/Frontend/ui-library/package.json#L20)，[示例2](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/blob/master/Frontend/ui-library/package.json#L38)）。
6. 提交对 `package.json` （以及可能的 `package-lock.json`）的更改。
7. 这会自动触发 [此操作](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/publish-ui-library-to-npm.yml)，并执行构建和推送到 NPM 的流程。

---

## 信令服务器容器（Signalling Server Container）
1. 切换到目标分支（例如 5.5）。
2. 将需要的更改合并或直接在 `/SignallingWebServer` 目录中进行修改。
3. 这会自动触发 [此操作](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/container-images.yml)，构建并推送信令服务器容器镜像。

---

## Github releases 归档
1. 切换到目标分支（例如 5.5）。
2. 在仓库任意位置进行或合并需要的更改。
3. 根据所做的更改，遵照 [semver](https://semver.org/) 规范，在 [`RELEASE_VERSION`](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/blob/master/RELEASE_VERSION) 文件中更新版本号。
4. 提交对 `RELEASE_VERSION` 文件的更改。
5. 这会自动触发 [此操作](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/actions/workflows/create-gh-release.yml)，在 Github 上创建带有 `.zip` 和 `.tar.gz` 归档文件的标签发布（tagged release）。

---

## 处理多项改动
如果同时有多项改动，需要发布多个内容，通常的发布顺序如下：

1. `/Common`
2. `/Signalling`
3. `/library`
4. `/ui-library`
5. `/SignallingWebServer`
6. `RELEASE_VERSION` 文件

---

## Github Actions 因为未发布的库而失败
如果你碰到一个情况：某个 PR 由于未发布的库而导致 Github Actions 检查失败，但是你已经确认所有内容都可以正常工作、只是库还没发布，那么你可以在提交信息中加入 `#bypass-publish-check` 这个字符串。这样就会跳过在构建时使用已发布库的检查。

在该 PR 合并之后，这个检查会再次运行。你可以在一个新的 PR 或提交中更新库的版本号。
