# BabyTime — 기술·데이터·문제 해결 분석

## 1. 공개 기술 현황

공식 제품 소스코드와 내부 기술스택은 공개 확인하지 못했다. [U]

확인 가능한 것은 제품의 기능적 계약이다.

- 다기기/다양육자 동기화 [A1/A2]
- 클라우드 기반 데이터 보관/백업 성격 [A1/A2]
- PDF 등 데이터 출력 기능 [A2]
- 다자녀 context [A2]

따라서 DB나 framework를 특정하지 않는다.

## 2. 필요한 핵심 엔터티

[C]

```
Baby
Caregiver
ActivityEvent
├─ type
├─ started_at
├─ ended_at
├─ amount/details
└─ note

GrowthMeasurement
DiaryEntry
Media
CaregiverMembership
```

## 3. Raw / Derived 구분

### Raw
- 개별 수유
- 개별 수면
- 개별 기저귀
- 성장 측정

### Derived
- 마지막 수유
- 평균 수유간격
- 하루 총 수면
- 주간 평균
- 활동 간 interval

좋은 구현은 Derived를 사용자가 다시 입력하게 하지 않고 Raw에서 계산해야 한다.

## 4. 얽힌 문제 1 — 빠른 기록 vs 정확한 기록

둘은 충돌한다.

정확성을 높이려고 첫 화면에서 모든 필드를 받으면 기록 누락이 늘어난다.

BabyTime식 해법:

```
minimal event first
→ optional correction/detail later
```

## 5. 얽힌 문제 2 — 데이터가 많아질수록 화면이 복잡해짐

모든 이벤트를 동시에 보여주면 timeline이 읽히지 않는다.

해법:
- 활동 toggle
- Pattern과 Stats 분리
- graph 선택/재정렬

즉 **데이터를 줄이지 않고 view를 줄인다.**

## 6. 얽힌 문제 3 — 여러 양육자의 기억 불일치

채팅으로 인계하면:
- 읽지 않을 수 있음
- 시각이 불명확
- 같은 질문 반복

BabyTime은 공유 상태를 source of truth로 둔다.

```
Caregiver action
→ Baby record
→ everyone sees same state
```

## 7. 공동양육 모델

Baby 중심 멤버십에 가깝다.

```
Baby
├─ caregiver(role=mom)
├─ caregiver(role=dad)
└─ caregiver(role=babysitter)
```

향후 의료데이터까지 다루려면:
- read
- write
- edit/delete
- health-only
- media-only

권한이 더 필요하다.

## 8. 알림·예측

공개 근거상 핵심 제품 정체성은 prediction보다 logging/understanding에 있다.

따라서 BabyTime에서 가져올 것은 **ground-truth layer**이고, 예측층은 다른 서비스 패턴과 결합하는 편이 낫다.

## 9. 데이터 이식성

장기간 아기 기록은 lock-in 위험이 크다.

필요 원칙:
- export
- backup
- restore
- child별 export
- media와 structured data 분리

## 10. 우리 시스템에 일반화

```
Event Store
→ Current Baby State
→ Timeline
→ Interval View
→ Aggregate View
```

이 다섯 층을 분리하는 것이 핵심이다.

AI보다 먼저 이 구조가 안정되어야 한다.
