# Directory Structure (MUST)

파일/컴포넌트 생성 시 반드시 아래 구조를 따른다.

## 프로젝트 디렉토리

```
src/
├── components/          # UI 컴포넌트 (기능 카테고리별 폴더)
│   ├── card/            # 카드 계열
│   ├── container/       # 컨테이너 계열
│   ├── content-transition/ # 콘텐츠 전환
│   ├── data-display/    # 데이터 표시 (Table 등)
│   ├── dynamic-color/   # 동적 색상
│   ├── in-page-navigation/ # 페이지 내 네비게이션 (Tabs 등)
│   ├── input/           # 입력 (Button, TextField, Select 등)
│   ├── kinetic-typography/ # 키네틱 타이포그래피
│   ├── layout/          # 레이아웃 (Grid, Split, AppShell 등)
│   ├── media/           # 미디어 (이미지, 캐러셀 등)
│   ├── motion/          # 모션/전환 효과
│   ├── navigation/      # 내비게이션 (GNB, NavMenu 등)
│   ├── overlay-feedback/ # 오버레이 (Dialog 등)
│   ├── scroll/          # 스크롤 기반 인터랙션
│   ├── templates/       # 페이지 템플릿
│   └── typography/      # 타이포그래피
├── common/ui/           # 공통 유틸리티 UI (Placeholder, Indicator 등)
├── stories/             # Storybook 전용 (style, overview, page, template)
├── styles/              # 테마, 글로벌 스타일
├── utils/               # 유틸리티 함수
└── data/                # 데이터 파일
```

## 파일 배치 규칙

### 컴포넌트

- **컴포넌트 파일**: `src/components/{카테고리}/{ComponentName}.jsx`
- **스토리 파일**: 같은 폴더에 `{ComponentName}.stories.jsx`
- **index.js**: 각 카테고리 폴더에 barrel export 파일 유지
- **커스텀 훅**: 해당 컴포넌트 폴더에 `use{HookName}.js`

### 새 카테고리 추가 시

- 기존 카테고리에 맞는 곳이 없을 때만 `src/components/` 하위에 새 폴더 생성
- 폴더명은 kebab-case 사용

### 공통 UI

- 여러 컴포넌트에서 재사용하는 소형 UI → `src/common/ui/`

### 스토리 전용

- 디자인 토큰 문서화 (색상, 타이포 등) → `src/stories/style/`
- 프로젝트 소개/가이드 → `src/stories/overview/`
