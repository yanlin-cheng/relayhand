# Cursor 适配

## 挂载方式

Cursor 支持自定义斜杠命令（以你所用版本的官方文档为准，命令目录与语法可能随版本变化）。把 [universal/relayhand.md](../universal/relayhand.md) 中分隔线以下的核心提示词保存为一个命令文件即可。

## 适配要点

- Cursor 没有参数替换机制（如 Claude Code 的 `$ARGUMENTS`）：核心提示词已改为自然语言约定——"用户附加任务"由用户在命令后或对话中直接给出，模型自行识别
- 正本指针一节依赖 Claude Code 的 `.claude/projects` 目录，核心模板不含该节，Cursor 环境下无需处理
- Cursor 的对话历史存放位置与 Claude Code 不同，如需"正本指针"能力，可在接力文档"文件"节后自行补一条当前会话可回溯方式的说明

## 核心提示词

见 [universal/relayhand.md](../universal/relayhand.md)——原样复制，不要改动模板与纪律部分（它们的设计依据见 [../DESIGN.md](../DESIGN.md)）。英文版核心提示词：[universal/relayhand-en.md](../universal/relayhand-en.md)。
