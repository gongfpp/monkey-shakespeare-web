# 猴子打字工作室 · Web 构建产物

本仓库是《猿与莎士比亚》的公开构建与 GitHub Pages 部署入口。`main` 保存构建工作流与发布说明，游戏源码及素材工程保存在私有的 `gongfpp/monkey-shakespeare`。构建在本仓库的 GitHub Actions 标准 Linux runner 中执行，只读拉取私有源码，检查通过后导出并上传 Web 静态产物。

- 在线试玩：https://gongfpp.github.io/monkey-shakespeare-web/
- 发布方式：GitHub Actions Pages artifact；`gh-pages` 只保留旧发布产物，不再作为线上发布源。
- 授权：构建产物按 AGPL-3.0 与商业授权双授权发布，构建内已包含第三方许可信息。

发布工作流为 `.github/workflows/publish-web.yml`，手动触发时传入私有源码 `main` 当前的完整提交 SHA。工作流会核对实际拉取的提交，运行敏感信息扫描与 `npm run verify`，再用 Godot 4.7.2 导出并部署；不会发布未合并的分支或混入另一个提交。

读取私有源码使用 `SOURCE_READ_KEY`，它对应仅限该私有仓库的只读 deploy key。不要使用个人账户的广泛权限令牌，不要上传源码目录作为 artifact。只有 `source/tmp/godot-web` 会进入 Pages。工作流仅支持 `workflow_dispatch`，不在外部 PR 上读取源码。

源码改动提交到私有仓库；本仓库只维护构建工作流和发布入口。未来不再构建或部署 Sites。
