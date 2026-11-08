# MOMI — 기술·AI·문제 해결 분석

## 1. 공개 기술 현황

내부 source/backend/LLM provider는 공식 스토어 정보만으로 확정하지 않는다. [U]

공식적으로 확인되는 것은 AI가 음성/텍스트를 분석해 구조화된 기록을 만든다는 사용자 기능이다.

## 2. 권장 AI pipeline

[C]

```
Audio
→ Speech Transcript
→ Event Extraction
→ Candidate Events
→ Validation
→ User Confirmation
→ Event Store
```

각 단계의 데이터를 분리해야 한다.

## 3. 데이터 계층

```
Raw Audio?
Transcript
ParsedCandidate
ConfirmedEvent
AI Summary
Diary
```

가능하면 Raw Audio는 목적 달성 후 최소 보관 원칙을 적용한다.

## 4. 얽힌 문제 — 편리함 vs 정확성

AI가 자동저장하면 빠르지만 오류가 ground truth에 들어간다.

해법:
`Candidate → Confirm`

## 5. 얽힌 문제 — 한 문장에 여러 사건

parser가 event array를 반환해야 한다.

각 event는 독립 수정/삭제가 가능해야 한다.

## 6. 얽힌 문제 — 고위험 데이터

약, 체온, 알레르기, 예방접종 완료는:
- 음성 인식
- 자연어 parsing

두 단계 오류가 있을 수 있다.

따라서:
- 단위 강제 확인
- 약명 확인
- 완료 여부 명시 확인

이 필요하다.

## 7. AI Q&A

기록질문과 건강질문은 tool policy가 달라야 한다.

### 기록질문
ground-truth event store 조회.

### 건강질문
공식 source / 의료전문가 escalation.

## 8. Derived Content

AI 일기/월간 리포트는 파생데이터다.

원자료 삭제 시:
- summary 재생성
- 파생결과 삭제
- lineage 추적

정책이 필요하다.

## 9. 우리 시스템에 일반화

AI는 데이터베이스가 아니다.

```
AI
= Capture Adapter
+ Query Adapter
+ Summary Adapter
```

ground truth는 별도 event store에 있어야 한다.
