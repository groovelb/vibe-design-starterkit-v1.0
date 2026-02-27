# Project Rules

## META INSTRUCTION

IMPORTANT: 이 문서와 참조된 모든 규칙은 프로젝트 법률이다.
YOU MUST 코드 작업 전 관련 규칙을 확인하고, 위반 가능성이 있으면 먼저 사용자에게 알려라.
YOU MUST NOT 명시적 허용 없이 규칙을 위반하는 코드를 작성하지 마라.

## 규칙 원본

### CRITICAL (절대 위반 불가)
@.claude/rules/project-summary.md
@.claude/rules/mui-grid-usage.md

### MUST (반드시 준수)
@.claude/rules/code-convention.md
@.claude/rules/design-system.md

### SHOULD (관련 작업 시 준수)
@.claude/rules/easy-refactoring.md
@.claude/rules/mui-theme.md

## Common Commands

```bash
pnpm dev              # Vite 개발 서버
pnpm storybook        # Storybook 실행 (포트 6006)
pnpm build            # 프로덕션 빌드
pnpm build-storybook  # Storybook 정적 빌드
pnpm lint             # ESLint 검사
```

## Workflow

### 모든 코드 변경 전 (MANDATORY)
1. 작업 대상 파일/폴더 확인
2. 관련 규칙 확인
3. 규칙 위반 가능성 체크
4. 충돌 시 → 사용자에게 먼저 알림

### 컴포넌트 작업 (생성/수정/삭제/스토리)
→ `component-work` Skill이 워크플로우를 담당.
   텍소노미 안내, 기존 컴포넌트 확인, 스토리 규칙 등 Skill이 점진적으로 로드.

### 리팩토링
1. 외부 동작 변경 없음 확인
2. easy-refactoring.md 참조
3. 기존 스토리 통과 확인

### 룰 수정/추가/삭제
1. 룰 파일 수정/추가/삭제
2. `src/data/ruleRelationships.js` 동기화:
   - 룰 추가/삭제 → `ruleNodes` 배열에 노드 추가/제거
   - 참조 관계 변경 → `ruleEdges` 배열에 엣지 추가/수정/제거
   - 작업 조건 변경 → `conditionMatrix` 배열 업데이트
3. `pnpm build-storybook`으로 `Overview/Rule Relationships` 시각화 정상 렌더링 확인

## 병렬 작업 규칙

- `run_in_background: true` 사용 금지 (알려진 버그: 세션 멈춤, GitHub #20679 #17540 #21048)
- 병렬 실행이 필요하면 하나의 메시지에서 여러 Task를 동시 호출하라 (`run_in_background` 플래그 없이)
- 에이전트 결과를 개별 확인(TaskOutput/Read)하지 마라. 에이전트가 끝나면 즉시 완료 보고하라
- 빌드 검증(pnpm build-storybook, pnpm build)은 사용자가 명시적으로 요청할 때만 실행하라. 자의적으로 빌드를 돌리지 마라

## 규칙 충돌 처리

사용자 요청이 규칙과 충돌할 경우:
1. "이 요청은 [규칙명]과 충돌합니다" 알림
2. 구체적 충돌 내용 설명
3. 사용자가 명시적으로 예외 허용할 때까지 진행 금지
