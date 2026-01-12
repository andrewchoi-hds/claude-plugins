# TIL (Today I Learned) - 2026-01-12

## Claude Code 플러그인 개발

### 1. 플러그인 디렉토리 구조

```
.claude/
├── agents/      # 에이전트 정의 (.md)
├── commands/    # 스킬/명령어 정의 (.md)
└── settings.json # 설정 (agents, skills, triggers)
```

**핵심**: `.claude/` 디렉토리가 플러그인의 루트. 파일만 만들면 안 되고 `settings.json`에 등록해야 작동함.

### 2. settings.json 이중 계층

```json
{
  "agents": {     // 에이전트 정의 (tools, description)
    "agent-name": {...}
  },
  "skills": {     // 트리거 정의 (triggers, description)
    "skill-name": {...}
  }
}
```

**핵심**: agents는 "무엇을 하는지", skills는 "언제 실행하는지" 분리.

### 3. 에이전트 Markdown 컨벤션

표준 섹션:
- `# [name] 에이전트` - 제목
- `## 목적` - 무엇을 하는지
- `## 출력 형식` - 구조화된 템플릿
- `## 사용 가능한 도구` - Read, Glob, Grep
- `## 지침` - 단계별 가이드
- `## 주의사항` - 제약사항

### 4. 한국어 트리거 확장

다양한 표현 방식 지원:
```json
"triggers": [
  "/wrap",           // 명령어
  "세션 정리",        // 기본
  "마무리해줘",       // 요청형
  "오늘은 여기까지",   // 대화형
  "랩"               // 축약
]
```

**핵심**: 사용자가 자연스럽게 말하는 모든 방식을 커버.

### 5. Phase 기반 에이전트 오케스트레이션

```
Phase 1: 병렬 실행 (독립 작업)
  ├── agent-1
  ├── agent-2
  └── agent-3

Phase 2: 순차 실행 (Phase 1 결과 필요)
  └── validator-agent

Phase 3: 사용자 인터랙션
  └── AskUserQuestion
```

**핵심**:
- 독립적 = 병렬 (효율성)
- 의존적 = 순차 (정확성)
- 최종 = 사용자 선택 (자율성)

---

## 효과적이었던 패턴

### 역할 분리
- 하나의 에이전트 = 하나의 책임
- 복잡한 작업 = 단순한 에이전트들의 조합

### 한/영 이중 언어
- description: 영어 + 한국어
- triggers: 두 언어 모두
- 출력: 한국어 우선

### 표준화된 명명
- kebab-case (doc-updater, automation-scout)
- 동사-명사 조합 (updater, extractor, checker)

---

## 피해야 할 것

1. **하나의 에이전트에 너무 많은 책임** → 역할 분리
2. **트리거 과도하게 추가** → 7-15개가 적당
3. **파일만 만들고 JSON 등록 안 함** → settings.json 확인 필수
