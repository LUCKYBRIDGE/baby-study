# Huckleberry — 페이지·UI·UX·버튼 지도

## 1. 제품 surface

[A1]

Huckleberry는 앱 내부 화면만으로 끝나지 않는다.

```
Mobile App
├─ Home tracking
├─ Reports
├─ SweetSpot
├─ Schedule Creator
└─ AI/Berry

Outside App
├─ Lock-screen live updates
├─ Widget
├─ Apple Watch
└─ Voice/Text/Photo input
```

기록 순간이 짧기 때문에 **interaction surface를 앱 바깥으로 확장**한다.

## 2. Home

공식 Tracking 설명상 Home에서는 필요한 tracker category를 선택하고 불필요한 카테고리를 숨길 수 있다.

예상 사용자 사고:
- 지금 기록하려는 것은 무엇인가?
- 마지막 상태는 무엇인가?
- timer가 진행 중인가?
- 다음 SweetSpot은 언제인가?

Home은 전 기능 메뉴보다 **현재 상황 dashboard** 역할이 중요하다.

## 3. Tracker별 interaction

### Sleep
- start
- pause
- resume
- complete/cancel
- retroactive log

[B2] 비공식 API 코드에서도 위 상태 전이가 명확히 드러난다.

### Nursing
- start side
- left/right switch
- pause/resume
- complete

### Bottle
- type
- amount
- unit
- note

### Solids
- food
- reaction
- note

### Diaper
- pee / poo / both / dry
- 세부 속성

### Health
- growth
- medicine
- temperature

즉 하나의 universal modal이 아니라 **domain별로 다른 interaction grammar**를 사용한다.

## 4. Reports

[A1]

공식 페이지에서:
- Day
- Week
- Summary
- List
- 7/14/30/90일
- 더 긴 수면 추세

등 여러 기간/보기 방식이 존재한다.

Plus에서는:
- Wake Window vs SweetSpot
- Rise/Bedtime
- age recommendation 비교

같은 분석이 추가된다.

## 5. SweetSpot

핵심 CTA는 과거를 보는 버튼이 아니라 **다음 낮잠/취침을 준비하게 하는 정보**다.

좋은 UX는:
- 예상시각
- 준비 알림
- 실제 잠든 시각
- 예측과 실제의 차이

를 자연스럽게 연결해야 한다.

## 6. Schedule Creator

SweetSpot과 달리 하루 전체를 계획하는 기능.

```
기상시각
+
낮잠 횟수
+
age-based wake windows
→ daily schedule
```

Prediction과 Planning을 분리한 점이 좋다.

## 7. AI logging

[A1]

자연어/음성으로:
- 이벤트 기록
- 빠뜨린 로그 보완
- timer 조작

을 줄이는 방향이다.

UI에서 중요한 것은 AI chat 자체보다 **결과가 어떤 event로 변환되는지 명확하게 보여주는 것**이다.

## 8. Caregiver UX

공식 안내는 같은 계정으로 여러 기기에 로그인하는 방식이다.

UX 장점:
- 초대/승인 단계 적음

단점:
- 작성자 identity가 희미함
- 역할별 권한 없음
- 자격증명 공유 문제

## 9. 유료벽

Free → Plus → Premium으로 올라갈수록:
- 기록
- 분석/예측
- 전문가/AI guidance

순으로 가치가 이동한다.

과금이 **기능 수**보다 **의사결정 지원 수준**에 맞춰진다.

## 10. 미확인

- 현재 네이티브 bottom tab exact 구성
- Android lock-screen surface 범위
- offline conflict UI
- 가족별 작성자 표시
- AI parse 실패 UX
