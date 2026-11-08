# CDC Milestone Tracker — 기술·안전·문제 해결 분석

## 1. 공개 기술 현황

현재 제품의 공식 소스구조는 공개 확인하지 못했다. [U]

제품적 기준은 기술스택보다 **안전 경계와 data minimization**에 있다.

## 2. 개념 데이터 모델

[C]

```
Child
MilestoneDefinition
├─ age
├─ domain
├─ observable_text
└─ media_example

MilestoneObservation
Concern
Appointment
WellVisitSnapshot
SummaryExport
```

## 3. 얽힌 문제 — 부모가 행동 문장을 다르게 해석

사진/영상 예시로 관찰 기준을 좁힌다.

이는 UI 장식이 아니라 **data quality control**이다.

## 4. 얽힌 문제 — 못한 항목을 진단처럼 오해

앱이 monitoring임을 반복 표시하고 standardized screening과 분리한다.

## 5. 얽힌 문제 — 기록이 진료실에서 쓸모없음

PDF/email summary로 의료진이 소비 가능한 형식으로 바꾼다.

## 6. Privacy

공식 설명상 personally identifying information을 CDC가 수집/공유하지 않는다고 안내한다.

민간앱이 모든 데이터를 서버에 저장할 필요가 있는지 다시 생각하게 하는 기준이다.

## 7. 한국 적용

```
일상 milestone monitoring
→ K-DST
→ 의료진 평가
```

세 단계를 절대 하나의 점수로 합치지 않는다.

## 8. 우리 시스템에 일반화

- 관찰 예시
- concern escalation
- doctor-ready summary
- screening boundary
- 최소수집

을 발달 모듈의 안전 기본값으로 둔다.
