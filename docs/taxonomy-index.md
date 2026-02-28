# Vibe Dictionary Index v0.4

> 전체 분류체계 빠른 참조용 인덱스

---

## 구조 요약

| Part | 이름 | 카테고리 수 | 항목 수 |
|------|-----|------------|--------|
| 1 | 기본 컴포넌트 | 10 | 125 |
| 2 | 인터랙티브 패턴 | 5 | 41 |
| 3 | 디자인 사조 | 1 | 8 |
| 4 | 레이아웃, 타이포, 컬러 | 5 | 33 |
| **총계** | | **21** | **207** |

---

## Part 1: 기본 컴포넌트

| # | 카테고리 | 항목 수 | 핵심 컴포넌트 |
|---|---------|--------|--------------|
| 1 | Typography | 9 | Heading, Paragraph, Label, Link, Caption, Blockquote, Code, Kbd, List |
| 2 | Container | 6 | Box, Separator, Collapse, ScrollArea, AspectRatio, Space |
| 3 | Card | 13 | BaseCard, ElevatedCard, OutlinedCard, MediaCard, BentoCard, SwipeableCard, ExpandingCard |
| 4 | Media | 8 | Image, Avatar, Carousel, Gallery, Lightbox, QRCode, VideoBackground, 3DObjectEmbed |
| 5 | Data Display | 13 | Table, DataTable, List, Tree, Timeline, Statistic, Badge, Tag, Progress, Calendar, Empty, Skeleton |
| 6 | In-page Navigation | 6 | Tabs, Anchor, Steps, Pagination, Breadcrumb, SegmentedControl |
| 7 | Input & Control | 26 | Button, Input, Select, Checkbox, Radio, Switch, Slider, DatePicker, Upload, Form, Chip |
| 8 | Layout | 15 | Grid, Flex, Layout, Resizable, Splitter, Masonry, BentoGrid, BrokenGrid, SplitScreen |
| 9 | Overlay & Feedback | 17 | Modal, Drawer, Sheet, Popover, Tooltip, Toast, Snackbar, Alert, Notification, Tour |
| 10 | Navigation (Global) | 12 | NavigationMenu, Menubar, Sidebar, BottomNavigation, AppBar, CommandPalette, Dock |

---

## Part 2: 인터랙티브 패턴

| # | 카테고리 | 항목 수 | 핵심 패턴 |
|---|---------|--------|----------|
| 11 | KineticTypography | 8 | CharacterStagger, TextScramble, Typewriter, BlurInReveal, LettersPullUp, GlitchText, FlipWords, AnimatedGradientText |
| 12 | Scroll | 8 | Parallax, ScrollReveal, ScrollScrubbing, ImageSequence, SmoothScroll, ScrollProgress, ScrollSnap, Scroll3DEffect |
| 13 | ContentTransition | 7 | StickyStacking, HorizontalScroll, PinnedContentSwap, SectionWipe, ViewTransition, ZoomTransition, BlockRevealWipe |
| 14 | Motion | 10 | FadeTransition, LayoutAnimation, StaggeredReveal, AnimatePresence, SharedLayoutAnimation, Marquee (scroll 옵션), SpringPhysics |
| 15 | DynamicColor | 8 | AuroraBackground, CursorReactiveGradient, AnimatedTextGradient, GrainyGradient, DarkModeTransition, Spotlight, MeshGradient, AmbientBackground |

---

## Part 3: 디자인 사조

| # | 사조 | 핵심 느낌 | 적합 |
|---|-----|----------|------|
| - | Flat Design | 깔끔, 빠름, 명확 | 대시보드, SaaS |
| - | Material Design | 체계적, 일관적 | Android, B2B |
| - | HIG (Apple Style) | 프리미엄, 세련 | iOS/macOS, 럭셔리 |
| - | Glassmorphism | 깊이감, 우아함 | 모달, 다크모드 |
| - | Neumorphism | 소프트, 촉각적 | 뮤직 플레이어, 스마트홈 |
| - | Claymorphism | 친근, 따뜻 | 어린이 앱, B2C |
| - | Neubrutalism | 대담, 반항 | 크리에이티브, 인디 |
| - | Swiss/Editorial | 명료, 콘텐츠 중심 | 블로그, 뉴스 |

---

## Part 4: 레이아웃, 타이포그래피, 컬러

| # | 카테고리 | 항목 수 | 핵심 항목 |
|---|---------|--------|----------|
| 16 | 그리드 시스템 | 5 | Bento Grid, Card Grid, Masonry, 12-Column, Broken Grid |
| 17 | 페이지 레이아웃 | 7 | Hero+스크롤, Split Screen, Z-Pattern, F-Pattern, Full-Bleed, Single Column |
| 18 | 타이포그래피 | 5 트렌드 + 6 스케일 + 5 페어링 | Oversized Display, Variable Fonts, Inter, Playfair, Space Grotesk |
| 19 | 컬러 전략 | 4 하모니 + 6 시맨틱 | 60-30-10 Rule, Monochromatic, Complementary, Primary/Success/Error |
| 20 | 조합 레시피 | 6 | SaaS 랜딩, 크리에이티브 에이전시, 이커머스, 테크 블로그, 프리미엄 제품, 핀테크 |

---

## 의존성 스택

```
[Core]
├── Framer Motion — Layout, Presence, Spring
├── GSAP + ScrollTrigger — Scroll, Timeline, Text
└── Lenis — Smooth Scroll

[Optional]
├── lottie-web — 벡터 애니메이션
├── Three.js — WebGL 메시 그라디언트
└── Motion One — Vue/Svelte 대응
```

---

## 횡단 속성

| 축 | 값 |
|---|---|
| 보편성 | Canonical → Common → Unusual → Experimental |
| 상호작용성 | Static → Reactive → Interactive → Animated |
| 밀도 | Minimal → Compact → Default → Expanded |

---

## 빠른 링크

- [Part 1: 기본 컴포넌트](#part-1-기본-컴포넌트)
- [Part 2: 인터랙티브 패턴](#part-2-인터랙티브-패턴)
- [Part 3: 디자인 사조](#part-3-디자인-사조)
- [Part 4: 레이아웃, 타이포, 컬러](#part-4-레이아웃-타이포그래피-컬러)
