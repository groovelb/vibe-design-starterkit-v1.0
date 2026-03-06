# Rule Visualization Skill

> 룰/스킬 추가, 수정, 삭제 시 `ruleRelationships.js` 동기화와 Storybook 시각화를 담당하는 워크플로우

## 활성화 조건

| 의도 | 트리거 예시 |
|------|-----------|
| 룰 추가 | "새 룰 추가해줘", "규칙 파일 만들어줘" |
| 룰 수정 | "룰 수정해줘", "규칙 변경해줘" |
| 룰 삭제 | "룰 삭제해줘", "규칙 제거해줘" |
| 스킬 추가/수정 | "새 스킬 만들어줘", "스킬 수정해줘" |
| 동기화 | "ruleRelationships 동기화", "룰 시각화 업데이트" |

---

## 워크플로우

```
1. 룰/스킬 변경 ──→ 2. 데이터 동기화 ──→ 3. CLAUDE.md 반영 ──→ 4. 검증 안내
```

### 1단계: 룰/스킬 변경

1. 대상 파일 수정/추가/삭제
2. 변경 유형 파악:
   - 룰 추가 → `.claude/rules/` 에 파일 생성
   - 룰 삭제 → 파일 제거 + 참조 정리
   - 스킬 추가 → `.claude/skills/{name}/SKILL.md` 생성
   - 스킬 리소스 변경 → `resources/` 하위 파일 수정

### 2단계: `ruleRelationships.js` 동기화

`src/data/ruleRelationships.js` 파일을 Read → 아래 항목 업데이트:

| 변경 유형 | 업데이트 대상 |
|----------|-------------|
| 노드 추가/삭제 | `ruleNodes` 배열에 노드 추가/제거 |
| 우선순위 변경 | `ruleNodes`의 `priority` 필드 수정 |
| 참조 관계 변경 | `ruleEdges` 배열에 엣지 추가/수정/제거 |
| 스킬 추가 | `ruleNodes` (Skill 노드) + `ruleEdges` (activates 엣지) |
| 스킬 리소스 변경 | `ruleNodes` (Skill Resource 노드) + `ruleEdges` (resources 엣지) |
| 작업 조건 변경 | `conditionMatrix` 배열 업데이트 |

#### 데이터 구조 참조

```js
// 노드
{ id: 'rule-id', name: 'rule-name.md', priority: 'MUST', path: '.claude/rules/...', description: '설명' }

// 엣지
{ from: 'source-id', to: 'target-id', type: 'loads|references|activates|resources', note: '비고' }

// 조건 매트릭스
{ task: '작업명', rules: ['rule-id'], skill: 'skill-id', skillResources: ['resource-id'], note: '비고' }
```

### 3단계: CLAUDE.md 반영

변경 내용에 따라 `CLAUDE.md` 업데이트:
- 룰 추가/삭제 → `## 규칙 원본` 섹션의 `@` 참조 추가/제거
- 스킬 추가 → `## Workflow` 섹션에 Skill 참조 추가
- Skill Resource 변경 → `### Skill Resources` 섹션 업데이트

### 4단계: 검증 안내

사용자에게 안내:
```
[동기화 완료]
- ruleRelationships.js 업데이트됨
- Storybook 확인: `pnpm storybook` → Overview/Rule Relationships
- 빌드 검증: `pnpm build-storybook` (선택)
```

---

## 시각화 구조

Storybook `Overview/Rule Relationships` 스토리가 `ruleRelationships.js`를 소비하여 4개 섹션을 렌더링:

| 섹션 | 내용 |
|------|------|
| 룰 계층 구조 | CLAUDE.md → 서브룰 트리 다이어그램 |
| 룰 목록 | 모든 노드의 이름, 우선순위, 설명 테이블 |
| 참조 관계 | 모든 엣지의 from → to, 유형, 비고 테이블 |
| 활용 조건 매트릭스 | 작업별 필요 룰/스킬/리소스 테이블 |

**스토리 파일**: `src/stories/overview/RuleRelationships.stories.jsx`
**데이터 파일**: `src/data/ruleRelationships.js`

---

## 핵심 원칙

- **동기화 누락 금지** — 룰/스킬 변경 시 `ruleRelationships.js` 동기화 필수
- **데이터 단일 소스** — `ruleRelationships.js`가 유일한 관계 데이터 원본
- **시각화 자동 반영** — 데이터만 올바르면 Storybook 시각화는 자동 갱신
