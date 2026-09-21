# relayhand —— 会话接力命令仓库

## 项目概述

跨 AI 产品的会话交接命令集合：把长对话压缩成面向"下一棒"任务的接力文档 + 可复制提示词，新对话粘贴即续。本仓库是 relayhand 的唯一源头，面向不同 AI 产品的用户分发。

## 技术栈

纯提示词资产（markdown），无代码。运行环境：任何支持自定义命令或可粘贴提示词的 AI 对话产品。

## 项目结构

```
relayhand/
├── README.md                  # 英文主门面（含 Mermaid 流程图）
├── README-ZH.md               # 简体中文门面（与英文版同构）
├── DESIGN.md                  # 设计依据与决策日志
├── .claude-plugin/            # 插件化分发（2026-09-21）：plugin.json + marketplace.json（仓库即市场）
├── commands/relayhand.md      # Claude Code 版命令（英文指令 + 语言跟随，$ARGUMENTS、jsonl 正本指针）
├── universal/relayhand.md     # 通用核心提示词（英文指令 + 语言跟随，手动粘贴）
└── adapters/                  # 各产品适配说明（核心引用 universal/，不复制）
```

## 开发规范

- 通用核心只改 `universal/relayhand.md`；`adapters/` 只写挂载方式，引用不复制，避免多份漂移
- 模板是单一版（指令英文 + 语言自动跟随），不为语言拆文件；README.md 与 README-ZH.md 同构同步
- `commands/relayhand.md` 允许用 Claude Code 专属机制，但不得含任何个人路径、个人知识库配置
- 发版必 bump `.claude-plugin/plugin.json` 与 `marketplace.json` 里的 version 字段（声明了 version 不 bump，插件用户会一直用缓存旧版）
- 模板或纪律的任何改动：先在 DESIGN.md 决策日志记一笔（为什么改），再改文件
- 本机实战副本在 `C:\Users\cyl\.claude\commands\relayhand.md`（含知识库增强层），仓库改动后手动同步过去
- 模板改动必须实测验证：找一场真实长对话跑 /relayhand，检查产出质量再定稿
- 提交信息用中文，说清"改了什么、为什么"

## 当前阶段

初版建成（2026-09-19），2026-09-20 由 relay 改名 relayhand（原因见 DESIGN.md 决策日志）。2026-09-21 插件化：仓库即市场 + 插件（yanlin-cheng 市场名 / relayhand 插件名 / /relayhand 命令名），阶段二规划见 DESIGN.md 决策日志；同日补齐 handoff 对比暴露的两块长板（模板 Suggested skills 栏、README"何时不用"边界节，见 DESIGN.md 当日条目）。待实战验证：模板总结质量、任务过滤效果、插件安装流程。
