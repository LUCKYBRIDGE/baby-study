# Huckleberry — 공식 사이트 + 공개 서드파티 저장소 직접 관찰

> 관찰일: 2026-11-08  
> 공식 사이트: A1  
> 공개 GitHub: B2 — 비공식 reverse-engineered 구현

## 1. 공식 사이트에서 실제로 확인되는 제품 계층

### Free
- sleep/feed/diaper 등 빠른 기록
- reports
- multi-device caregiver sync
- growing child에 따라 Home Screen 조정

### Plus
- SweetSpot 수면 예측
- Insights
- Schedule Creator
- AI logging
- lock-screen live updates
- Enhanced Reports
- Widgets/Apple Watch(iOS)

### Premium
- Plus 전체
- Berry AI parenting guidance
- expert-designed personalized sleep plan

제품 구조는 매우 선명합니다.

```
Free
Ground-truth logging

Plus
Prediction + friction reduction + advanced analysis

Premium
Problem-solving guidance
```

## 2. 공식 사이트상 caregiver 구조

공식 FAQ는 여러 caregiver가 **같은 계정으로 각 기기에 로그인**한다고 설명합니다.

즉:

```
Account
├─ Device A
├─ Device B
└─ Baby data
```

BabyTime처럼 caregiver별 관계/계정을 연결하는 workspace 모델과 다릅니다.

### 장점
- 초대 UX 단순
- sync 구현 단순

### 한계
- 누가 기록했는지 identity 약함
- 역할별 권한 어려움
- 비밀번호 공유 모델

## 3. 공식 tracking IA

Tracking 페이지의 메시지는:
- timers
- smart reminders
- caregiver sync
- hide what you do not need

입니다.

따라서 홈은 **모든 카테고리 고정 노출**이 아니라 사용자 선택형 tracker입니다.

## 4. 공개 비공식 저장소에서 확인되는 기술 구조

중요: 아래는 Huckleberry 공식 개발문서가 아닙니다.

공개 저장소:
- `Woyken/py-huckleberry-api`
- `Woyken/huckleberry-homeassistant`
- `bckenstler/py-huckleberry-mcp`
- `jayhickey/huckleberry-cli`

여러 독립 구현이 비슷한 데이터 구조를 다루는 점은 기술적 관찰 가치가 있습니다.

## 5. 공개 코드상 최상위 데이터 구조

`py-huckleberry-api`의 strict schema 기준:

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

### users
- childList
- lastChild
- subscription
- timezone
- onboarding 상태 등

### childs
- name
- birthdate
- gender
- nightStart
- morningCutoff
- naps
- categories
- SweetSpot 관련 데이터
- questionnaire progress

즉 user identity와 child state가 분리됩니다.

## 6. 반복되는 domain collection 패턴

여러 collection이 거의 공통 형태를 갖습니다.

```
<domain>/{child}
├─ timer
├─ prefs
│  ├─ last*
│  ├─ reminder
│  └─ timestamp
└─ intervals/ or data/
   └─ historical events
```

이는 상당히 좋은 실시간 육아 기록 패턴입니다.

### root document
"지금"과 "마지막 상태"에 최적화.

### subcollection
과거 이력 조회/통계에 최적화.

즉:

```
Fast current-state read
+
Append-style history
```

를 분리합니다.

## 7. sleep 구조

공개 schema에서 확인되는 항목:
- timer active/paused
- start/end
- details
- sleep location
- 시작/종료 컨디션
- notes
- SweetSpot analytics
- prefs.lastSleep

과거 수면은:
`sleep/{child}/intervals`
에 별도로 저장됩니다.

즉 현재 진행중 sleep timer와 완료된 sleep event를 **별도 상태**로 둡니다.

## 8. feed 구조

feed root 아래에서:
- nursing
- bottle
- solids

를 같은 feed domain의 서로 다른 mode로 취급합니다.

### nursing
- left/right duration
- last side

### bottle
- type
- amount
- units

### solids
- foods map
- reaction
  - LOVED
  - MEH
  - HATED
  - ALLERGIC
- notes

즉 feed를 화면상 카테고리가 아니라 **polymorphic event type**으로 설계한 셈입니다.

## 9. solids DB 구조

비공식 공개 schema에서는:
- curated food DB는 Firebase Storage
- custom food는 `types/{child}/custom/{food_id}`

형태로 구분됩니다.

이 패턴은 좋습니다.

```
Global curated catalog
+
Child-specific custom catalog
+
Personal event history
```

Solid Starts류 음식 DB와 결합할 때도 유용합니다.

## 10. diaper 구조

instant event이며 timer가 아닙니다.

- pee / poo / both / dry
- quantity
- color
- consistency
- diaper rash
- potty 여부
- potty result

즉 도메인별로 timer abstraction을 강제하지 않습니다.

## 11. health 구조

`health/{child}`에서:
- growth
- medication
- temperature

를 같은 health domain의 mode로 취급합니다.

### Medication
별도 selectable medication type이 존재하고 실제 복용 이력이 연결됩니다.

### Temperature
최신 상태가 prefs에 있고 history는 data에 존재합니다.

### Growth
height/weight/head circumference가 하나의 measurement event입니다.

## 12. activity 구조

확인되는 activity mode:
- bath
- tummyTime
- storyTime
- screenTime
- skinToSkin
- outdoorPlay
- indoorPlay
- brushTeeth

각 activity는 동일한 timer/event skeleton을 공유합니다.

즉 새 활동을 추가하기 쉬운 **mode-based extensible tracker** 구조입니다.

## 13. reminder 구조

feed/diaper/health/pump 등에 `reminderV2`가 있고:
- 특정 시각(at)
- 일정 시간 후(in)
- 요일
- daytime only
- sound
- vibration

등의 속성이 있습니다.

즉 reminder를 event 자체와 분리하면서 **domain prefs에 붙이는 방식**입니다.

## 14. 실시간 동기화

Home Assistant integration과 API client 모두 Firestore snapshot listener를 사용합니다.

실시간 UI 관점에서:

```
Write Event
→ Firebase
→ Snapshot Listener
→ Other device state update
```

구조가 가능합니다.

공식 사이트의 caregiver sync 메시지와 기술적으로 잘 맞습니다.

## 15. batch/history 저장 관찰

공개 코드에는 `multi`, `hasMoreRoom`, `data` 형태의 batched wrapper가 존재합니다.

즉 오래된 이벤트를 document 하나씩 무한 증식시키기보다 일부 history를 묶어 저장하는 최적화가 관찰됩니다.

이는 Firestore 비용/문서 수 관리와 연관된 설계로 추정할 수 있습니다.

## 16. 공개 export 생태계

`archiewood/baby-tracker`는 Huckleberry가 이메일로 전달하는 CSV export를 자동 다운로드해:
- sleep
- feed
- diaper
- growth
- tummy time

을 별도 dashboard로 가공합니다.

즉 Huckleberry에는 외부 분석 가능한 **CSV export 경로가 실제 사용되고 있음**을 간접 확인할 수 있습니다.

## 17. 직접 관찰로 얻은 가장 큰 시사점

Huckleberry는 UI 기능이 많아 보여도 기술적으로는:

```
Child
+
Domain Current State
+
Domain Historical Events
+
Derived Intelligence
```

의 구조로 이해하면 단순합니다.

특히:
- 현재 timer
- 마지막 상태
- 과거 interval

을 분리한 점은 향후 육아 기록 서비스 데이터 모델에 그대로 참고할 가치가 큽니다.

## 18. 주의

공개 저장소의 reverse engineering 결과는:
- 공식 API 계약이 아님
- 언제든 변경 가능
- 일부 필드가 추정일 수 있음

따라서 이를 그대로 복제하거나 비공개 API에 의존하는 구현은 권장하지 않습니다.

연구 목적은 **제품 구조를 이해하는 것**입니다.

## 19. 참고

공식:
- https://huckleberrycare.com/product/tracking
- https://huckleberrycare.com/product/free
- https://huckleberrycare.com/product/plus
- https://huckleberrycare.com/product/premium

공개 비공식 저장소:
- https://github.com/Woyken/py-huckleberry-api
- https://github.com/Woyken/huckleberry-homeassistant
- https://github.com/bckenstler/py-huckleberry-mcp
- https://github.com/jayhickey/huckleberry-cli
- https://github.com/archiewood/baby-tracker
