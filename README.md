# Skywork Skills

[English](README.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

Agent Skills for AI office suites, including AI PPT, AI Document, AI Excel, AI Image, AI Search/DeepResearch and AI Music.

These skills can be used by any skills-compatible agent, including Claude Code, Codex CLI and OpenClaw.

Get started at [skywork.ai/skill-landing](https://skywork.ai/skill-landing).

## Installation

### `npx skills`

```bash
npx skills add git@github.com:SkyworkAI/Skywork-Skills.git
```

### Claude Code

Add the contents of this repo to a `/.claude` folder in the root of your project (or whichever folder you're using with Claude Code). See more in the official [Claude Skills documentation](https://docs.anthropic.com/en/docs/claude-code/skills).

### Codex CLI

Copy the `skills/` directory into your Codex skills path (typically `~/.codex/skills`).

### OpenCode

Clone the entire repo into the OpenCode skills directory (`~/.opencode/skills/`):

```bash
git clone https://github.com/SkyworkAI/Skywork-Skills.git ~/.opencode/skills/skywork-skills
```

Do not copy only the inner skills folder — clone the full repo so the directory structure is `~/.opencode/skills/skywork-skills/<skill-name>/SKILL.md`.

OpenCode auto-discovers all `SKILL.md` files under `~/.opencode/skills/`. No config changes needed. Skills become available after restarting OpenCode.

### ClawHub

Install individual skills directly from ClawHub:

- [skywork-ppt](https://clawhub.ai/gxcun17/skywork-ppt)
- [skywork-excel](https://clawhub.ai/gxcun17/skywork-excel)
- [skywork-design](https://clawhub.ai/gxcun17/skywork-design)
- [skywork-doc](https://clawhub.ai/gxcun17/skywork-doc)
- [skywork-search](https://clawhub.ai/gxcun17/skywork-search)
- [skywork-music-maker](https://clawhub.ai/gxcun17/skywork-music-maker)

### OpenClaw

Copy the skill folders into the OpenClaw skills workspace (`~/.openclaw/workspace/skills/`):

```bash
mkdir -p ~/.openclaw/workspace/skills
cp -R skywork-doc skywork-ppt skywork-design skywork-excel skywork-search skywork-music-maker ~/.openclaw/workspace/skills/
```

Then restart the OpenClaw gateway to reload skills:

```bash
openclaw gateway restart
```

## Skills

| Skill | Description |
|-------|-------------|
| **skywork-doc** | Generate professional documents (docx, pdf, html, markdown) from prompts and reference files with automatic web search for up-to-date content |
| **skywork-ppt** | Generate, imitate, and edit PowerPoint presentations — create from topic, use existing .pptx as style template, or edit via natural language |
| **skywork-design** | Generate and edit images via Skywork Image API — posters, logos, illustrations, image-to-image editing with aspect ratio and resolution control |
| **skywork-excel** | AI-powered spreadsheet operations — create Excel files with data, formulas, charts; analyze existing files; generate HTML analysis reports |
| **skywork-search** | AI-powered web search for real-time information — retrieve up-to-date content from the Skywork Search API for research, fact-checking, and content generation workflows |
| **skywork-music-maker** | Create professional music with Mureka AI API — songs, instrumentals, lyrics, and vocal cloning from natural language descriptions in any language |


## License

[MIT](LICENSE)
