# mp4-player 项目指南

## 负责工程师：Atlas

本项目由 **Atlas**（FullStackEngineerAgent，用户的全栈开发工程师）负责维护——本项目内的开发 / 维护需求由 Atlas 统一处理（Atlas 的角色定义与工作原则见 FullStackEngineerAgent 项目根 `CLAUDE.md`）。

mp4-player 是一个 VSCode 视频播放扩展：视频直接在编辑器标签页里带声音播放，支持 MP4 / MOV / M4V / MKV / AVI / M2TS / MTS / FLV / F4V / WebM 等格式（Chromium 解不了的 AAC 音频、以及 HEVC / WebM 转码，全部由内置的 ffmpeg WebAssembly 在本地完成；严格 CSP、无本地服务、零外部依赖）。本仓库（`github.com/xhqing/mp4-player`）是上游 **Brodazz/mp4-player**（Marketplace 的 `Brodazz.mp4-player`）的**独立仓库**：已与上游解绑、不自动同步上游、自主演进；**保留上游 LICENSE 与版权署名**（MIT 许可要求）；README 的徽章 / 图片 URL 与 `package.json` 的 repository / bugs / homepage 仍指向上游（暂未改动）。本仓库自身的改动：右键菜单「文件操作」三件（**Copy Video File** / **Copy File Path** / **Show in Folder**，替换掉 VSCode 默认那组在视频上无效的 Cut / Copy / Paste）。

### 开发与发布约定

- **本地开发目录**：`~/Developer/mp4-player`。
- **main 分支保护**：禁止直推；一切经 PR + CI（required check `build`）+ auto-merge（只允许 squash、合并后自动删分支）。
- **版本号**：项目根 `VERSION` 为唯一权威，与 `package.json`、`package-lock.json`、`CHANGELOG.md`、README 保持一致；不在功能分支 bump。
- **发版**：走家里链条 `/bump` → `/add` → `/commit` → `/release`（正式版只从 main 打 tag）；发布产物 = GitHub Release 附 vsix（发布时本地构建上传）。原「tag 触发构建并创建 Release」的 `.github/workflows/release.yml` 已于 2026-10-09 删除——它与本地 `/release` 双头创建 Release、会互相撞车。
- **安装**：从 GitHub Release 取 vsix、按 vsce-install 流程干净安装（卸载旧版 → 删残留目录 → 清缓存 → 再装）；实际使用的版本必须来自 Release 产物，不用本地开发构建长期顶替。
- **CHANGELOG 纪律**：每次文件增删改都记录（为什么改 + 改了什么），按全局规则执行。
- 通用工作规则（读取优先、增改查优先慎用删除、汇报前验证、临时产物放 `tmp/`、敏感信息不进会被 git 跟踪的文件等）见全局 `~/.pi/agent/CLAUDE.md`。


（本文件 2026-10-12 由原 `CLAUDE.md` 的项目指南迁入；按新规，非 Agent 项目不再保留 CLAUDE.md / AGENTS.md 等智能体专属文件。）
