# 육아 앱·웹 아키텍처 비교 지도

> 기능표보다 한 단계 깊게, 각 서비스가 **어떤 입력을 받아 무엇으로 변환하고 어떤 행동을 만드는가**를 비교한다.

# 1. 서비스별 핵심 변환

| 서비스 | Input | Internal Transformation | Output / Action |
|---|---|---|---|
| BabyTime | 육아 이벤트 | 타임라인·간격·집계 | 현재 상태/패턴 |
| Huckleberry | 육아 이벤트 | 추세·SweetSpot·Insights | 다음 수면/계획 |
| Napper | 수면 이벤트 | wake window·개인화 | 다음 낮잠/취침 |
| MOMI | 자연어/음성 | AI 구조화 | 이벤트 기록 |
| Kinedu | 발달 관찰 | skill model | 오늘 활동 |
| BabySparks | 나이/진도 | activity curriculum | 일일 프로그램 |
| Pathways | 행동 체크 | 영역별 progress | 관련 정보/활동 |
| CDC | milestone 체크 | concern detection | 의료진 대화 준비 |
| Solid Starts | 음식/월령 | 전문가 DB + 개인이력 | 제공방법/다음 음식 |
| FamilyAlbum | 사진/영상 | 연령 정리·권한·자동편집 | 가족 공유/회고 |
| 베이비빌리 | 주수/월령 | 콘텐츠·커뮤니티 큐레이션 | 오늘 필요한 정보 |
| 마미톡 | 병원 초음파/주수 | 의료접점+생애주기 | 정보/커뮤니티/육아 |
| 아이사랑 | 월령/행정수요 | 공식 taxonomy/행정 | 정보·어린이집·결제 |
| 예방접종도우미 | 생년월일/기록 | 공식 접종 규칙 | 일정·알림·기관 |
| 영유아검진 | 월령/문진 | 국가 screening protocol | 결과·교육·의뢰 |

---

# 2. 제품 아키타입

## A. Event Logger
대표: BabyTime

```
Event
→ Store
→ Timeline
→ Aggregate
```

가장 안정적인 기반층.

## B. Predictive Assistant
대표: Huckleberry, Napper

```
Event History
→ Pattern Model
→ Prediction
→ Reminder
→ Feedback
```

기록 데이터가 충분할수록 가치가 커진다.

## C. AI Capture Layer
대표: MOMI, Huckleberry AI logging

```
Natural Language
→ Parse
→ Candidate
→ User Confirm
→ Event
```

기존 기록 시스템 위에 붙는 입력 어댑터다.

## D. Development Recommendation Engine
대표: Kinedu

```
Observation
→ Child Skill Model
→ Next Best Activity
→ Observation
```

교육용 adaptive system과 유사하다.

## E. Structured Knowledge Graph
대표: Pathways, Solid Starts

```
Object / Behavior
→ Expert Knowledge
→ Age Context
→ Action
```

검색과 실행을 강하게 연결한다.

## F. Memory Platform
대표: FamilyAlbum

```
Media
→ Age-relative Archive
→ Family Interaction
→ Automated Recap
```

즉시 utility보다 장기 감정가치가 핵심.

## G. Lifecycle Super-app
대표: 베이비빌리, 마미톡

```
Age/Stage
→ Module Priority
→ Feed/Community/Commerce
```

기능 수보다 orchestration이 중요하다.

## H. Authoritative Public System
대표: 예방접종도우미, NHIS, 아이사랑

```
Policy / Guideline
→ Eligibility
→ Official Action
```

정확성·최신성·제도 연결이 핵심.

---

# 3. 한 앱으로 통합할 때의 권장 계층

```
┌─────────────────────────────┐
│ Experience Orchestration    │
│ 주수/월령/현재상태 기반 홈   │
└──────────────┬──────────────┘
               │
┌──────────────▼──────────────┐
│ Action Layer                │
│ 다음 수유/수면/검진/놀이     │
└──────────────┬──────────────┘
               │
┌──────────────▼──────────────┐
│ Intelligence Layer          │
│ 패턴·예측·추천·AI            │
└──────────────┬──────────────┘
               │
┌──────────────▼──────────────┐
│ Domain Modules              │
│ 수유 수면 발달 이유식 건강   │
└──────────────┬──────────────┘
               │
┌──────────────▼──────────────┐
│ Shared Baby Event Store     │
│ 시간기반 원자료              │
└──────────────┬──────────────┘
               │
┌──────────────▼──────────────┐
│ Identity / Permission       │
│ 아기·부모·가족·돌봄자        │
└─────────────────────────────┘
```

공공 데이터는 Domain/Intelligence가 아니라 **authoritative reference layer**로 별도 관리한다.

---

# 4. 핵심 엔터티

```
Baby
Caregiver
Event
├─ Feeding
├─ Sleep
├─ Diaper
├─ Health
├─ Medication
└─ Activity

Measurement
ScheduleDefinition
ScheduledTask
ActualCompletion
MilestoneDefinition
MilestoneObservation
Food
FoodExposure
Media
ClinicalVisit
SourceReference
Prediction
Recommendation
```

## 절대 합치지 말아야 할 데이터

- 예정 vs 실제
- 사용자 관찰 vs 의료진 판단
- raw record vs AI 추론
- prediction vs actual
- 공식 기준 vs 개인 이력
- 가족 사진 권한 vs 의료정보 권한

---

# 5. 정보구조를 월령별로 바꾸는 방법

## 출생~3개월

```
HOME
├─ 현재 수면
├─ 마지막 수유
├─ 기저귀
├─ 오늘 체온/증상
└─ 검진/접종
```

## 4~6개월

```
HOME
├─ 수면/수유
├─ 성장
├─ 터미타임/발달
├─ 이유식 준비
└─ 접종
```

## 7~12개월

```
HOME
├─ 이유식/음식
├─ 수면
├─ 이동 발달
├─ 안전
└─ 검진
```

## 12~24개월

```
HOME
├─ 언어/발달
├─ 식사
├─ 놀이
├─ 생활습관
└─ 검진/치아
```

고정 탭에 기능을 추가하는 것보다 **home orchestration**이 중요하다.

---

# 6. 입력 UX 계층

## Level 1 — One Tap
기저귀, 약 완료, 간단 이벤트.

## Level 2 — Timer
수면, 수유, 유축, tummy time.

## Level 3 — Natural Language
여러 이벤트 catch-up, 메모.

## Level 4 — Structured Form
체온, 약 용량, 성장, 알레르기 반응.

고위험 데이터일수록 자유형 AI보다 structured confirmation이 강해야 한다.

---

# 7. 알림 분류

모든 알림을 같은 시스템으로 처리하지 않는다.

| 알림 | 특징 | 예 |
|---|---|---|
| Due | 놓치면 비용 큼 | 예방접종/검진 |
| Interval | 최근 기록 기반 | 수유/약 |
| Prediction | 모델 기반 | 낮잠 |
| Routine | 사용자 지정 | 양치/목욕 |
| Content | 정보성 | 월령 팁 |
| Social | 관계 | 가족 댓글 |
| Marketing | 서비스 목적 | 쇼핑/구독 |

사용자는 알림 종류별로 별도 제어할 수 있어야 한다.

---

# 8. 제품 우선순위

## P0 — 신뢰 가능한 기반
- Baby profile
- Caregiver
- Event log
- One-tap/timer
- Shared state
- Backup/export
- 공식 일정 link

## P1 — 일상 이해
- Timeline
- Daily summary
- Trend
- Growth
- Checkup/vaccination

## P2 — 행동 지원
- Sleep prediction
- Development activities
- Food exposure
- Doctor-ready summary

## P3 — AI
- Voice/text logging
- Record Q&A
- Summarization

## P4 — 확장
- Community
- Memory automation
- Commerce

AI를 먼저 만들기보다 **ground-truth event store**가 먼저다.

---

# 9. 좋은 서비스가 반복적으로 푼 문제

## "언제 했지?"
BabyTime/Huckleberry

## "다음에는 언제 하지?"
Huckleberry/Napper

## "지금 뭘 해주지?"
Kinedu/BabySparks

## "이 행동은 정상적으로 어떻게 보이지?"
Pathways/CDC

## "이 음식은 어떻게 주지?"
Solid Starts

## "가족에게 어떻게 보여주지?"
FamilyAlbum

## "지금 시기에 뭘 알아야 하지?"
BabyBilly/아이사랑

## "공식적으로 언제 해야 하지?"
KDCA/NHIS

---

# 10. 최종 관점

가장 좋은 통합 육아 서비스는 기능을 많이 넣은 앱이 아니라 **현재 부모가 가진 질문을 자동으로 분류하고 가장 적절한 모듈을 전면에 배치하는 시스템**이다.

```
What happened?
→ Record

What is happening?
→ State

What is changing?
→ Pattern

What happens next?
→ Prediction

What should I do?
→ Recommendation

Is this concerning?
→ Official/Clinical Escalation

How do I remember this?
→ Memory
```

이 7개의 질문이 전체 제품 구조를 구성한다.
