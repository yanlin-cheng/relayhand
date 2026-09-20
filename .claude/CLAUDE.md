# relayhand — 项目记忆

## 项目概述

会话接力命令的开源仓库：模板抄自 Cline 压缩器源码的真实指令，跨 AI 产品分发。

## 技术栈

纯 markdown 提示词资产，无代码。

## 工作流与技能选择

本项目是内容/提示词项目，日常任务轻量：

- 改模板、改纪律 → 直接改 `universal/relayhand.md` + DESIGN.md 决策日志补记，不需求助技能
- 涉及"要不要加新机制"的方案讨论 → 先读 DESIGN.md 第三节，看是否已有取舍记录，避免重新论证
- 上 GitHub、开源协作相关经验 → 参考知识库 `开源项目经验/`

## 关键决策

- 模板与总纲源自 Cline 源码（DESIGN.md 第二节有原文证据），不要凭感觉改
- 知识库日志默认关闭（用户 2026-09-19 拍板）；个人增强层不进仓库
- 自动注入（钩子）与自动开新对话（扩展）方案均被否，理由在 DESIGN.md 第三节
- 2026-09-20 改名 relayhand（relay 是通用词搜索易撞车），命令同步改 /relayhand，理由见 DESIGN.md 决策日志

## 待办事项

- [ ] 实战验证模板效果（跑真实长对话，顺便把个人副本同步到 relayhand 新版）
- [ ] 核实 Cline / Cursor 适配说明与最新官方文档是否一致
- [ ] 用户说推才推 GitHub

## 更新日志

### 2026-09-19 仓库初建
- 从个人命令 `/relay` 升级为分发仓库：README、DESIGN、claude-code 版、universal 版、两个适配器
- 个人实战副本（C:\Users\cyl\.claude\commands\relay.md）保留知识库增强层，与仓库通用版并存

### 2026-09-20 改名 relayhand
- relay 是通用词、网上已有同名仓库，搜索易被淹没；改名为 relayhand，命令同步改 `/relayhand`
- 文件改名：claude-code/relayhand.md、universal/relayhand.md；README 安装 URL 全部更新
- 个人实战副本同步改名为 C:\Users\cyl\.claude\commands\relayhand.md

### 2026-09-20 双语化
- README.md 改为英文主门面，新增 README-ZH.md（同构），顶部互相切换
- README 用 Mermaid 图讲三件事：核心接力链路、接力棒栏目结构、安装使用路径（为录视频讲解服务）
- 模板合并为单一版（英文指令 + 语言跟随对话的纪律），当日曾拆中英两份模板、旋即撤回合并（理由见 DESIGN.md 决策日志）

### 2026-09-20 内核优化 1-5
- 模板加"坑（勿重蹈）"栏；写作纪律新增两条：用户原话逐字保护、接力链指针（纪律变 10 条）
- 两个新会话提示词升级：禁止复述接力文档内容 + 先跑 git status 对账仓库实际状态
- 依据三家同类项目交叉印证 + Cline/Claude Code 源码证据，详见 DESIGN.md 决策日志当日条目；提案 6（环境备忘栏）未获表态，默认不做
