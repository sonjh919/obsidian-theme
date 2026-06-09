# Obsidian CSS Variables Cheatsheet

옵시디언 테마에서 가장 많이 사용되는 CSS 변수들. 카테고리별로 정리. 변수를 `body` 또는 `.theme-light` / `.theme-dark` 블록에서 override 하면 옵시디언 hot reload.

> 출처: 옵시디언 공식 CSS 변수 문서 (https://docs.obsidian.md/Reference/CSS+variables) 와 교차 검증됨.
> 이 표는 "테마 빌드에 자주 쓰이는 핵심 변수만" 추린 cheatsheet. 전체 목록은 공식 문서 참조.

## 카테고리별 변수

### Base Color System (Foundations/Colors — 옵시디언 권장 패턴)

옵시디언은 11-step base color 토큰을 제공한다. 다른 의미론적 색 (`--background-primary` 등) 은 기본적으로 이 토큰을 참조한다. **테마 빌드 시 base 토큰을 먼저 라이트/다크 11단으로 정의해두면 일관성 ↑**.

| 변수 | 라이트 기본 | 다크 기본 | 용도 |
|---|---|---|---|
| `--color-base-00` | `#ffffff` | `#1e1e1e` | 가장 밝은 면 (라이트) / 가장 어두운 면 (다크) |
| `--color-base-10` | … | … | |
| `--color-base-20` | … | … | |
| `--color-base-30` | … | … | |
| `--color-base-40` | … | … | |
| `--color-base-50` | … | … | 중간 — 보더·구분선 |
| `--color-base-60` | … | … | |
| `--color-base-70` | … | … | 흐린 텍스트 |
| `--color-base-100` | … | … | 가장 진한 텍스트 |

### 확장 색상 (Extended Colors)

라이트·다크 둘 다 정의됨. 의미론적 사용 (액센트·태그·에러 등) 의 기반.

| 변수 | 라이트 | 다크 |
|---|---|---|
| `--color-red` | `#e93147` | `#fb464c` |
| `--color-orange` | `#ec7500` | `#e9973f` |
| `--color-yellow` | `#e0ac00` | `#e0de71` |
| `--color-green` | `#08b94e` | `#44cf6e` |
| `--color-cyan` | `#00bfbc` | `#53dfdd` |
| `--color-blue` | `#086ddd` | `#027aff` |
| `--color-purple` | `#7852ee` | `#a882ff` |
| `--color-pink` | `#ce518c` | `#fa99cd` |

### 배경 (Background)
| 변수 | 영향 범위 |
|---|---|
| `--background-primary` | 메인 노트 배경 |
| `--background-primary-alt` | 사이드바 패널 일부 |
| `--background-secondary` | 사이드바·탭 배경 |
| `--background-secondary-alt` | 사이드바 내부 hover |
| `--background-modifier-border` | 경계선·구분선 |
| `--background-modifier-hover` | hover 상태 배경 |

### 텍스트 (Text)
| 변수 | 영향 범위 |
|---|---|
| `--text-normal` | 본문 텍스트 |
| `--text-muted` | 부제·헬프 텍스트 |
| `--text-faint` | placeholder·메타 |
| `--text-on-accent` | 액센트 위 텍스트 (버튼 글자) |
| `--text-error` | 에러 메시지 |
| `--caret-color` | 텍스트 입력 캐럿 |
| `--bold-color` | 굵게 강조 색 |
| `--italic-color` | 이탤릭 색 |

### 액센트 (Accent)
| 변수 | 영향 범위 | 권장 형식 |
|---|---|---|
| `--accent-h` | 액센트 색 hue (0-360) | 정수 |
| `--accent-s` | 액센트 채도 % | `70%` |
| `--accent-l` | 액센트 명도 % | `50%` |
| `--interactive-accent` | 액센트 색 (자동 계산) | HSL 결과 |
| `--interactive-accent-hover` | 액센트 hover | HSL 결과 |
| `--interactive-normal` | 일반 인터랙티브 요소 | |

옵시디언은 `--accent-h/s/l` 를 받아 `--interactive-accent` 등을 자동 계산. hex 가 아니라 HSL 컴포넌트로 분리되어 있음. **직접 hex 박지 말고 h/s/l 만 세팅하면 옵시디언이 나머지 처리**.

### 링크 (Link — Editor/Link 카테고리)
| 변수 | 영향 범위 |
|---|---|
| `--link-color` | 내부 [[wikilink]] (해결된 링크) 색 |
| `--link-color-hover` | wikilink hover |
| `--link-weight` | wikilink 폰트 굵기 |
| `--link-decoration` | wikilink 텍스트 장식 (underline 등) |
| `--link-external-color` | 외부 URL 링크 색 |
| `--link-external-color-hover` | 외부 링크 hover |
| `--link-unresolved-color` | 미해결 (존재 안 하는 노트) 링크 색 |
| `--link-unresolved-opacity` | 미해결 링크 투명도 |

### 태그 (Tag — Editor/Tag 카테고리)
| 변수 | 영향 범위 |
|---|---|
| `--tag-color` | #태그 텍스트 색 |
| `--tag-color-hover` | #태그 hover 색 |
| `--tag-background` | #태그 배경 |
| `--tag-background-hover` | #태그 hover 배경 |
| `--tag-border-color` | #태그 테두리 |
| `--tag-radius` | #태그 모서리 둥글기 |
| `--tag-padding-x` | #태그 좌우 여백 |
| `--tag-padding-y` | #태그 상하 여백 |
| `--tag-size` | #태그 글자 크기 |
| `--tag-weight` | #태그 글자 굵기 |

### 코드 (Code — Editor/Code 카테고리)
| 변수 | 영향 범위 |
|---|---|
| `--code-background` | 코드블록·인라인 코드 배경 |
| `--code-size` | 코드 글꼴 크기 |
| `--code-normal` | 강조 안 된 코드 글자 |
| `--code-comment` | 주석 색 |
| `--code-keyword` | 키워드 색 |
| `--code-string` | 문자열 색 |
| `--code-function` | 함수 색 |
| `--code-operator` | 연산자 색 |
| `--code-property` | 속성 색 |
| `--code-tag` | 태그·기호·상수 색 |
| `--code-value` | 값 색 |
| `--code-punctuation` | 구두점 색 |

### 탭 (Tabs — Components/Tabs 카테고리)
| 변수 | 영향 범위 |
|---|---|
| `--tab-background-active` | 활성 탭 배경 |
| `--tab-container-background` | 탭 컨테이너 배경 |
| `--tab-text-color-active` | 비포커스 창의 활성 탭 글자색 |
| `--tab-text-color-focused-active` | 포커스 창의 활성 탭 글자색 |
| `--tab-divider-color` | 탭 구분선 |
| `--tab-radius` | 탭 모서리 |
| `--tab-radius-active` | 활성 탭 모서리 |
| `--tab-curve` | 탭 곡선 반경 |
| `--tab-font-size` | 탭 글자 크기 |

### 리본 (Ribbon — Window/Ribbon 카테고리)
| 변수 | 영향 범위 |
|---|---|
| `--ribbon-background` | 좌측 리본 (워크스페이스 아이콘) 배경 |
| `--ribbon-background-collapsed` | 사이드바 접힌 상태의 리본 배경 |
| `--ribbon-width` | 리본 너비 |
| `--ribbon-padding` | 리본 패딩 |

### 타이틀바 (Window Frame — Window 카테고리)
| 변수 | 영향 범위 |
|---|---|
| `--titlebar-background` | 윈도우 타이틀바 배경 |
| `--titlebar-background-focused` | 포커스 윈도우의 타이틀바 배경 |
| `--titlebar-text-color` | 타이틀바 글자색 |
| `--titlebar-border-color` | 타이틀바 테두리 |
| `--header-height` | 프레임 요소 기본 높이 |

> 주의: 옵시디언 타이틀바를 보려면 **Settings → Appearance → Window frame style** 을 `Obsidian frame` 으로 설정해야 함. 시스템 frame 모드는 OS 타이틀바를 사용.

### 폰트 (Typography — Foundations/Typography 카테고리)

⚠️ **변수명에 `-theme` suffix 필수** (커뮤니티에서 흔히 헷갈리는 부분):

| 변수 | 영향 범위 |
|---|---|
| `--font-text-theme` | 본문 폰트 (font-family) |
| `--font-interface-theme` | UI 폰트 |
| `--font-monospace-theme` | 모노스페이스 (코드블록) |
| `--font-text-size` | 본문 폰트 크기 (기본 16px) |
| `--font-smallest` ~ `--font-small` | 상대 크기 토큰 |
| `--font-ui-smaller` ~ `--font-ui-large` | UI 고정 크기 토큰 |
| `--font-thin` (100) ~ `--font-black` (900) | 굵기 토큰 |
| `--line-height-normal` | 본문 줄간격 (기본 1.5) |
| `--line-height-tight` | 작은 줄간격 (기본 1.3) |

### 모서리 둥글기 (Radiuses — Foundations/Radiuses 카테고리)
| 변수 | 기본값 |
|---|---|
| `--radius-s` | `4px` |
| `--radius-m` | `8px` |
| `--radius-l` | `12px` |
| `--radius-xl` | `16px` |

### 간격 (Spacing — Foundations/Spacing 카테고리)

옵시디언은 **4-pixel grid** 기반 토큰 시스템. 패딩·마진에 4의 배수 사용 권장.

| 변수 | 값 |
|---|---|
| `--size-4-1` | 4px |
| `--size-4-2` | 8px |
| `--size-4-3` | 12px |
| `--size-4-4` | 16px |
| `--size-4-5` | 20px |
| `--size-4-6` | 24px |
| `--size-4-8` | 32px |
| `--size-4-12` | 48px |
| `--size-4-16` | 64px |
| `--size-2-1` | 2px (sparingly) |
| `--size-2-2` | 4px (sparingly) |
| `--size-2-3` | 6px (sparingly) |

## 자연어 → 변수 매핑표

수정 모드에서 사용자가 자연어로 변경 위치를 말하면 이 표를 참조하여 변수를 식별한다.

| 사용자 표현 | 매핑 변수 |
|---|---|
| "본문 배경", "노트 배경" | `--background-primary` |
| "사이드바 배경", "왼쪽 패널", "오른쪽 패널" | `--background-secondary` |
| "본문 글자색", "텍스트 색" | `--text-normal` |
| "부제 글자색", "흐린 글자" | `--text-muted` |
| "캐럿", "커서" | `--caret-color` |
| "굵게 강조 색", "볼드 색" | `--bold-color` |
| "이탤릭 색", "기울임 색" | `--italic-color` |
| "액센트", "강조색", "메인 컬러" | `--accent-h`, `--accent-s`, `--accent-l` (HSL 분해) |
| "링크 색", "위키링크 색", "[[ ]] 색" | `--link-color` |
| "외부 링크 색", "URL 색" | `--link-external-color` |
| "미해결 링크 색", "빈 링크" | `--link-unresolved-color` |
| "태그 색", "#태그 색" | `--tag-color` (글자) / `--tag-background` (배경) |
| "태그 모서리" | `--tag-radius` |
| "코드블록 배경" | `--code-background` |
| "코드블록 글자색", "코드 글자" | `--code-normal` |
| "코드 주석 색" | `--code-comment` |
| "코드 키워드 색" | `--code-keyword` |
| "코드 문자열 색" | `--code-string` |
| "코드 함수 색" | `--code-function` |
| "코드 폰트 크기" | `--code-size` |
| "탭 색", "탭 배경" | `--tab-background-active` |
| "탭 글자색" | `--tab-text-color-focused-active` |
| "탭 모서리" | `--tab-radius` |
| "리본", "왼쪽 아이콘 바" | `--ribbon-background` |
| "타이틀바", "윈도우 상단" | `--titlebar-background` |
| "본문 폰트", "글꼴" | `--font-text-theme` |
| "UI 폰트", "메뉴 폰트" | `--font-interface-theme` |
| "코드 폰트", "모노스페이스" | `--font-monospace-theme` |
| "글자 크기", "본문 크기" | `--font-text-size` |
| "모서리 둥글게", "라운드" | `--radius-s` / `--radius-m` / `--radius-l` / `--radius-xl` |
| "줄간격", "행간" | `--line-height-normal` |

자연어가 모호하면 후보 2~3개 hint 로 제시한 뒤 사용자 선택을 받는다.

## 라이트/다크 분기 패턴

라이트/다크 둘 다 지원하는 테마는 다음 구조로 작성. **`-theme` suffix 폰트 변수명에 주의**:

```css
/* obsidian-theme: managed */

.theme-light {
  --background-primary: #fefefe;
  --text-normal: #2a2a2a;
  --accent-h: 25;
  --accent-s: 60%;
  --accent-l: 50%;
  /* ... */
}

.theme-dark {
  --background-primary: #1a1a1a;
  --text-normal: #e8e8e8;
  --accent-h: 25;
  --accent-s: 70%;
  --accent-l: 60%;
  /* ... */
}

/* 라이트·다크 공통 (폰트·간격·둥글기 등) */
body {
  --font-text-theme: 'Inter', -apple-system, sans-serif;
  --font-interface-theme: -apple-system, BlinkMacSystemFont, sans-serif;
  --font-monospace-theme: 'JetBrains Mono', Menlo, monospace;
  --radius-m: 8px;
  --line-height-normal: 1.6;
}
```

라이트 또는 다크만 지원하면 해당 블록만 작성한다.

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

이 패턴은 유지보수성을 크게 높이고, 옵시디언 코어가 base 토큰을 활용하는 것과 일치한다.
