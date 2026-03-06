# Vibe Dictionary: UI 컴포넌트 분류체계 v0.4

---

## 핵심 원칙

### 프로젝트 목표

**Vibe Dictionary**는 "디자인이 개발의 메타 언어"라는 관점에서, vibe coding 환경에 최적화된 UX/UI 텍소노미 시스템이다.

**목표**: 포화상태 분류체계
- 새로운 UI 패턴이 등장해도 체계 안에서 설명 가능
- 다윈의 종의 기원처럼, 분류 원리가 목록이 아닌 관계를 정의

---

### 분류체계 기준점

**기준으로 삼는 것:**
- Apple Human Interface Guidelines (HIG)
- Google Material Design
- Nielsen Norman Group 리서치
- WCAG / WAI-ARIA 패턴

**기준으로 삼지 않는 것:**
- V0, Lovable, Bolt 등 vibe coding 도구의 출력물
- 이들은 암묵적 LLM 패턴 인식에 의존하며, 표준이 아님

**구조:**
```
[1층] 인터랙션 목적 (원론에서 도출)
[2층] 패턴 원형 (HIG, Material 등에서 정의)
[3층] 플랫폼별 구현 어휘 (vibe coding 도구별 매핑)
```

---

### 디자인 토큰 원칙

**결정사항**: Vibe Dictionary는 **MUI 수준의 체계적인 시멘틱 디자인 토큰 구조**를 기반으로 한다.

**토큰 구조:**

| 토큰 유형 | 패턴 | 예시 |
|----------|------|------|
| 색상 | main / light / dark / contrastText | primary.main, primary.light |
| 상태 | error / warning / success / info | 기본 제공 |
| 타이포그래피 | 명확한 variant 체계 | h1-h6, body1, body2, caption |
| 간격 | 일관된 스케일 | spacing(1) = 8px |
| 반경 | 단계별 정의 | sm, md, lg, xl |

**확장 규칙:**
- 새 토큰 추가 시 기존 패턴 따름
- 예: 새 색상 `brand` 추가 → `brand.main`, `brand.light`, `brand.dark`, `brand.contrastText`

---

### 컴포넌트 vs 스타일 분리 원칙

**결정:**
- 컴포넌트 목록에서 스타일 조합 제거
- 스타일링은 시멘틱 토큰 값 수정 방식으로 처리
- 스타일 프리셋 시스템 (Glass, Brutal, Soft 등)은 **별도 논의**

**올바른 프롬프트 방식:**
```
❌ "GlassCard 만들어줘"
✅ "Card에 glass 스타일 적용해줘"
✅ "Card, surface: transparent, backdrop: blur"
```

---

### 인터랙티브 패턴 원칙

**결정:**
- 인터랙티브 패턴은 **동작(behavior)**을 담당
- 스타일(모양)은 디자인 토큰/CSS가 담당
- hover, click 효과는 기존 컴포넌트 props로 처리

**분리 원칙:**
```
[디자인 토큰/CSS]      → "모양" 담당 (색상, 크기, 간격, 폰트)
[애니메이션 라이브러리] → "동작" 담당 (transform, opacity, timing)
```

---

## 분석 기반

**참조 디자인 시스템:**
- Shadcn/ui (57개 컴포넌트)
- Material Design 3 (30+ 컴포넌트)
- Ant Design (71개 컴포넌트)

**인터랙티브 패턴 참조:**
- Awwwards 수상작 트렌드
- GSAP / Framer Motion 공식 예시
- Codrops 튜토리얼
- Apple, Stripe, Linear 등 프로덕션 사이트

---

## 카테고리 구조

### Part 1: 기본 컴포넌트 (10개)

정적 UI 구성 요소

### Part 2: 인터랙티브 패턴 (5개)

동적 행동과 효과를 정의하는 패턴

### Part 3: 디자인 사조 (8개)

시각적 스타일의 철학과 적용 맥락

### Part 4: 레이아웃, 타이포그래피, 컬러 (5개)

공간 배치와 시각적 표현 체계

---

# Part 1: 기본 컴포넌트

## 1. Typography — 텍스트 표현과 장식

> **정의**: 텍스트의 의미적 표현과 시각적 장식을 위한 패턴

| 컴포넌트 | 설명 | 출처 |
|---------|------|------|
| Heading | 제목 계층 (h1-h6) | 공통 |
| Paragraph | 본문 텍스트 | 공통 |
| Label | 폼/UI 요소 라벨 | 공통 |
| Link | 텍스트 링크 | 공통 |
| Caption | 보조 설명 텍스트 | 공통 |
| Blockquote | 인용문 | Shadcn, Ant |
| Code | 코드 블록/인라인 | Shadcn |
| Kbd | 키보드 단축키 표시 | Shadcn |
| List | 순서/비순서 목록 | 공통 |

---

## 2. Container — 시각적 경계와 그룹핑의 기본 단위

> **정의**: 다른 요소를 담는 시각적 경계의 기본 단위. 독립적 의미 없이 구조적 역할 수행
>
> **Card와의 구분**: Container는 내용물 없이 의미 없음. Card는 독립적 정보 단위

| 컴포넌트 | 설명 | 출처 |
|---------|------|------|
| Box | 기본 래퍼 컨테이너 | 공통 |
| Separator/Divider | 구분선 | Shadcn, MD3, Ant |
| Collapse/Accordion | 접히는 컨테이너 | Shadcn, Ant |
| ScrollArea | 스크롤 가능 영역 | Shadcn |
| AspectRatio | 비율 고정 컨테이너 | Shadcn |
| Space | 간격 조절 컨테이너 | Ant |

---

## 3. Card — 독립적 정보 단위의 표준 패턴

> **정의**: 자기완결적 정보 단위를 그룹핑하는 패턴. 단독으로 의미 전달 가능

#### 기본 컴포넌트
| 컴포넌트 | 설명 | 출처 |
|---------|------|------|
| BaseCard | 기본 카드 구조 | 공통 |
| ElevatedCard | 그림자 강조 카드 | MD3 |
| OutlinedCard | 테두리 강조 카드 | MD3 |
| FilledCard | 배경색 강조 카드 | MD3 |
| MediaCard | 미디어 포함 카드 | 공통 |
| ActionCard | 액션 버튼 포함 카드 | Ant |

#### 구조적 확장
| 컴포넌트 | 설명 | 보편성 |
|---------|------|--------|
| BentoCard | 벤토 그리드용 가변 크기 카드 | Common |
| TallCard | 9:16 세로형 (모바일/소셜 최적화) | Common |
| StackedCard | 레이어드 카드 덱 | Unusual |
| SwipeableCard | 틴더 스타일 스와이프 카드 | Common |
| ExpandingCard | 클릭시 확장되는 카드 | Common |
| FramelessCard | 경계선 없는 콘텐츠 카드 | Unusual |
| SplitCard | 내부 분할 카드 | Common |

---

## 4. Media — 이미지, 비디오, 오디오 표시 및 관리

> **정의**: 미디어 콘텐츠의 표시와 인터랙션 관리

#### 기본 컴포넌트
| 컴포넌트 | 설명 | 출처 |
|---------|------|------|
| Image | 이미지 표시 (lazy load, fallback) | Ant |
| Avatar | 프로필 이미지 | Shadcn, Ant |
| Carousel | 미디어 슬라이더 | Shadcn, MD3, Ant |
| Gallery | 이미지 갤러리/그리드 | - |
| Lightbox | 전체화면 미디어 뷰어 | - |
| QRCode | QR 코드 생성 | Ant |

#### 확장
| 컴포넌트 | 설명 | 보편성 |
|---------|------|--------|
| VideoBackground | 섹션 배경 비디오 | Common |
| 3DObjectEmbed | 3D 모델 임베드 | Unusual |

---

## 5. Data Display — 구조화된 데이터의 시각화

> **정의**: 반복적/비교적 데이터를 보여주는 패턴

| 컴포넌트 | 설명 | 출처 |
|---------|------|------|
| Table | 데이터 테이블 | Shadcn, Ant |
| DataTable | 정렬/필터/페이지네이션 테이블 | Shadcn |
| List | 데이터 목록 | MD3, Ant |
| Tree | 트리 구조 | Ant |
| Timeline | 시간순 이벤트 | Ant |
| Statistic | 통계 수치 표시 | Ant |
| Descriptions | 키-값 설명 목록 | Ant |
| Badge | 상태/수량 표시 | Shadcn, MD3, Ant |
| Tag | 라벨/카테고리 표시 | Ant |
| Progress | 진행률 표시 | Shadcn, MD3, Ant |
| Calendar | 캘린더/날짜 표시 | Ant |
| Empty | 빈 상태 표시 | Shadcn, Ant |
| Skeleton | 로딩 스켈레톤 | Shadcn, Ant |

---

## 6. In-page Navigation — 페이지 내 콘텐츠 탐색

> **정의**: 같은 페이지 내 다른 콘텐츠를 연결하는 패턴
>
> **Global Navigation과의 구분**: 페이지/라우트 전환 없이 동일 페이지 내 이동

| 컴포넌트 | 설명 | 출처 |
|---------|------|------|
| Tabs | 탭 전환 | Shadcn, MD3, Ant |
| Anchor | 목차/앵커 링크 | Ant |
| Steps | 단계 표시 | Ant |
| Pagination | 페이지네이션 | Shadcn, Ant |
| Breadcrumb | 경로 표시 | Shadcn, Ant |
| SegmentedControl | 세그먼트 선택 | MD3 |

---

## 7. Input & Control — 사용자 입력 수집 및 조작

> **정의**: 사용자로부터 값을 받는 패턴

| 컴포넌트 | 설명 | 출처 |
|---------|------|------|
| Button | 기본 버튼 | 공통 |
| IconButton | 아이콘 버튼 | MD3 |
| FAB | 플로팅 액션 버튼 | MD3, Ant |
| Input | 텍스트 입력 | 공통 |
| Textarea | 멀티라인 입력 | 공통 |
| Select | 드롭다운 선택 | 공통 |
| Combobox | 검색 가능 선택 | Shadcn |
| Checkbox | 체크박스 | 공통 |
| Radio | 라디오 버튼 | 공통 |
| Switch | 토글 스위치 | 공통 |
| Slider | 슬라이더 | 공통 |
| DatePicker | 날짜 선택 | Shadcn, MD3, Ant |
| TimePicker | 시간 선택 | MD3, Ant |
| ColorPicker | 색상 선택 | Ant |
| Upload | 파일 업로드 | Ant |
| InputOTP | OTP 입력 | Shadcn |
| InputNumber | 숫자 입력 | Ant |
| Rate | 별점 입력 | Ant |
| Transfer | 항목 이동 선택 | Ant |
| Cascader | 계층 선택 | Ant |
| Mentions | @멘션 입력 | Ant |
| AutoComplete | 자동완성 | Ant |
| Form | 폼 래퍼/검증 | Shadcn, Ant |
| Chip | 선택/필터/입력 칩 | MD3 |

---

## 8. Layout — 공간 배치와 구조

> **정의**: 다른 요소들의 위치를 결정하는 패턴

#### 기본 컴포넌트
| 컴포넌트 | 설명 | 출처 |
|---------|------|------|
| Grid | 그리드 시스템 | Ant |
| Flex | 플렉스 컨테이너 | Ant |
| Layout | 페이지 레이아웃 (Header, Sider, Content, Footer) | Ant |
| Resizable | 리사이즈 가능 패널 | Shadcn |
| Splitter | 분할 패널 | Ant |
| Masonry | 메이슨리 레이아웃 | Ant (v6) |
| Affix | 고정 위치 | Ant |

#### 창의적 확장
| 컴포넌트 | 설명 | 보편성 |
|---------|------|--------|
| BentoGrid | 벤토 박스 레이아웃 (Apple 스타일) | Common |
| BrokenGrid | 의도적 비대칭 그리드 | Unusual |
| OffsetLayout | 불균등 컬럼 (2fr 1fr) | Common |
| OverlappingStack | Z-index 레이어드 배치 | Common |
| DiagonalGrid | 대각선 배치 | Unusual |
| CollageLayout | 이미지/텍스트 콜라주 | Unusual |
| SplitScreen | 불균등 분할 히어로 (70/30, 60/40) | Common |
| FullBleed | 전체 너비 섹션 | Common |

---

## 9. Overlay & Feedback — 맥락적 정보 표시와 상태 피드백

> **정의**: 콘텐츠 위에 나타나 상태를 전달하거나 입력을 요청하는 패턴

| 컴포넌트 | 설명 | 출처 |
|---------|------|------|
| Modal/Dialog | 모달 다이얼로그 | 공통 |
| AlertDialog | 확인 다이얼로그 | Shadcn |
| Drawer | 드로어 패널 | Shadcn, MD3, Ant |
| Sheet | 시트 (Bottom/Side) | Shadcn, MD3 |
| Popover | 팝오버 | Shadcn, Ant |
| Tooltip | 툴팁 | 공통 |
| HoverCard | 호버 카드 | Shadcn |
| Toast | 토스트 알림 | Shadcn |
| Snackbar | 스낵바 | MD3 |
| Alert | 인라인 알림 | Shadcn, Ant |
| Message | 전역 메시지 | Ant |
| Notification | 알림 | Ant |
| Popconfirm | 확인 팝오버 | Ant |
| Spin/Spinner | 로딩 스피너 | Shadcn, Ant |
| Result | 결과 피드백 | Ant |
| Tour | 온보딩 투어 | Ant |
| Watermark | 워터마크 | Ant |

---

## 10. Navigation (Global) — 페이지/앱 간 이동

> **정의**: 페이지 또는 라우트 간 이동을 위한 패턴

| 컴포넌트 | 설명 | 출처 |
|---------|------|------|
| NavigationMenu | 메인 네비게이션 | Shadcn |
| Menubar | 메뉴바 | Shadcn |
| Sidebar | 사이드바 | Shadcn |
| Menu | 메뉴 (horizontal, vertical, inline) | Ant |
| NavigationBar | 하단 네비게이션 바 | MD3 |
| NavigationRail | 사이드 레일 | MD3 |
| NavigationDrawer | 네비게이션 드로어 | MD3 |
| TopAppBar | 상단 앱바 | MD3 |
| BottomAppBar | 하단 앱바 | MD3 |
| DropdownMenu | 드롭다운 메뉴 | Shadcn, Ant |
| ContextMenu | 컨텍스트 메뉴 | Shadcn |
| Command | ⌘K 커맨드 팔레트 | Shadcn |

---

# Part 2: 인터랙티브 패턴

## 11. KineticTypography — 텍스트 자체 효과

> **정의**: 텍스트 자체에 동적 효과를 부여하는 패턴. 다른 시각 요소에 의존하지 않고 타이포그래피 단독으로 작동

| 컴포넌트 | 설명 | 의존성 | 사용 빈도 |
|---------|------|--------|----------|
| CharacterStagger | 문자/단어/줄 단위 순차 애니메이션 | GSAP SplitText / Framer Motion | 높음 |
| TextScramble | 무작위 문자 → 최종 텍스트 디코딩 효과 | GSAP ScrambleTextPlugin | 높음 |
| Typewriter | 한 글자씩 타이핑 + 블링킹 커서 | CSS / GSAP | 높음 |
| BlurInReveal | 흐릿함 → 선명 포커스 등장 | Framer Motion / GSAP | 높음 |
| LettersPullUp | 마스크 통과 수직 등장 | GSAP SplitText | 높음 |
| GlitchText | RGB 분리, 디지털 간섭 효과 | 순수 CSS | 중간 |
| FlipWords | 단어 회전/순환 애니메이션 | Framer Motion / GSAP | 높음 |
| AnimatedGradientText | 텍스트 그라디언트 색상 순환 | 순수 CSS | 중간 |

---

## 12. Scroll — 스크롤 위치 기반 요소 효과

> **정의**: 스크롤 위치에 따라 개별 요소에 효과를 적용하는 패턴

| 컴포넌트 | 설명 | 의존성 | 사용 빈도 |
|---------|------|--------|----------|
| Parallax | 배경/전경 다중 속도 이동으로 깊이감 | GSAP ScrollTrigger | 높음 |
| ScrollReveal | 뷰포트 진입 시 페이드/슬라이드 등장 | GSAP ScrollTrigger / IO API | 높음 |
| ScrollScrubbing | 애니메이션 진행 = 스크롤 위치 연동 | GSAP ScrollTrigger scrub | 높음 |
| ImageSequence | 스크롤에 따른 이미지 프레임 재생 | GSAP + Canvas | 중간 |
| SmoothScroll | 관성 기반 부드러운 스크롤 | Lenis | 높음 |
| ScrollProgress | 페이지 읽기 진행률 표시 | CSS / GSAP | 중간 |
| ScrollSnap | 섹션 경계 자동 정렬 | 순수 CSS | 중간 |
| Scroll3DEffect | 스크롤 연동 3D 회전/이동 | GSAP + CSS 3D | 중간 |

---

## 13. ContentTransition — 섹션 간 맥락 연결

> **정의**: 섹션 간 전후 맥락을 연결하고 콘텐츠 흐름의 연속성을 만드는 패턴

| 컴포넌트 | 설명 | 의존성 | 사용 빈도 |
|---------|------|--------|----------|
| StickyStacking | 카드가 덱처럼 쌓이는 효과 | CSS sticky + GSAP | 높음 |
| HorizontalScroll | 세로 스크롤 → 가로 이동 변환 | GSAP ScrollTrigger pin | 높음 |
| PinnedContentSwap | 섹션 고정 + 내부 콘텐츠만 전환 | GSAP ScrollTrigger | 높음 |
| SectionWipe | clip-path로 섹션 드러내기 | GSAP + clip-path | 중간 |
| ViewTransition | 브라우저 네이티브 페이지/상태 전환 | View Transitions API | 중간 |
| ZoomTransition | 스크롤 연동 확대/축소 전환 | GSAP ScrollTrigger | 중간 |
| BlockRevealWipe | 단색 블록 슬라이드 후 콘텐츠 노출 | CSS / GSAP | 중간 |

---

## 14. Motion — 스토리텔링/연출 목적 모션

> **정의**: 스토리텔링/연출 목적으로 레이아웃이나 콘텐츠의 상태 변화를 시각화하는 패턴
>
> **hover, click 효과와의 구분**: 단순 피드백은 컴포넌트 props, 연출 목적 모션은 여기

| 컴포넌트 | 설명 | 의존성 | 사용 빈도 |
|---------|------|--------|----------|
| FadeTransition | 기본 opacity 전환 (등장/퇴장/교차) | CSS / Framer Motion | 높음 |
| LayoutAnimation | 동일 요소의 위치/크기 변화 부드러운 전환 (토글, 아코디언) | Framer Motion layout | 높음 |
| StaggeredReveal | 요소들 시간차 순차 애니메이션 | Framer Motion / GSAP | 높음 |
| AnimatePresence | 퇴장 애니메이션 (DOM 제거 전) | Framer Motion | 높음 |
| SharedLayoutAnimation | 서로 다른 요소 간 모핑 전환 (카드→모달, 탭 인디케이터) | Framer Motion layoutId | 높음 |
| FLIPGridAnimation | 필터/정렬 시 그리드 아이템 위치 이동 | GSAP Flip / Framer Motion | 높음 |
| SpringPhysics | 스프링 물리 기반 바운스/오버슈트 | Framer Motion / GSAP | 높음 |
| Marquee | 무한 루프 수평 흐름 (텍스트/이미지/카드). scroll 옵션으로 스크롤 연동 가능 | CSS / GSAP | 높음 |
| SVGMorphing | SVG 경로 간 형태 변환 | GSAP MorphSVG / Flubber | 중간 |
| LottieAnimation | After Effects 기반 벡터 애니메이션 | lottie-web | 중간 |

---

## 15. DynamicColor — 동적 색상 변화

> **정의**: 동적으로 색상 변화를 다루는 패턴

| 컴포넌트 | 설명 | 의존성 | 사용 빈도 |
|---------|------|--------|----------|
| AuroraBackground | 블러 처리된 컬러 블롭 흐름 | 순수 CSS | 높음 |
| CursorReactiveGradient | 커서 위치 반응 그라디언트/글로우 | JS + CSS 변수 | 높음 |
| AnimatedTextGradient | 텍스트 그라디언트 색상 순환 | 순수 CSS | 높음 |
| GrainyGradient | 노이즈 텍스처 오버레이 그라디언트 | SVG 필터 + CSS | 중간 |
| DarkModeTransition | 테마 전환 시 확장/와이프 애니메이션 | View Transitions API | 중간 |
| Spotlight | 특정 영역 집중 조명 효과 | CSS radial-gradient | 중간 |
| MeshGradient | WebGL 기반 유기적 다중 색상 흐름 | Three.js / Gradient.js | 중간 |
| AmbientBackground | 파티클/블롭 미묘한 지속 움직임 | CSS / Canvas | 중간 |

---

## 스타일 프리셋 (별도 논의)

> **현재 상태**: 미정의. 별도 논의 필요.

스타일 프리셋은 컴포넌트와 조합되는 시각적 스타일 세트:

- Glass (글래스모피즘)
- Brutal (네오브루탈리즘)
- Soft (뉴모피즘)
- Clay (클레이모피즘)
- Retro (90년대 스타일)

---

## 분류 근거 및 결정 사항

### 경계 판정이 필요했던 케이스

| 컴포넌트 | 후보 카테고리 | 최종 결정 | 근거 |
|---------|-------------|----------|------|
| Chip/Tag | Input & Control vs Data Display | **Input & Control** | 사용자 선택 액션이 주목적 |
| Accordion | Container vs In-page Navigation | **Container** | 그룹핑이 주목적, 탐색은 부수 기능 |
| Steps | In-page Navigation vs Data Display | **In-page Navigation** | 프로세스 안내/이동이 주목적 |
| Empty | Data Display vs Feedback | **Data Display** | 데이터 상태 표시가 주목적 |
| Command | Navigation vs Input & Control | **Navigation (Global)** | 페이지/액션 이동이 주목적 |
| Carousel | Media vs In-page Navigation | **Media** | 미디어 표시가 주목적 |
| ScrollReveal | Scroll vs Motion | **Scroll** | 스크롤 위치가 트리거 |
| StaggeredReveal | Motion vs Scroll | **Motion** | 연출 목적, 트리거 다양 |

### 제외된 컴포넌트

| 컴포넌트 | 제외 이유 |
|---------|----------|
| ConfigProvider | 시스템 설정용, UI 패턴 아님 |
| App | 앱 래퍼, UI 패턴 아님 |
| Portal | 기술적 유틸리티 |
| Theme | 디자인 토큰, 별도 영역 |

---

## 텍소노미 운영 시나리오

### 확장 (Extension) 예시

**시나리오**: AI 챗봇 UI가 보편화되면서 ChatBubble 컴포넌트 추가 요청

```
[EXTEND] Overlay & Feedback
  + ChatBubble
    - 설명: AI/사용자 대화 메시지 버블
    - 변형: UserBubble, AssistantBubble, SystemBubble
    - 보편성: Common → Canonical (예상)
    - 근거: ChatGPT, Claude, Gemini 등 대화형 AI 인터페이스 표준화
```

### 합성 (Composition) 예시

**시나리오**: PricingCard가 반복 사용되어 독립 패턴으로 등재 요청

```
[COMPOSE] PricingCard = Card.Base + Typography.Heading + Data.Statistic + Input.Radio + Input.Button
  - 구성: 플랜명 + 가격 + 기능 목록 + 선택 + CTA
  - 용도: SaaS 가격 페이지
  - 보편성: Common
  - 카테고리: Card (합성 카드)
```

### 수정 (Revision) 예시

**시나리오**: Accordion이 Container와 In-page Navigation 양쪽에서 혼동 발생

```
[REVISE] Accordion
  - Before: Container 카테고리 단독 배치
  - After: Container 기본 + In-page Navigation 변형 추가
  - 근거: 사용 맥락에 따라 주목적이 다름
  - 영향: Minor (하위 변형 추가)
```

### 도태 (Deprecation) 예시

**시나리오**: BottomAppBar가 MD3 Expressive에서 제거됨

```
[DEPRECATE] Navigation.BottomAppBar
  - 이유: MD3 Expressive에서 FloatingToolbar로 대체
  - 대안: Navigation.FloatingToolbar 또는 Navigation.NavigationBar
  - 유예 기간: 2025-06 ~ 2025-12
  - 상태: Deprecated → Archive
```

---

## 컴포넌트 수 요약

### Part 1: 기본 컴포넌트

| 카테고리 | 기본 | 확장 | 합계 |
|---------|------|------|------|
| Typography | 9 | 0 | 9 |
| Container | 6 | 0 | 6 |
| Card | 6 | 7 | 13 |
| Media | 6 | 2 | 8 |
| Data Display | 13 | 0 | 13 |
| In-page Navigation | 6 | 0 | 6 |
| Input & Control | 26 | 0 | 26 |
| Layout | 7 | 8 | 15 |
| Overlay & Feedback | 17 | 0 | 17 |
| Navigation (Global) | 12 | 0 | 12 |
| **소계** | **108** | **17** | **125** |

### Part 2: 인터랙티브 패턴

| 카테고리 | 컴포넌트 수 |
|---------|------------|
| KineticTypography | 8 |
| Scroll | 8 |
| ContentTransition | 7 |
| Motion | 10 |
| DynamicColor | 8 |
| **소계** | **41** |

### Part 3: 디자인 사조

| 카테고리 | 항목 수 |
|---------|--------|
| 디자인 사조 | 8 |
| **소계** | **8** |

### Part 4: 레이아웃, 타이포그래피, 컬러

| 카테고리 | 항목 수 |
|---------|--------|
| 그리드 시스템 | 5 |
| 페이지 레이아웃 패턴 | 7 |
| 타이포그래피 트렌드 | 5 |
| 컬러 전략 | 4 (하모니) + 6 (시맨틱) |
| 조합 레시피 | 6 |
| **소계** | **33** |

### 총계: 207개

---

## 횡단 속성 (모든 컴포넌트에 적용)

**Axis 1: 보편성 (Prevalence)**
- Canonical: HIG/Material 표준
- Common: 널리 사용
- Unusual: 특수/스타일 목적
- Experimental: 미검증 신규

**Axis 2: 상호작용성 (Interactivity)**
- Static: 상태 변화 없음
- Reactive: 데이터 바인딩
- Interactive: 사용자 액션 반응
- Animated: 자동 상태 변화

**Axis 3: 밀도 (Density)**
- Minimal / Compact / Default / Expanded

---

## 인터랙티브 패턴 의존성 가이드

### 핵심 라이브러리 스택

```
[Core - 필수]
├── Framer Motion (React) — Layout, Presence, Spring
├── GSAP + ScrollTrigger — Scroll, Timeline, Text
└── Lenis — Smooth Scroll

[Optional - 필요시]
├── lottie-web — 복잡한 벡터 애니메이션
├── Three.js — WebGL 메시 그라디언트
└── Motion One — Vue/Svelte 대응
```

### 라이브러리별 역할

| 라이브러리 | 주요 역할 | 스타일 영향 | 프레임워크 |
|------------|----------|-------------|------------|
| **Framer Motion** | 레이아웃 전환, 상태 애니메이션, 스프링 물리 | 낮음 | React 전용 |
| **GSAP** | 타임라인, 스크롤 트리거, 텍스트 분리 | 중간 (인라인 스타일) | 무관 |
| **Lenis** | 스무스 스크롤 | 거의 없음 | 무관 |
| **lottie-web** | 벡터 애니메이션 재생 | 없음 | 무관 |
| **Three.js** | WebGL 그라디언트, 3D | 없음 (Canvas) | 무관 |

### 카테고리별 의존성 맵

| 카테고리 | 필수 | 선택 |
|---------|------|------|
| KineticTypography | GSAP (SplitText) | Framer Motion |
| Scroll | GSAP (ScrollTrigger), Lenis | - |
| ContentTransition | GSAP (ScrollTrigger) | View Transitions API |
| Motion | Framer Motion | GSAP (Flip), lottie-web |
| DynamicColor | 순수 CSS/JS | Three.js (MeshGradient) |

### 스타일 분리 원칙

**GSAP 사용 시:**
```js
// ✓ 권장: transform, opacity만 조작
gsap.to(element, { 
  x: 100,
  opacity: 0.5,
  scale: 1.1
});

// ❌ 피하기: 색상, 배경 직접 조작
gsap.to(element, { 
  backgroundColor: "#ff0000"  // 토큰 시스템 우회
});

// ✓ 색상 변경이 필요하면 클래스 토글
gsap.to(element, {
  onComplete: () => element.classList.add("active")
});
```

**Framer Motion 사용 시:**
```tsx
// ✓ 권장: className으로 스타일, animate는 동작만
<motion.div
  className="card bg-primary"  // 스타일은 CSS
  animate={{ x: 100, opacity: 1 }}  // 동작만
  layout  // 레이아웃 전환
/>

// ❌ 피하기: animate에서 색상 지정
<motion.div
  animate={{ backgroundColor: "#ff0000" }}
/>
```

### 프레임워크별 대응

| 프레임워크 | Framer Motion 대체 | 비고 |
|-----------|-------------------|------|
| React | Framer Motion | 기본 |
| Vue | @vueuse/motion, Motion One | |
| Svelte | svelte/motion, Motion One | |
| Vanilla | Motion One, GSAP | |

### 순수 CSS로 해결 가능한 패턴

라이브러리 없이 CSS만으로 구현 가능:

| 패턴 | CSS 구현 방식 |
|------|--------------|
| GlitchText | ::before/::after + clip 애니메이션 |
| ScrollSnap | scroll-snap-type |
| AuroraBackground | filter: blur + keyframes |
| AnimatedTextGradient | background-clip: text + keyframes |
| GrainyGradient | SVG feTurbulence |
| Spotlight | radial-gradient + CSS 변수 |
| Marquee | translateX 무한 애니메이션 |

### 브라우저 네이티브 API

외부 라이브러리 대신 사용 가능:

| API | 용도 | 지원 현황 |
|-----|------|----------|
| View Transitions API | 페이지/상태 전환 | Chrome 111+, Safari 18+ |
| CSS scroll-timeline | 스크롤 연동 애니메이션 | Chrome 115+ |
| Intersection Observer | 뷰포트 진입 감지 | 모든 브라우저 |

---

# Part 3: 디자인 사조

> **정의**: 시각적 스타일의 철학과 적용 맥락. "언제 쓸까?" 관점에서 정리.

| 사조 | 핵심 느낌 | 언제 쓰면 좋은가 | 피해야 할 상황 |
|-----|----------|-----------------|---------------|
| Flat Design | 깔끔, 빠름, 명확 | 대시보드, SaaS, 복잡한 정보 UI | 프리미엄/럭셔리 브랜딩 |
| Material Design | 체계적, 일관적, 구글 느낌 | Android 앱, B2B 엔터프라이즈, 디자인 시스템 필요할 때 | Apple 생태계, 독특한 브랜드 정체성 필요 시 |
| HIG (Apple Style) | 프리미엄, 세련, blur 레이어 | iOS/macOS 앱, 프리미엄 제품, 미니멀 럭셔리 | 저사양 기기 타겟, 복잡한 데이터 UI |
| Glassmorphism | 깊이감, 우아함, 모던 | 모달/카드 오버레이, 다크모드 UI, 로그인 폼, 히어로 섹션 | 텍스트 집약 UI, 단순 배경, 저사양 기기 |
| Neumorphism | 소프트, 촉각적, 미래적 | 뮤직 플레이어, 스마트홈 컨트롤, 토글/슬라이더 | 텍스트 많은 UI, 접근성 중요 시 (낮은 대비) |
| Claymorphism | 친근, 따뜻, 유기적 | 어린이 앱, 핀테크 카드, 친근한 B2C | 엔터프라이즈, 진지한 톤 |
| Neubrutalism | 대담, 반항, Gen-Z | 크리에이티브 에이전시, 인디 제품, 포트폴리오, 스타트업 랜딩 | 금융, 헬스케어, 엔터프라이즈 |
| Swiss/Editorial | 명료, 콘텐츠 중심, 시간을 초월 | 블로그, 뉴스, 케이스 스터디, 문서 기반 사이트 | 인터랙티브 중심, 시각적 임팩트 필요 시 |

---

# Part 4: 레이아웃, 타이포그래피, 컬러

## 16. 그리드 시스템

> **정의**: 콘텐츠 배치의 구조적 프레임워크

| 패턴 | 설명 | 언제 쓰면 좋은가 | 예시 |
|-----|------|-----------------|------|
| Bento Grid | 다양한 크기의 박스가 퍼즐처럼 맞춤, Apple 스타일 | 제품 피처 소개, SaaS 랜딩, 포트폴리오, 대시보드 | Apple, Notion, Framer, Supabase |
| Card Grid (균등) | 동일 크기 카드 반복 | 이커머스 제품 목록, 갤러리, 피드 | Dribbble, 쇼핑몰 상품 |
| Masonry | 핀터레스트 스타일, 높이 가변 | 이미지 갤러리, UGC 피드, 포트폴리오 | Pinterest, Unsplash |
| 12-Column | 반응형 표준, Flexbox/Grid | 대부분의 반응형 웹사이트 | Bootstrap, Tailwind 기반 사이트 |
| Broken Grid | 의도적 비대칭, 요소 오버랩 | 크리에이티브 에이전시, 아트/패션, 차별화 필요 시 | 디자인 스튜디오, 아티스트 포트폴리오 |

### Bento Grid 상세

**효과적인 상황:**
- 제품 피처를 한눈에 보여줘야 할 때 (Apple 스타일)
- 다양한 콘텐츠 타입(텍스트, 이미지, 비디오, 통계)을 섞을 때
- "스캔 가능한" 정보 제공이 필요할 때
- 모바일에서 자연스럽게 스택되어야 할 때

**피해야 할 상황:**
- 복잡한 이커머스 (상품이 너무 많으면 혼란)
- 긴 텍스트 콘텐츠 (읽기 흐름 방해)
- 명확한 순서/단계가 필요한 UI

**토큰 특성:**
- gap: 16-24px (일관된 거터)
- border-radius: 12-24px (둥근 모서리)
- aspect-ratio: 자유롭되 기본 단위 기반
- background: 카드별 차별화 가능

---

## 17. 페이지 레이아웃 패턴

> **정의**: 페이지 전체 구조와 시선 흐름을 결정하는 패턴

| 패턴 | 설명 | 언제 쓰면 좋은가 |
|-----|------|-----------------|
| Hero + 스크롤 | 큰 히어로 → 아래로 콘텐츠 | 랜딩페이지, 제품 소개, 마케팅 사이트 |
| Split Screen (50/50) | 화면 양분, 이미지+텍스트 | 패션, 비교, 두 가지 선택지 제시 |
| Asymmetric Split (60/40, 70/30) | 불균등 분할, 시선 유도 | 중요 콘텐츠 강조, 동적인 느낌 |
| Z-Pattern | Z자 시선 흐름 | 이미지 중심 랜딩, 간결한 페이지 |
| F-Pattern | F자 시선 흐름 | 텍스트 중심 페이지, 블로그, 문서 |
| Full-Bleed | 여백 없이 가장자리까지 | 몰입감, 이미지/영상 강조 |
| Single Column | 단일 컬럼, 집중된 읽기 | 아티클, 블로그 포스트, 랜딩 |

---

## 18. 타이포그래피

> **정의**: 텍스트의 시각적 표현 체계

### 2024-2025 타이포그래피 트렌드

| 트렌드 | 설명 | 언제 쓰면 좋은가 |
|-------|------|-----------------|
| Oversized Display | 48-120px+ 대형 헤드라인 | 히어로 섹션, 브랜드 스테이트먼트, 임팩트 필요 시 |
| Variable Fonts | 단일 파일로 weight/width 조절 | 성능 중요, 반응형, 동적 UI |
| High-Contrast Serif | 굵기 대비 강한 세리프 | 에디토리얼, 럭셔리, 패션 |
| Neo-Grotesque Sans | Inter, Satoshi 등 현대적 산세리프 | SaaS, 테크, 범용 UI |
| Kinetic Typography | 움직이는 텍스트 | 히어로, 인터랙티브, 브랜딩 모먼트 |

### 실전 타입 스케일 (웹 기준)

| 요소 | 크기 | 용도 |
|-----|------|------|
| Display | 48-72px | 히어로 헤드라인 |
| H1 | 32-48px | 페이지 제목 |
| H2 | 24-32px | 섹션 제목 |
| H3 | 20-24px | 서브섹션 |
| Body | 16-18px | 본문 (16px 최소) |
| Small/Caption | 12-14px | 캡션, 라벨 |

### 폰트 페어링 레시피 (2025 버전)

| 용도 | 헤드라인 | 본문 | 느낌 |
|-----|---------|------|------|
| 테크/SaaS | Inter Bold | Inter Regular | 깔끔, 현대적 |
| 프리미엄 | Playfair Display | Source Serif | 우아, 고급 |
| 스타트업 | Satoshi Bold | Satoshi Regular | 신선, 친근 |
| 에디토리얼 | Fraunces | Lora | 개성 있는 읽기 |
| Neubrutalism | Space Grotesk | Space Mono | 대담, 테크 |

### 가독성 체크리스트

- [ ] 본문 최소 16px
- [ ] 줄 높이 1.5-1.7
- [ ] 줄 길이 45-75자 (max-width: 65ch)
- [ ] 대비 4.5:1 이상 (WCAG AA)
- [ ] 다크모드에서 weight 줄이기 (400→350)

---

## 19. 컬러 전략

> **정의**: UI에서 색상의 역할과 적용 규칙

### 60-30-10 Rule (UI 버전)

| 비율 | 역할 | UI에서의 적용 |
|-----|------|--------------|
| 60% | Dominant | 배경, 빈 공간, surface |
| 30% | Secondary | 카드 배경, 네비게이션, 섹션 구분 |
| 10% | Accent | CTA 버튼, 링크, 알림 뱃지, 포커스 상태 |

### 컬러 하모니 → UI 적용

| 하모니 | UI 적용 | 느낌 |
|-------|--------|------|
| Monochromatic | 미니멀 SaaS, 포트폴리오 | 세련, 집중 |
| Analogous | 자연/웰니스 앱, 친근한 B2C | 조화, 편안 |
| Complementary | CTA 강조, 게임화 | 에너지, 대비 |
| Split-Complementary | 대부분의 웹사이트 | 균형 잡힌 대비 |

### 시맨틱 컬러 (표준)

| 상태 | 컬러 | 용도 |
|-----|------|------|
| Primary | 브랜드 컬러 | CTA, 주요 액션 |
| Success | Green | 완료, 확인, 긍정 |
| Error | Red | 에러, 삭제, 위험 |
| Warning | Yellow/Orange | 주의, 경고 |
| Info | Blue | 정보, 힌트 |
| Neutral | Gray | 비활성, 보조 텍스트 |

### 다크모드 변환 규칙

| 라이트 | 다크 | 주의점 |
|-------|------|-------|
| white | gray-900 | 순백이 아닌 약간 따뜻한 톤 |
| gray-100 surface | gray-800 | 레이어별 명도 차이 유지 |
| Primary 600 | Primary 400 | 밝게 조정 |
| Shadow | Glow 또는 Border | 그림자 대신 빛 |

---

## 20. 조합 레시피

> **정의**: 사조 + 레이아웃 + 타이포의 실전 조합

| 프로젝트 유형 | 사조 | 레이아웃 | 타이포 |
|-------------|------|---------|-------|
| SaaS 랜딩 | Flat + Corporate | Bento Grid + Hero | Inter + Oversized Display |
| 크리에이티브 에이전시 | Neubrutalism | Broken Grid | Space Grotesk + Kinetic |
| 이커머스 | Material / Flat | Card Grid + F-Pattern | System UI + Clear Hierarchy |
| 테크 블로그 | Swiss/Editorial | Single Column + F-Pattern | Serif Headline + Sans Body |
| 프리미엄 제품 | HIG + Glassmorphism | Full-Bleed Hero + Bento | SF Pro / Playfair |
| 핀테크 앱 | Material + Neumorphism | Card Grid | Inter + High Contrast |

---

## 다음 단계

1. **스타일 프리셋 시스템 정의**
2. **각 컴포넌트별 프롬프트 키워드 정의**
3. **시멘틱 토큰 상세 스펙 작성**
4. **합성 패턴 레시피 30개 작성**
5. **베타 사용자 테스트**

---

## 변경 이력

| 버전 | 날짜 | 변경 사항 |
|-----|------|----------|
| 0.1 | - | 초안 작성 |
| 0.2 | - | 디자인 토큰 원칙 추가, 분류 기준점 명시, 스타일 조합 컴포넌트 분리 |
| 0.3 | - | 인터랙티브 패턴 5개 카테고리 추가 (KineticTypography, Scroll, ContentTransition, Motion, DynamicColor), 의존성 가이드 추가 |
| 0.4 | - | Part 3 디자인 사조 추가 (8개 사조), Part 4 레이아웃/타이포그래피/컬러 추가 (그리드 시스템, 페이지 레이아웃, 타입 스케일, 컬러 전략, 조합 레시피). Marquee를 KineticTypography→Motion으로 이동 (scroll 옵션 명시), FadeTransition 추가 |