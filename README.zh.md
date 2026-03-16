# Skywork Skills

[English](README.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

面向 AI 办公套件的 Agent Skills，覆盖 AI PPT、AI 文档、AI Excel、AI 图像、AI 搜索/深度研究与 AI 音乐。

这些技能可用于任何兼容 skills 的 agent，包括 Claude Code 和 Codex CLI。

## 安装

### `npx skills`

```bash
npx skills add git@github.com:SkyworkAI/Skywork-Skills.git
```

### Claude Code

将本仓库内容添加到你项目根目录下的 `/.claude` 文件夹（或你在 Claude Code 中使用的目录）。更多说明请参考官方 [Claude Skills 文档](https://docs.anthropic.com/en/docs/claude-code/skills)。

### Codex CLI

将 `skills/` 目录复制到你的 Codex skills 路径（通常是 `~/.codex/skills`）。标准技能格式请参考 [Agent Skills 规范](https://github.com/anthropics/agent-skills)。

### OpenCode

将完整仓库克隆到 OpenCode skills 目录（`~/.opencode/skills/`）：

```bash
git clone https://github.com/SkyworkAI/Skywork-Skills.git ~/.opencode/skills/skywork-skills
```

不要只复制内部 skills 文件夹。请克隆完整仓库，以确保目录结构为 `~/.opencode/skills/skywork-skills/<skill-name>/SKILL.md`。

OpenCode 会自动发现 `~/.opencode/skills/` 下所有 `SKILL.md` 文件。无需额外配置，重启 OpenCode 后即可使用这些技能。

### ClawHub

从 ClawHub 直接安装各个技能：

- [skywork-ppt](https://clawhub.ai/gxcun17/skywork-ppt)
- [skywork-excel](https://clawhub.ai/gxcun17/skywork-excel)
- [skywork-design](https://clawhub.ai/gxcun17/skywork-design)
- [skywork-doc](https://clawhub.ai/gxcun17/skywork-doc)
- [skywork-search](https://clawhub.ai/gxcun17/skywork-search)
- [skywork-music-maker](https://clawhub.ai/gxcun17/skywork-music-maker)

### OpenClaw

将技能目录复制到 OpenClaw 的 skills 工作目录（`~/.openclaw/workspace/skills/`）：

```bash
mkdir -p ~/.openclaw/workspace/skills
cp -R skywork-doc skywork-ppt skywork-design skywork-excel skywork-search skywork-music-maker ~/.openclaw/workspace/skills/
```

然后重启 OpenClaw 网关以重新加载技能：

```bash
openclaw gateway restart
```

## 技能列表

| 技能 | 说明 |
|------|------|
| **skywork-doc** | 基于提示词和参考文件生成专业文档（docx、pdf、html、markdown），并可通过自动网页搜索获取最新内容 |
| **skywork-ppt** | 生成、仿写与编辑 PowerPoint 演示文稿，可从主题创建、基于现有 .pptx 作为风格模板，或通过自然语言修改 |
| **skywork-design** | 通过 Skywork Image API 生成与编辑图像，支持海报、Logo、插画、图生图编辑，以及宽高比和分辨率控制 |
| **skywork-excel** | AI 驱动的电子表格能力，可创建含数据/公式/图表的 Excel 文件，分析现有文件并生成 HTML 分析报告 |
| **skywork-search** | AI 驱动的实时网页搜索，通过 Skywork Search API 获取最新信息，用于研究、事实核查与内容生成流程 |
| **skywork-music-maker** | 通过 Mureka AI API 创作专业音乐，支持歌曲、伴奏、歌词与人声克隆，并支持任意语言的自然语言描述 |

## 许可证

[MIT](LICENSE)
