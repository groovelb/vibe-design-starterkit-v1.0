# Storybook Writing Rules (SHOULD)

Storybook 스토리 작성 시 준수해야 할 규칙

## 스토리 카테고리 구조

| 카테고리 | title 접두사 | 설명 |
|---------|-------------|------|
| **Style** | `Style/` | 디자인 토큰 문서 (색상, 타이포그래피, 간격 등) |
| **Custom Component** | `Custom Component/` | 프로젝트에서 새로 만든 재사용 컴포넌트 |
| **Template** | `Template/` | 여러 컴포넌트를 조합한 템플릿 |
| **Section** | `Section/` | 페이지를 구성하는 섹션 단위 컴포넌트 |
| **Page** | `Page/` | 전체 페이지 레벨 컴포넌트 |

## 필수 규칙

### 공통

| Rule | Description |
|------|-------------|
| First Story Named "Docs" | **첫 번째 스토리의 export 이름은 반드시 `Docs`** (autodocs 제외). Storybook 사이드바에서 Docs가 최상단에 표시됨 |
| Single Component per Story | 스토리 한 개당 단일 컴포넌트/토큰만 보여준다 |
| Docs First with Controls | (Component) 항상 첫 문서는 Docs이며, 해당 컴포넌트의 모든 props를 타입에 맞는 `argTypes`와 `control`로 유저가 확인/조작할 수 있도록 적용 |
| Style Docs Structure | (Style) 첫 스토리(`Docs`)는 1줄 개요 → 토큰 구조 (트리 뷰) → 토큰 값 (테이블) → 사용 예시 → Vibe Coding Prompt 순서로 구성. 기존 상세 스토리(Palette, SemanticTokens 등)는 유지 |
| DocumentTitle English | DocumentTitle의 모든 props (`title`, `status`, `note`, `brandName`, `systemName`) 값은 영어로 작성 |
| Description Korean | DocumentTitle 외의 설명 (페이지 제목, 섹션 설명, 테이블 내용 등)은 한글로 작성 |
| Props Table Required | (Component) 모든 스토리 Doc의 최상단에 컴포넌트 설명과 함께 Props 테이블을 표시 |
| SectionTitle Usage | 2개 이상의 섹션이 있을 경우 반드시 `SectionTitle`로 구분 |
| Placeholder Required | 스토리 예제의 더미 콘텐츠는 반드시 `Placeholder` 컴포넌트를 사용 (`common/ui/Placeholder.jsx`) |

### Placeholder 사용 규칙

스토리에서 실제 콘텐츠 대신 보여줄 더미 블록은 `Placeholder` 서브컴포넌트를 사용한다.
FPO(For Position Only) 데모 블록 용도이며, 로딩 스켈레톤이 아니다.

#### Import

```jsx
// 기본: 서브컴포넌트 조합 사용
import Placeholder from '../../common/ui/Placeholder';

// SVG만 단독 사용 (다른 컴포넌트에서 <img src={}>로 활용)
import { placeholderSvg } from '../../common/ui/Placeholder';
```

> **주의**: `@/` alias가 아닌 상대 경로를 사용한다 (Storybook Vite 빌드 호환).

#### 서브컴포넌트 선택 가이드

| 용도 | 컴포넌트 | 설명 | 예시 |
|------|---------|------|------|
| 레이아웃 영역 | `Placeholder.Box` | dashed border + 중앙 라벨. 공간 구조 데모 | 그리드 셀, 사이드바, 패널 |
| 이미지 슬롯 (구조) | `Placeholder.Image` | **점 패턴 SVG** 기반. 비율만 표시하는 FPO 블록 | 카드 이미지, 히어로, 썸네일 구조 |
| 이미지 슬롯 (실제) | `Placeholder.Media` | **grayscale 스톡 이미지**. 실제 이미지가 필요한 데모 | 캐러셀, 갤러리, 포트폴리오 |
| 제목 자리 | `Placeholder.Text variant="heading"` | 높이 24px, 폭 60% 솔리드 바 | 카드 제목, 섹션 헤딩 |
| 본문 자리 | `Placeholder.Paragraph` | 여러 줄 텍스트 블록 (마지막 줄 자동 짧게) | 카드 본문, 설명 텍스트 |
| 캡션/메타 자리 | `Placeholder.Text variant="caption"` | 높이 10px, 폭 40% 솔리드 바 | 날짜, 태그, 부가 정보 |
| 카드형 복합 | `Placeholder.Card` | Image + Paragraph 조합 | 카드 내부 전체 |

#### Image vs Media 판단 기준

- **`Placeholder.Image`**: 이미지 내용이 중요하지 않고 **공간/비율만** 보여주면 될 때. 점 그리드 SVG로 가상 공간 표현.
- **`Placeholder.Media`**: 실제 이미지가 들어간 **시각적 맥락**이 필요할 때. grayscale 스톡 이미지로 중립 톤 유지.

#### Placeholder.Media 상세

```jsx
// 기본 사용 (전체 풀에서 첫 번째 이미지)
<Placeholder.Media />

// 특정 인덱스 (같은 index = 같은 이미지, 결정적 렌더링)
<Placeholder.Media index={2} ratio="16/9" />

// 카테고리 지정: abstract | fineart | illustration | poster | gradient | photography | portrait | spatial
<Placeholder.Media category="spatial" index={1} size="large" />

// 크기: small | medium (기본) | large
<Placeholder.Media size="small" width={120} />
```

#### placeholderSvg — 독립 SVG 헬퍼

다른 컴포넌트에서 이미지 슬롯에 점 패턴 SVG를 직접 넣을 때 사용:

```jsx
import { placeholderSvg } from '../../common/ui/Placeholder';

// <img> 태그에 직접 사용
<img src={placeholderSvg(800, 450)} alt="placeholder" />

// 네임스페이스로도 접근 가능
<img src={Placeholder.svg(800, 450)} alt="" />
```

- `placeholderSvg(width?, height?)` — 기본값: 400×300
- 16px 간격 점 그리드, `#f5f5f5` 배경, `#bdbdbd` 점
- `data:image/svg+xml` data URI 반환 → 네트워크 요청 없음

#### 금지사항

- 스토리에서 ad-hoc DemoBox/DemoCell 등을 새로 만들지 않는다
- 실제 이미지 URL을 하드코딩하지 않는다 (이미지 컴포넌트 자체 테스트 제외)
- 플레이스홀더에 브랜드 컬러(`#667eea` 등)를 직접 지정하지 않는다
- Placeholder.Image에 실제 이미지 URL을 넣지 않는다 (SVG 전용)
- Placeholder.Media의 grayscale 필터를 제거하지 않는다

### Story Types

| Type | autodocs | Doc Story | DocumentTitle | Use Case |
|------|----------|-----------|---------------|----------|
| Component (interactive) | `tags: ['autodocs']` | NOT needed | NOT supported in Docs tab | Components with props (Button, Card, Icons) |
| Documentation (static) | None | Required | Required | Overview, Style sections (Introduction, Typography) |

**Note:** `docs.page` with JSX causes dynamic import errors in Vite + Storybook. Do NOT use DocumentTitle in autodocs Docs tab.

### Component Story (autodocs)

Use `tags: ['autodocs']` for automatic documentation. No separate Doc story needed. DocumentTitle cannot be added to autodocs Docs tab.

**중요**: 모든 props에 대해 타입에 맞는 `argTypes`와 `control`을 정의하여 사용자가 Docs 탭에서 직접 값을 조작하며 확인할 수 있도록 한다.

```jsx
export default {
  title: 'Custom Component/ComponentName',
  component: Component,
  tags: ['autodocs'],
  argTypes: {
    label: { control: 'text', description: '버튼 텍스트' },
    isDisabled: { control: 'boolean', description: '비활성화 여부' },
    variant: {
      control: 'select',
      options: ['primary', 'secondary'],
      description: '스타일 변형'
    },
    size: {
      control: { type: 'number', min: 1, max: 10 },
      description: '크기',
    },
    backgroundColor: { control: 'color', description: '배경색' },
    onClick: { action: 'clicked', description: '클릭 핸들러' },
  },
};

export const Default = {
  args: {
    label: '버튼',
    isDisabled: false,
    variant: 'primary',
  },
};
```

### argTypes Control 타입 가이드

| Props 타입 | control | 예시 |
|-----------|---------|------|
| string | `'text'` | `control: 'text'` |
| boolean | `'boolean'` | `control: 'boolean'` |
| number | `{ type: 'number' }` | `control: { type: 'number', min: 0, max: 100 }` |
| enum/선택지 | `'select'` 또는 `'radio'` | `control: 'select', options: ['a', 'b']` |
| color | `'color'` | `control: 'color'` |
| object | `'object'` | `control: 'object'` |
| array | `'object'` | `control: 'object'` |
| date | `'date'` | `control: 'date'` |
| function | `action()` | `action: 'clicked'` |

### Documentation Story (Doc)

For static documentation pages (Overview, Style), use Doc story with DocumentTitle.

```jsx
export const Doc = {
  render: () => (
    <>
      <DocumentTitle
        title="ComponentName"
        status="Available"
        note="Brief description"
        brandName="Design System"
        systemName="Starter Kit"
        version="1.0"
      />
      <PageContainer>
        <SectionTitle title="Section 1" />
        {/* Content */}
      </PageContainer>
    </>
  ),
};
```

---

## Props 테이블 (필수)

**모든 스토리 Doc의 최상단**에 컴포넌트 설명 직후 Props 테이블을 배치한다.

### Props 테이블 구조

| 컬럼 | 설명 |
|------|------|
| Prop | Props 이름 (monospace) |
| Type | 데이터 타입 |
| Default | 기본값 |
| Description | 한글 설명 |

### Props 테이블 템플릿

```jsx
<SectionTitle title="Props" description="컴포넌트의 Props 목록입니다." />
<TableContainer>
  <Table size="small">
    <TableHead>
      <TableRow>
        <TableCell sx={ { fontWeight: 600 } }>Prop</TableCell>
        <TableCell sx={ { fontWeight: 600 } }>Type</TableCell>
        <TableCell sx={ { fontWeight: 600 } }>Default</TableCell>
        <TableCell sx={ { fontWeight: 600 } }>Description</TableCell>
      </TableRow>
    </TableHead>
    <TableBody>
      <TableRow>
        <TableCell sx={ { fontFamily: 'monospace' } }>propName</TableCell>
        <TableCell>string</TableCell>
        <TableCell>-</TableCell>
        <TableCell>Props 설명 (한글)</TableCell>
      </TableRow>
    </TableBody>
  </Table>
</TableContainer>
```

---

## Style 스토리 (디자인 토큰 문서)

Style 섹션은 MUI theme 기반 디자인 토큰 문서이다. **autodocs를 사용하지 않고** 직접 Doc 스토리를 작성한다.

### Style 스토리 필수 구조

```
1. DocumentTitle (영문)
2. PageContainer
   ├── 페이지 제목 (h4)
   ├── 스토리 개요 (1줄 설명)
   ├── SectionTitle: "토큰 구조" → 트리 뷰로 theme 계층 표시 (필수)
   ├── SectionTitle: "토큰 값" → 테이블로 토큰값 표시 (필수)
   ├── SectionTitle: "사용 예시" → MUI sx prop 코드 예시 (필수)
   └── SectionTitle: "Vibe Coding Prompt" → AI 코딩용 프롬프트 예시 (필수)
```

#### 1. 스토리 개요 (1줄)

페이지 제목 바로 아래에 **한 줄**로 해당 토큰의 역할을 설명한다.

```jsx
<Typography variant="h4" sx={ { fontWeight: 700, mb: 1 } }>
  Color System
</Typography>
<Typography variant="body1" color="text.secondary" sx={ { mb: 4 } }>
  프로젝트에서 사용하는 색상 팔레트와 시멘틱 컬러 토큰입니다.
</Typography>
```

#### 2. 토큰 구조 (트리 뷰) - 필수

`Overview.stories.jsx`의 TreeNode 패턴을 사용하여 MUI theme 계층 구조를 트리 형태로 보여준다.

```jsx
const tokenStructure = {
  palette: {
    primary: theme.palette.primary,
    secondary: theme.palette.secondary,
    error: theme.palette.error,
  },
};

<SectionTitle title="토큰 구조" description="theme.palette 계층 구조" />
<Box sx={ { p: 2, border: '1px solid', borderColor: 'divider', borderRadius: 1 } }>
  { Object.entries(tokenStructure).map(([key, value]) => (
    <TreeNode key={ key } keyName={ key } value={ value } />
  )) }
</Box>
```

#### 3. 토큰 값 (테이블) - 필수

```jsx
<SectionTitle title="토큰 값" description="주요 토큰의 실제 값" />
<TableContainer>
  <Table size="small">
    <TableHead>
      <TableRow>
        <TableCell sx={ { fontWeight: 600 } }>Token</TableCell>
        <TableCell sx={ { fontWeight: 600 } }>Value</TableCell>
        <TableCell sx={ { fontWeight: 600 } }>설명</TableCell>
      </TableRow>
    </TableHead>
    <TableBody>
      <TableRow>
        <TableCell sx={ { fontFamily: 'monospace' } }>primary.main</TableCell>
        <TableCell sx={ { fontFamily: 'monospace' } }>#0000FF</TableCell>
        <TableCell>주요 브랜드 색상</TableCell>
      </TableRow>
    </TableBody>
  </Table>
</TableContainer>
```

#### 4. 사용 예시 (MUI sx prop) - 필수

```jsx
<SectionTitle title="사용 예시" description="MUI sx prop에서의 토큰 활용" />
<Box
  component="pre"
  sx={ {
    backgroundColor: 'grey.100',
    p: 2,
    fontSize: 12,
    fontFamily: 'monospace',
    overflow: 'auto',
    borderRadius: 1,
  } }
>
{`// 색상 토큰 사용
<Box sx={{ backgroundColor: 'primary.main' }} />
<Typography sx={{ color: 'text.secondary' }} />

// 간격 토큰 사용
<Box sx={{ p: 2, m: 3, gap: 1 }} />`}
</Box>
```

#### 5. Vibe Coding Prompt - 필수

AI 코딩 도구에서 해당 토큰을 활용할 때 사용할 수 있는 프롬프트 예시를 제공한다.

```jsx
<SectionTitle
  title="Vibe Coding Prompt"
  description="AI 코딩 도구에서 활용할 수 있는 프롬프트 예시"
/>
<Box
  component="pre"
  sx={ {
    backgroundColor: 'grey.900',
    color: 'grey.100',
    p: 2,
    fontSize: 12,
    fontFamily: 'monospace',
    overflow: 'auto',
    borderRadius: 1,
  } }
>
{`"primary.main (#0000FF)을 사용해서 CTA 버튼을 만들어줘.
hover 시 primary.dark로 변경되도록 해줘."`}
</Box>
```

**Vibe Coding Prompt 작성 가이드:**

| 요소 | 설명 |
|------|------|
| 토큰 명시 | 사용할 토큰 경로를 명확히 언급 (예: `primary.main`) |
| 값 참고 | 필요시 실제 값도 함께 표기 (예: `#0000FF`) |
| 컨텍스트 | 어떤 상황에서 사용하는지 설명 |
| 상호작용 | hover, active 등 상태별 토큰 변화 명시 |

### Style 스토리 템플릿

```jsx
import { useTheme } from '@mui/material/styles';
import { DocumentTitle, PageContainer, SectionTitle } from '../../components/storybookDocumentation';

export default {
  title: 'Style/TokenName',
  parameters: {
    layout: 'padded',
  },
};

export const Default = {
  render: () => {
    const theme = useTheme();

    const tokenStructure = {
      // theme에서 필요한 부분만 추출
    };

    return (
      <>
        <DocumentTitle
          title="Token Name"
          status="Available"
          note="Brief description in English"
          brandName="Design System"
          systemName="Starter Kit"
          version="1.0"
        />
        <PageContainer>
          <Typography variant="h4" sx={ { fontWeight: 700, mb: 1 } }>
            토큰 제목
          </Typography>
          <Typography variant="body1" color="text.secondary" sx={ { mb: 4 } }>
            한 줄로 토큰의 역할을 설명합니다.
          </Typography>

          <SectionTitle title="토큰 구조" description="MUI theme 계층 구조" />
          <Box sx={ { p: 2, border: '1px solid', borderColor: 'divider', borderRadius: 1, mb: 4 } }>
            {/* TreeNode로 트리 뷰 렌더링 */}
          </Box>

          <SectionTitle title="토큰 값" description="주요 토큰의 실제 값" />
          <TableContainer sx={ { mb: 4 } }>
            {/* 테이블로 토큰값 표시 */}
          </TableContainer>

          <SectionTitle title="사용 예시" description="MUI sx prop에서의 토큰 활용" />
          <Box component="pre" sx={ { backgroundColor: 'grey.100', p: 2, mb: 4 } }>
            {/* MUI sx prop 코드 예시 */}
          </Box>

          <SectionTitle title="Vibe Coding Prompt" description="AI 코딩 도구에서 활용할 수 있는 프롬프트 예시" />
          <Box component="pre" sx={ { backgroundColor: 'grey.900', color: 'grey.100', p: 2 } }>
            {/* AI 프롬프트 예시 */}
          </Box>
        </PageContainer>
      </>
    );
  },
};
```

### Style vs Component 비교

| 구분 | Style 스토리 | Component 스토리 |
|------|-------------|-----------------|
| autodocs | 사용 안 함 | `tags: ['autodocs']` |
| 최상단 필수 | 토큰 구조 (theme 경로) | Props 테이블 |
| 인터랙션 | 없음 (정적 참조) | argTypes/controls |
| 목적 | 디자인 토큰 문서화 | 컴포넌트 사용법 |

---

## 문서 스타일 원칙

공식 기술 문서 스타일을 따른다. 장식보다 정보 전달에 집중한다.

| 원칙 | 설명 |
|------|------|
| 보수적 | 최소한의 스타일링, 장식 요소 배제 |
| 전문적 | 기술 문서처럼 신뢰감 있는 톤 |
| 구조적 | 명확한 계층과 섹션 구분 |
| 일관성 | 모든 문서가 동일한 레이아웃 구조 |

### 금지 사항

- Paper, Card 컴포넌트의 장식적 사용 금지
- elevation, boxShadow 사용 금지
- 불필요한 배경색, 그라데이션 금지
- 이모지 과다 사용 금지
- 마케팅 문구 금지

---

## 베리에이션 작성 원칙

**지양:**
```jsx
// Props 조합별로 스토리를 과도하게 생성
export const PrimarySmall = { args: { variant: 'primary', size: 'small' } };
export const PrimaryMedium = { args: { variant: 'primary', size: 'medium' } };
```

**권장:**
```jsx
// Default 스토리 + Controls로 사용자가 직접 조작
export const Default = { args: { variant: 'primary', size: 'medium' } };

// 필요 시 하나의 스토리에서 주요 변형만 간단히 나열
export const Variants = {
  render: () => (
    <Stack direction="row" spacing={2}>
      <Button variant="primary">Primary</Button>
      <Button variant="secondary">Secondary</Button>
    </Stack>
  ),
};
```

---

## 콘텐츠 스타일링 규칙

### 정보 표시용 컴포넌트

| 용도 | 권장 | 금지 |
|------|------|------|
| 데이터 나열 | Table, TableContainer | Card 그리드 |
| 섹션 구분 | SectionTitle, Divider | Paper elevation |
| 색상 블록 | Box with backgroundColor | Card, Paper |
| 코드 예시 | Box component="pre" | Paper elevation |

### 허용되는 스타일링

```jsx
// 테이블로 정보 표시
<TableContainer>
  <Table size="small">
    <TableBody>
      <TableRow>
        <TableCell sx={ { fontWeight: 600 } }>키</TableCell>
        <TableCell>값</TableCell>
      </TableRow>
    </TableBody>
  </Table>
</TableContainer>

// 색상 블록 (장식 없음)
<Box
  sx={ {
    width: 80,
    height: 80,
    backgroundColor: color,
    display: 'flex',
    alignItems: 'center',
    justifyContent: 'center',
  } }
>
  <Typography variant="caption">{ label }</Typography>
</Box>

// 코드 블록
<Box
  component="pre"
  sx={ {
    backgroundColor: 'grey.100',
    p: 2,
    fontSize: 12,
    fontFamily: 'monospace',
    overflow: 'auto',
  } }
>
  {code}
</Box>
```

### 금지되는 스타일링

```jsx
// 장식적 Paper 사용
<Paper sx={ { p: 3, elevation: 2 } }> ... </Paper>

// Card 그리드
<Grid container spacing={ 2 }>
  <Grid item>
    <Card><CardContent>...</CardContent></Card>
  </Grid>
</Grid>

// 그림자, 보더 장식
<Box sx={ { boxShadow: 3, border: '2px solid primary.main' } }>
```

---

## 필수 문서 컴포넌트

`src/components/storybookDocumentation/` 내 컴포넌트를 적극 사용한다.

- `DocumentTitle` - 모든 스토리 상단에 문서 메타 정보 표시 (모든 props 값은 영어)
- `PageContainer` - 모든 스토리 콘텐츠를 감싸는 컨테이너 (xl 브레이크포인트 기준 최대 너비)
- `SectionTitle` - 콘텐츠 섹션 구분용 타이틀 (하단 보더로 시각적 구분)

---

## 스토리 구성 규칙

### Style 섹션

| 접근 방식 | 설명 |
|----------|------|
| 단일 스토리 | 모든 정보를 하나의 Default 스토리에 SectionTitle로 구분 |
| 다중 스토리 | 정보량이 많을 경우 주제별로 분리 (최대 3-4개) |

### Component 섹션

| 스토리 | 목적 | 필수 |
|--------|------|------|
| Default | 기본 사용 예시, args 연동 | 필수 |
| Variants | 주요 변형 비교 | 선택 |

### 스토리 개수 제한

- Style 섹션: 1-3개 권장
- Component 섹션: 1-5개 권장

---

## 타이포그래피 규칙

### 페이지 제목

```jsx
<Typography variant="h4" sx={ { fontWeight: 700, mb: 1 } }>
  제목
</Typography>
<Typography variant="body1" color="text.secondary" sx={ { mb: 4 } }>
  부제목/설명
</Typography>
```

### 테이블 스타일

```jsx
<TableCell sx={ { fontWeight: 600 } }>헤더</TableCell>
<TableCell sx={ { fontFamily: 'monospace', fontSize: 12 } }>코드값</TableCell>
<TableCell sx={ { color: 'text.secondary', fontSize: 13 } }>설명</TableCell>
```

---

## 체크리스트

스토리 작성 완료 전 확인:

### MUST (Required)

**공통**
- [ ] 스토리 한 개당 단일 컴포넌트/토큰만 보여주는가?
- [ ] DocumentTitle props가 모두 영어로 작성되었는가?
- [ ] 설명(페이지 제목, 섹션 설명, 테이블 내용)이 한글로 작성되었는가?
- [ ] 2개 이상의 섹션에 SectionTitle이 사용되었는가?

**Component 스토리**
- [ ] `tags: ['autodocs']`가 적용되었는가?
- [ ] 모든 props에 타입에 맞는 argTypes와 control이 적용되었는가?
- [ ] 최상단에 Props 테이블이 있는가?

**Style 스토리**
- [ ] autodocs 없이 직접 Doc 스토리를 작성했는가?
- [ ] 1줄 개요가 페이지 제목 아래에 있는가?
- [ ] 토큰 구조가 트리 뷰로 표시되어 있는가? (Overview.stories.jsx TreeNode 패턴)
- [ ] 토큰 값이 테이블로 정리되어 있는가?
- [ ] MUI sx prop 사용 예시가 포함되어 있는가?
- [ ] Vibe Coding Prompt 예시가 포함되어 있는가?
- [ ] `useTheme()` 훅으로 실제 theme 값을 참조하는가?

### SHOULD (Recommended)
- [ ] PageContainer로 콘텐츠가 감싸져 있는가? (Doc stories)
- [ ] Paper, Card, elevation 장식이 없는가?
- [ ] 불필요한 색상/장식이 없는가?
