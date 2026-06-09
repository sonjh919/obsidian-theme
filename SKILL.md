---
name: obsidian-theme
description: Claude 와 함께 옵시디언 테마를 자연어로 만들고·수정하고·전환하는 스킬. 사용자가 "옵시디언 테마", "옵시디언 꾸미기", "테마 만들어줘", "테마 바꿔줘", "테마 갈아끼우자", "/obsidian-theme" 라고 하면 이 스킬을 사용한다. CSS 지식 없이도 "따뜻한 카페", "레트로 터미널" 같은 자연어 묘사만으로 풀 테마를 생성한다.
user-invocable: true
---

# Obsidian Theme 스킬

Claude Code + 옵시디언 사용자가 자연어로 옵시디언 테마를 만들고·수정하고·전환할 수 있게 돕는 스킬이다. 세 모드 (**스위치 / 새로 / 수정**) 를 호출 시점에 분기로 선택한다.

## 모드 개요

- **스위치** — vault 의 테마들 중 하나로 갈아끼기 (`switch-flow.md`)
- **새로** — 자연어 묘사로 새 풀 테마 생성 (`create-flow.md`)
- **수정** — 현재 활성 테마의 일부를 자연어로 튜닝 (`edit-flow.md`)

세 모드는 별도 흐름 파일로 분리되어 있다. 분기 후 해당 파일을 Read 하여 그 절차를 따른다.

## Step 0: Vault 식별

사용자의 옵시디언 vault 위치를 확인한다. vault 가 여러 개일 수 있으므로 자동 가정 X.

```bash
find ~/Documents ~ -maxdepth 4 -type d -name .obsidian 2>/dev/null | head -20
```

- 현재 작업 디렉터리(`pwd`) 가 vault (`.obsidian/` 존재) 면 **기본값** 으로 제시
- 여러 개 발견 시 번호 매겨서 사용자에게 선택받음
- 옵시디언이 현재 열어둔 vault 정보: `~/Library/Application Support/obsidian/obsidian.json` 의 `vaults` 항목에서 `open: true` 확인 가능 (있으면 표시)
- 선택한 vault 의 절대경로를 `$VAULT` 로 세션 내내 기억

## Step 1: 모드 분기 질문

vault 의 `.obsidian/themes/` 와 `.obsidian/appearance.json` 의 `cssTheme` 을 먼저 확인하여 추천 표시를 결정한다.

```bash
ls "$VAULT/.obsidian/themes/" 2>/dev/null
cat "$VAULT/.obsidian/appearance.json" 2>/dev/null
```

**추천 표시 규칙**:

| vault 상태 | 추천 모드 |
|---|---|
| 테마 2개 이상 (이 스킬 만든 것 1개 이상 포함) | 스위치 |
| 이 스킬 만든 테마 1개 + 그 테마가 현재 활성 | 수정 |
| 이 스킬 만든 테마 0개 | 새로 |

"이 스킬이 만든 테마" 는 `themes/<name>/theme.css` 첫 줄에 다음 marker 가 있는지로 판별:

```
/* obsidian-theme: managed */
```

사용자에게 질문:

```
어떤 작업을 할까요?

1. 스위치 — 만들어둔 테마들 중 하나로 갈아끼기
2. 새로   — 자연어 묘사로 새 테마 만들기
3. 수정   — 현재 테마의 일부를 자연어로 튜닝
```

추천 모드 옆에 `(추천)` 표시. 사용자가 번호 또는 이름으로 답하면 해당 흐름 파일을 Read 하여 진입한다.

## Step 2: 흐름 파일 Read 후 위임

| 사용자 선택 | Read 할 파일 |
|---|---|
| 1 / 스위치 | `~/.claude/skills/obsidian-theme/switch-flow.md` |
| 2 / 새로 | `~/.claude/skills/obsidian-theme/create-flow.md` |
| 3 / 수정 | `~/.claude/skills/obsidian-theme/edit-flow.md` |

해당 파일을 Read 한 뒤 그 안의 Step 1 부터 순서대로 진행한다. 흐름 파일은 `$VAULT` 가 이미 식별되어 있다고 가정하고 시작한다.

## 보조 자산

세 흐름이 공통으로 참조하는 카탈로그 파일들이다. 흐름 안에서 필요한 시점에 Read.

- `variables.md` — 옵시디언 CSS 변수 cheatsheet. 자연어 → 변수 매핑표 포함. 새로·수정 모드가 사용
- `palettes.md` — 무드 → 4색 hex 카탈로그 (warm-cafe, retro-terminal, nordic-cold 등). 새로 모드가 사용

## 주의사항

- 사용자 vault 의 파일을 수정할 때는 항상 사용자 확인을 받은 뒤 진행한다 (`.obsidian/appearance.json`, `.obsidian/themes/*`, `.obsidian/snippets/*`)
- 기존 테마를 덮어쓰지 않는다. 새 테마는 항상 새 이름으로 추가하여 옵시디언 themes 폴더에 공존하게 한다. 구 테마 삭제는 사용자가 명시적으로 요청할 때만 안내
- 외부 테마 (AnuPpuccin 등 marker 없는 테마) 는 절대 직접 수정하지 않는다. 수정 모드에서 외부 테마가 현재 활성이면 `.obsidian/snippets/obsidian-theme-override.css` snippet 으로 override 한다
- CSS 변경은 옵시디언이 hot reload 한다 (파일 저장 즉시 반영). 사용자에게 "옵시디언 화면 확인하세요" 안내만 충분
- `appearance.json` 패치 후 옵시디언이 켜져 있어야 즉시 반영. 꺼져 있으면 다음 실행 시 반영
