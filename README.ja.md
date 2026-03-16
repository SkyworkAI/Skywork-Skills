# Skywork Skills

[English](README.md) | [中文](README.zh.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

AIオフィススイート向けのAgent Skills。AI PPT、AI Document、AI Excel、AI Image、AI Search/DeepResearch、AI Musicに対応しています。

これらのスキルは、Claude Code、Codex CLI、OpenClaw を含む、skills互換エージェントで利用できます。

## インストール

### `npx skills`

```bash
npx skills add git@github.com:SkyworkAI/Skywork-Skills.git
```

### Claude Code

このリポジトリの内容を、プロジェクトルート（または Claude Code で使用しているディレクトリ）の `/.claude` フォルダに追加してください。詳細は公式の [Claude Skills ドキュメント](https://docs.anthropic.com/en/docs/claude-code/skills) を参照してください。

### Codex CLI

`skills/` ディレクトリを Codex の skills パス（通常は `~/.codex/skills`）にコピーしてください。標準フォーマットは [Agent Skills specification](https://github.com/anthropics/agent-skills) を参照してください。

### OpenCode

OpenCode の skills ディレクトリ（`~/.opencode/skills/`）に、このリポジトリ全体をクローンします。

```bash
git clone https://github.com/SkyworkAI/Skywork-Skills.git ~/.opencode/skills/skywork-skills
```

内部の skills フォルダだけをコピーしないでください。ディレクトリ構造が `~/.opencode/skills/skywork-skills/<skill-name>/SKILL.md` になるよう、リポジトリ全体をクローンしてください。

OpenCode は `~/.opencode/skills/` 配下の `SKILL.md` を自動検出します。追加設定は不要で、OpenCode 再起動後にスキルが利用可能になります。

### ClawHub

ClawHub から各スキルを直接インストールできます：

- [skywork-ppt](https://clawhub.ai/gxcun17/skywork-ppt)
- [skywork-excel](https://clawhub.ai/gxcun17/skywork-excel)
- [skywork-design](https://clawhub.ai/gxcun17/skywork-design)
- [skywork-doc](https://clawhub.ai/gxcun17/skywork-doc)
- [skywork-search](https://clawhub.ai/gxcun17/skywork-search)
- [skywork-music-maker](https://clawhub.ai/gxcun17/skywork-music-maker)

### OpenClaw

スキルフォルダを OpenClaw の skills ワークスペース（`~/.openclaw/workspace/skills/`）にコピーします。

```bash
mkdir -p ~/.openclaw/workspace/skills
cp -R skywork-doc skywork-ppt skywork-design skywork-excel skywork-search skywork-music-maker ~/.openclaw/workspace/skills/
```

その後、OpenClaw のゲートウェイを再起動してスキルを再読み込みしてください。

```bash
openclaw gateway restart
```

## スキル一覧

| スキル | 説明 |
|-------|------|
| **skywork-doc** | プロンプトと参照ファイルからプロフェッショナルな文書（docx、pdf、html、markdown）を生成し、自動Web検索で最新情報を反映 |
| **skywork-ppt** | PowerPoint資料の生成・模倣・編集に対応。トピックから新規作成、既存 .pptx をスタイルテンプレートとして利用、自然言語で編集 |
| **skywork-design** | Skywork Image API で画像を生成・編集。ポスター、ロゴ、イラスト、画像編集（image-to-image）、アスペクト比と解像度の制御に対応 |
| **skywork-excel** | AIによるスプレッドシート操作。データ/数式/グラフ付きExcel作成、既存ファイル分析、HTML分析レポート生成 |
| **skywork-search** | AIによるリアルタイムWeb検索。Skywork Search API から最新情報を取得し、リサーチ、ファクトチェック、コンテンツ生成ワークフローに活用 |
| **skywork-music-maker** | Mureka AI API でプロ品質の音楽を作成。楽曲、インストゥルメンタル、歌詞、音声クローンを多言語の自然言語入力から生成 |

## ライセンス

[MIT](LICENSE)
