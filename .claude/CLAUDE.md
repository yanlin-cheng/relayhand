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
- 2026-09-21 插件化（仓库即市场 + 插件）；形态定 command 不做 skill；命名三层：市场 yanlin-cheng / 插件 relayhand / 命令 /relayhand，理由见 DESIGN.md 决策日志
- 2026-09-21 起 DESIGN.md 私有化：不随仓库分发、已从全部 git 历史抹除；决策日志只在本机维护，仓库内"见 DESIGN.md"均指本机文件

## 待办事项

- [ ] 实战验证模板效果（跑真实长对话；个人副本已于 2026-09-20 同步到内核优化 1-5 新版，2026-09-21 同步加 Suggested skills 栏）
- [ ] 核实 Cline / Cursor 适配说明与最新官方文档是否一致
- [ ] 阶段二（暂缓）：第二个可发布工具成型时建 yanlin-cheng 独立市场仓库收编各插件
- [ ] 推送后实测插件安装流程（/plugin marketplace add yanlin-cheng/relayhand）
- [ ] 用户说推才推 GitHub

## 更新日志

### 2026-09-19 仓库初建
- 从个人命令 `/relay` 升级为分发仓库：README、DESIGN、claude-code 版、universal 版、两个适配器
- 个人实战副本（~/.claude/commands/relay.md）保留知识库增强层，与仓库通用版并存

### 2026-09-20 改名 relayhand
- relay 是通用词、网上已有同名仓库，搜索易被淹没；改名为 relayhand，命令同步改 `/relayhand`
- 文件改名：claude-code/relayhand.md、universal/relayhand.md；README 安装 URL 全部更新
- 个人实战副本同步改名为 ~/.claude/commands/relayhand.md

### 2026-09-20 双语化
- README.md 改为英文主门面，新增 README-ZH.md（同构），顶部互相切换
- README 用 Mermaid 图讲三件事：核心接力链路、接力棒栏目结构、安装使用路径（为录视频讲解服务）
- 模板合并为单一版（英文指令 + 语言跟随对话的纪律），当日曾拆中英两份模板、旋即撤回合并（理由见 DESIGN.md 决策日志）

### 2026-09-20 内核优化 1-5
- 模板加"坑（勿重蹈）"栏；写作纪律新增两条：用户原话逐字保护、接力链指针（纪律变 10 条）
- 两个新会话提示词升级：禁止复述接力文档内容 + 先跑 git status 对账仓库实际状态
- 依据三家同类项目交叉印证 + Cline/Claude Code 源码证据，详见 DESIGN.md 决策日志当日条目；提案 6（环境备忘栏）未获表态，默认不做

### 2026-09-20 消费端首验（任务即过滤器模式）
- 新会话按接力文档提示词先跑 git status 对账，抓到生成端漏记的未提交改动（.claude/CLAUDE.md 待办行），已补交 b45e517——对账机制首验通过，不是走过场
- "任务即过滤器"首验通过：目标/状态/坑/下一步只装测试任务内容，上一棒环境坑被整条滤掉
- 纪律 6（原话保护）与真长对话压测仍未验，需真长对话跑 /relayhand 补验
- 测试暴露生成端改进提案（"改过"栏应记未提交仓库改动），待用户拍板，未动模板

### 2026-09-20 会话命名对齐接力链
- 用户发现新会话标题被自动摘要改掉，接力链在会话列表对不上账；查证官方文档后拍板双保险：提示词块首行加"命名素材行"（Relay relayhand-<时间戳> — 任务一句话，喂给标题生成器）+ 块旁人读附注（粘贴后 /rename，100% 精确）
- 两个模板 + 个人副本四步提示词同步更新；依据与措辞细节见 DESIGN.md 决策日志当日条目

### 2026-09-20 README 门面升级
- 中英 README 四处升级：三方案对比表、精工细节节（接力链图 + 六微机制表）、"源自源码交叉验证"证据节、MIT 徽章
- 依据见 DESIGN.md 当日条目；此为推送前打磨

### 2026-09-20 安装流程重构：Agent 自装
- 用户拍板：非 Claude Code 产品不再"逐次复制粘贴"，改为一段可一键复制的 Agent 安装提示词——Agent 自己读仓库自己装，一次安装长期跑命令
- 产品行只硬编码 Claude Code；Codex/Cursor/Cline/Qoder/WorkBuddy 等统一走 Agent 安装提示词（理由见 DESIGN.md 当日条目）
- "安装与使用"节上移至第四节

### 2026-09-21 插件化：仓库即市场 + 插件（阶段一）
- 起因：抖音评论拿 Matt Pocock 的 handoff 技能对比本项目；调研发现对手走官方插件市场分发，且 superpowers / mattpocock 两个标本同用"仓库即市场 + 插件（source "./"）"模式
- 新增 .claude-plugin/plugin.json + marketplace.json（市场名 yanlin-cheng，插件名 relayhand，source "./"）；claude-code/relayhand.md 迁移至 commands/relayhand.md
- README 双语安装节改为插件两行命令为主、裸文件 curl 降为退路；Step 0 自检加"插件安装跳过"并更新 URL
- 发版纪律新增：version 字段必 bump；阶段二规划记入 DESIGN.md，暂不执行

### 2026-09-21 补长板：Suggested skills 栏 + "何时不用 relayhand"边界节
- 对照 Matt Pocock handoff 技能暴露的两块长板当日补齐；决策与依据记 DESIGN.md 决策日志当日条目
- Suggested skills 栏拍板只进 commands/ 版（Claude Code 增强层），universal 版不收；version 两处 bump 1.0.0 → 1.1.0
- 个人副本同步：加"建议技能"栏 + 修正第零步正本 URL（claude-code/ → commands/，上轮漏同步）

### 2026-09-21 review 修复 + DESIGN.md 私有化
- review 窗口三项结论当日修复提交（README 重复标题、.gitignore 补本地日志/、DESIGN 序号笔误）
- 用户拍板 DESIGN.md 私有化：退出跟踪 + 历史抹除 + force push，决策依据记 DESIGN.md 当日条目；门面（README 双语、模板、CLAUDE.md）引用全部改为自足表述；version bump 1.1.0 → 1.1.1（模板 Personal extensions 节去 DESIGN.md 引用）
