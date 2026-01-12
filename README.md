# session-wrap

Claude Code 세션 마무리 자동화 플러그인

## 설치

```bash
# 플러그인 디렉토리를 프로젝트에 복사
cp -r session-wrap/.claude /your/project/
```

## 사용법

```bash
/wrap
```

또는 자연어로:

```
세션 정리해줘
마무리하자
오늘은 여기까지
```

## 지원하는 트리거

### 명령어
- `/wrap`

### 한국어 (자연어)
| 트리거 | 설명 |
|--------|------|
| 세션 정리 / 세션 마무리 / 세션 끝 | 기본 |
| 마무리해줘 / 정리해줘 | 요청형 |
| 이제 정리하자 / 오늘은 여기까지 | 대화형 |
| 끝내자 / 마치자 | 간단형 |
| 오늘 끝 / 오늘 작업 끝 | 종료형 |
| 커밋할거 있어 / 뭐 기록해야해 | 질문형 |
| 랩 / 랩업 | 영어 축약 |

### 영어
- `wrap up session`
- `end session`
- `session wrap`

## 동작 방식

### Phase 1: 병렬 분석 (4개 에이전트)

| 에이전트 | 역할 |
|----------|------|
| `doc-updater` | CLAUDE.md, context.md에 추가할 내용 제안 |
| `automation-scout` | 반복 패턴을 skill/command/agent로 자동화할 기회 탐지 |
| `learning-extractor` | 배운 것, 실수한 것, 새로 발견한 것 추출 |
| `followup-suggester` | 미완성 작업, 다음 세션 우선순위 정리 |

4개 에이전트가 **동시에** 실행됩니다.

### Phase 2: 중복 검증 (1개 에이전트)

| 에이전트 | 역할 |
|----------|------|
| `duplicate-checker` | Phase 1 결과가 기존 문서와 중복되는지 검증 |

### Phase 3: 사용자 선택

분석 끝나면 선택지를 줍니다:

- [ ] 변경사항 커밋
- [ ] CLAUDE.md 업데이트
- [ ] 자동화 생성
- [ ] 배운 것 저장
- [ ] 후속 작업 저장

## 플러그인 구조

```
session-wrap/
├── .claude/
│   ├── agents/
│   │   ├── doc-updater.md        # 문서 업데이트 제안
│   │   ├── automation-scout.md   # 자동화 기회 탐지
│   │   ├── learning-extractor.md # 배운 것 추출
│   │   ├── followup-suggester.md # 다음 할 일 제안
│   │   └── duplicate-checker.md  # 중복 검증
│   ├── commands/
│   │   └── wrap.md               # /wrap 스킬 정의
│   └── settings.json             # 플러그인 설정
└── README.md
```

## 왜 좋은가요?

1. **CLAUDE.md가 자연스럽게 풍부해집니다**
   - 매번 "이건 기록해야지" 하고 까먹었던 것들이 차곡차곡 쌓입니다

2. **자동화 아이디어를 놓치지 않습니다**
   - 반복 패턴을 발견하면 알려줍니다

3. **다음 세션 시작이 빨라집니다**
   - 뭘 해야 하는지 이미 정리되어 있습니다

4. **배운 것이 사라지지 않습니다**
   - TIL 형식으로 기록됩니다

## 출력 예시

```
## 세션 마무리 완료

### 문서 업데이트
- CLAUDE.md에 3개 제안

### 자동화 기회
- 2개 잠재적 자동화 발견

### 배운 것
- 4개 TIL 추출

### 후속 작업
- 다음 세션에 5개 작업

무엇을 할까요?
```

## License

MIT
