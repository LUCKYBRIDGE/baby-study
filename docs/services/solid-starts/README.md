# Solid Starts — 서비스 정본 분석

> 유형: 이유식·유아식 / 음식 DB / 알레르기 / meal planning  
> 공개 제품코드: 확인 못함 [U]  
> 직접 검증: 공식 App/Product 페이지 [A1]

## 1. 서비스 정의

Solid Starts는 **음식 객체를 중심으로 연령별 제공방법·안전·알레르기·영양 정보와 개인 섭취이력을 연결하고, 그 기록을 다음 음식과 meal plan으로 이어주는 이유식 전문 플랫폼**이다.

## 2. 전체 구조

[A1]

```
Baby Stage
├─ Food Database 500+
│  ├─ serving by age
│  ├─ photo/video
│  ├─ nutrition
│  ├─ safety
│  └─ allergen
├─ Food Log
├─ Allergen Guidance
├─ First 100 Foods
├─ Meal Plan
├─ Recipes 300+
└─ Expert Library
```

## 3. 공개 코드/폴더 구조

공식 제품 repository는 확인하지 못했다.

유사 이유식 프로젝트는 제품 근거로 사용하지 않는다.

## 4. 핵심 IA

일반적인:
`초기/중기/후기 이유식 글 목록`

이 아니라:

```
Mango
Egg
Peanut
Apple
...
```

처럼 **음식 객체가 검색 진입점**이다.

## 5. 핵심 사용자 흐름

```
Food Search
→ Age-specific Serving
→ Visual Example
→ Feed Baby
→ Log Tried/Reaction
→ Next Food / Meal Plan
```

## 6. 월령 단계

공식 제품 페이지:
- 0–4m
- 5–6m
- 7–9m
- 10–12m
- 12m+

같은 stage selector를 직접 노출한다.

## 7. 가장 잘 푼 문제

"이 음식을 지금 우리 아기에게 어떻게 줘야 하는가?"라는 상황적 질문에 바로 답한다.

## 8. 위험

- 알레르기 정보는 고위험
- food count 게임화
- 국가별 권고 차이
- 앱 계획이 실제 아기 반응보다 우선될 위험

## 9. 참고할 패턴

- Object-centered IA
- Age-specific Object View
- Visual Instruction
- Knowledge + Personal History
- Exposure/Reaction Log
- Database → Recommendation

## 10. 관련 문서

- [화면·UI·UX](surface-map.md)
- [기술·데이터·문제 해결](system-analysis.md)
- [직접 관찰](../../direct-inspection/apps/solid-starts-site.md)
