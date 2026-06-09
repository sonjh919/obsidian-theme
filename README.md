# obsidian-theme

A Claude Code skill that lets you create, edit, and switch Obsidian themes using natural language — no CSS knowledge required.

> "따뜻한 카페" → a full Obsidian theme. "코드블록 배경 좀 더 어둡게" → live diff and apply.

## What it does

Three modes, picked at invocation time:

- **새로 (Create)** — Describe a mood in plain language. The skill suggests 3 palette candidates from a curated catalog, asks 4 quick questions (light/dark, font, corner radius, spacing), and writes a complete theme into your vault's `.obsidian/themes/<name>/`.
- **수정 (Edit)** — Tell it what to change ("link color to orange"). It maps your words to the right CSS variables (using a cheatsheet validated against Obsidian's official docs), shows a diff, applies it. External themes (AnuPpuccin etc.) are never modified — they get a snippet override instead.
- **스위치 (Switch)** — Lists all themes in your vault. Pick one, it patches `appearance.json`. CLI-only theme switching.

The skill never overwrites an existing theme. New themes are added under fresh names so multiple themes coexist in your vault.

## Install

```bash
# Clone into your Claude Code skills directory
git clone https://github.com/sonjh919/obsidian-theme.git ~/.claude/skills/obsidian-theme
```

That's it. Claude Code auto-discovers skills under `~/.claude/skills/`.

To update later:

```bash
cd ~/.claude/skills/obsidian-theme && git pull
```

## Usage

In Claude Code, invoke with any of:

- `/obsidian-theme`
- "옵시디언 테마 만들어줘"
- "테마 바꿔줘"
- "옵시디언 꾸미기"

The skill will:

1. Find your vault (scans `~/Documents` and `~`; if multiple, you pick)
2. Ask which mode (스위치 / 새로 / 수정) — vault state determines the recommended default
3. Walk you through that mode's flow

### Example session — Create

```
You: /obsidian-theme
Skill: 어떤 작업을 할까요?
       1. 스위치 — 만들어둔 테마들 중 하나로 갈아끼기
       2. 새로 — 자연어 묘사로 새 테마 만들기  (추천)
       3. 수정 — 현재 테마의 일부를 자연어로 튜닝

You: 2
Skill: 어떤 느낌의 테마를 원하세요?
You: 따뜻한 카페 같은 느낌

Skill: 세 가지 팔레트 후보예요. 어느 게 가장 가까워요?
       [1] warm-cafe ☕  배경 #f7f1e8 · 액센트 #c97b3b
       [2] sunset-warm 🌅  배경 #1f1410 · 액센트 #ff8847
       [3] (즉석) 배경 #faf3e7 · 액센트 #d4925c

You: 1
Skill: 네 가지만 더 정해주세요.
       Q1. 라이트 / 다크 / 둘 다  →  둘 다
       Q2. 폰트  →  Serif
       Q3. 모서리  →  8px
       Q4. 간격  →  보통

Skill: ✅ 테마 "warm-cafe" 생성 완료
       📂 <vault>/.obsidian/themes/warm-cafe/theme.css
       🎨 appearance.json 패치 완료 — 옵시디언에서 즉시 확인하세요
```

## What's inside

```
obsidian-theme/
├── SKILL.md           # Routing entry — vault detection + 3-mode branch
├── create-flow.md     # New theme bootstrap (7 steps)
├── edit-flow.md       # Existing theme tuning (5 steps)
├── switch-flow.md     # Theme switching (3 steps)
├── variables.md       # CSS variable cheatsheet + natural-language mapping
│                      # Cross-validated against docs.obsidian.md
└── palettes.md        # 14-mood palette catalog (warm-cafe, retro-terminal,
                       # nordic-cold, sakura, dracula, tokyo-rain, …)
```

## Design choices

- **Single full theme** as the unit, not multiple snippets. Cleaner for users starting from scratch.
- **Never overwrite** — new themes get fresh names; old themes stay in the `themes/` folder so you can A/B compare.
- **External themes are sacred** — edits to AnuPpuccin, Minimal, etc. go into a separate snippet (`.obsidian/snippets/obsidian-theme-override.css`), leaving the original untouched.
- **Marker header** (`/* obsidian-theme: managed */`) on every generated theme so edit-mode can distinguish "ours" from "yours."
- **HSL accent system** — uses Obsidian's `--accent-h/s/l` so the rest (`--interactive-accent` etc.) auto-derives.
- **Routing-only SKILL.md** (~80 lines), heavy content lazy-loaded from flow/catalog files. Keeps first-invocation context cheap.

## Caveats

- **Cascade priority**: if your vault has many CSS snippets active (or `textFontFamily`/`interfaceFontFamily` set in `appearance.json`), they can override theme CSS. On a clean vault, themes apply 100% as intended. See `variables.md` for details.
- **Obsidian must be running** for hot reload. Otherwise changes apply on next launch.
- **Tested on**: macOS, Obsidian 1.x. Should work cross-platform but Windows/Linux paths in flow files assume Unix `find`.

## Requirements

- [Claude Code](https://www.anthropic.com/claude-code)
- [Obsidian](https://obsidian.md/) 1.0+
- Bash (macOS/Linux). Windows users may need to adjust path handling.

## License

MIT — see [LICENSE](LICENSE).

## Contributing

Issues and PRs welcome. Especially:

- More moods for `palettes.md`
- Additional CSS variables for `variables.md` (with docs.obsidian.md cross-reference)
- Windows path compatibility
- Image-upload mode (color extraction from reference screenshots)
