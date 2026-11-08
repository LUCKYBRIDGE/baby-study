# 페이지·UI·UX·버튼 비교 매트릭스

## 1. 핵심 홈의 목적

| 서비스 | 홈이 답하는 질문 | 대표 UI |
|---|---|---|
| BabyTime | 방금 무엇을 했나? 마지막 기록은? | 활동 아이콘 + 오늘 기록 |
| Huckleberry | 지금 상태와 다음 수면은? | tracker + timer + prediction |
| Napper | 다음 낮잠/취침은 언제? | next sleep 중심 dashboard |
| MOMI | 손 안 쓰고 기록하려면? | 마이크 + 빠른 기록 |
| Kinedu | 오늘 무엇을 해줄까? | daily activity |
| BabySparks | 오늘의 발달 프로그램은? | daily program |
| Pathways | 오늘 무엇을 관찰/놀이할까? | Today cards |
| Solid Starts | 이 음식을 어떻게 줄까? | food search |
| FamilyAlbum | 오늘 가족에게 무엇을 공유했나? | media timeline |
| 베이비빌리 | 지금 시기에 무엇을 알아야 하나? | stage feed |
| 마미톡 | 임신/육아 현재 상태는? | ultrasound/stage/tracker |
| CDC | 지금 확인할 milestone은? | illustrated checklist |
| 아이사랑 | 이 월령에 무엇을 알아야 하나? | age taxonomy |
| 예방접종도우미 | 다음 공식 접종은? | schedule/record/provider |
| NHIS | 검진을 어떻게 준비하지? | eligibility/questionnaire |

## 2. 빠른 기록 버튼

### 가장 강한 사례
**BabyTime**
- 아이콘 탭 즉시 이벤트 생성
- 상세는 나중

**MOMI**
- 음성 + 직접버튼 hybrid

**Huckleberry**
- domain별 timer/instant interaction

### 설계 결론

모든 domain에 같은 버튼을 쓰지 않는다.

```
Instant
├─ diaper
├─ medicine complete
└─ temperature

Timer
├─ sleep
├─ nursing
└─ pumping

Structured
├─ growth
├─ medication dose
└─ allergen reaction

Natural Language
└─ catch-up / multi-event
```

## 3. 대표 버튼/행동 패턴

| 패턴 | 서비스 | 의미 |
|---|---|---|
| 한 번 탭해 즉시 생성 | BabyTime | capture 우선 |
| Start/Pause/Resume/Complete | Huckleberry | 상태형 timer |
| 마이크 → 확인 → 저장 | MOMI | AI 입력 안전장치 |
| Search food | Solid Starts | 객체 중심 진입 |
| I see this / Not yet / Not sure | Kinedu | 불확실성 허용 |
| Not Started / Making Progress / Achieved | Pathways | 연속적 발달상태 |
| Admin/Member permission | FamilyAlbum | 역할 기반 공유 |
| Find provider | KDCA/NHIS | 정보→행동 연결 |
| PDF/Email summary | CDC | 앱→의료진 handoff |

## 4. 탐색 UI

### Fixed taxonomy
- 아이사랑
- Pathways

사용자가 메뉴 위치를 학습하기 쉽다.

### Adaptive home
- 베이비빌리
- Huckleberry
- Kinedu

시기/상태에 따라 우선순위가 달라진다.

### Object search
- Solid Starts

현재 손에 든 객체가 entry point다.

## 5. Progressive Disclosure

좋은 사례:
- BabyTime: 기록 먼저, detail later
- Solid Starts: 검색 결과 → age-specific detail
- Kinedu: 3문항 preview → 전체 assessment
- CDC: checklist → concern guide
- KDCA: 현재 일정 → 공식 상세

## 6. Dashboard 종류

| Dashboard | 대표 |
|---|---|
| Current State | BabyTime, Huckleberry |
| Prediction | Napper, Huckleberry |
| Development Progress | Kinedu, Pathways |
| Age Context | 베이비빌리 |
| Memory | FamilyAlbum |
| Official Schedule | KDCA |
| Clinical Preparation | NHIS |

## 7. 우리가 참고할 UI 조합

신생아기 홈:

```
[마지막 수유] [현재 수면] [마지막 기저귀]
[수유] [수면 시작] [기저귀] [말로 기록]
오늘 타임라인
다음 공식 일정
```

발달/이유식기:

```
오늘 할 것
├─ 추천 놀이
├─ 다음 음식
└─ 검진/접종

빠른 기록
오늘의 변화
```

기능을 모두 보여주지 않고 월령에 따라 home composition을 바꾼다.
