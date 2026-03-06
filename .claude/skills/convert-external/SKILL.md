# Convert External Skill

> `src/externalComponents/`에 붙여넣은 외부 코드를 프로젝트 규칙에 맞게 변환하는 워크플로우

## 활성화 조건

| 의도 | 트리거 예시 |
|------|-----------|
| 외부 코드 변환 | "이거 변환해줘", "외부 컴포넌트 적용해줘", "프로젝트에 맞게 바꿔줘" |
| externalComponents 참조 | `@src/externalComponents/...` 파일 언급 |

---

## 워크플로우

```
1. 분석 ──→ 2. 분류 ──→ 3. 변환 계획 ──→ 4. 구현 ──→ 5. 등록
```

### 1단계: 코드 분석

1. `src/externalComponents/` 대상 파일 Read
2. `resources/conversion-checklist.md` Read → 변환 항목 감지
3. 감지 결과를 사용자에게 리포트:

```
[분석 결과]
- 파일: ComponentName.tsx
- 언어: TypeScript → JSX 변환 필요
- 스타일: Tailwind 클래스 12개 → MUI sx 변환 필요
- 외부 의존성: Three.js (프로젝트 미설치)
- 외부 import: ../constants → Props로 외부화 필요
- 변환 난이도: 복잡 (외부 라이브러리 + 스타일 전환)
```

### 2단계: 텍소노미 분류

1. `component-work`의 `resources/taxonomy-index.md` Read → 카테고리 후보 제시
2. `components.md` (rules에서 이미 로드됨) → 기존 컴포넌트와 중복/유사 확인
3. 사용자에게 카테고리 후보 제시 → 확인 후 결정

```
[분류 후보]
- #15 DynamicColor → "동적 색상 변화" (가장 유사)
- #12 Scroll → "스크롤 기반 효과" (부분 해당)
→ 어떤 카테고리가 적절할까요?
```

### 3단계: 변환 계획 (사용자 승인 필수)

감지 항목별 구체적 변환 방법을 제시하고 사용자 승인을 받는다:

```
[변환 계획]
1. TypeScript → JSX: interface Props 제거, JSDoc 주석으로 대체
2. Tailwind → sx: className="fixed inset-0 ..." → sx={{ position: 'fixed', inset: 0, ... }}
3. ../constants 제거: COLORS.bgLight → Props (colorLight, colorDark)로 외부화
4. Three.js 유지: pnpm add three 필요 (사용자 확인)
5. default export → named export
```

**승인 없이 구현 진행 금지.**

### 4단계: 구현

승인된 계획에 따라 변환 실행:

1. **파일 변환**
   - `.tsx` → `.jsx` (TypeScript 제거)
   - Tailwind → MUI sx prop
   - 외부 import → Props 또는 theme 토큰
   - 코드 컨벤션 적용 (`code-convention.md` 준수)
     - Props 구조분해 + JSDoc 주석
     - camelCase 함수, PascalCase 컴포넌트
     - single quotes, `{ value }` JSX 스페이싱

2. **위치 결정**
   - `project-directory.md`에 따라 텍소노미 카테고리 디렉토리에 배치

3. **스토리 작성**
   - `component-work`의 `resources/storybook-writing.md` Read → 스토리 규칙 확인
   - Placeholder 시스템 사용 (하드코딩 이미지/데모 금지)
   - `project-directory.md`의 Storybook 카테고리 매핑에 따라 title 설정

4. **인터랙티브 감지**
   - 아래 조건 해당 시 → `component-work`의 `resources/interactive-principles.md` Read
     - Framer Motion, GSAP, Three.js 등 애니메이션 라이브러리
     - 스크롤 기반 인터랙션
     - 텍소노미 #11~#15 카테고리
     - CSS 애니메이션을 넘어서는 인터랙션

### 5단계: 등록

1. `components.md` 업데이트 (MUST)
   - 해당 카테고리 섹션에 컴포넌트 추가
   - 형식: `- ComponentName: 한줄 설명 (\`components/category/ComponentName.jsx\`)`
2. 사용자 확인 후 `src/externalComponents/` 원본 삭제

---

## Resources

| 파일 | 용도 | 언제 Read |
|------|------|----------|
| `conversion-checklist.md` | 변환 항목 감지 규칙 | 1단계 (항상) |

### 참조하는 외부 리소스 (복제하지 않음)

| 파일 | 위치 | 언제 Read |
|------|------|----------|
| `taxonomy-index.md` | `component-work/resources/` | 2단계 |
| `storybook-writing.md` | `component-work/resources/` | 4단계 |
| `interactive-principles.md` | `component-work/resources/` | 4단계 (인터랙티브 감지 시) |

---

## 핵심 원칙

- **변환 계획 승인 없이 코드 작성 금지** — 3단계에서 반드시 사용자 확인
- **외부 라이브러리는 사용자 확인** — 프로젝트에 없는 의존성 설치 전 승인
- **원본 보존** — `src/externalComponents/` 원본은 5단계에서 사용자 확인 후에만 삭제
- **규칙 우선** — CLAUDE.md의 CRITICAL/MUST 규칙은 변환 중에도 절대 위반 불가
