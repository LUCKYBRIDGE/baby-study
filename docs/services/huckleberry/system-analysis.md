# Huckleberry — 기술·데이터·공개 저장소 분석

> 아래 기술 세부는 공식 제품 소스가 아니라 공개 비공식 구현 [B2]에서 관찰한 내용이다.

## 1. 실제 확인한 공개 저장소 구조

### py-huckleberry-api

```
src/huckleberry_api/
├─ api.py
├─ const.py
├─ firebase_types.py
└─ models.py

tests/
├─ test_sleep.py
├─ test_feeding.py
├─ test_bottle_feeding.py
├─ test_diaper.py
├─ test_growth.py
├─ test_medicine.py
├─ test_temperature.py
├─ test_pump.py
├─ test_solids.py
├─ test_activity.py
├─ test_listeners.py
├─ test_timezone.py
└─ test_write_failures.py
```

특히 `firebase_types.py`를 schema reference로 관리한다.

## 2. 관찰된 데이터 path

```
users/{uid}
childs/{child_id}
types/{child_id}

sleep/{child_id}
feed/{child_id}
diaper/{child_id}
health/{child_id}
pump/{child_id}
activities/{child_id}
```

## 3. Current state와 History 분리

가장 중요한 구조다.

예:

```
sleep/{child}
├─ timer
├─ prefs.lastSleep
└─ intervals/{...}
```

홈이 "마지막 수면"을 보여주기 위해 history 전체를 다시 계산할 필요가 없다.

### 일반화
```
Event Store
→ Projection(last/current)
```

## 4. Feed의 polymorphic model

```
FeedEvent
├─ breast
├─ bottle
└─ solids
```

공통:
- start
- offset
- note

mode별:
- nursing: left/right duration
- bottle: type/amount/unit
- solids: food/reaction

새 domain을 만드는 대신 상위 개념 안에서 mode를 확장한다.

## 5. Instant vs Timer Event

### Timer
- sleep
- nursing
- pump
- 일부 activity

### Instant
- diaper
- bottle
- temperature
- medication
- growth

모든 기록에 동일 timer UX를 강요하지 않는다.

## 6. Reminder model

공개 schema에는:
- 특정 시각
- 일정 시간 후
- 요일
- 낮시간만
- sound
- vibration

을 가진 reminder 형태가 보인다.

즉 reminder는 event history가 아니라 **domain preference**다.

## 7. Realtime

Home Assistant와 API client에서 Firestore snapshot listener 기반 동기화가 관찰된다.

```
Write
→ Firestore
→ Snapshot
→ Other consumer
```

현재 상태 공유와 home automation에 적합하다.

## 8. 외부 활용 생태계

### Home Assistant
current state를 sensor, history를 calendar로 투영.

### MCP
domain action을 AI tool로 노출.

### CLI
복잡한 UI를 명령형 verb로 단순화.

### baby-tracker
CSV export를 받아 SQL dashboard로 분석.

이것은 좋은 데이터 시스템이 **여러 presentation layer**를 가질 수 있음을 보여준다.

## 9. 얽힌 문제 — prediction과 실제의 차이

SweetSpot 같은 prediction은 반드시:
- observed actual
- prediction
- user adjustment

를 분리해야 한다.

```
PredictedNap
≠
SleepEvent
```

## 10. 얽힌 문제 — 동기화와 작성자 identity

실시간 공유는 쉽지만 shared account 방식은:
- 누가 수정했는가
- 누가 약을 줬는가
- 누가 삭제했는가

를 약하게 만든다.

고위험 domain에서는 audit metadata가 필요하다.

## 11. 가져올 구조

```
Baby
├─ Domain state projections
├─ Active timers
├─ Historical events
├─ Reminders
└─ Intelligence outputs
```

이 구조는 독립적인 육아앱을 설계할 때 가장 참고 가치가 크다.

## 12. 주의

비공식 API endpoint나 private backend에 의존하는 구현은 만들지 않는다. 참고 대상은 **아키텍처 패턴**이지 비공개 인터페이스 자체가 아니다.
