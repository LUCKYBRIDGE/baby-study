# BabySparks — 기술·데이터·문제 해결 분석

## 1. 공개 기술 현황

제품 내부 코드/DB는 공개 확인하지 못했다. [U]

그러나 상품 구조상 필요한 계층은 관찰 가능하다.

```
Content Library
Child Profile
Milestone Progress
Activity Recommendation
Family Membership
Organization / Location
```

## 2. 개념 데이터 모델

[C]

```
Child
Milestone
Activity
├─ target_milestones[]
└─ age_range

ActivityCompletion
ProgressSnapshot

Organization
Location
Caregiver
FamilyConnection
```

## 3. 얽힌 문제 — 콘텐츠가 너무 많음

수천 개 활동을 검색하게 하면 사용자가 선택하지 못한다.

해법:
```
Library
→ Recommendation Engine
→ Today Program
```

## 4. 얽힌 문제 — 발달 progress가 경쟁이 됨

progress를 rank/score보다 **관찰과 다음 활동** 중심으로 표현해야 한다.

## 5. B2B hierarchy

기관용 확장을 고려하면 child 데이터가 개인계정 아래만 있으면 어렵다.

```
Organization
└─ Location
   ├─ Staff
   └─ Child
      └─ Family
```

처럼 ownership과 access를 분리해야 한다.

## 6. 콘텐츠 재사용

같은 core content를:
- B2C parent
- childcare professional
- employer benefit

로 제공한다.

좋은 content object는 audience-specific presentation과 분리되어야 한다.

## 7. corrected age

추천 엔진에:
- chronological age
- corrected age

를 분리해 전달할 필요가 있다.

## 8. 우리 시스템에 일반화

발달활동은 "활동 목록"이 아니라:
```
Child State
→ Activity Selection
→ Observation
→ Progress
```
라는 curriculum loop로 설계한다.
