---
name: Skywork-ppt
description: |
  Use this skill when the user wants to work with PowerPoint presentations. Triggers include:
  - Generating a new PPT from a topic: 'generate a PPT' / '帮我做个PPT' / 'PPTを作って' / 'PPT 만들어줘', 'create a presentation about X' / '生成关于X的演示文稿' / 'Xについてのプレゼンを作って' / 'X에 대한 발표 자료 만들어줘', 'help me make slides' / '帮我做幻灯片' / 'スライドを作って' / '슬라이드 만들어줘'
  - Imitating an existing .pptx style/template: 'use this template' / '用这个模板' / 'このテンプレートを使って' / '이 템플릿을 써줘', 'imitate this PPT' / '仿照这个PPT' / 'このPPTを真似して' / '이 PPT를 따라 해줘', 'imitate this style' / '仿照这个风格' / 'このスタイルを真似して' / '이 스타일을 따라 해줘'
  - Editing an existing PPT via natural language: 'modify slide N' / '修改第N页' / 'N枚目のスライドを修正して' / 'N번 슬라이드 수정해줘', 'change the background' / '更换背景' / '背景を変えて' / '배경 바꿔줘', 'add a slide' / '新增一页幻灯片' / 'スライドを追加して' / '슬라이드 추가해줘', 'make it more beautiful' / '美化一下PPT' / 'もっときれいにして' / '더 예쁘게 다듬어줘', 'edit this PPT' / '改一下这个PPT' / 'このPPTを編集して' / '이 PPT 수정해줘'
  - Local file operations on .pptx (no backend): 'delete slide N' / '删除第N页' / 'N枚目のスライドを削除して' / 'N번 슬라이드 삭제해줘', 'reorder slides' / '调整幻灯片顺序' / 'スライドを並べ替えて' / '슬라이드 순서 바꿔줘', 'merge pptx' / '合并PPT' / 'pptxを結合して' / 'pptx 합쳐줘', 'extract slides' / '提取幻灯片' / 'スライドを抽出して' / '슬라이드 추출해줘', 'how many slides' / '有多少页幻灯片' / 'スライドは何枚ある' / '슬라이드 몇 장이야'
metadata:
  openclaw:
    requires:
      bins:
        - python3
      env:
        - SKYWORK_API_KEY
    primaryEnv: SKYWORK_API_KEY
---

# PPT Write Skill

Four capabilities: **generate**, **template imitation**, **edit existing PPT**, and **local file operations**.

---

## Prerequisites

### API Key Configuration (Required First)
This skill requires a **SKYWORK_API_KEY** to be configured in OpenClaw.

If you don't have an API key yet, please visit:
**https://skywork.ai**

For detailed setup instructions, see:
[references/apikey-fetch.md](references/apikey-fetch.md)

---

## Privacy & Remote Calls (Read Before Use)

- **Remote upload & processing**: Layers 1/2/4 upload local files and send the full, verbatim user query to the Skywork service. Avoid sensitive or confidential content unless you trust the remote service and its data handling policies.
- **Local-only operations**: Layer 3 (local ops) runs entirely on-device and does **not** call the remote gateway. Use Layer 3 if you need strict local processing.
- **Polling behavior**: The generation/edit workflows include periodic status polling (about every 5 seconds) while waiting for backend jobs. This is expected.

---

## Routing — Identify the user's intent first

| User intent | Which path |
|-------------|------------|
| Generate a new PPT from a topic, set of requirements or reference files | **Layer 1** — Generate |
| Use an existing .pptx as a layout/style template to create a new presentation | **Layer 2** — Imitate |
| Edit an existing PPT: modify slides, add slides, change style, split/merge | **Layer 4** — Edit |
| Delete / reorder / extract / merge slides in a local file (no backend) | **Layer 3** — Local ops |

---

## Environment check (always run this first)

**This skill requires Python 3 (>=3.8). Run the following before any script to locate a valid Python binary and install dependencies.**

```bash
PYTHON_CMD=""
for cmd in python3 python python3.13 python3.12 python3.11 python3.10 python3.9 python3.8; do
  if command -v "$cmd" &>/dev/null && "$cmd" -c "import sys; exit(0 if sys.version_info >= (3,8) else 1)" 2>/dev/null; then
    PYTHON_CMD="$cmd"
    break
  fi
done

if [ -z "$PYTHON_CMD" ]; then
  echo "ERROR: Python 3.8+ not found."
  echo "Install on macOS: brew install python3  or visit https://www.python.org/downloads/"
  exit 1
fi

echo "Found Python: $PYTHON_CMD ($($PYTHON_CMD --version))"

$PYTHON_CMD -m pip install -q --break-system-packages python-pptx
echo "Dependencies ready."
```

> After this check, replace `python` with the discovered `$PYTHON_CMD` (e.g. `python3`) in all subsequent commands.

---

## Layer 1 — Generate PPT

### Steps
0. **REQUIRED FIRST STEP** — Read [workflow_generate.md](workflow_generate.md) NOW, before taking any other action. After reading, output exactly: `✅ workflow_generate.md loaded.` — then proceed.
1. **Environment check** — run the check above to get `$PYTHON_CMD`.
2. **Upload reference files** (if the user provides local files as content source) — parse the file using tool in script/parse_file.py and pass the result to `--files`. See the `--files` note below.
3. **Web search** (required if no relevant content is already in the conversation) — call web_search tool in script to search the topic and distill results into a `reference-file` file of ≤ 2000 words.
4. **Run the script**:
   > **Important**: set exec tool `yieldMs` to `600000` (10 minutes).
5. **Deliver** — provide the absolute `.pptx` path and the download URL.

---

## Layer 2 — Imitate PPT (template-based generation)

### Steps
0. **REQUIRED FIRST STEP** - Read [workflow_imitate.md](workflow_imitate.md) immidiately before any action you do!!!
1. **Environment check** — run the check above to get `$PYTHON_CMD`.
2. **Locate the template** — extract the absolute path of the local `.pptx` from the user's message; ask the user if it's unclear.
3. **Upload the template** — upload it and extract `TEMPLATE_URL` from the output.
4. **Upload reference files** (if the user provides additional local files as content source) — parse the file using tool in script/parse_file.py and pass the result to `--files`. See the `--files` 
5. **Web search** (required if no relevant content is already in the conversation) — call web_search tool in script to search the new topic and distill results into a `reference-file` file of ≤ 2000 words.
6. **Run the script**:
   > **Important**: set exec tool `yieldMs` to `600000` (10 minutes).
7. **Deliver** — provide the absolute `.pptx` path, the download URL, and the template filename used.

---

## Layer 4 — Edit PPT (AI-powered modification)

Use this layer when the user wants to modify an existing PPT using natural language. Requires an OSS/CDN URL of the PPTX (from a previous generation or upload).

### Steps
0. **Detailed workflow** - Read [workflow_edit.md](workflow_edit.md) immediately before any action you do!!!
1. **Environment check** — run the check above to get `$PYTHON_CMD`.
2. **Get PPTX URL** — from the user's message or upload a local file first.
3. **Run the script** with `--pptx-url`:
   ```bash
   $PYTHON_CMD scripts/run_ppt_write.py "edit instruction" \
     --language Chinese \
     --pptx-url "https://cdn.example.com/file.pptx" \
     -o /absolute/path/output.pptx
   ```
   > **Important**: set exec tool `yieldMs` to `600000` (10 minutes).
4. **Deliver** — provide download link, local path, and summary of changes.

---

## Layer 3 — Local file operations

```bash
# Inspect slide count and titles
$PYTHON_CMD scripts/local_pptx_ops.py info --file my.pptx

# Delete slides (1-based index; supports ranges like 3,5,7-9; omit -o to overwrite in place)
$PYTHON_CMD scripts/local_pptx_ops.py delete --file my.pptx --slides 3,5,7-9 -o trimmed.pptx

# Reorder slides (must list every slide, no omissions)
$PYTHON_CMD scripts/local_pptx_ops.py reorder --file my.pptx --order 2,1,4,3,5

# Extract a subset of slides into a new file
$PYTHON_CMD scripts/local_pptx_ops.py extract --file my.pptx --slides 1-3 -o subset.pptx

# Merge multiple files
$PYTHON_CMD scripts/local_pptx_ops.py merge --files a.pptx b.pptx -o merged.pptx
```

Read [workflow_local.md](workflow_local.md) immidiately before any action you do!!!

---

## Error Handling

- **Insufficient benefit**: When calling scripts (generate, imitate, or edit), the script or log may show a message like `Insufficient benefit. Please upgrade your account at {url}`, meaning the user's benefit level does not meet the requirement for this skill.

### How to reply when benefit is insufficient

When you detect the above, **reply in the user's current language** — do not echo the English message. Use this pattern:

- Convey: "Sorry, PPT generation failed. This skill requires upgrading your Skywork membership to use." then a single call-to-action link.
- **Format**: One short sentence in the user's language + a link like `[Upgrade now →](url)` or the equivalent in their language .
- **URL**: Extract the upgrade URL from the log/script output (e.g. the `at https://...` part).

> Note: Only suggest upgrading when the error is **Insufficient benefit**. For auth errors like `NO_TOKEN` / `INVALID_TOKEN` / `401` / “invalid API key”, keep the error code / raw message and guide users to update `SKYWORK_API_KEY`. **Do not** suggest upgrading membership.

---

## Dependencies

- **Python 3.8+** (required) — `python3` / `python` must be on PATH
- Layer 3 local ops: `pip install python-pptx --break-system-packages`

(The environment check step installs all required dependencies automatically.)

---

## Which layer to trigger?

| Scenario | Use |
|----------|-----|
| Generate a PPT from a topic or existing reference files | Layer 1 |
| Imitate the layout/style of an existing .pptx | Layer 2 |
| Edit/modify an existing PPT via natural language | Layer 4 |
| Delete / reorder / extract / merge local .pptx files (no backend) | Layer 3 |
