# relay —— 会话接力命令

跨 AI 产品的会话交接方案：把一场长对话压缩成一份面向"下一棒"的**接力文档** + **可复制提示词**，新对话粘贴即续。

> **English**: relay turns a long AI coding session into a handoff note + a copy-paste prompt, so a fresh conversation (in any AI product) picks up where you left off. Install for Claude Code:
>
> ```bash
> mkdir -p ~/.claude/commands && curl -fsSL https://raw.githubusercontent.com/yanlin-cheng/relay/main/claude-code/relay.md -o ~/.claude/commands/relay.md
> ```
>
> Then type `/relay` in a long session. Other tools → [universal/relay.md](universal/relay.md) (paste-in prompt, works anywhere).

## 它解决什么问题

对话很长之后，原地压缩（各家 AI 的 compact 类功能）有两个硬伤：压缩后的上下文依然不小（还是慢），压缩即丢失（细节没了就没了）。

relay 的做法：

1. **摘要进新会话**——新对话上下文干净，快
2. **正本不丢**——Claude Code 版会把完整对话记录（.jsonl）的路径写进文档，缺细节时新会话自己去搜原文（借鉴 Cline 的 sidecar 理念）
3. **任务即过滤器**——接力时可以指定下一棒任务，文档只总结该任务需要知道的内容，不做泛泛的全文摘要

## 快速开始

**Claude Code**——一条命令装好（Windows 用 PowerShell 版）：

```bash
mkdir -p ~/.claude/commands && curl -fsSL https://raw.githubusercontent.com/yanlin-cheng/relay/main/claude-code/relay.md -o ~/.claude/commands/relay.md
```

```powershell
# Windows PowerShell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude\commands" | Out-Null
irm https://raw.githubusercontent.com/yanlin-cheng/relay/main/claude-code/relay.md -OutFile "$env:USERPROFILE\.claude\commands\relay.md"
```

装完在长对话里输入 `/relay` 即可（详见下面"用法"）。

**其他产品**——不用命令功能，打开文件复制粘贴即可：

| 你用什么 | 拿法 |
|---|---|
| Cline | 见 [adapters/cline.md](adapters/cline.md) |
| Cursor | 见 [adapters/cursor.md](adapters/cursor.md) |
| 其他任何 AI 产品 | 打开 [universal/relay.md](universal/relay.md)，把分隔线以下整段复制进想交接的对话发送 |

## 用法（以 Claude Code 版为例）

```
/relay                    # 通用总结：整场对话该知道的都提炼
/relay 重构登录模块        # 任务定制：只捞该任务需要的背景/决策/文件/坑
/relay 跨产品             # 额外输出可粘进其他 AI 产品的内嵌版提示词
```

流程：跑命令 → 过目它展示的接力文档（不满意直接说，重写）→ 复制末尾提示词 → 开新对话粘贴回车。

## 设计依据

模板不是凭感觉写的——骨架和"整体克制，唯独下一步要详细"的总纲抄自 **Cline 压缩器的真实源码指令**，设计推演过程见 [DESIGN.md](DESIGN.md)。

## 迭代

本仓库是 relay 的唯一源头。欢迎 issue / PR 反馈模板与纪律的改进。核心原则：**整体克制，唯独下一步要详细**。
