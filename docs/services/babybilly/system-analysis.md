# 베이비빌리 — 기술·데이터·문제 해결 분석

## 1. 공개 기술 현황

내부 framework/DB는 공개 확인하지 못했다. [U]

제품 구조상 중요한 것은 기술스택보다 **orchestration model**이다.

## 2. 핵심 데이터 모델

[C]

```
LifecycleProfile
├─ pregnancy_due_date
├─ pregnancy_week
├─ birth_date
└─ baby_age

Content
├─ stage_range
├─ category
└─ provenance

CommunityPost
├─ cohort_context
└─ topic

Measurement
ProductRecommendation
```

## 3. Lifecycle State Machine

출산은 mode change다.

```
Pregnancy
→ Birth Event
→ Parenting
```

각 상태에서:
- 홈
- 콘텐츠
- 기록
- 상품

우선순위가 바뀐다.

## 4. 얽힌 문제 — 기능이 많으면 홈이 무너짐

Super-app은 기능을 추가할수록 복잡해진다.

해결 원리:
```
Stage Context
→ Module Ranking
```

즉 메뉴를 없애기보다 **현재 필요도에 따라 전면 노출을 바꾼다.**

## 5. 얽힌 문제 — content와 commerce 충돌

건강/육아 정보를 보러 온 사용자에게 상품 추천이 같은 권위로 보이면 신뢰 문제가 생긴다.

필요:
- Sponsored/commerce 표시
- editorial provenance
- recommendation rationale 분리

## 6. Cohort Model

```
User
→ lifecycle cohort
→ community relevance
```

커뮤니티 검색/추천에도 age context를 재사용한다.

## 7. 건강기록

일반 평균범위와 개인 측정을 결합하지만, 공식 의료검진 결과와 user-entered measurement는 별도 source type으로 구분해야 한다.

## 8. 우리 시스템에 일반화

주수·월령은 단순 profile field가 아니라 **전체 IA를 조정하는 orchestration key**로 써야 한다.
