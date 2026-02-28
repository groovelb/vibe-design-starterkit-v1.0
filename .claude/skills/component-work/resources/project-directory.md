# Project Directory Rules

새로운 컴포넌트를 추가할 때는 아래 디렉토리 구조를 따른다.

## 디렉토리 구조

```
src/
  components/
    typography/                 # #1 텍스트 표현과 장식
                                #    Heading, Paragraph, Label, Link, Caption, Blockquote, Code, Kbd, List
    container/                  # #2 시각적 경계와 그룹핑
                                #    Box, Separator, Collapse, ScrollArea, AspectRatio, Space
    card/                       # #3 독립적 정보 단위
                                #    BaseCard, ElevatedCard, OutlinedCard, MediaCard, BentoCard, SwipeableCard, ExpandingCard
    media/                      # #4 이미지, 비디오 표시
                                #    Image, Avatar, Carousel, Gallery, Lightbox, QRCode, VideoBackground, 3DObjectEmbed
    data-display/               # #5 구조화된 데이터 시각화
                                #    Table, DataTable, List, Tree, Timeline, Statistic, Badge, Tag, Progress, Calendar, Empty, Skeleton
    in-page-navigation/         # #6 페이지 내 탐색
                                #    Tabs, Anchor, Steps, Pagination, Breadcrumb, SegmentedControl
    input/                      # #7 사용자 입력
                                #    Button, Input, Select, Checkbox, Radio, Switch, Slider, DatePicker, Upload, Form, Chip
    layout/                     # #8 공간 배치와 구조
                                #    Grid, Flex, Layout, Resizable, Splitter, Masonry, BentoGrid, BrokenGrid, SplitScreen
    overlay-feedback/           # #9 맥락적 정보 표시
                                #    Modal, Drawer, Sheet, Popover, Tooltip, Toast, Snackbar, Alert, Notification, Tour
    navigation/                 # #10 페이지 간 이동
                                #    NavigationMenu, Menubar, Sidebar, BottomNavigation, AppBar, CommandPalette, Dock
    kinetic-typography/         # #11 텍스트 애니메이션 효과
                                #    CharacterStagger, TextScramble, Typewriter, BlurInReveal, LettersPullUp, GlitchText, FlipWords, AnimatedGradientText
    scroll/                     # #12 스크롤 기반 효과
                                #    Parallax, ScrollReveal, ScrollScrubbing, ImageSequence, SmoothScroll, ScrollProgress, ScrollSnap, Scroll3DEffect
    content-transition/         # #13 섹션 간 전환
                                #    StickyStacking, HorizontalScroll, PinnedContentSwap, SectionWipe, ViewTransition, ZoomTransition, BlockRevealWipe
    motion/                     # #14 스토리텔링 모션
                                #    FadeTransition, LayoutAnimation, StaggeredReveal, AnimatePresence, SharedLayoutAnimation, Marquee, SpringPhysics
    dynamic-color/              # #15 동적 색상 변화
                                #    AuroraBackground, CursorReactiveGradient, AnimatedTextGradient, GrainyGradient, DarkModeTransition, Spotlight, MeshGradient, AmbientBackground
    templates/                  # 다수 컴포넌트 조합 템플릿
    storybookDocumentation/     # Storybook 문서 유틸
    *.stories.jsx               # 컴포넌트와 같은 폴더에 co-locate

  common/ui/                    # 공통 UI 요소
  stories/                      # 문서 전용 스토리 (style, overview, page, template, test-data)
  hooks/                        # 커스텀 React 훅
  utils/                        # 유틸리티 함수
  styles/                       # 전역 스타일, 테마
  data/                         # 데이터 파일
  assets/                       # 이미지, 폰트, 비디오 등 정적 자원

.storybook/                     # Storybook 설정 (main.js, preview.jsx)
```

## 새 컴포넌트 추가 시

1. 위 구조에서 카테고리 결정 (원형 목록은 절대 기준이 아닌 맥락 안내)
2. 해당 카테고리 디렉토리에 컴포넌트 생성
3. 스토리 파일은 같은 디렉토리에 `ComponentName.stories.jsx`로 생성
4. 카테고리 디렉토리가 없으면 새로 생성
5. 기존 컴포넌트와 중복 여부는 해당 디렉토리의 파일 목록으로 직접 확인
