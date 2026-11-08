# Napper — 기술·데이터·문제 해결 분석

## 1. 공개 기술 현황

내부 소스/DB는 공개 확인하지 못했다. [U]

공식 Privacy에서 확인되는 것은 다음 데이터 범주다. [A2]

- account data
- sleep
- feeding
- diaper
- pumping
- device/usage data
- IP 기반 대략 위치

AI personalization에 아기 나이·수면·수유·기저귀·체온 등의 정보가 사용될 수 있다.

## 2. 개념 데이터 모델

[C]

```
Baby
SleepEvent
├─ start
├─ end
└─ duration

WakeWindow
Prediction
├─ predicted_at
├─ based_on
└─ confidence/range

Schedule
Reminder
```

## 3. Raw와 Prediction 분리

가장 중요하다.

```
SleepEvent = 실제
Prediction = 모델 출력
```

예측을 실제기록으로 덮어쓰면 안 된다.

## 4. 얽힌 문제 — 데이터가 없으면 예측 불가

Cold start 해결:
- age-based default

데이터 축적 후:
- personalized model

## 5. 얽힌 문제 — 예측이 틀릴 수 있음

prediction은 feedback을 받아야 한다.

```
Predicted
→ Actual
→ Error
→ Recalibration
```

이 구조가 있어야 장기 개인화가 가능하다.

## 6. AI 개인정보

공식 정책상 외부 LLM technology provider 예시가 공개되어 있다.

따라서 AI 시스템에는:
- 전송 필드 최소화
- 목적별 consent
- retention 설명
- delete/export
- high-risk data 제한

이 필요하다.

## 7. 수면 특수상황

일반 모델이 잘 작동하지 않을 수 있는 상황:
- 질병
- 여행
- 시차
- 수면환경 변화
- 성장 변화

이때 prediction을 자동 정답처럼 유지하면 안 된다.

## 8. 우리 시스템에 일반화

```
Age Baseline
+
Observed Events
→ Personal Pattern
→ Prediction Range
→ Preparation Action
→ Actual Feedback
```

prediction engine의 좋은 기본형이다.
