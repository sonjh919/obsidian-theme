# Create Flow — 새 테마 부트스트랩

`SKILL.md` 에서 "새로" 모드 선택 후 진입하는 흐름. `$VAULT` 가 이미 식별되어 있다고 가정한다.

## Step 1: 자연어 묘사 수집

사용자에게 묻는다:

```
어떤 느낌의 테마를 원하세요? 한두 문장으로 자유롭게 말해주세요.

예시:
- "따뜻한 카페 같은 느낌"
- "레트로 터미널, CRT 모니터 분위기"
- "노션처럼 깔끔하게"
- "차가운 북유럽 다크"
```

사용자 답변을 받으면 키워드 추출 (분위기·색·용도).

## Step 2: 팔레트 3안 제시 (텍스트 + 미리보기 노트 — 둘 다 필수)

> ⚠️ **이 Step 은 반드시 두 작업을 *모두* 한다**:
> 1. 채팅에 텍스트 후보 출력 (2-A)
> 2. **옵시디언에 미리보기 노트 생성·자동 열기 (2-B) — hex 만 텍스트로 보면 색 판단 못 함. 이 단계 절대 생략 X**

`palettes.md` 를 Read 한다. 사용자 묘사 → 카탈로그 매핑:

1. **카탈로그 후보 2개**: 묘사 키워드와 가장 가까운 무드 2개 선택 (palettes.md 의 "무드 키워드 → 후보 매핑 가이드" 참조)
2. **즉석 생성 1개**: 카탈로그에 없는 새 팔레트 1개 (palettes.md 의 "즉석 생성 가이드" 따름)

### 2-A. 팔레트 선택 — `AskUserQuestion` 도구 사용 (필수)

사용자에게 채팅으로 짧은 안내 한 줄 출력:

```
세 가지 팔레트 후보예요. 옵시디언에 미리보기 노트 _theme-preview.md 도 띄웠으니 거기서 실제 색 보면서 선택하세요.
```

그 다음 `AskUserQuestion` 도구 호출:

```
question: "어느 팔레트가 가장 가까워요? (실제 색은 _theme-preview.md 에서 확인)"
header: "팔레트"
multiSelect: false
options:
  - label: "warm-cafe ☕"
    description: "따뜻한 카페·종이책. 배경 #f7f1e8 · 액센트 #c97b3b"
  - label: "sunset-warm 🌅"
    description: "석양·따뜻한 다크. 배경 #1f1410 · 액센트 #ff8847"
  - label: "(즉석) <묘사 기반 이름>"
    description: "당신 묘사로 즉석 생성. 배경 #faf3e7 · 액센트 #d4925c"
```

사용자가 "Other" 로 미세 조정 요청 시 (예: "1번 베이스에 액센트만 더 진한 갈색") → 그 hex 수정 후 최종 팔레트 확정.

### 2-B. 옵시디언 미리보기 노트 — **필수** (이 단계 생략 시 사용자가 색 판단 불가)

hex 6자리·폰트 이름은 텍스트만으로 판단 어려움. 팔레트 후보 3개와 폰트 후보 4개를 한 노트에 넣어 옵시디언에서 시각적으로 비교하게 한다 (Step 3 의 폰트 선택까지 같이 처리).

**2-B 는 2-A 와 함께 같은 응답에서 수행해야 한다. 사용자 답변을 기다리지 말고 채팅 출력 직후 바로 진행.**

#### 노트 작성

Write 도구로 `$VAULT/_theme-preview.md` 생성 (기존 파일 있으면 덮어쓰기). 팔레트 + 폰트 두 섹션:

**핵심 원칙**: 각 팔레트를 *그 팔레트의 배경·텍스트 색으로 감싼 큰 컨테이너* 안에 표시. 옵시디언 모드 (라이트/다크) 와 무관하게 팔레트 컨셉 분위기가 살아남. 컨테이너 안에는 *미니 미리보기* (헤딩 + 본문 + 링크 + 인라인 코드 + 코드블록) + 4색 스와치를 모두 박아 실제 노트가 어떻게 보일지 한눈에 감 잡히게.

```markdown
# 테마 미리보기

> 이 노트는 obsidian-theme 스킬이 자동 생성합니다. 다음 호출 시 덮어씁니다.

## 🎨 팔레트 후보

### [1] warm-cafe ☕ (따뜻한 카페, 종이책)

<div style="background:#f7f1e8; padding:24px; border-radius:12px; color:#3d2f24; font-family:Georgia,serif;">
<h2 style="color:#3d2f24; margin-top:0; border:0;">샘플 헤딩</h2>
<p style="color:#3d2f24;">본문 텍스트는 이렇게 보입니다. <a style="color:#c97b3b; font-weight:600;">위키링크</a>와 <code style="background:#eee5d5; padding:2px 6px; border-radius:4px; color:#3d2f24;">인라인 코드</code>도 함께.</p>
<div style="background:#eee5d5; padding:12px 16px; border-radius:6px; font-family:'JetBrains Mono',Menlo,monospace; font-size:12px; color:#3d2f24; margin:12px 0;">// 코드블록 샘플<br>const message = "hello cafe";</div>
<div style="display:flex; gap:6px; margin-top:16px; flex-wrap:wrap;">
<div style="background:#f7f1e8; padding:10px 14px; border-radius:6px; font-family:monospace; font-size:11px; color:#3d2f24; border:1px solid #d9ccae;">배경 #f7f1e8</div>
<div style="background:#eee5d5; padding:10px 14px; border-radius:6px; font-family:monospace; font-size:11px; color:#3d2f24;">표면 #eee5d5</div>
<div style="background:#3d2f24; color:#f7f1e8; padding:10px 14px; border-radius:6px; font-family:monospace; font-size:11px;">텍스트 #3d2f24</div>
<div style="background:#c97b3b; color:#ffffff; padding:10px 14px; border-radius:6px; font-family:monospace; font-size:11px;">액센트 #c97b3b</div>
</div>
</div>

### [2] sunset-warm 🌅 (석양, 따뜻한 다크)

<div style="background:#1f1410; padding:24px; border-radius:12px; color:#f4d4b1; font-family:Georgia,serif;">
<h2 style="color:#f4d4b1; margin-top:0; border:0;">샘플 헤딩</h2>
<p style="color:#f4d4b1;">본문 텍스트는 이렇게 보입니다. <a style="color:#ff8847; font-weight:600;">위키링크</a>와 <code style="background:#2d1f17; padding:2px 6px; border-radius:4px; color:#f4d4b1;">인라인 코드</code>도 함께.</p>
<div style="background:#2d1f17; padding:12px 16px; border-radius:6px; font-family:'JetBrains Mono',Menlo,monospace; font-size:12px; color:#f4d4b1; margin:12px 0;">// 코드블록 샘플<br>const message = "hello sunset";</div>
<div style="display:flex; gap:6px; margin-top:16px; flex-wrap:wrap;">
<div style="background:#1f1410; color:#f4d4b1; padding:10px 14px; border-radius:6px; font-family:monospace; font-size:11px; border:1px solid #4a3024;">배경 #1f1410</div>
<div style="background:#2d1f17; color:#f4d4b1; padding:10px 14px; border-radius:6px; font-family:monospace; font-size:11px;">표면 #2d1f17</div>
<div style="background:#f4d4b1; color:#1f1410; padding:10px 14px; border-radius:6px; font-family:monospace; font-size:11px;">텍스트 #f4d4b1</div>
<div style="background:#ff8847; color:#1f1410; padding:10px 14px; border-radius:6px; font-family:monospace; font-size:11px;">액센트 #ff8847</div>
</div>
</div>

### [3] (즉석) — "<사용자 묘사>"

<div style="background:<배경>; padding:24px; border-radius:12px; color:<텍스트>; font-family:Georgia,serif;">
... (위와 동일 구조, 즉석 팔레트 4색으로 채움)
</div>

---

## 🔤 폰트 후보

샘플: `The quick brown fox jumps over the lazy dog. 따뜻한 카페에서 책을 읽는다. 0123456789`

폰트는 자형 비교가 핵심이라 *고정 라이트 박스* 안에서 보여줌 (옵시디언 다크 모드여도 안정적으로 자형 식별 가능).

### [1] 시스템 기본

<div style="background:#fafafa; padding:18px; border-radius:8px; color:#222;">
<p style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif; font-size: 17px; line-height: 1.6; margin:0; color:#222;">
The quick brown fox jumps over the lazy dog.<br>
따뜻한 카페에서 책을 읽는다. 0123456789
</p>
</div>

### [2] Sans (Inter)

<div style="background:#fafafa; padding:18px; border-radius:8px; color:#222;">
<p style="font-family: 'Inter', -apple-system, sans-serif; font-size: 17px; line-height: 1.6; margin:0; color:#222;">
The quick brown fox jumps over the lazy dog.<br>
따뜻한 카페에서 책을 읽는다. 0123456789
</p>
</div>

### [3] Serif (Crimson Pro · 글쓰기용)

<div style="background:#fafafa; padding:18px; border-radius:8px; color:#222;">
<p style="font-family: 'Crimson Pro', Georgia, serif; font-size: 18px; line-height: 1.6; margin:0; color:#222;">
The quick brown fox jumps over the lazy dog.<br>
따뜻한 카페에서 책을 읽는다. 0123456789
</p>
</div>

### [4] Mono 강조 (JetBrains Mono · 본문도 모노)

<div style="background:#fafafa; padding:18px; border-radius:8px; color:#222;">
<p style="font-family: 'JetBrains Mono', Menlo, Consolas, monospace; font-size: 15px; line-height: 1.6; margin:0; color:#222;">
The quick brown fox jumps over the lazy dog.<br>
따뜻한 카페에서 책을 읽는다. 0123456789
</p>
</div>

> 시스템에 해당 폰트가 없으면 fallback 으로 렌더됩니다 (Inter → 시스템 산세리프, Crimson Pro → Georgia, JetBrains Mono → Menlo/Consolas). 그래도 대략 분위기는 비슷.
```

**규칙**:
- 노트 첫 줄에 "스킬 자동 생성, 다음 호출 시 덮어씁니다" 메모 (사용자 혼란 방지)
- **팔레트 각 후보는 그 팔레트 배경·텍스트 색으로 감싼 큰 컨테이너 (`<div style="background:<bg>; color:<text>;">`)** 안에 미니 미리보기 (헤딩·본문·링크·인라인 코드·코드블록) + 4색 스와치를 모두 박는다. 컨테이너 안의 모든 요소에 inline `color:` 명시 (옵시디언 테마 색에 의해 override 안 되도록)
- 액센트는 미니 미리보기의 링크 색 + 4 스와치 중 하나로 보여줌
- 폰트 샘플은 *고정 라이트 박스* (`#fafafa` 배경 + `#222` 텍스트) 안에서 자형만 비교
- 모든 샘플 텍스트는 영문·한글·숫자 포함

#### 옵시디언에서 자동 열기 (시도) + fallback 안내 (필수)

`obsidian-cli` 가 설치되어 있고 활성 vault 가 `$VAULT` 면 자동 열기:

```bash
command -v obsidian >/dev/null 2>&1 && \
  obsidian open path="_theme-preview.md" 2>/dev/null | grep -v "Loading\|installer\|out of date"
```

#### 사용자 안내 (필수)

미리보기 노트 작성·열기 결과를 사용자에게 *반드시* 알린다. 둘 중 하나는 무조건:

자동 열기 성공:
```
🎨 옵시디언에 "_theme-preview.md" 노트를 만들었어요. 새 탭에서 색 비교 후 선택해주세요.
```

자동 열기 실패 (obsidian-cli 없음 또는 활성 vault 다름):
```
🎨 vault 루트에 "_theme-preview.md" 를 만들었어요. 옵시디언에서 직접 열어주세요.
   (Cmd+O → "_theme-preview" 검색)
```

**노트만 만들고 사용자에게 안내 안 하는 것은 실패**. obsidian-cli 자동 열기 안 되어도 노트 작성은 반드시 한다 (Write 도구).

사용자가 선택을 마치면 노트는 그대로 둔다 (사용자가 다시 볼 수 있도록). 다음 호출 시 덮어씀. 영구 삭제 원하면 사용자가 직접 `rm $VAULT/_theme-preview.md`.

## Step 3: 구체화 4 질문 — `AskUserQuestion` (multi-question 한 번에) 도구 사용 (필수)

팔레트 확정 후 4개 질문을 *AskUserQuestion 한 번 호출에 다 담아서* 한 화면에 띄운다. 채팅 텍스트로 "Q1, Q2..." 묻지 말 것.

채팅에 짧은 안내 한 줄:
```
네 가지만 더 정해주세요. 폰트는 _theme-preview.md 의 🔤 섹션에서 실제로 보면서 고르세요.
```

그 다음 `AskUserQuestion` (questions 배열에 4개 묶어서) 호출:

```
[Q1]
question: "라이트 / 다크?"
header: "모드"
multiSelect: false
options: 라이트 / 다크 / 둘 다

[Q2]
question: "본문 폰트?"
header: "폰트"
multiSelect: false
options:
  - 시스템 기본
  - Sans (Inter)
  - Serif (Crimson Pro · 글쓰기용)
  - Mono 강조 (JetBrains Mono · 본문도 모노)

[Q3]
question: "모서리 둥글기?"
header: "모서리"
multiSelect: false
options: 0px (날카로움) / 8px (부드러움) / 12px (둥글) / 16px (매우 둥글)

[Q4]
question: "간격?"
header: "간격"
multiSelect: false
options: 빽빽 / 보통 / 여유
```

답을 안 한 항목은 기본값 (둘 다 / 시스템 / 8px / 보통) 으로 가정하고 명시.

## Step 4: 테마 이름 결정

사용자 묘사에서 이름 자동 추출:
- "따뜻한 카페" → `warm-cafe`
- "레트로 터미널" → `retro-terminal`
- 카탈로그 무드를 선택했으면 그 이름 사용

`$VAULT/.obsidian/themes/` 에 이미 같은 이름이 있으면 `-2`, `-3` suffix:

```bash
ls "$VAULT/.obsidian/themes/" 2>/dev/null
```

사용자에게 확인:

```
테마 이름을 "warm-cafe" 로 만들게요. 다른 이름 원하면 알려주세요.
```

이름 확정 후 `$THEME_NAME` 으로 기억.

## Step 5: CSS 생성

`variables.md` 를 Read 하여 변수 매핑을 확인한 뒤, 결정사항을 CSS 변수로 변환.

### 5-1. 폴더 생성

```bash
mkdir -p "$VAULT/.obsidian/themes/$THEME_NAME"
```

### 5-2. theme.css 작성

Write 도구로 `$VAULT/.obsidian/themes/$THEME_NAME/theme.css` 생성.

**필수 첫 줄 marker** (수정 모드에서 식별용):

```css
/* obsidian-theme: managed */
```

**구조 템플릿** (라이트+다크 둘 다 선택한 경우):

```css
/* obsidian-theme: managed */
/* Theme: warm-cafe */
/* Generated by obsidian-theme skill */

.theme-light {
  --background-primary: #f7f1e8;
  --background-primary-alt: #f2ecdf;
  --background-secondary: #eee5d5;
  --background-secondary-alt: #e5dac4;
  --background-modifier-border: #d9ccae;
  --background-modifier-hover: #ebe1cb;

  --text-normal: #3d2f24;
  --text-muted: #7a6651;
  --text-faint: #a8957c;

  --accent-h: 25;
  --accent-s: 60%;
  --accent-l: 50%;

  --link-color: #c97b3b;
  --code-background: #ebe1cb;
  --code-normal: #3d2f24;
  --tag-color: #c97b3b;
  --tag-background: #f0e5cf;
}

.theme-dark {
  /* 다크 변형 — 사용자가 둘 다 선택한 경우 */
  --background-primary: #1f1814;
  /* ... */
}

/* 공통: 폰트, 간격, 모서리 */
body {
  --font-text-theme: 'Inter', -apple-system, sans-serif;
  --font-interface-theme: -apple-system, BlinkMacSystemFont, sans-serif;
  --font-monospace-theme: 'JetBrains Mono', Menlo, monospace;
  --radius-s: 4px;
  --radius-m: 8px;
  --radius-l: 12px;
  --line-height-normal: 1.5;
}
```

**규칙**:
- 사용자가 라이트만 선택했으면 `.theme-light` 블록만, 다크만 선택했으면 `.theme-dark` 블록만
- 폰트 선택에 따라 `--font-text-theme` / `--font-interface-theme` / `--font-monospace-theme` 결정 (⚠️ `-theme` suffix 필수 — 옵시디언 공식 변수명)
  - 시스템: `-apple-system, BlinkMacSystemFont, sans-serif`
  - Sans: `'Inter', -apple-system, sans-serif`
  - Serif: `'Crimson Pro', Georgia, serif`
  - Mono 강조: 본문도 모노 → `'JetBrains Mono', Menlo, monospace`
- 모서리: 사용자 선택값을 `--radius-m` 에 적용 (--radius-s 는 -4, --radius-l 은 +4, --radius-xl 은 +8). 기본 옵시디언 값은 4/8/12/16
- 간격: 빽빽 = `--line-height-normal: 1.4`, 보통 = `1.5`, 여유 = `1.7`

### 5-3. manifest.json 작성

Write 도구로 `$VAULT/.obsidian/themes/$THEME_NAME/manifest.json`:

```json
{
  "name": "warm-cafe",
  "version": "1.0.0",
  "minAppVersion": "1.0.0",
  "author": "obsidian-theme skill",
  "authorUrl": ""
}
```

## Step 6: 활성화 — `AskUserQuestion` 사용 (필수)

```
question: "방금 만든 \"warm-cafe\" 테마를 지금 적용할까요?"
header: "활성화"
multiSelect: false
options:
  - label: "네, 지금 적용"
    description: "appearance.json 패치 → 옵시디언이 켜져 있으면 즉시 hot reload"
  - label: "아니요, 나중에 직접"
    description: "옵시디언 Settings → Appearance → Themes 에서 직접 선택"
```

승인하면 `$VAULT/.obsidian/appearance.json` 의 `cssTheme` 필드를 패치한다.

```bash
cat "$VAULT/.obsidian/appearance.json"
```

JSON 파싱 후 `cssTheme` 키를 `"$THEME_NAME"` 으로 변경하고 Write 로 덮어쓰기. 다른 필드는 보존.

## Step 7: 결과 보고

```
✅ 테마 "warm-cafe" 생성 완료

📂 생성 파일:
  - /path/to/vault/.obsidian/themes/warm-cafe/theme.css
  - /path/to/vault/.obsidian/themes/warm-cafe/manifest.json

🎨 활성화: appearance.json 패치 완료 (옵시디언에서 즉시 적용됨)
   적용 안 됐다면: Settings → Appearance → Themes 에서 "warm-cafe" 선택
```

vault 에 이전 테마가 있었다면 추가 안내:

```
구 테마는 그대로 themes/ 폴더에 남아있어요. 토글로 언제든 돌아갈 수 있습니다.
완전히 삭제하려면: rm -rf <vault>/.obsidian/themes/<old-name>
```

## Step 8: 디테일링 권유

기본 4질문 (라이트/다크, 폰트, 모서리, 간격) 으로 만든 테마는 옵시디언 자동 파생으로 80% 정도 어울리게 적용됨. 하지만 더 세밀한 영역 (h1~h6 색·굵기, 콜아웃 타입별 색, 코드 syntax, 리스트 marker, 표 헤더, 사이드바 nav 등) 은 직접 지정해야 함.

채팅으로 디테일링 옵션 예시 짧게 안내:

```
지금 테마는 기본만 정해진 상태예요. 더 세밀하게 만질 수 있는 영역:
- 헤딩 (h1~h6) · 강조 (bold · italic · ==highlight==) · 링크 디테일
- 코드 syntax 11종 · 콜아웃 14타입별 색 · 표 · 리스트 marker
- 사이드바 · 탭 · 리본 · 타이틀바 · 상태바 · 캔버스 · 그래프
```

그 다음 `AskUserQuestion` 호출 (필수):

```
question: "더 세밀하게 만져볼까요?"
header: "디테일링"
multiSelect: false
options:
  - label: "네, 수정 모드로"
    description: "edit-flow.md 자동 진입 — 자연어 또는 카테고리 메뉴로 디테일링"
  - label: "아니요, 지금 충분"
    description: "끝. 나중에 /obsidian-theme → 수정 으로 언제든 호출"
```

**사용자가 "1" 또는 "네" 선택 시**:

`~/.claude/skills/obsidian-theme/edit-flow.md` 를 Read 한 뒤 그 흐름으로 진입한다. 단, 첫 진입 시 사용자 안내를 디테일링 맥락에 맞게 조정:

```
좋아요! 어떤 부분부터 만져볼까요?
자연어로 말해주세요. 예: "h1 색을 액센트로", "콜아웃 info 배경을 파랑으로", "코드 키워드를 보라색으로"

또는 카테고리를 말하면 그 영역의 변수 목록을 보여드릴게요. 예: "헤딩 보여줘", "콜아웃 변수 알려줘"
```

이후는 `edit-flow.md` Step 2 (수정 위치 자연어 수집) 부터 동일. `variables.md` 의 카테고리 인덱스 + 자연어 매핑표를 적극 활용한다 (특히 사용자가 "헤딩 보여줘" 처럼 카테고리 단위 요청 시 해당 섹션의 변수 표를 보여줌).

**"0" 또는 "아니오" 선택 시**:

```
다음에 더 조정하려면: /obsidian-theme → 수정
끝!
```
