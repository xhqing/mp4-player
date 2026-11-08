# mp4-player · 项目硬约束

身份与角色见本仓库根 `AGENTS.md`；团队通用规则见全局 `~/.pi/agent/AGENTS.md`，此处不重述。

## 本项目是什么

VSCode 视频播放扩展：视频在编辑器标签页里带声音播放（MP4 / MOV / M4V / MKV / AVI / M2TS / MTS / FLV / F4V / WebM 等）。Chromium 解不了的 AAC 音频与 HEVC / WebM 转码全部由内置 ffmpeg WebAssembly 在本地完成；严格 CSP、无本地服务、零外部依赖。

本仓库是上游 **Brodazz/mp4-player** 的**独立仓库**：已与上游解绑、不自动同步上游、自主演进。

## 硬约束

- **保留上游 LICENSE 与版权署名**（MIT 许可要求）——不要改动或删除 LICENSE，不要抹掉 README / 源码里的上游署名。
- **main 分支保护**：禁止直推；一切改动经 PR + CI（required check `build`）+ squash 合并 + 合并后自动删分支。
- **版本号以 `VERSION` 为唯一权威**：与 `package.json`、`package-lock.json`、`CHANGELOG.md`、README 保持一致；**不在功能分支上 bump**（bump 由 Leader 在专门的 bump 分支上做）。
- **不要恢复 `.github/workflows/release.yml`**：它已于 2026-10-09 删除——原设计是 tag 触发构建并创建 Release，会与本地 `/release` 流程双头创建 Release、互相撞车。发版产物由本地构建并在 `/release` 时上传。
- **安装走 vsce-install 流程**：从 GitHub Release 取 vsix，卸载旧版 → 删残留目录 → 清 contribution 缓存 → 再装。实际使用的版本必须来自 Release 产物，不用本地开发构建长期顶替。
- **改动记 `CHANGELOG.md`**：写清为什么改 + 改了什么。
- **临时产物放项目 `tmp/`**（已忽略）。

## 验证要求

- 改播放器 / 解码相关逻辑时，实测至少两种格式（一种浏览器原生可解、一种需要 wasm 转码）。
- 涉及 CSP 的改动要确认 WebAssembly 仍能加载，不要为了「修 CSP 报错」放宽到 `unsafe-eval` 之外更宽的程度。

## 详细说明

开发与发布约定见项目根 `DEVELOPMENT.md`；通用工作规则见全局 `~/.pi/agent/AGENTS.md`。
