# 영유아 건강검진 — 기술·의료경계·문제 해결 분석

## 1. 핵심 엔터티

[C]

```
CheckupRoundDefinition
├─ eligible_age
├─ questionnaire
├─ screening_required
└─ education_topics

ChildEligibility
QuestionnaireResponse
KDSTResult
ClinicalMeasurement
CheckupResult
Referral
FollowUpTask
```

## 2. 데이터 경계

절대 합치지 않는다.

```
Parent Observation
≠
Official Questionnaire
≠
K-DST Result
≠
Clinician Assessment
```

source type이 중요하다.

## 3. 얽힌 문제 — 평소 기록과 검진은 따로 존재

민간앱의 좋은 역할:

```
Daily Care Data
→ Doctor-ready Summary
→ Official Questionnaire Link
→ Visit
```

공식 검사를 대체하지 않고 **준비 비용을 줄인다.**

## 4. 얽힌 문제 — 검진 후 할 일을 잊음

Result를 archive만 하면 follow-up이 끊긴다.

```
Result
→ Referral
→ Appointment
→ Follow-up Task
→ Completion
```

으로 task system과 연결해야 한다.

## 5. Eligibility

검진은 항상 가능한 것이 아니라 차수별 대상기간이 있다.

따라서 schedule은 단일 D-day보다:
- window start
- window end
- status

가 중요하다.

## 6. 부모 질문 Inbox

일상에서 생긴:
- 수면
- 식사
- 배변
- 발달
- 행동

질문을 진료 전까지 저장해 두고 검진 화면에서 모아주는 기능의 가치가 크다.

## 7. 우리 시스템에 일반화

민간 육아앱의 의료모듈은 진단엔진보다 **공식 검진으로 잘 넘기는 handoff layer**가 되는 편이 안전하고 실용적이다.
