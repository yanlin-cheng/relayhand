# Cline 适配

## 定位说明

Cline 自带 `/newtask`（最新版已改为 `/compact` 的别名，做原地压缩）和 `/smol`。relay 的差异：产出**跨会话的接力棒**——接力文档 + 可复制提示词，新任务粘贴即续，且原对话正本不丢。

## 挂载方式

Cline 支持通过 markdown 文件注册自定义斜杠命令（以你所用版本的官方文档为准，目录名和识别规则可能随版本变化）。把 [universal/relayhand.md](../universal/relayhand.md) 中分隔线以下的核心提示词保存为一个命令文件即可。

## 适配要点

- Cline 没有参数替换机制（如 Claude Code 的 `$ARGUMENTS`）：核心提示词已改为自然语言约定——"用户附加任务"由用户在命令后或对话中直接给出，模型自行识别
- 正本指针一节依赖 Claude Code 的 `.claude/projects` 目录，Cline 环境下由核心提示词的正本栏目自行省略（核心模板本就不含该节，只有 Claude Code 版有）
- 若你的 Cline 版本支持工作区命令或 .clinerules，同样可以挂载这份核心提示词

## 核心提示词

见 [universal/relayhand.md](../universal/relayhand.md)——原样复制，不要改动模板与纪律部分（它们的设计依据见 [../DESIGN.md](../DESIGN.md)）。
