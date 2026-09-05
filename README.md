# make-knowledge-cards

`make-knowledge-cards` 是一个轻量级 Codex Skill，用于把文章整理成少量、可独立复习的 Markdown 知识卡片。项目只包含 Skill 指令和界面元数据，不依赖额外脚本、第三方服务或网络访问。

## 项目解决什么问题

普通摘要容易把多个观点混在一起，也可能保留大量重复或次要内容。本项目帮助用户从一篇文章中筛选真正重要的知识，将其拆成单点卡片，并确保每张卡片都能追溯到原文。

它适合阅读复盘、学习笔记和文章要点整理，但不会用外部知识补充原文，也不会为了达到固定数量而编造内容。

## 主要功能

- 接受用户粘贴的文章，或本地 `.md`、`.markdown`、`.txt` 文件。
- 按重要性、实用性和解释价值筛选核心知识。
- 一张卡片只讲一个知识点，并合并重复或高度重叠的内容。
- 原文信息充足时生成 5–8 张卡片；不足时生成更少，最多不超过 8 张。
- 每张卡片包含标题、核心知识、简明解释，以及原文中的具体例子或一个可由卡片内容回答的自测问题。
- 保留原文中的限定条件、不确定性、数字、因果方向和观点归属，不添加原文之外的信息。
- 默认使用原文的主要语言，也可以按用户要求切换输出语言。

当前不支持网页抓取、PDF、Word 文档、Anki 导出或图形界面。网页或其他文档格式需要先转换为粘贴文本、Markdown 或 TXT。

## 安装方法

将 [`skills/make-knowledge-cards`](skills/make-knowledge-cards) 复制到 Codex 的 Skills 目录中。

Windows PowerShell：

```powershell
$codexRoot = if ($env:CODEX_HOME) { $env:CODEX_HOME } else { Join-Path $env:USERPROFILE ".codex" }
$skillsRoot = Join-Path $codexRoot "skills"
New-Item -ItemType Directory -Force $skillsRoot | Out-Null
Copy-Item -Recurse ".\skills\make-knowledge-cards" $skillsRoot
```

macOS 或 Linux：

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R skills/make-knowledge-cards "${CODEX_HOME:-$HOME/.codex}/skills/"
```

安装后的 Skill 名称为 `$make-knowledge-cards`。

## 使用方法

处理粘贴的文章：

```text
使用 $make-knowledge-cards，把下面的文章整理成知识卡片：

<粘贴文章正文>
```

处理本地 Markdown 或 TXT 文件：

```text
使用 $make-knowledge-cards，把 C:\notes\article.md 整理成知识卡片。
```

指定输出语言：

```text
使用 $make-knowledge-cards 处理 C:\notes\article.txt，并用英文输出。
```

结果默认直接返回为 Markdown。只有明确提出保存要求时，Codex 才会把结果写入文件。

## 输入输出示例

输入：

```text
检索练习要求学习者在不查看答案时主动回忆信息。只反复阅读不要求学习者检索答案，因此不容易暴露知识缺口。间隔学习把复习分散到多个时间点；文章建议在每次间隔复习时先尝试回忆，再核对答案。
```

输出（短材料只有两个重要知识点，因此不会强行生成 5 张）：

```markdown
# 知识卡片

## 1. 检索练习依靠主动回忆

**核心知识：** 检索练习要求学习者在不查看答案时主动回忆信息。

**简明解释：** 主动回忆能暴露尚未掌握的内容；单纯反复阅读不要求检索答案，因此不容易暴露这些缺口。

**自测问题：** 为什么检索练习有助于发现知识缺口？

## 2. 间隔复习应结合检索练习

**核心知识：** 间隔学习把复习分散到多个时间点，并可在每次复习时先回忆、再核对答案。

**简明解释：** 这种做法把文章中的时间安排与主动回忆流程结合起来。

**自测问题：** 一次间隔复习应按什么顺序进行？
```

Skill 指令位于 [`skills/make-knowledge-cards/SKILL.md`](skills/make-knowledge-cards/SKILL.md)，界面元数据位于 [`skills/make-knowledge-cards/agents/openai.yaml`](skills/make-knowledge-cards/agents/openai.yaml)。
