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
├── claude-code/relayhand.md   # Claude Code 中文版（$ARGUMENTS、jsonl 正本指针）
├── claude-code/relayhand-en.md# Claude Code 英文版
├── universal/relayhand.md     # 通用核心提示词中文版（无命令功能的产品手动粘贴）
├── universal/relayhand-en.md  # 通用核心提示词英文版
└── adapters/                  # 各产品适配说明（核心引用 universal/，不复制）
```

## 开发规范

- 通用核心只改 `universal/relayhand.md`；`adapters/` 只写挂载方式，引用不复制，避免多份漂移
- 模板有中英两版：改内容必须同步改 `-en.md` 版本，README.md 与 README-ZH.md 同构同步
- `claude-code/relayhand.md` 允许用 Claude Code 专属机制，但不得含任何个人路径、个人知识库配置
- 模板或纪律的任何改动：先在 DESIGN.md 决策日志记一笔（为什么改），再改文件
- 本机实战副本在 `C:\Users\cyl\.claude\commands\relayhand.md`（含知识库增强层），仓库改动后手动同步过去
- 模板改动必须实测验证：找一场真实长对话跑 /relayhand，检查产出质量再定稿
- 提交信息用中文，说清"改了什么、为什么"

## 当前阶段

初版建成（2026-09-19），2026-09-20 由 relay 改名 relayhand（原因见 DESIGN.md 决策日志）。待实战验证：模板总结质量、任务过滤效果、各平台适配说明准确性。
