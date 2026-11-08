# Huckleberry Deep Dive — 구조·기능·문제 해결 방식

> 조사 기준일: 2026-11-08  
> 공식 근거: Huckleberry Free/Plus/Premium, Tracking, Reports, Activity Tracking, Schedule Creator

## 1. 서비스 한 문장

Huckleberry는 **육아 기록을 무료 기반층으로 제공하고, 누적된 기록을 수면 예측·일정 계획·개인화 인사이트·AI 입력·전문가형 지원으로 단계적으로 가치화하는 데이터 중심 육아 플랫폼**이다.

## 2. 전체 제품 레이어

```
Free Layer
├─ Sleep
├─ Feeding
├─ Diaper
├─ Pumping
├─ Solids
├─ Growth
├─ Medication / Temperature
├─ Activities
├─ Timer / Reminder
├─ Reports
└─ Multi-device sync

Plus Layer
├─ SweetSpot sleep prediction
├─ Insights
├─ Schedule Creator
├─ AI logging
├─ Enhanced Reports
├─ Lock-screen updates
├─ Widgets
└─ Apple Watch

Premium Layer
├─ Berry AI guidance
├─ Expert-designed personalized sleep plan
└─ Plus 전체 기능
```

이 구조 자체가 매우 중요하다.

**데이터 생성은 무료, 데이터 해석은 유료, 문제 해결 지원은 더 높은 유료층**으로 배치되어 있다.

## 3. 홈 구조의 철학

공식 Tracking 페이지는 홈 화면에서 필요한 tracking category만 선택하고 나머지는 숨길 수 있음을 강조한다.

즉 홈은 고정 메뉴가 아니라:

```
Baby Age
+
Current Family Need
+
User-selected Tracking Categories
```

로 구성된다.

이것은 BabyTime의 수동 아이콘 재배치보다 한 단계 확장된 **생애주기형 커스터마이즈 홈**이다.

## 4. 기록 모델

[확인] 공식 자료에서 다음 범위를 확인할 수 있다.

- sleep
- breastfeeding
- bottles
- tube feeding
- solids
- diapers
- pumping
- growth
- medication
- temperature
- skin-to-skin
- storytime
- outdoor/indoor play
- teeth brushing
- tummy time
- screen time
- bath time
- potty trips / accidents 등

중요한 것은 tracking category가 계속 확장돼도 **하나의 event log 패턴**으로 유지된다는 점이다.

## 5. 활동 유형마다 기록 방식이 다름

Activity Tracking은 두 방식을 지원한다.

- timer 기반
- 했는지 여부만 기록

이는 좋은 추상화다.

모든 행동에 시작/종료시각을 강요하지 않는다.

예:
- tummy time → duration 의미 있음
- teeth brushing → completion이 더 중요할 수 있음

즉 데이터 모델을 UX에 맞춘다.

## 6. 보고서 구조

공식 자료에서 다음 report view가 확인된다.

- Day
- Week
- Summary
- List
- 7/14/30/90일
- 최대 1년 수면 추세

Plus/Premium에서는:
- Wake Window vs SweetSpot
- Rise and Bedtime
- 또래 연령 권장수면량과 비교

가 추가된다.

이 구조는 데이터 maturity를 보여준다.

```
Raw Event
→ Daily View
→ Aggregation
→ Trend
→ Recommendation Comparison
```

## 7. SweetSpot의 역할

SweetSpot은 2개월 이상에서 낮잠/취침 시점을 예측한다.

제품적으로 중요한 점은 **정적인 월령표를 개인 기록에 맞춰 보정**한다는 것이다.

정적 정보:
> 6개월 아기는 보통 2~3시간 깨어 있음.

개인화:
> 오늘 실제 수면과 기상시각을 반영하면 다음 낮잠 예상은 ...

Huckleberry는 기록을 "보관해야 할 것"이 아니라 **예측에 필요한 입력값**으로 만든다.

## 8. Schedule Creator와 SweetSpot의 구분

두 기능을 구분한 점이 좋다.

### SweetSpot
다음 이벤트 중심:
```
Next nap / bedtime
```

### Schedule Creator
하루 계획 중심:
```
Wake time
+ nap count
+ age-based wake windows
→ daily schedule
```

Schedule Creator는 예정된 외출·수업·취침 등 미래 계획과 연결된다.

즉:
- prediction
- planning

을 별도 제품 기능으로 본다.

## 9. AI Logging

공식 설명상 text, voice, photo 입력을 지원한다.

특히 voice/text는 자연어로 여러 기록을 한 번에 처리할 수 있다.

예:
> Baby had a bottle at 7 and napped from 9 to 10:30.

↓

```
Bottle Event
Sleep Event
```

이는 육아 AI에서 가장 현실적인 활용 사례 중 하나다.

AI를 바로 의료상담에 쓰기보다 먼저:
- missed log catch-up
- timer start
- multi-event parsing
- next SweetSpot 확인

에 사용한다.

## 10. 잠금화면·위젯·Watch

Plus 이상에서는 앱을 열지 않고도 tracking을 지원한다.

이 기능은 단순 편의기능이 아니라 **interaction surface 확장**이다.

```
App
├─ Lock Screen
├─ Widget
├─ Watch
└─ Voice/Text
```

육아 기록에서는 앱 내부 UX만 최적화해서는 부족하다. 입력이 필요한 순간이 매우 짧기 때문이다.

## 11. 공동양육 구조

공식 FAQ상 여러 기기에서 **같은 계정에 로그인**하여 caregiver sync를 사용한다.

장점:
- 구현/사용이 단순
- 기록 동기화가 쉬움

단점:
- 사용자별 identity/권한이 약해질 수 있음
- 누가 어떤 기록을 수정했는지 명확하지 않을 수 있음

FamilyAlbum의 role-based membership와 비교하면 Huckleberry는 **공유계정형 공동양육**에 가깝다.

향후 의료·권한 추적이 중요하면 독립 사용자 계정 + baby workspace 방식이 더 확장성이 좋다.

## 12. 수익모델 구조

### Free
기록 습관과 데이터 축적

### Plus
- 예측
- 인사이트
- 입력 편의
- 고급 리포트

### Premium
- AI guidance
- 전문가형 맞춤 계획

이 구조는 유료화를 사용자의 데이터 lock-in에만 기대지 않고 **더 높은 분석 가치**에 배치한다는 점이 좋다.

## 13. 핵심 사용 루프

```
1. 사건 기록
2. 홈 최신 상태 갱신
3. 하루/주간 패턴 형성
4. SweetSpot/Insight 생성
5. 알림/계획
6. 다음 행동
7. 실제 결과 다시 기록
8. 모델 보정
```

이것이 BabyTime과 가장 큰 차이다.

BabyTime:
`Record → Understand`

Huckleberry:
`Record → Understand → Predict → Act → Learn`

## 14. 강점

- 기록과 분석이 하나의 데이터 파이프라인
- 아이 성장에 따라 홈 카테고리 조절 가능
- 입력 경로가 앱 밖까지 확장
- 예측과 계획을 분리
- 무료/유료 경계가 제품 가치 단계와 맞음
- 복수 자녀 지원
- potty까지 확장하며 toddler 단계도 유지

## 15. 구조적 한계

### 공유 계정형 caregiver
권한·감사로그가 약할 수 있다.

### 예측 과신 위험
수면 추천과 실제 아이 신호 사이 우선순위가 명확해야 한다.

### 기능 비대화 위험
sleep 중심 서비스에서 feeding, activity, potty, AI chat까지 확장하면서 복잡해질 수 있다.

### 유료 기능과 필수 정보 경계
예측은 유료여도 되지만 안전수면·위험신호 등 안전정보는 paywall과 분리되어야 한다.

## 16. 가져올 패턴

1. **Free Data Layer / Paid Intelligence Layer**
2. **Adaptive Tracking Home**
3. **Multiple Input Surfaces**
4. **AI Multi-event Logging**
5. **Prediction vs Planning 분리**
6. **Report Time-scale Expansion**
7. **Age-transition Category Switching**
8. **Feedback Loop 기반 개인화**

## 17. 근거

- https://huckleberrycare.com/product/free
- https://huckleberrycare.com/product/plus
- https://huckleberrycare.com/product/premium
- https://huckleberrycare.com/product/tracking
- https://huckleberrycare.com/blog/activities-tracking
- https://huckleberrycare.com/blog/how-to-access-enhanced-sleep-reports-on-huckleberry
- https://huckleberrycare.com/blog/visualize-your-daily-schedule-with-schedule-creator
- https://huckleberrycare.com/blog/huckleberry-ai-chat

## 결론

Huckleberry는 **육아 기록 데이터를 어떻게 제품 지능으로 승격시키는가**를 분석하기 가장 좋은 사례다.

가장 중요한 구조는:

**Event Log → Reports → Prediction → Planning → AI/Expert Support**

다.
