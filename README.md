# CET Tailor

> 🎯 一套围绕个人学习档案运转的四六级 AI 技能包。
> 告别千篇一律的课程和题库，打造只属于你的备考路径。

CET Tailor 不是课程，不是题库，也不是又一个背单词 App。
它是一组 AI 原生技能，围绕一个核心理念：**每个学习者都应该有一个活档案，随着每一次练习不断更新。**

每个技能都会读取你的档案、根据你的薄弱项调整，并把本次结果写回档案。
最终形成的，是一条真正属于你的备考路径，而不是给所有人准备的同一套课程。

**如果觉得这个项目有点意思，点个 ⭐ 就是最大的鼓励！**

---

## 这是什么

CET Tailor 是一套 [Agent Skills](https://github.com/anthropics/skills) 技能包，用于大学英语四六级备考。

它的核心不是“教英语”，而是“围绕你的档案，组织一套个性化的训练流程”。

- **不是课程**：没有固定课时，没有统一进度。
- **不是题库**：不托管真题，只推荐来源。
- **不是 App**：没有独立的客户端，运行在支持 Agent Skills 的 AI 代理中。

---

## 核心理念

| 理念 | 说明 |
|---|---|
| **活档案** | 学习者档案不是一次性问卷，每次训练后都会更新 |
| **技能协同** | 词汇、阅读、翻译、写作等技能共享同一个档案和错题本 |
| **个性化路由** | 先导技能根据你的最新薄弱项，推荐下一步该练什么 |
| **AI 原生** | 构建为 Agent Skills，而非独立应用或网站 |

---

## 技能列表

| 技能 | 作用 |
|---|---|
| `cet4-6-profiler` | 先导：建档、诊断、更新档案、分发请求 |
| `cet4-6-vocab-trainer` | 词汇：词典查询、词汇量检测、背单词 |
| `cet4-6-reading-coach` | 阅读：选词填空、长篇阅读、仔细阅读、长难句分析 |
| `cet4-6-translation-tutor` | 翻译：逐句批改、词汇搭配语法讲解 |
| `cet4-6-writing-tutor` | 写作：逐段批改、内容结构语言分析 |
| `cet4-6-listening-trainer` | 听力：语音规则、真题练习、错因分析 |
| `cet4-6-speaking-coach` | 口语：框架讲解、文本模拟练习 |
| `cet4-6-mistake-book` | 错题本：半自动记录、复习、薄弱点分析 |
| `cet4-6-study-planner` | 学习计划：按时间、薄弱项生成周计划 |
| `cet4-6-past-paper-analyzer` | 真题限时练习：组卷、计时、分发批改、数据分析 |

---

## 安装

### 前提

你的 AI 代理需要支持 Agent Skills。目前支持的主流宿主包括：

- **Claude Code**
- **Cursor**
- **GitHub Copilot**
- **Cline / Roo Code / Windsurf**
- 其他兼容 `SKILL.md` 格式的 AI 代理

### 方式一：使用 `gh skill`（GitHub 官方）

确保已安装 [GitHub CLI](https://cli.github.com/)（v2.90.0 或以上）：

```bash
gh skill install <你的GitHub用户名>/cet4-6-skills --all
指定安装到某个宿主：

bash
gh skill install <你的GitHub用户名>/cet4-6-skills --all --agent claude-code
方式二：使用 npx skills
确保已安装 Node.js：

bash
npx skills add <你的GitHub用户名>/cet4-6-skills -g
安装时按提示选择目标宿主。

方式三：手动复制
把 skills/ 目录下的技能文件夹复制到你所用宿主的技能目录中。常见位置：

宿主	技能目录
Claude Code	~/.claude/skills/ 或 .claude/skills/
Cursor	~/.cursor/skills/ 或 .cursor/skills/
GitHub Copilot	.github/skills/ 或 ~/.copilot/skills/
方式四：当作提示词使用
如果你的宿主不支持 Agent Skills，可以打开任意一个 SKILL.md，把正文内容粘贴给 AI 作为提示词使用。功能会打折扣，但核心流程仍然可用。

使用
安装后，直接对 AI 说话即可。你不需要记住技能名，AI 会根据你的意图自动匹配。

示例
首次使用，让 AI 了解你：

我准备考六级，不知道怎么开始。

练习阅读：

帮我看看这篇六级仔细阅读。（附题目和原文）

我想练阅读。

批改翻译：

帮我批改这篇翻译。（附中文原文和英文译文）

批改作文：

帮我看看这篇六级作文。（附题目和作文）

背单词：

significant 这个词怎么用？

我想测一下词汇量。

我想背单词。

限时做真题：

帮我限时做一套六级真题。

查看错题：

打开错题本。

制定计划：

帮我制定一个 30 天的六级备考计划。

工作流程
text
用户请求
    ↓
cet4-6-profiler（先导，总入口）
    ↓ 判断意图，分发到具体技能
    ↓
cet4-6-vocab-trainer / reading-coach / translation-tutor
cet4-6-writing-tutor / listening-trainer / speaking-coach
cet4-6-past-paper-analyzer / study-planner
    ↓ 训练结束
    ↓
cet4-6-mistake-book（错题本，半自动记录）
    ↓
cet4-6-profiler（更新档案）
目录结构
text
cet4-6-skills/
├── README.md
├── LICENSE
├── question-bank/                             ← 全局题库
│   ├── index.md
│   ├── vocab.md
│   ├── grammar.md
│   ├── listening.md
│   ├── reading.md
│   ├── translation.md
│   ├── writing.md
│   └── past-papers.md
└── skills/
    ├── cet4-6-profiler/
    │   ├── SKILL.md
    │   └── references/
    ├── cet4-6-vocab-trainer/
    │   ├── SKILL.md
    │   └── references/
    ├── cet4-6-reading-coach/
    │   ├── SKILL.md
    │   └── references/
    ├── cet4-6-translation-tutor/
    │   ├── SKILL.md
    │   └── references/
    ├── cet4-6-writing-tutor/
    │   ├── SKILL.md
    │   └── references/
    ├── cet4-6-listening-trainer/
    │   ├── SKILL.md
    │   └── references/
    ├── cet4-6-speaking-coach/
    │   ├── SKILL.md
    │   └── references/
    ├── cet4-6-mistake-book/
    │   └── SKILL.md
    ├── cet4-6-study-planner/
    │   └── SKILL.md
    └── cet4-6-past-paper-analyzer/
        └── SKILL.md
常见问题
需要什么宿主？
需要支持 Agent Skills 的 AI 代理，例如 Claude Code、Cursor、GitHub Copilot 等。如果你的宿主不支持，也可以把 SKILL.md 内容当作提示词使用。

能离线用吗？
技能文件本身是纯文字的，可以离线保存。但运行时需要 AI 代理，AI 代理通常需要联网。

档案存在哪里？
取决于你的宿主：

支持文件读写的宿主 → 保存为 learner-profile.md

支持长期记忆的宿主 → 存在记忆中

都不支持 → 每次更新后提醒你手动复制保存

题目从哪来？
不托管真题。技能会推荐合法的真题来源（官方渠道、新东方官网、学校数据库等），由你自己获取。找不到真题时，AI 会现场生成同等难度的模拟题，并标注“非真题”。

会侵权吗？
不会。本项目不托管、不存储、不播放任何受版权保护的真题文件。只推荐来源，由用户自行获取。

能保证通过吗？
不能。CET Tailor 帮你最大化准备效率，但不承诺考试结果。

贡献
欢迎提交 Issue 或 Pull Request。

如果你有好的四六级学习流程、诊断题、范文、错因分类，欢迎补充到对应的 references/ 或 question-bank/ 中。

如果这个项目帮你省了几百块报班费，或者让你的备考稍微不那么痛苦，回来点个 ⭐ 呗～