# Solid Starts — 기술·데이터·문제 해결 분석

## 1. 공개 기술 현황

내부 제품코드는 공개 확인하지 못했다. [U]

공식 기능을 기준으로 필요한 domain model은 비교적 명확하다.

## 2. 핵심 데이터 모델

[C]

```
Food
├─ nutrition
├─ hazard
├─ allergen
└─ serving_guides[]

ServingGuide
├─ age_range
├─ text
├─ image
└─ video

BabyFoodExposure
├─ food_id
├─ time
├─ preparation
├─ amount
└─ reaction

Recipe
MealPlan
```

## 3. Global Knowledge + Personal History

가장 중요한 구조:

```
Food Catalog
+
Baby Exposure History
```

일반 지식과 개인 기록이 같은 `food_id`를 통해 연결된다.

## 4. 얽힌 문제 — 검색과 기록을 따로 두면 맥락이 끊김

부모가 food article을 읽은 뒤 다른 화면에서 기록을 찾으면 friction이 크다.

해법:
`object detail → log`

을 바로 연결한다.

## 5. 얽힌 문제 — 알레르기는 일반 food log와 위험도가 다름

Reaction은 단순 "싫어함"과 의료적 반응을 같은 필드로 처리하면 안 된다.

우리 시스템에서는 최소:
- preference
- intolerance/uncertain
- allergic reaction concern

을 분리하는 것이 필요하다.

## 6. recommendation

```
Age
+
Tried Foods
+
Reaction History
→ Next Food / Meal Plan
```

단, 의료상황은 recommendation engine보다 전문가 지침이 우선되어야 한다.

## 7. 콘텐츠 provenance

전문가 검토 콘텐츠는:
- author/reviewer
- updated_at
- source
- locale

가 필요하다.

## 8. 우리 시스템에 일반화

음식뿐 아니라:
- vaccine
- medicine
- milestone

도 **Global Definition + Baby-specific History** 패턴으로 만들 수 있다.
