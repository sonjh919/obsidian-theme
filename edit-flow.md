# Edit Flow — 기존 테마 튜닝

`SKILL.md` 에서 "수정" 모드 선택 후 진입하는 흐름. `$VAULT` 가 이미 식별되어 있다고 가정한다.

## Step 1: 현재 테마 식별

`$VAULT/.obsidian/appearance.json` 을 읽어 `cssTheme` 필드 확인.

```bash
cat "$VAULT/.obsidian/appearance.json"
```

`cssTheme` 값에 따라 분기:

### (a) 빈 문자열 `""`
옵시디언 디폴트 테마 사용 중. 디폴트 자체는 수정 불가하므로 안내:

```
현재 옵시디언 기본 테마를 쓰고 있어요. 기본 테마는 직접 수정할 수 없어요.

옵션:
1. 새 테마 만들기 (/obsidian-theme → 새로)
2. snippet 으로 부분 커스터마이즈만 (이 흐름 계속)
```

사용자가 2를 선택하면 → **(c) snippet override 모드** 로 진입.

### (b) 이 스킬이 만든 테마
`$VAULT/.obsidian/themes/<cssTheme>/theme.css` 의 첫 줄에 `/* obsidian-theme: managed */` marker 가 있는지 확인:

```bash
head -1 "$VAULT/.obsidian/themes/<cssTheme>/theme.css"
```

marker 있으면 → **직접 수정 모드**. `$TARGET_FILE = $VAULT/.obsidian/themes/<cssTheme>/theme.css`

### (c) 외부 테마 (marker 없음)
AnuPpuccin, Minimal, Things 등. 원본을 건드리지 않고 snippet override 로 처리.

```
현재 "<cssTheme>" 테마를 쓰고 있어요. 원본 테마는 건드리지 않고,
별도 snippet 으로 위에 덮어쓰는 방식으로 수정할게요.

snippet 위치: <vault>/.obsidian/snippets/obsidian-theme-override.css
```

`$TARGET_FILE = $VAULT/.obsidian/snippets/obsidian-theme-override.css`. 파일이 없으면 첫 호출 시 새로 만든다 (첫 줄에 `/* obsidian-theme: override */` marker).

snippet 활성화 안내:

```
처음이면 옵시디언에서 한 번만:
Settings → Appearance → CSS snippets → "obsidian-theme-override" 토글 ON
이후 변경은 자동 반영.
```

## Step 2: 수정 위치 입력 — 진입 경로별 default

| 진입 경로 | 기본 모드 |
|---|---|
| `/obsidian-theme → 수정` 직접 호출 | **2-A 자연어** default (사용자가 만질 변수를 이미 알고 있을 가능성 ↑) |
| `create-flow.md` Step 8 디테일링 → 진입 | **2-B 카테고리 메뉴** default (사용자가 뭘 만질지 모르는 상황) |
| 사용자가 "뭘 만질 수 있어?", "카테고리 보여줘", "메뉴" 같은 표현 사용 | **2-B 카테고리 메뉴** |

사용자는 언제든 2-A ↔ 2-B 전환 가능 ("카테고리로 보여줘" / "그냥 자연어로 할게").

### 2-A. 자연어 모드

```
어디를 어떻게 바꿀까요?

예시:
- "코드블록 배경을 좀 더 어둡게"
- "링크 색을 주황으로"
- "사이드바 폰트를 좀 작게"
- "본문 줄간격 더 여유롭게"
```

여러 변경을 한 번에 받을 수 있음. 한 번에 처리한다.

### 2-B. 카테고리 메뉴 모드 — 2단 `AskUserQuestion` (디테일링 진입 시 default)

사용자가 어떤 변수를 만질지 모를 때, 또는 `create-flow.md` Step 8 에서 디테일링 진입한 직후. 25개 평탄 메뉴는 인지부담 ↑ — **4 큰 카테고리로 묶어서 2단으로 좁혀간다**.

#### 2-B-1. 큰 카테고리 선택 — `AskUserQuestion` (필수)

```
question: "어떤 영역을 만져볼까요?"
header: "디테일 영역"
multiSelect: false
options:
  - label: "🎨 글자·색"
    description: "본문·부제·헤딩 h1~h6·링크·태그·강조·하이라이트·액센트"
  - label: "📝 블록 요소"
    description: "콜아웃 14타입·코드 syntax 11종·표·리스트·인용·임베드"
  - label: "🖼 UI 크롬"
    description: "탭·리본·타이틀바·상태바·사이드바 nav·모달·팝오버"
  - label: "🔧 레이아웃·기타"
    description: "폰트·줄간격·모서리·간격·캔버스·그래프·properties"
```

#### 2-B-2. 카테고리 안 sub 항목 — `AskUserQuestion` (옵션 ≤ 4) 또는 텍스트 메뉴 (≥ 5)

사용자 선택에 따라 다음 sub-메뉴를 보여준다. 각 sub-카테고리의 변수 표는 `variables.md` 의 해당 섹션 Read 후 첨부.

**🎨 글자·색 선택 시** (옵션 4개 — `AskUserQuestion`):
```
options:
  - "본문 텍스트"       (--text-normal · --text-muted · --text-faint · --bold-color · --italic-color)
  - "헤딩 h1~h6"        (--h1-color~--h6-color · 크기·굵기·폰트)
  - "링크·태그"          (--link-color · --link-external-color · --tag-color · --tag-background)
  - "액센트·하이라이트"   (--accent-h/s/l · --text-highlight-bg)
```

**📝 블록 요소 선택 시** (옵션 4개 — `AskUserQuestion`):
```
options:
  - "콜아웃"   (--callout-* 일반 + 14 타입별 색)
  - "코드"     (--code-background + 11 syntax 색)
  - "표"       (--table-header-background · --table-row-alt-background 등)
  - "리스트·인용·기타"  (--list-marker-color · --blockquote-* · --hr-color · --embed-*)
```

**🖼 UI 크롬 선택 시** (옵션 4개 — `AskUserQuestion`):
```
options:
  - "탭·리본"      (--tab-* · --ribbon-*)
  - "타이틀바·상태바"   (--titlebar-* · --status-bar-*)
  - "사이드바 nav"       (--nav-item-* · --nav-heading-*)
  - "모달·팝오버"     (--modal-* · --popover-* · --dialog-* · --prompt-*)
```

**🔧 레이아웃·기타 선택 시** (옵션 4개 — `AskUserQuestion`):
```
options:
  - "폰트·타이포"    (--font-text-theme · --font-text-size · --line-height-* · --bold-modifier)
  - "모서리·간격"    (--radius-* · --size-*)
  - "캔버스·그래프"   (--canvas-* · --graph-*)
  - "Properties·기타"  (--metadata-* · --file-line-width · --divider-*)
```

#### 2-B-3. sub 카테고리 안 변수 표 출력 + 자연어 입력

sub 카테고리 선택 후 `variables.md` 의 해당 섹션을 Read 하여 변수 표 (변수명 + 현재 값 + 설명) 를 출력. 그 다음 채팅으로:

```
이 영역에서 뭘 바꿀까요? 자연어로 알려주세요.
예: "h1 만 액센트 색으로", "코드 키워드를 보라색으로", "탭 모서리 좀 더 둥글게"
```

사용자 답변을 받으면 Step 3 (변수 식별) → Step 4 (diff 승인) → Step 5 (적용) 진행.

#### 자유 입력으로 바로 진입

사용자가 디테일링 시작부터 변수가 명확하면 (예: "h1 색을 액센트로 바꿔줘") 2-B-1 의 큰 카테고리 메뉴 건너뛰고 Step 3 로 바로. 즉 2-B 메뉴는 *모르는 사용자용 가이드*, 아는 사용자는 자유 입력.

## Step 3: 변수 식별 (variables.md 참조)

`~/.claude/skills/obsidian-theme/variables.md` 를 Read 한다. "자연어 → 변수 매핑표" 섹션에서 사용자 표현을 변수로 매핑.

매핑 결과를 사용자에게 확인:

```
바꿀 부분을 정리하면:

1. "코드블록 배경 어둡게"
   → --code-background : #ebe1cb → #c9bc9e

2. "링크 색을 주황으로"
   → --link-color : #c97b3b → #ff7f3f
```

매핑이 모호하면 후보 제시:

```
"태그 색"이라고 하셨는데, 두 가지 중 어느 거예요?

[1] 태그 글자 색 (--tag-color)
[2] 태그 배경 (--tag-background)
[3] 둘 다
```

색 값 결정은:
- 사용자가 hex 를 직접 줬으면 그대로
- 자연어 ("어둡게", "주황으로") 면 현재 값에서 추론 (어둡게 = 명도 -15%, 밝게 = +15%, 주황 = hue 25 부근 등)

## Step 4: diff 미리보기 → `AskUserQuestion` 으로 승인 (필수)

채팅에 변경 전/후 표 출력:

```
변경 사항 미리보기:

변수                   |  현재         |  변경 후
--code-background      |  #ebe1cb     |  #c9bc9e
--link-color           |  #c97b3b     |  #ff7f3f
```

그 다음 `AskUserQuestion` 호출 (필수, "Y/n" 텍스트 X):

```
question: "이렇게 적용할까요?"
header: "diff 승인"
multiSelect: false
options:
  - label: "네, 적용"
    description: "위 변경사항 모두 반영 → 옵시디언 hot reload"
  - label: "아니요, 다시"
    description: "Step 2 로 돌아가 다시 수정 요청"
```

거절하면 Step 2 로 돌아가 다시 수집.

## Step 5: 적용 + 보고

### 5-1. 직접 수정 모드 (b)
`$TARGET_FILE` (`themes/<name>/theme.css`) 을 Read 한 뒤 Edit 도구로 변수 라인만 교체. 라이트/다크 분기가 있으면 사용자가 현재 보고 있는 모드 (옵시디언 `cssTheme` 외 `cssTheme` 파일은 분기 정보 X — `cssTheme` 모드는 별도) 를 추정하기 어려우면 양쪽 다 변경하거나 사용자에게 묻기.

### 5-2. snippet override 모드 (c)
`$TARGET_FILE` (`snippets/obsidian-theme-override.css`) 에 변수를 append/replace. 같은 변수가 이미 있으면 Edit 으로 값만 교체, 없으면 추가:

```css
/* obsidian-theme: override */

body {
  --code-background: #c9bc9e;
  --link-color: #ff7f3f;
}
```

### 5-3. 결과 보고

```
✅ 수정 완료

📝 변경된 파일: /path/to/file.css

변경된 변수:
- --code-background : #ebe1cb → #c9bc9e
- --link-color      : #c97b3b → #ff7f3f

옵시디언에서 즉시 확인하세요. (CSS 는 저장 즉시 hot reload)

다음에 더 조정하려면: /obsidian-theme → 수정
```

옵시디언이 꺼져 있으면 다음 실행 시 반영된다는 안내 추가.
