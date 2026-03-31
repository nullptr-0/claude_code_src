# Claude Code 2.1.88 Source Recovery

这个仓库是对 `@anthropic-ai/claude-code` `2.1.88` 版本的一次源码整理与重建。

该版本发布到 npm 时附带了可还原源码的 source map，我基于其中的 `sources` 和 `sourcesContent` 将项目重新整理为可直接阅读的源码目录，方便研究 Claude Code 的 CLI 架构、命令系统、Ink TUI 组件组织方式，以及 MCP / 插件 / skills 等能力的实现。

## 说明

- 版本来源：`@anthropic-ai/claude-code@2.1.88`
- 当前内容：以 source map 恢复出来的源码目录
- 当前状态：以阅读、检索、分析为主，不保证开箱即用可构建
- 仓库定位：研究归档、结构分析、源码阅读

## 免责声明

- 本仓库不是 Anthropic 官方仓库，也不代表 Anthropic 立场
- 原始代码的版权、商标及相关权利归原权利方所有
- 此仓库的目标是归档与研究源码结构，不应被误解为 Anthropic 官方开源项目
- 如你计划公开分发、二次发布或商用，请自行确认相关许可、服务条款与法律风险

## 项目结构

当前仓库以 `src/` 为主，已经可以较完整地反映 Claude Code CLI 的代码组织：

- `src/entrypoints/`：入口文件，包括 CLI 入口与相关启动逻辑
- `src/commands/`：命令系统，包含 `login`、`config`、`mcp`、`review`、`status`、`tasks` 等子命令
- `src/components/`：终端 UI 组件，主要基于 React + Ink 风格组织
- `src/hooks/`：交互式终端状态与行为 hooks
- `src/utils/`：认证、配置、进程、文件、调试、格式化等基础工具
- `src/services/`：策略、设置同步、远程能力、team memory 等服务层实现
- `src/bridge/`：remote control / bridge 相关能力
- `src/ink/`：定制终端渲染与 UI 基础设施
- `src/constants/`：系统提示词、限制、工具定义、产品常量等

## 从代码里能看到什么

从当前恢复结果里，可以比较直观地看到 Claude Code 的一些核心设计：

- CLI 启动入口存在明显的快速路径分发逻辑
- 命令系统支持内建命令、动态 skills、插件命令、MCP 命令混合装载
- 终端界面大量使用 React 组件和自定义 Ink 能力
- 项目包含远程控制、后台会话、MCP、插件、技能系统等模块
- 部分功能受构建期 feature flag 控制，源码中可以看到大量按特性裁剪的路径

例如：

- CLI 入口在 `src/entrypoints/cli.tsx`
- 命令注册与加载逻辑在 `src/commands.ts`

## 已恢复内容的特点

- 恢复来源是 source map，因此可读性远高于打包后的单文件 CLI
- 文件结构基本接近原始项目结构
- 一些构建产物依赖、内部宏、发布时裁剪逻辑、原始工程配置未必完整保留
- 某些内部能力、私有服务接入、vendor 模块或运行时资源可能仍需额外补齐

## 适合拿来做什么

- 阅读 Claude Code 的整体架构
- 分析命令系统与技能系统的实现方式
- 研究 MCP、插件、终端 UI 的组织方式
- 做代码检索、逆向学习、产品设计参考

## 不保证的内容

- 不保证可以直接 `install` / `build` / `run`
- 不保证包含完整工程配置、锁文件、原始脚本和内部依赖
- 不保证 Anthropic 内部 feature flag、服务端接口、私有能力可以正常工作

## 如果你准备继续整理这个仓库

建议按下面顺序继续补齐：

1. 增加 `package.json`
2. 补齐构建工具链与依赖版本
3. 识别 `bun:bundle`、宏替换、feature flag 等发布期能力
4. 梳理缺失的 vendor 文件、native 模块与运行时资源
5. 为入口与核心命令补充最小可运行验证

## 致谢

感谢 source map 没有被移除，这才使得这份源码结构得以被重新整理出来。
