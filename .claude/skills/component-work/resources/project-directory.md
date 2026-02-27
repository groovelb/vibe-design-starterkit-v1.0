# Project Directory Rules

새로운 컴포넌트를 추가할 때는 아래 디렉토리 룰을 따른다.
분류 기준: Vibe Dictionary 텍소노미 v0.4 (`.claude/skills/component-work/resources/taxonomy-v0.4.md`)

## 디렉토리 구조

```
src/
  components/                   # Vibe Dictionary 텍소노미 기반 분류
    typography/                 # #1 텍스트 표현과 장식
    container/                  # #2 시각적 경계와 그룹핑
    card/                       # #3 독립적 정보 단위
    media/                      # #4 이미지, 비디오 표시
    data-display/               # #5 구조화된 데이터 시각화
    in-page-navigation/         # #6 페이지 내 탐색
    input/                      # #7 사용자 입력
    layout/                     # #8 공간 배치와 구조
    overlay-feedback/           # #9 맥락적 정보 표시
    navigation/                 # #10 페이지 간 이동
    kinetic-typography/         # #11 텍스트 애니메이션 효과
    scroll/                     # #12 스크롤 기반 효과
    content-transition/         # #13 섹션 간 전환
    motion/                     # #14 스토리텔링 모션
    dynamic-color/              # #15 동적 색상 변화
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

## 신규 컴포넌트 배치 가이드

컴포넌트의 **주된 역할**에 따라 카테고리 디렉토리를 결정한다.

| 주된 역할 | 디렉토리 | 예시 |
|-----------|----------|------|
| 텍스트 표현/장식 | `typography/` | 타이틀, 문단, 인용 |
| 시각적 경계/그룹핑 | `container/` | 섹션 래퍼, 캐로셀 래퍼 |
| 독립적 정보 단위 | `card/` | 미디어 카드, 프로필 카드 |
| 이미지/비디오 표시 | `media/` | 캐로셀, 갤러리 |
| 구조화된 데이터 시각화 | `data-display/` | 테이블, 리스트 |
| 페이지 내 탐색 | `in-page-navigation/` | 탭, 앵커 네비 |
| 사용자 입력 | `input/` | 검색바, 태그 입력 |
| 공간 배치/구조 | `layout/` | 그리드, 분할 레이아웃 |
| 맥락적 정보 표시 | `overlay-feedback/` | 다이얼로그, 토스트 |
| 페이지 간 이동 | `navigation/` | GNB, 메뉴 |
| 텍스트 애니메이션 | `kinetic-typography/` | 리빌, 스크램블 |
| 스크롤 기반 효과 | `scroll/` | 비디오 스크러빙, 스케일 |
| 섹션 간 전환 | `content-transition/` | 가로 스크롤 변환 |
| 스토리텔링 모션 | `motion/` | 페이드, 마키 |
| 동적 색상 변화 | `dynamic-color/` | 그라데이션 오버레이 |
| 다수 컴포넌트 조합 | `templates/` | 필터바, 페이지 템플릿 |

판단이 애매하면 `taxonomy-index.md`에서 가장 가까운 카테고리를 참조한다.

## 새 컴포넌트 추가 시

1. 위 배치 가이드에서 카테고리 결정
2. 해당 카테고리 디렉토리에 컴포넌트 생성
3. 스토리 파일은 컴포넌트와 같은 디렉토리에 `ComponentName.stories.jsx`로 생성
4. 스토리 title prefix는 `storybook-writing.md`의 카테고리 매핑 참조
5. 카테고리 디렉토리가 없으면 새로 생성
6. 기존 컴포넌트와 중복 여부는 해당 디렉토리의 파일 목록으로 직접 확인
