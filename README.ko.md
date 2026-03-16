# Skywork Skills

[English](README.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

AI 오피스 스위트를 위한 Agent Skills로, AI PPT, AI Document, AI Excel, AI Image, AI Search/DeepResearch, AI Music을 지원합니다.

이 스킬들은 Claude Code, Codex CLI, OpenClaw를 포함한 모든 skills 호환 에이전트에서 사용할 수 있습니다.

## 설치

### `npx skills`

```bash
npx skills add git@github.com:SkyworkAI/Skywork-Skills.git
```

### Claude Code

이 저장소의 내용을 프로젝트 루트(또는 Claude Code에서 사용하는 폴더)의 `/.claude` 디렉터리에 추가하세요. 자세한 내용은 공식 [Claude Skills 문서](https://docs.anthropic.com/en/docs/claude-code/skills)를 참고하세요.

### Codex CLI

`skills/` 디렉터리를 Codex skills 경로(보통 `~/.codex/skills`)에 복사하세요. 표준 스킬 형식은 [Agent Skills specification](https://github.com/anthropics/agent-skills)을 참고하세요.

### OpenCode

OpenCode skills 디렉터리(`~/.opencode/skills/`)에 전체 저장소를 클론하세요:

```bash
git clone https://github.com/SkyworkAI/Skywork-Skills.git ~/.opencode/skills/skywork-skills
```

내부 skills 폴더만 복사하지 마세요. 디렉터리 구조가 `~/.opencode/skills/skywork-skills/<skill-name>/SKILL.md`가 되도록 전체 저장소를 클론해야 합니다.

OpenCode는 `~/.opencode/skills/` 아래의 모든 `SKILL.md` 파일을 자동으로 감지합니다. 별도 설정은 필요 없으며, OpenCode를 재시작하면 스킬을 사용할 수 있습니다.

### ClawHub

ClawHub에서 개별 스킬을 직접 설치할 수 있습니다:

- [skywork-ppt](https://clawhub.ai/gxcun17/skywork-ppt)
- [skywork-excel](https://clawhub.ai/gxcun17/skywork-excel)
- [skywork-design](https://clawhub.ai/gxcun17/skywork-design)
- [skywork-doc](https://clawhub.ai/gxcun17/skywork-doc)
- [skywork-search](https://clawhub.ai/gxcun17/skywork-search)
- [skywork-music-maker](https://clawhub.ai/gxcun17/skywork-music-maker)

### OpenClaw

스킬 폴더를 OpenClaw skills 작업 디렉터리(`~/.openclaw/workspace/skills/`)에 복사하세요:

```bash
mkdir -p ~/.openclaw/workspace/skills
cp -R skywork-doc skywork-ppt skywork-design skywork-excel skywork-search skywork-music-maker ~/.openclaw/workspace/skills/
```

그다음 OpenClaw 게이트웨이를 재시작해 스킬을 다시 로드하세요:

```bash
openclaw gateway restart
```

## 스킬 목록

| 스킬 | 설명 |
|------|------|
| **skywork-doc** | 프롬프트와 참고 파일을 기반으로 전문 문서(docx, pdf, html, markdown)를 생성하고, 자동 웹 검색으로 최신 정보를 반영 |
| **skywork-ppt** | PowerPoint 생성/모사/편집 지원 - 주제 기반 생성, 기존 .pptx 스타일 템플릿 활용, 자연어 편집 |
| **skywork-design** | Skywork Image API로 이미지 생성 및 편집 - 포스터, 로고, 일러스트, image-to-image 편집, 화면비/해상도 제어 |
| **skywork-excel** | AI 기반 스프레드시트 작업 - 데이터/수식/차트가 포함된 Excel 생성, 기존 파일 분석, HTML 분석 리포트 생성 |
| **skywork-search** | AI 기반 실시간 웹 검색 - Skywork Search API에서 최신 정보를 가져와 리서치, 팩트체크, 콘텐츠 생성 워크플로우에 활용 |
| **skywork-music-maker** | Mureka AI API로 전문 음악 생성 - 노래, 연주곡, 가사, 보컬 클로닝을 자연어 설명(다국어)으로 제작 |

## 라이선스

[MIT](LICENSE)
