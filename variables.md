# Obsidian CSS Variables — 풀세트 Cheatsheet

옵시디언 공식 [CSS variables 문서](https://docs.obsidian.md/Reference/CSS+variables) 전체 (5 카테고리 × 약 450 변수) 를 카테고리별로 정리. 변수에 사용 빈도 표시 (★★★ 거의 모든 테마 / ★★ 자주 / ★ 가끔·니치).

## 카테고리 인덱스

| 영역 | 카테고리 | 변수 수 |
|---|---|---|
| **Foundations** | [Colors](#colors-) · [Typography](#typography-) · [Spacing](#spacing-) · [Radiuses](#radiuses-) · [Borders](#borders-) · [Icons](#icons-) · [Cursor](#cursor) · [Layers](#layers) | ~110 |
| **Editor** | [Headings](#headings-) · [Inline title](#inline-title-) · [Blockquote](#blockquote-) · [Callout](#callout-) · [Code](#code-) · [Link](#link-) · [Tag](#tag-) · [Table](#table-) · [List](#list-) · [Embed](#embed) · [Footnote](#footnote) · [Horizontal rule](#horizontal-rule-) · [Block](#block) · [File](#file) · [Properties](#properties) · [Bases](#bases) | ~230 |
| **Components** | [Tabs](#tabs-) · [Button](#button-) · [Modal](#modal-) · [Dialog](#dialog) · [Popover](#popover-) · [Prompt](#prompt) · [Dropdowns](#dropdowns) · [Text input](#text-input) · [Color input](#color-input) · [Checkbox](#checkbox-) · [Toggle](#toggle) · [Slider](#slider) · [Multi-select](#multi-select) · [Navigation](#navigation-) · [Indentation guides](#indentation-guides) · [Dragging](#dragging) | ~150 |
| **Window** | [Window frame](#window-frame-) · [Ribbon](#ribbon-) · [Sidebar](#sidebar) · [Status bar](#status-bar-) · [Divider](#divider) · [Scrollbar](#scrollbar) · [Vault profile](#vault-profile) · [Workspace](#workspace) | ~40 |
| **Plugins** | [Canvas](#canvas-) · [File explorer](#file-explorer) · [Graph](#graph-) · [Search](#search) · [Sync](#sync) | ~40 |

> 빈도 표시: 카테고리 헤더 옆에 묶음 빈도 표시. 개별 변수 빈도는 본문 표에 일부 ★ 표시. ★ 안 붙은 변수는 *니치* 또는 *디테일* 로 가정.

---

## Foundations

### Colors ★★★

옵시디언 색 시스템의 기반. 다른 영역의 변수 (e.g. `--background-primary`) 는 보통 이 토큰에서 파생.

#### Base colors — 11단 무채색 (라이트/다크 별도) ★★★

| 변수 | 라이트 | 다크 |
|---|---|---|
| `--color-base-00` | `#ffffff` | `#1e1e1e` |
| `--color-base-05` | `#fcfcfc` | `#212121` |
| `--color-base-10` | `#fafafa` | `#242424` |
| `--color-base-20` | `#f6f6f6` | `#262626` |
| `--color-base-25` | `#e3e3e3` | `#2a2a2a` |
| `--color-base-30` | `#e0e0e0` | `#363636` |
| `--color-base-35` | `#d4d4d4` | `#3f3f3f` |
| `--color-base-40` | `#bdbdbd` | `#555555` |
| `--color-base-50` | `#ababab` | `#666666` |
| `--color-base-60` | `#707070` | `#999999` |
| `--color-base-70` | `#5a5a5a` | `#bababa` |
| `--color-base-100` | `#222222` | `#dadada` |

#### Accent — HSL 분해 ★★★

| 변수 | 기본값 |
|---|---|
| `--accent-h` | `254` (hue) |
| `--accent-s` | `80%` |
| `--accent-l` | `68%` |

→ `--interactive-accent` 등은 이 HSL 에서 자동 파생. hex 가 아닌 H/S/L 분리.

#### Extended colors — 8색 × 라이트/다크 + RGB 변형 ★★

| 변수 | 라이트 | 다크 |
|---|---|---|
| `--color-red` | `#e93147` | `#fb464c` |
| `--color-orange` | `#ec7500` | `#e9973f` |
| `--color-yellow` | `#e0ac00` | `#e0de71` |
| `--color-green` | `#08b94e` | `#44cf6e` |
| `--color-cyan` | `#00bfbc` | `#53dfdd` |
| `--color-blue` | `#086ddd` | `#027aff` |
| `--color-purple` | `#7852ee` | `#a882ff` |
| `--color-pink` | `#d53984` | `#fa99cd` |

각 색의 RGB 변형 (`--color-red-rgb` 등) 도 있음. `rgba(var(--color-red-rgb), 0.2)` 같은 투명도 합성에 사용.

#### Surface colors — 의미론적 표면 ★★★

| 변수 | 영향 |
|---|---|
| `--background-primary` | 메인 노트 배경 ★★★ |
| `--background-primary-alt` | primary 위 표면 |
| `--background-secondary` | 사이드바·탭 배경 ★★★ |
| `--background-secondary-alt` | secondary 위 표면 |
| `--background-modifier-hover` | hover 배경 ★★ |
| `--background-modifier-active-hover` | active hover 배경 |
| `--background-modifier-border` | 경계선 ★★ |
| `--background-modifier-border-hover` | 경계선 (hover) |
| `--background-modifier-border-focus` | 경계선 (focus) |
| `--background-modifier-error` | 에러 배경 |
| `--background-modifier-error-rgb` | 에러 배경 RGB |
| `--background-modifier-error-hover` | 에러 배경 (hover) |
| `--background-modifier-success` | 성공 배경 |
| `--background-modifier-success-rgb` | 성공 배경 RGB |
| `--background-modifier-message` | 메시지 배경 |
| `--background-modifier-form-field` | 입력 필드 배경 |

#### Interactive colors ★★

| 변수 | 영향 |
|---|---|
| `--interactive-normal` | 일반 인터랙티브 배경 |
| `--interactive-hover` | 일반 인터랙티브 hover |
| `--interactive-accent` | 액센트 인터랙티브 배경 (액센트 HSL 에서 파생) ★★★ |
| `--interactive-accent-hsl` | 액센트 HSL |
| `--interactive-accent-hover` | 액센트 hover |

#### Text foreground ★★★

| 변수 | 영향 |
|---|---|
| `--text-normal` | 본문 텍스트 ★★★ |
| `--text-muted` | 부제·헬프 ★★★ |
| `--text-faint` | placeholder·메타 |
| `--text-on-accent` | 액센트 위 (다크 액센트 시) |
| `--text-on-accent-inverted` | 액센트 위 (라이트 액센트 시) |
| `--text-success` | 성공 텍스트 |
| `--text-warning` | 경고 텍스트 |
| `--text-error` | 에러 텍스트 |
| `--text-accent` | 액센트 텍스트 ★★ |
| `--text-accent-hover` | 액센트 텍스트 (hover) |

#### Text background ★

| 변수 | 영향 |
|---|---|
| `--text-selection` | 선택 영역 배경 |
| `--text-highlight-bg` | ==하이라이트== 배경 ★★ |

#### Caret ★

| 변수 | 영향 |
|---|---|
| `--caret-color` | 입력 캐럿 색 |

#### Black/White (수정 비권장) ★

| 변수 | 영향 |
|---|---|
| `--mono-rgb-0` | 흰색/검은색 RGB (라이트/다크 반전) |
| `--mono-rgb-100` | 반대 |

> ⚠️ 옵시디언 공식 안내: black/white 변수는 수정 안 하는 것 권장.

### Typography ★★★

#### Fonts — `-theme` suffix 필수! ★★★

| 변수 | 영향 |
|---|---|
| `--font-text-theme` | 본문 폰트 |
| `--font-interface-theme` | UI 폰트 |
| `--font-monospace-theme` | 모노스페이스 (코드) |

#### Font sizes

| 변수 | 기본값 | 용도 |
|---|---|---|
| `--font-text-size` | `16px` | 본문 (사용자가 Appearance 에서 조정) ★★ |
| `--font-smallest` | `0.8em` | 상대 |
| `--font-smaller` | `0.875em` | 상대 |
| `--font-small` | `0.933em` | 상대 |
| `--font-ui-smaller` | `12px` | UI 고정 |
| `--font-ui-small` | `13px` | UI 고정 |
| `--font-ui-medium` | `15px` | UI 고정 |
| `--font-ui-large` | `20px` | UI 고정 |

#### Font weights

| 변수 | 값 |
|---|---|
| `--font-thin` | `100` |
| `--font-extralight` | `200` |
| `--font-light` | `300` |
| `--font-normal` | `400` |
| `--font-medium` | `500` |
| `--font-semibold` | `600` |
| `--font-bold` | `700` |
| `--font-extrabold` | `800` |
| `--font-black` | `900` |

#### Text formatting ★★

| 변수 | 영향 |
|---|---|
| `--font-weight` | 일반 텍스트 굵기 |
| `--bold-modifier` | 굵게 추가 굵기 (옵시디언 1.6+ 권장 방식. 100~300 권장) |
| `--bold-weight` | 굵게 굵기 |
| `--bold-color` | 굵게 색 ★★ |
| `--italic-color` | 이탤릭 색 ★★ |

#### Line heights ★★

| 변수 | 기본값 | 용도 |
|---|---|---|
| `--line-height-normal` | `1.5` | 본문 |
| `--line-height-tight` | `1.3` | 검색결과·트리·툴팁 등 좁은 공간 |

#### Paragraph spacing ★★

| 변수 | 영향 |
|---|---|
| `--heading-spacing` | 헤딩 위 여백 |
| `--p-spacing` | 문단 사이 여백 |

### Spacing ★★

옵시디언 4-pixel grid. 패딩·마진에 4의 배수 권장.

| 변수 | 값 | 변수 | 값 |
|---|---|---|---|
| `--size-2-1` | 2px | `--size-4-5` | 20px |
| `--size-2-2` | 4px | `--size-4-6` | 24px |
| `--size-2-3` | 6px | `--size-4-8` | 32px |
| `--size-4-1` | 4px | `--size-4-9` | 36px |
| `--size-4-2` | 8px | `--size-4-12` | 48px |
| `--size-4-3` | 12px | `--size-4-16` | 64px |
| `--size-4-4` | 16px | `--size-4-18` | 72px |

### Radiuses ★★

| 변수 | 기본값 |
|---|---|
| `--radius-s` | `4px` |
| `--radius-m` | `8px` |
| `--radius-l` | `12px` |
| `--radius-xl` | `16px` |

### Borders ★

| 변수 | 기본값 |
|---|---|
| `--border-width` | `1px` |

### Icons ★

| 변수 | 영향 |
|---|---|
| `--icon-size` / `--icon-stroke` | 크기·두께 shorthand |
| `--icon-color` / `--icon-color-hover` / `--icon-color-active` / `--icon-color-focused` | 아이콘 색 |
| `--icon-opacity` / `--icon-opacity-hover` / `--icon-opacity-active` | 투명도 |
| `--clickable-icon-radius` | 클릭 가능 아이콘 버튼 모서리 |
| `--icon-xs ~ --icon-xl` | 14/16/18/18/32 px |
| `--icon-xs-stroke-width ~ --icon-xl-stroke-width` | 2/2/1.75/1.75/1.25 px |

### Cursor ★

| 변수 | 기본값 |
|---|---|
| `--cursor` | `default` (인터랙티브 요소) |
| `--cursor-link` | `pointer` (링크) |

### Layers ★

z-index 우선순위. 보통 만질 일 없음.

| 변수 | 값 | 변수 | 값 |
|---|---|---|---|
| `--layer-cover` | 5 | `--layer-modal` | 50 |
| `--layer-sidedock` | 10 | `--layer-notice` | 60 |
| `--layer-status-bar` | 15 | `--layer-menu` | 65 |
| `--layer-popover` | 30 | `--layer-tooltip` | 70 |
| `--layer-slides` | 45 | `--layer-dragged-item` | 80 |

---

## Editor

### Headings ★★★

h1~h6 각 7가지 (color, font, size, weight, line-height, style, variant). 총 44 변수.

| 변수 패턴 | 영향 |
|---|---|
| `--h{1..6}-color` | 각 헤딩 색 ★★★ |
| `--h{1..6}-font` | 각 헤딩 폰트 |
| `--h{1..6}-size` | 각 헤딩 크기 ★★ |
| `--h{1..6}-weight` | 각 헤딩 굵기 ★★ |
| `--h{1..6}-line-height` | 각 헤딩 줄간격 |
| `--h{1..6}-style` | 각 헤딩 스타일 (normal/italic) |
| `--h{1..6}-variant` | 각 헤딩 변형 (small-caps 등) |
| `--heading-formatting` | 헤딩 `# ##` 마크다운 심볼 색 |
| `--heading-spacing` | 헤딩 위 여백 (Typography 참조) |

### Inline title ★★

옵시디언 Settings → Appearance → Show inline title 켜야 보임. 노트 제목.

| 변수 | 영향 |
|---|---|
| `--inline-title-color` | 색 |
| `--inline-title-font` | 폰트 |
| `--inline-title-line-height` | 줄간격 |
| `--inline-title-size` | 크기 |
| `--inline-title-style` | 스타일 |
| `--inline-title-variant` | 변형 |
| `--inline-title-weight` | 굵기 |

### Blockquote ★★

| 변수 | 영향 |
|---|---|
| `--blockquote-background-color` | 배경 |
| `--blockquote-border-thickness` | 왼쪽 보더 두께 |
| `--blockquote-border-color` | 왼쪽 보더 색 ★★ |
| `--blockquote-font-style` | 폰트 스타일 (italic 등) |
| `--blockquote-color` | 텍스트 색 |

### Callout ★★

옵시디언 `> [!note]` 블록.

| 변수 | 영향 |
|---|---|
| `--callout-border-width` | 보더 두께 |
| `--callout-border-opacity` | 보더 투명도 |
| `--callout-padding` | 내부 패딩 |
| `--callout-radius` | 모서리 |
| `--callout-blend-mode` | 블렌드 모드 (중첩 콜아웃 색 합성) |
| `--callout-title-color` | 제목 색 ★★ |
| `--callout-title-padding` | 제목 패딩 |
| `--callout-title-size` | 제목 크기 |
| `--callout-title-weight` | 제목 굵기 |
| `--callout-content-padding` | 내용 패딩 |
| `--callout-content-background` | 내용 배경 |

#### Callout 타입별 색 ★★

| 변수 | 콜아웃 타입 |
|---|---|
| `--callout-bug` | `bug` |
| `--callout-default` | `default`, `note` |
| `--callout-error` | `error`, `danger` |
| `--callout-example` | `example` |
| `--callout-fail` | `fail`, `failure`, `missing` |
| `--callout-important` | `important` |
| `--callout-info` | `info` |
| `--callout-question` | `question`, `help`, `faq` |
| `--callout-success` | `success`, `check`, `done` |
| `--callout-summary` | `summary`, `abstract`, `tldr` |
| `--callout-tip` | `tip`, `hint` |
| `--callout-todo` | `todo` |
| `--callout-warning` | `warning`, `caution`, `attention` |
| `--callout-quote` | `quote`, `cite` |

### Code ★★★

#### Code 기본

| 변수 | 영향 |
|---|---|
| `--code-background` | 코드블록·인라인 배경 ★★★ |
| `--code-white-space` | `white-space` 속성 |
| `--code-size` | 코드 폰트 크기 |

#### Code syntax highlighting ★★

| 변수 | 영향 |
|---|---|
| `--code-normal` | 강조 안 된 코드 글자 |
| `--code-comment` | 주석 |
| `--code-function` | 함수 |
| `--code-important` | 중요·정규식 |
| `--code-keyword` | 키워드 ★★ |
| `--code-operator` | 연산자 |
| `--code-property` | 속성 |
| `--code-punctuation` | 구두점 |
| `--code-string` | 문자열 ★★ |
| `--code-tag` | 태그·기호·상수 |
| `--code-value` | 값 |

### Link ★★★

| 변수 | 영향 |
|---|---|
| `--link-color` | [[wikilink]] 색 ★★★ |
| `--link-color-hover` | hover |
| `--link-decoration` | 텍스트 장식 |
| `--link-decoration-hover` | 장식 (hover) |
| `--link-decoration-thickness` | 장식 두께 |
| `--link-weight` | 굵기 |
| `--link-unresolved-color` | 미해결 링크 색 ★★ |
| `--link-unresolved-opacity` | 미해결 투명도 |
| `--link-unresolved-filter` | 필터 (hue-rotate 등) |
| `--link-unresolved-decoration-style` | 장식 스타일 |
| `--link-unresolved-decoration-color` | 장식 색 |
| `--link-external-color` | 외부 URL 색 ★★ |
| `--link-external-color-hover` | hover |
| `--link-external-decoration` | 장식 |
| `--link-external-decoration-hover` | 장식 (hover) |

### Tag ★★

| 변수 | 영향 |
|---|---|
| `--tag-size` | 폰트 크기 |
| `--tag-color` | 글자 색 ★★ |
| `--tag-color-hover` | hover |
| `--tag-decoration` | 장식 |
| `--tag-decoration-hover` | 장식 (hover) |
| `--tag-background` | 배경 ★★ |
| `--tag-background-hover` | hover 배경 |
| `--tag-border-color` | 보더 |
| `--tag-border-color-hover` | 보더 (hover) |
| `--tag-border-width` | 보더 두께 |
| `--tag-padding-x` | 좌우 패딩 |
| `--tag-padding-y` | 상하 패딩 |
| `--tag-radius` | 모서리 |
| `--tag-weight` | 굵기 |

### Table ★★

총 33 변수. 자주 만지는 것만 ★ 표시.

| 변수 | 영향 |
|---|---|
| `--table-background` | 전체 배경 |
| `--table-border-width` / `--table-border-color` | 테두리 |
| `--table-cell-vertical-alignment` | 셀 수직 정렬 |
| `--table-white-space` | `white-space` |
| `--table-header-background` | 헤더 배경 ★★ |
| `--table-header-background-hover` | 헤더 hover |
| `--table-header-border-width` / `--table-header-border-color` | 헤더 보더 |
| `--table-header-font` / `--table-header-size` / `--table-header-weight` | 헤더 폰트 |
| `--table-header-color` | 헤더 텍스트 ★ |
| `--table-line-height` | 셀 줄간격 |
| `--table-text-size` / `--table-text-color` | 셀 폰트·색 |
| `--table-column-max-width` | 열 최대 너비 |
| `--table-column-alt-background` | 교대 열 배경 |
| `--table-column-first-border-width` / `--table-column-last-border-width` | 첫·끝 열 보더 |
| `--table-row-background-hover` | 행 hover |
| `--table-row-alt-background` / `--table-row-alt-background-hover` | 교대 행 ★ |
| `--table-row-last-border-width` | 마지막 행 보더 |
| `--table-selection` / `--table-selection-blend-mode` / `--table-selection-border-color` / `--table-selection-border-width` / `--table-selection-border-radius` | 선택 영역 |
| `--table-drag-handle-background` / `--table-drag-handle-background-active` / `--table-drag-handle-color` / `--table-drag-handle-color-active` | 드래그 핸들 |
| `--table-add-button-background` / `--table-add-button-border-width` / `--table-add-button-border-color` | "추가" 버튼 |

### List ★★

| 변수 | 영향 |
|---|---|
| `--list-indent` | 중첩 항목 들여쓰기 ★ |
| `--list-indent-editing` | Live Preview 들여쓰기 |
| `--list-indent-source` | Source mode 들여쓰기 |
| `--list-spacing` | 항목 간 수직 간격 ★ |
| `--list-marker-color` | bullet·번호 색 ★★ |
| `--list-marker-color-hover` | hover |
| `--list-marker-color-collapsed` | 접힌 상태 |
| `--list-bullet-border` | bullet 보더 |
| `--list-bullet-end-padding` | bullet 뒤 패딩 |
| `--list-bullet-radius` | bullet 모서리 |
| `--list-bullet-size` | bullet 크기 |
| `--list-bullet-transform` | bullet `transform` |
| `--list-numbered-style` | 번호 리스트 `list-style-type` |

### Embed

마크다운 `![[file]]` 임베드.

| 변수 | 영향 |
|---|---|
| `--embed-max-height` / `--embed-canvas-max-height` | 최대 높이 |
| `--embed-background` | 배경 |
| `--embed-border-end` / `--embed-border-start` / `--embed-border-top` / `--embed-border-bottom` | 보더 shorthand |
| `--embed-padding` | 패딩 |
| `--embed-font-style` | 폰트 스타일 |

### Footnote

| 변수 | 영향 |
|---|---|
| `--footnote-size` | 각주 폰트 크기 |

### Horizontal rule ★

마크다운 `---`.

| 변수 | 영향 |
|---|---|
| `--hr-color` | 색 |
| `--hr-thickness` | 두께 |

### Block

| 변수 | 영향 |
|---|---|
| `--embed-block-shadow-hover` | Live Preview 임베드 블록 hover 그림자 |

### File

옵시디언 노트 본문 영역.

| 변수 | 영향 |
|---|---|
| `--file-line-width` | "Readable line width" 켰을 때 줄 너비 ★ |
| `--file-folding-offset` | 폴드 인디케이터 너비 |
| `--file-margins` | 파일 여백 |
| `--file-header-font-size` / `--file-header-font-weight` | 파일 헤더 폰트 |
| `--file-header-border` | 헤더 보더 |
| `--file-header-justify` | 헤더 텍스트 정렬 |

### Properties

YAML frontmatter UI. 총 35 변수 — `--metadata-*` prefix.

대표:
| 변수 | 영향 |
|---|---|
| `--metadata-background` | 전체 배경 |
| `--metadata-padding` / `--metadata-border-color` / `--metadata-border-radius` / `--metadata-border-width` | 외곽 |
| `--metadata-label-text-color` / `--metadata-label-text-color-hover` / `--metadata-label-font-size` / `--metadata-label-font-weight` | 속성 라벨 |
| `--metadata-input-text-color` / `--metadata-input-background` / `--metadata-input-height` / `--metadata-input-font-size` | 속성 값 입력 |
| `--metadata-divider-color` | 속성 사이 구분선 |

전체 35 변수는 [공식 docs Properties](https://docs.obsidian.md/Reference/CSS+variables/Editor/Properties) 참조.

### Bases

옵시디언 Bases (DB뷰) — 옵시디언 1.7+. 총 33 변수 — `--bases-*` prefix. 베이스 컨테이너, 테이블 뷰, 카드 뷰 변수 다수. [공식 docs Bases](https://docs.obsidian.md/Reference/CSS+variables/Editor/Bases) 참조.

---

## Components

### Tabs ★★★

| 변수 | 영향 |
|---|---|
| `--tab-background-active` | 활성 탭 배경 ★★ |
| `--tab-text-color` | 탭 글자색 |
| `--tab-text-color-active` | 비포커스 창의 활성 탭 글자 |
| `--tab-text-color-focused` | 포커스 창의 탭 |
| `--tab-text-color-focused-active` | 포커스 창의 활성 탭 ★ |
| `--tab-text-color-focused-highlighted` | 포커스 창 강조 |
| `--tab-text-color-focused-active-current` | 포커스 창 현재 탭 |
| `--tab-font-size` / `--tab-font-weight` | 탭 폰트 |
| `--tab-container-background` | 탭 컨테이너 배경 ★ |
| `--tab-divider-color` | 탭 구분선 |
| `--tab-outline-color` / `--tab-outline-width` | 탭 외곽선 |
| `--tab-curve` | 탭 곡선 반경 |
| `--tab-radius` / `--tab-radius-active` | 탭 모서리 |
| `--tab-width` / `--tab-max-width` | 탭 너비 |

#### 스택 탭

| 변수 | 영향 |
|---|---|
| `--tab-stacked-pane-width` / `--tab-stacked-header-width` | 스택 너비 |
| `--tab-stacked-font-size` / `--tab-stacked-font-weight` | 스택 폰트 |
| `--tab-stacked-text-align` / `--tab-stacked-text-transform` / `--tab-stacked-text-writing-mode` | 스택 텍스트 |
| `--tab-stacked-shadow` | 스택 그림자 |

### Button ★

| 변수 | 영향 |
|---|---|
| `--button-radius` | 버튼 모서리 |

> 버튼 색은 [Colors / Interactive colors](#interactive-colors-) 의 `--interactive-normal`, `--interactive-accent` 참조.

### Modal ★★

| 변수 | 영향 |
|---|---|
| `--modal-background` | 배경 ★ |
| `--modal-width` / `--modal-height` | 기본 크기 |
| `--modal-max-width` / `--modal-max-height` | 최대 크기 |
| `--modal-max-width-narrow` | 좁은 모달 최대 너비 |
| `--modal-border-width` / `--modal-border-color` | 보더 |
| `--modal-radius` | 모서리 |
| `--modal-community-sidebar-width` | 커뮤니티 플러그인/테마 사이드바 너비 |

### Dialog

| 변수 | 영향 |
|---|---|
| `--dialog-width` / `--dialog-max-width` / `--dialog-max-height` | 크기 |

### Popover ★

파일 hover 미리보기 등.

| 변수 | 영향 |
|---|---|
| `--popover-width` / `--popover-height` / `--popover-max-height` | 크기 |
| `--popover-font-size` | 폰트 크기 |
| `--popover-pdf-width` / `--popover-pdf-height` | PDF 미리보기 크기 |

### Prompt

Quick switcher, Command palette.

| 변수 | 영향 |
|---|---|
| `--prompt-input-height` | 입력 높이 |
| `--prompt-width` / `--prompt-max-width` / `--prompt-max-height` | 크기 |
| `--prompt-border-width` / `--prompt-border-color` | 보더 |

### Dropdowns

| 변수 | 영향 |
|---|---|
| `--dropdown-background` / `--dropdown-background-hover` | 배경 |
| `--dropdown-background-blend-mode` / `--dropdown-background-position` / `--dropdown-background-size` | 배경 스타일 |
| `--dropdown-padding` | 패딩 |

### Text input

| 변수 | 영향 |
|---|---|
| `--input-height` / `--input-radius` / `--input-font-weight` / `--input-border-width` | 입력 박스 스타일 |

### Color input

| 변수 | 영향 |
|---|---|
| `--swatch-radius` / `--swatch-height` / `--swatch-width` / `--swatch-shadow` | 색 스와치 |

### Checkbox ★

| 변수 | 영향 |
|---|---|
| `--checkbox-radius` / `--checkbox-size` | 모양 |
| `--checkbox-marker-color` | 체크 마커 색 |
| `--checkbox-color` / `--checkbox-color-hover` | 배경 |
| `--checkbox-border-color` / `--checkbox-border-color-hover` | 보더 |
| `--checklist-done-decoration` | 체크된 텍스트 장식 (line-through 등) ★ |
| `--checklist-done-color` | 체크된 텍스트 색 |
| `--checkbox-margin-inline-start` | `start` margin |

### Toggle

| 변수 | 영향 |
|---|---|
| `--toggle-border-width` / `--toggle-width` / `--toggle-radius` | 토글 모양 |
| `--toggle-thumb-color` / `--toggle-thumb-radius` / `--toggle-thumb-height` / `--toggle-thumb-width` | 토글 thumb |
| `--toggle-s-*` | 작은 토글 변형 |

### Slider

| 변수 | 영향 |
|---|---|
| `--slider-thumb-border-width` / `--slider-thumb-border-color` / `--slider-thumb-height` / `--slider-thumb-width` / `--slider-thumb-y` / `--slider-thumb-radius` | thumb |
| `--slider-track-background` / `--slider-track-height` | 트랙 |

### Multi-select

Pill 형식 다중 선택.

| 변수 | 영향 |
|---|---|
| `--pill-color` / `--pill-color-hover` / `--pill-color-remove` / `--pill-color-remove-hover` | 글자색 |
| `--pill-decoration` / `--pill-decoration-hover` | 장식 |
| `--pill-background` / `--pill-background-hover` | 배경 |
| `--pill-border-color` / `--pill-border-color-hover` / `--pill-border-width` | 보더 |
| `--pill-padding-x` / `--pill-padding-y` | 패딩 |
| `--pill-radius` / `--pill-weight` | 모서리·굵기 |

### Navigation ★★

파일 탐색기 등 트리 nav.

| 변수 | 영향 |
|---|---|
| `--nav-item-size` | 폰트 크기 |
| `--nav-item-color` / `--nav-item-color-hover` / `--nav-item-color-active` / `--nav-item-color-selected` / `--nav-item-color-highlighted` | 텍스트 색 ★ |
| `--nav-item-background-hover` / `--nav-item-background-active` / `--nav-item-background-selected` | 배경 ★ |
| `--nav-item-padding` / `--nav-item-parent-padding` | 패딩 |
| `--nav-item-children-padding-start` / `--nav-item-children-margin-start` | 자식 들여쓰기 |
| `--nav-item-weight` / `--nav-item-weight-hover` / `--nav-item-weight-active` | 굵기 |
| `--nav-item-white-space` | `white-space` |
| `--nav-indentation-guide-width` / `--nav-indentation-guide-color` | 들여쓰기 가이드 |
| `--nav-collapse-icon-color` / `--nav-collapse-icon-color-collapsed` | 접기 chevron 색 |

#### Navigation headings

| 변수 | 영향 |
|---|---|
| `--nav-heading-color` / `--nav-heading-color-hover` / `--nav-heading-color-collapsed` / `--nav-heading-color-colapsed-hover` | 색 |
| `--nav-heading-weight` / `--nav-heading-weight-hover` | 굵기 |

### Indentation guides

| 변수 | 영향 |
|---|---|
| `--indentation-guide-width` / `--indentation-guide-width-active` | 보더 두께 |
| `--indentation-guide-color` / `--indentation-guide-color-active` | 보더 색 |
| `--indentation-guide-editing-indent` / `--indentation-guide-reading-indent` / `--indentation-guide-source-indent` | 모드별 들여쓰기 |

### Dragging

| 변수 | 영향 |
|---|---|
| `--drag-ghost-background` / `--drag-ghost-text-color` | 드래그 ghost |

---

## Window

### Window frame ★★

옵시디언 Settings → Appearance → Window frame style 을 `Obsidian frame` 으로 해야 보임.

| 변수 | 영향 |
|---|---|
| `--titlebar-background` | 타이틀바 배경 |
| `--titlebar-background-focused` | 포커스 타이틀바 |
| `--titlebar-border-width` / `--titlebar-border-color` | 보더 |
| `--titlebar-text-color` / `--titlebar-text-color-focused` | 텍스트 |
| `--titlebar-text-weight` | 폰트 굵기 |
| `--header-height` | 프레임 기본 높이 |

### Ribbon ★★

좌측 워크스페이스 아이콘 바.

| 변수 | 영향 |
|---|---|
| `--ribbon-background` | 배경 ★ |
| `--ribbon-background-collapsed` | 사이드바 접힌 상태 배경 |
| `--ribbon-width` / `--ribbon-padding` | 너비·패딩 |

### Sidebar

| 변수 | 영향 |
|---|---|
| `--sidebar-markdown-font-size` | 사이드바 마크다운 파일 폰트 크기 |
| `--sidebar-tab-text-display` | 탭 텍스트 `display` 속성 |

### Status bar ★

| 변수 | 영향 |
|---|---|
| `--status-bar-background` | 배경 ★ |
| `--status-bar-border-color` / `--status-bar-border-width` | 보더 |
| `--status-bar-font-size` | 폰트 크기 |
| `--status-bar-text-color` | 텍스트 |
| `--status-bar-position` | `position` 속성 |
| `--status-bar-radius` | 모서리 |
| `--status-bar-scroll-padding` | 스크롤 패딩 |

### Divider

사이드바·탭·split pane 사이 구분선.

| 변수 | 영향 |
|---|---|
| `--divider-color` / `--divider-color-hover` | 색 |
| `--divider-width` / `--divider-width-hover` | 너비 |
| `--divider-vertical-height` | 수직 높이 |

### Scrollbar

Windows/Linux 만 사용 (macOS 는 OS 스크롤바).

| 변수 | 영향 |
|---|---|
| `--scrollbar-bg` | 배경 |
| `--scrollbar-thumb-bg` | thumb 배경 |
| `--scrollbar-active-thumb-bg` | thumb 활성 |

### Vault profile

좌측 사이드바 하단 vault 프로필.

| 변수 | 영향 |
|---|---|
| `--vault-profile-display` / `--vault-profile-actions-display` | `display` 속성 |
| `--vault-profile-font-size` / `--vault-profile-font-weight` | 폰트 |
| `--vault-profile-color` / `--vault-profile-color-hover` | 색 |

### Workspace

| 변수 | 영향 |
|---|---|
| `--workspace-background-translucent` | 반투명 윈도우 배경 |

---

## Plugins

### Canvas ★

| 변수 | 영향 |
|---|---|
| `--canvas-background` | 캔버스 배경 |
| `--canvas-card-label-color` | 카드 라벨 텍스트 |
| `--canvas-dot-pattern` | 닷 패턴 색 |
| `--canvas-color-1 ~ --canvas-color-6` | 카드 색 6종 |

### File explorer

Vault profile 과 변수 공유.

| 변수 | 영향 |
|---|---|
| (Vault profile 참조) |

### Graph ★

| 변수 | 영향 |
|---|---|
| `--graph-controls-width` | 컨트롤 너비 |
| `--graph-text` | 노드 텍스트 |
| `--graph-line` | 연결선 |
| `--graph-node` | 해결된 노드 |
| `--graph-node-unresolved` | 미해결 노드 |
| `--graph-node-focused` | 포커스 노드 |
| `--graph-node-tag` | 태그 노드 |
| `--graph-node-attachment` | 첨부 노드 |

### Search

| 변수 | 영향 |
|---|---|
| `--search-clear-button-color` / `--search-clear-button-size` | 클리어 버튼 |
| `--search-icon-color` / `--search-icon-size` | 검색 아이콘 |
| `--search-result-background` | 결과 배경 |

### Sync

| 변수 | 영향 |
|---|---|
| `--sync-avatar-color-current-user` | 현재 사용자 아바타 |
| `--sync-avatar-color-1 ~ --sync-avatar-color-8` | 8가지 아바타 색 |

---

## 자연어 → 변수 매핑 (수정 모드용)

사용자가 자연어로 "X 를 어떻게 바꿔줘" 라고 하면 이 표로 매핑. 모호하면 후보 2~3개 hint 제시 후 사용자 선택.

### 색

| 사용자 표현 | 매핑 변수 |
|---|---|
| "본문 배경", "노트 배경" | `--background-primary` |
| "사이드바 배경", "왼쪽/오른쪽 패널" | `--background-secondary` |
| "본문 글자색", "텍스트 색" | `--text-normal` |
| "흐린 글자", "부제" | `--text-muted` |
| "캐럿", "커서" | `--caret-color` |
| "굵게 강조 색", "볼드 색" | `--bold-color` |
| "이탤릭 색", "기울임" | `--italic-color` |
| "액센트", "강조색", "메인 컬러" | `--accent-h` / `--accent-s` / `--accent-l` |
| "에러 색" | `--text-error` / `--background-modifier-error` |
| "성공 색" | `--text-success` / `--background-modifier-success` |

### 헤딩 / 인라인 제목

| 사용자 표현 | 매핑 변수 |
|---|---|
| "h1 색", "큰 제목 색" | `--h1-color` |
| "h{N} 크기" | `--h{N}-size` |
| "h{N} 굵기" | `--h{N}-weight` |
| "h{N} 폰트" | `--h{N}-font` |
| "헤딩 # 기호 색" | `--heading-formatting` |
| "노트 제목", "인라인 타이틀" | `--inline-title-color` / `--inline-title-size` |

### 링크 / 태그

| 사용자 표현 | 매핑 변수 |
|---|---|
| "링크 색", "위키링크 색" | `--link-color` |
| "외부 링크 색", "URL 색" | `--link-external-color` |
| "미해결 링크 색", "빈 링크" | `--link-unresolved-color` |
| "링크 밑줄" | `--link-decoration` |
| "태그 글자", "#태그 색" | `--tag-color` |
| "태그 배경" | `--tag-background` |
| "태그 모서리" | `--tag-radius` |

### 코드

| 사용자 표현 | 매핑 변수 |
|---|---|
| "코드블록 배경" | `--code-background` |
| "코드 글자", "강조 안 된 코드" | `--code-normal` |
| "코드 주석" | `--code-comment` |
| "코드 키워드" | `--code-keyword` |
| "코드 문자열" | `--code-string` |
| "코드 함수" | `--code-function` |
| "코드 연산자" | `--code-operator` |
| "코드 폰트 크기" | `--code-size` |

### 콜아웃 / 인용 / 강조

| 사용자 표현 | 매핑 변수 |
|---|---|
| "콜아웃 제목" | `--callout-title-color` |
| "콜아웃 내용 배경" | `--callout-content-background` |
| "콜아웃 모서리" | `--callout-radius` |
| "info 콜아웃 색" | `--callout-info` (또는 `--callout-<타입>`) |
| "인용 색", "blockquote" | `--blockquote-color` / `--blockquote-border-color` |
| "==하이라이트== 배경" | `--text-highlight-bg` |
| "구분선 색" | `--hr-color` |

### 리스트 / 표

| 사용자 표현 | 매핑 변수 |
|---|---|
| "bullet 색", "리스트 점" | `--list-marker-color` |
| "리스트 들여쓰기" | `--list-indent` |
| "리스트 항목 사이" | `--list-spacing` |
| "체크박스 색" | `--checkbox-color` / `--checkbox-marker-color` |
| "완료된 체크 글자" | `--checklist-done-color` / `--checklist-done-decoration` |
| "표 헤더 배경" | `--table-header-background` |
| "표 교대 행" | `--table-row-alt-background` |
| "표 경계선" | `--table-border-color` |

### UI 크롬

| 사용자 표현 | 매핑 변수 |
|---|---|
| "탭 배경", "활성 탭" | `--tab-background-active` |
| "탭 모서리" | `--tab-radius` |
| "탭 글자" | `--tab-text-color-focused-active` |
| "리본", "왼쪽 아이콘 바" | `--ribbon-background` |
| "타이틀바", "윈도우 상단" | `--titlebar-background` |
| "상태바", "아래쪽 바" | `--status-bar-background` |
| "사이드바 파일 글자" | `--nav-item-color` |
| "선택된 파일 배경" | `--nav-item-background-selected` |
| "구분선", "사이드바 경계" | `--divider-color` |
| "모달 배경" | `--modal-background` |
| "팝오버", "파일 hover 미리보기" | `--popover-width` 등 |
| "스크롤바" (Windows/Linux) | `--scrollbar-thumb-bg` |
| "아이콘 색" | `--icon-color` |

### 폰트

| 사용자 표현 | 매핑 변수 |
|---|---|
| "본문 폰트" | `--font-text-theme` |
| "UI 폰트", "메뉴 폰트" | `--font-interface-theme` |
| "코드 폰트", "모노스페이스" | `--font-monospace-theme` |
| "글자 크기" | `--font-text-size` |
| "줄간격" | `--line-height-normal` |
| "헤딩 위 여백" | `--heading-spacing` |
| "문단 사이 여백" | `--p-spacing` |

### 간격 / 모서리

| 사용자 표현 | 매핑 변수 |
|---|---|
| "모서리 둥글게" | `--radius-s` / `--radius-m` / `--radius-l` / `--radius-xl` |
| "보더 두께" | `--border-width` |
| "노트 본문 너비" | `--file-line-width` |

### 캔버스 / 그래프

| 사용자 표현 | 매핑 변수 |
|---|---|
| "캔버스 배경" | `--canvas-background` |
| "캔버스 카드 색" | `--canvas-color-1 ~ -6` |
| "그래프 노드" | `--graph-node` |
| "그래프 연결선" | `--graph-line` |

---

## ⚠️ Cascade 우선순위 (다른 커스텀이 있는 vault 에서 주의)

옵시디언 CSS 로딩 순서 (약함 → 강함):

1. 옵시디언 코어 CSS
2. **테마 CSS** (`.obsidian/themes/<name>/theme.css`)
3. **CSS snippet** (`.obsidian/snippets/*.css`) — 마지막 로드라 가장 강력
4. `appearance.json` 의 `textFontFamily`/`interfaceFontFamily`/`monospaceFontFamily` — inline 으로 박혀서 보통 테마 CSS 보다 강함

→ **백지 vault** (snippet 0개 + appearance.json 폰트 필드 비어있음) 에서는 이 스킬이 만든 테마가 의도대로 100% 적용된다.
→ **기존 snippet/폰트 설정이 있는 vault** 에서는 일부 변수가 override 될 수 있다. 의도와 다르게 보이면:
- Settings → Appearance → CSS snippets 에서 충돌 가능한 snippet 일시 토글 OFF
- appearance.json 의 폰트 필드를 비워두면 테마 CSS 가 적용됨

수정 모드에서 외부 테마 위에 `snippets/obsidian-theme-override.css` 로 작성하는 것은 이 cascade 를 활용한 의도된 설계 (snippet 이 가장 강하므로 외부 테마 위에 안전하게 덮어쓰기 가능).

## 권장 작성 패턴

테마를 처음부터 빌드할 때 권장 순서:

1. **Base color 11-step 정의** (라이트·다크 별도) — `--color-base-00 ~ 100`
2. **확장 색 정의** (필요한 색만) — `--color-red`, `--color-blue` 등
3. **액센트 정의** — `--accent-h/s/l`
4. **의미론적 색은 base/확장에서 참조** — `--background-primary: var(--color-base-00)` 처럼
5. **공통 (폰트·간격·둥글기) 는 `body` 블록** — 라이트·다크 분기 X
6. **디테일 영역 (h1~h6 · 콜아웃 · 코드 syntax 등) 은 수정 모드로 점진 보강** — 한 번에 다 정하지 않고, 시각적 확인하며 조정

라이트/다크 둘 다 지원하는 테마는 다음 구조로 작성:

```css
/* obsidian-theme: managed */

.theme-light {
  /* Base 11-step */
  --color-base-00: #fefefe;
  /* ... */

  /* Accent */
  --accent-h: 25;
  --accent-s: 60%;
  --accent-l: 50%;

  /* 의미론적 색 */
  --background-primary: var(--color-base-00);
  --text-normal: var(--color-base-100);
}

.theme-dark {
  /* 다크 11-step + 동일 의미론적 매핑 */
}

/* 라이트·다크 공통 */
body {
  --font-text-theme: 'Inter', -apple-system, sans-serif;
  --font-interface-theme: -apple-system, BlinkMacSystemFont, sans-serif;
  --font-monospace-theme: 'JetBrains Mono', Menlo, monospace;
  --radius-m: 8px;
  --line-height-normal: 1.6;
}
```
