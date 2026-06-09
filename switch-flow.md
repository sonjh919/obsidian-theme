# Switch Flow — 테마 전환

`SKILL.md` 에서 "스위치" 모드 선택 후 진입하는 흐름. `$VAULT` 가 이미 식별되어 있다고 가정한다.

## Step 1: 테마 목록 표시

`$VAULT/.obsidian/themes/` 스캔 + 현재 활성 테마 확인:

```bash
ls "$VAULT/.obsidian/themes/" 2>/dev/null
cat "$VAULT/.obsidian/appearance.json" 2>/dev/null
```

각 테마 폴더에 대해 `theme.css` 첫 줄 marker 확인 (이 스킬이 만든 테마인지 판별):

```bash
for d in "$VAULT/.obsidian/themes/"*/; do
  name=$(basename "$d")
  first=$(head -1 "$d/theme.css" 2>/dev/null)
  echo "$name | $first"
done
```

사용자에게 번호 매겨서 표시:

```
이 vault 에 있는 테마들:

[1] warm-cafe       (현재)  (이 스킬 만든)
[2] nordic-cold              (이 스킬 만든)
[3] AnuPpuccin               (외부)
[4] Minimal                  (외부)
[0] (옵시디언 기본 테마)

어느 걸로 갈아끼울까요?
```

- 현재 활성 테마는 `(현재)` 표시
- `theme.css` 첫 줄에 `/* obsidian-theme: managed */` marker 있으면 `(이 스킬 만든)`, 없으면 `(외부)`
- 번호 `[0]` 으로 옵시디언 기본 테마 (`cssTheme: ""`) 도 선택지에 포함

## Step 2: 사용자 선택 — `AskUserQuestion` (테마 ≤ 4개일 때) / 채팅 텍스트 (≥ 5개)

**테마 + "옵시디언 기본" 합쳐 4개 이하**: `AskUserQuestion` 도구 사용 (필수). 각 option label 에 테마 이름, description 에 `(현재)·(이 스킬 만든)·(외부)` 표시.

```
question: "어느 테마로 갈아끼울까요?"
header: "테마 전환"
multiSelect: false
options:
  - label: "warm-cafe"
    description: "(현재) (이 스킬 만든)"
  - label: "nordic-cold"
    description: "(이 스킬 만든)"
  - label: "AnuPpuccin"
    description: "(외부)"
  - label: "옵시디언 기본 테마"
    description: "디폴트 (cssTheme: \"\")"
```

**테마 5개 이상**: `AskUserQuestion` 4 옵션 한도 초과. 채팅 텍스트 번호 메뉴로 fallback (Step 1 의 텍스트 출력 그대로). 사용자가 번호 또는 이름으로 답.

처리:
- 현재 활성 테마 다시 선택 시 → "이미 적용 중" 안내 후 Step 1 로 돌아가 다시 받기
- "옵시디언 기본" 선택 시 → `$TARGET = ""` (빈 문자열)
- 그 외 → `$TARGET = "<선택한 테마 이름>"`

## Step 3: 적용 + 보고

`$VAULT/.obsidian/appearance.json` 을 Read → JSON 파싱 → `cssTheme` 키만 `$TARGET` 으로 교체 → Write 로 덮어쓰기. 다른 필드 (accentColor, baseFontSize, interfaceFontFamily 등) 는 그대로 보존.

### 적용 예시 (appearance.json 일부)

변경 전:
```json
{
  "cssTheme": "warm-cafe",
  "accentColor": "#c97b3b",
  "baseFontSize": 16
}
```

변경 후:
```json
{
  "cssTheme": "nordic-cold",
  "accentColor": "#c97b3b",
  "baseFontSize": 16
}
```

### 결과 보고

```
✅ 테마 전환 완료

🎨 warm-cafe → nordic-cold

옵시디언이 켜져 있으면 즉시 적용됩니다.
꺼져 있다면 다음 실행 시 반영됩니다.

다른 테마로 또 갈아끼우려면: /obsidian-theme → 스위치
```

옵시디언 기본 테마로 돌아갔으면 메시지 미세 수정:

```
🎨 warm-cafe → 옵시디언 기본 테마
```
