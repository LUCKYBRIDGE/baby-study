# 직접 관찰 후 수정된 핵심 비교

공식 소개자료만 읽었을 때와 실제 사이트·FAQ·공개 코드를 따라갔을 때 달라진 해석을 정리합니다.

# 1. 공동양육 모델은 세 종류로 나뉨

## BabyTime — Child-centered Invite

```
Baby
├─ Mom
├─ Dad
├─ Babysitter
└─ Family
```

- 관계를 선택
- 6자리 초대코드
- 개별 계정 연결

### 적합
역할/작성자 구분이 중요한 서비스.

---

## Huckleberry — Shared Account / Multi-device

```
Account
├─ Device A
└─ Device B
```

### 적합
가입/초대 마찰을 줄이고 빠르게 공동 기록할 때.

### 한계
역할별 권한과 감사로그에 약함.

---

## FamilyAlbum — Workspace + Role Permission

```
Album
├─ Admin
├─ App Member
└─ Browser Member
```

가장 정교한 권한모델.

### 통합 앱에 적합한 결론

BabyTime의 child-centered identity와 FamilyAlbum의 role permission을 결합하는 편이 좋습니다.

---

# 2. 기록 저장 구조 — Huckleberry 공개 코드가 중요한 이유

직접 공개 코드를 보면 단순 `events[]` 하나로만 저장하지 않습니다.

```
Domain Root
├─ current timer
├─ last event summary
└─ historical events
```

즉 UX에서 자주 읽는 "현재 상태"를 history 전체에서 매번 계산하지 않습니다.

### 우리 설계에서 참고

```
BabyStateProjection
├─ last_feeding
├─ active_sleep
├─ last_diaper
├─ last_medication
└─ next_due
```

을 event log에서 별도 projection으로 유지하면 홈 응답이 빨라집니다.

---

# 3. 발달앱의 실제 구조 차이

## Kinedu
평가 → skill model → personalized activities

## Pathways
공식/전문 행동 taxonomy → tracking → activity

## CDC
monitoring → concern → doctor handoff

### 결합하면

```
Pathways
관찰 정의

+

Kinedu
추천 엔진

+

CDC
안전/의료 경계
```

가 이상적입니다.

---

# 4. 임신→육아 슈퍼앱의 차이

## BabyBilly
Age context가 전체 feed/community/commerce를 라우팅.

## MommyTalk
Hospital ultrasound가 acquisition point이고 이후 육아 tracker로 확장.

## MOMI
Voice AI가 입력 interface이고 pregnancy/baby data type이 lifecycle에 따라 전환.

세 제품의 강점이 서로 다릅니다.

---

# 5. "기록 후 가치"의 단계

직접 관찰 결과 제품들은 다음 maturity ladder에 배치할 수 있습니다.

### Level 1
`Record`

### Level 2
`Record → Current State`

BabyTime

### Level 3
`Record → Pattern/Stats`

BabyTime, MommyTalk

### Level 4
`Record → Prediction`

Huckleberry, Napper

### Level 5
`Observation → Recommendation`

Kinedu, Pathways

### Level 6
`Record → Clinical Handoff`

CDC, NHIS

### Level 7
`Record → Memory Reward`

FamilyAlbum

좋은 통합 시스템은 이 모든 레벨을 한 화면에 넣는 것이 아니라 **상황에 맞는 출력만 보여줘야 합니다.**

---

# 6. Derived Artifact 개인정보 문제

FamilyAlbum을 직접 확인하며 중요한 문제가 드러났습니다.

```
Original Photo
→ Auto-generated Movie
```

이후 original의 공개범위를 바꿔도 이미 생성된 결과물이 유지될 수 있습니다.

AI 시대에는 더 중요합니다.

예:
```
Voice
→ Transcript
→ Structured Event
→ AI Summary
→ Monthly Report
```

원자료 삭제 시 파생데이터를:
- 같이 삭제할지
- 익명화할지
- 재생성할지

정책이 필요합니다.

---

# 7. 가장 중요한 최종 구조

직접 관찰 후 현재 가장 합리적인 통합 아키텍처:

```
Baby Workspace
│
├─ Identity / Roles
│
├─ Ground-truth Event Store
│
├─ Current-state Projection
│
├─ Domain Modules
│  ├─ Feeding
│  ├─ Sleep
│  ├─ Diaper
│  ├─ Health
│  ├─ Food
│  └─ Development
│
├─ Intelligence
│  ├─ Pattern
│  ├─ Prediction
│  └─ Recommendation
│
├─ Official Health Bridge
│  ├─ Vaccination
│  ├─ Checkup
│  └─ Screening
│
└─ Memory
   ├─ Media
   └─ Recap
```

AI는 이 구조의 맨 아래 데이터베이스가 아니라 **입력/분석 어댑터**여야 합니다.
