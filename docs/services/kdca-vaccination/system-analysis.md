# 예방접종도우미 — 기술·규칙엔진·문제 해결 분석

## 1. 핵심 데이터 분리

절대 합치지 말아야 한다.

```
ScheduleDefinition
≠
VaccinationRecord
```

### Definition
- vaccine
- dose
- age/window
- eligibility
- authority
- effective_from/to
- reviewed_at

### Actual
- child
- vaccine/dose
- administered_at
- provider
- source

## 2. Versioning

[A1]

국가사업 페이지에 최종검토일이 명시된다.

일정 시스템에는:
- source version
- last reviewed
- effective period

가 필수다.

## 3. Routine vs Seasonal

```
RoutineSchedule
SeasonalCampaign
```

인플루엔자는 사업기간과 이전 접종력에 따라 횟수가 달라질 수 있어 일반 schedule row와 다른 rule engine이 필요하다.

## 4. 얽힌 문제 — 지연/누락/예외

민간앱이 임의로 catch-up schedule을 확정해서는 안 된다.

```
Rule applies?
├─ yes → upcoming
└─ special/uncertain → official guidance / clinician
```

## 5. 알림

Reminder는:
- scheduled due
- official consent
- channel
- contact
- completion

과 연결된다.

접종완료가 확인되면 잘못된 알림을 멈춰야 한다.

## 6. Provider

일정 엔진과 기관검색을 연결해야 complete loop가 된다.

```
Eligible
→ Reminder
→ Find Provider
→ Visit
→ Actual Record
→ Next Dose
```

## 7. 우리 시스템에 일반화

공식 일정은 콘텐츠가 아니라 **버전 관리되는 규칙 데이터**로 다뤄야 한다.
