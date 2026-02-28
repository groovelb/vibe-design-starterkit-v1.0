# Storybook Writing Rules (SHOULD)

## 핵심 규칙

### 1. Docs 항상 첫 번째

- Component 스토리: `tags: ['autodocs']` 사용. 첫 번째 export는 반드시 `Docs`
- Documentation 스토리: autodocs 없이 직접 Doc 스토리 작성

### 2. 과한 Variant 금지 — Props Controls 중심

```jsx
// 지양: Props 조합별 스토리 과다 생성
export const PrimarySmall = { args: { variant: 'primary', size: 'small' } };
export const PrimaryMedium = { args: { variant: 'primary', size: 'medium' } };

// 권장: Default + argTypes controls로 사용자가 직접 조작
export default {
  title: 'Component/Category/Name',
  component: Component,
  tags: ['autodocs'],
  argTypes: {
    label: { control: 'text', description: '버튼 텍스트' },
    isDisabled: { control: 'boolean', description: '비활성화 여부' },
    variant: { control: 'select', options: ['primary', 'secondary'] },
  },
};

export const Default = {
  args: { label: '버튼', variant: 'primary' },
};
```

### 3. 스토리 파일은 원본 컴포넌트와 같은 폴더

컴포넌트와 스토리를 같은 디렉토리에 배치한다.

```
components/card/
├── BaseCard.jsx
└── BaseCard.stories.jsx
```

### 4. DocumentTitle 사용

Documentation 스토리에서는 `DocumentTitle`을 사용하여 문서 메타 정보를 표시한다. **모든 props 값은 영어로 작성.**

```jsx
import { DocumentTitle, PageContainer, SectionTitle } from '../../components/storybookDocumentation';

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
        <SectionTitle title="Section" />
        {/* Content */}
      </PageContainer>
    </>
  ),
};
```

> **Note:** `docs.page`에 JSX를 사용하면 Vite + Storybook에서 dynamic import 에러 발생. autodocs Docs 탭에서는 DocumentTitle 사용 불가.
