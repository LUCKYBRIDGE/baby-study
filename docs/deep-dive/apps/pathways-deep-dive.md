# Pathways.org Deep Dive — 구조·기능·문제 해결 방식

> 조사 기준일: 2026-11-08  
> 공식 근거: Pathways.org 공식 Milestones / Activities / Today / Checklist

## 1. 서비스 한 문장

Pathways.org는 **아기 발달을 추상적 평가가 아니라 관찰 가능한 행동·영상·활동으로 정의하고, 월령·조산/NICU 등 맥락별로 무료 제공하는 전문가 기반 발달 지식 플랫폼**이다.

## 2. 전체 정보구조

```
Age Context
├─ Baby on the Way
├─ Preemie
├─ NICU
├─ 0-2m
├─ 2-4m
├─ ...
└─ 6+ years

Development Topics
├─ Motor
├─ Sensory
├─ Communication
├─ Feeding
├─ Tummy Time
├─ Play
├─ Social Emotional
└─ Executive Function

Resource Types
├─ Milestones
├─ Abilities
├─ Activities
├─ Videos
├─ Articles
├─ Checklists
├─ Warning Signs
└─ Early Intervention
```

이 사이트의 강점은 **연령 x 발달영역 x 콘텐츠 유형**의 3차원 taxonomy다.

## 3. 추상어 대신 Observable Behavior

예:
- "운동발달이 좋다"가 아니라
- "가구를 잡고 이동한다"
- "두 손으로 장난감을 탐색한다"

처럼 부모가 실제로 볼 수 있는 행동으로 정의한다.

데이터 품질 측면에서 매우 중요하다.

```
Abstract Judgment
↓
Observable Behavior
↓
More Reliable Caregiver Report
```

## 4. 상태가 3단계

공식 checklist는:
- Not Started
- Making Progress
- Achieved

를 사용한다.

이것은 단순 true/false보다 발달의 연속성을 잘 표현한다.

특히 "Making Progress"는:
- 부모 불안 완화
- emerging skill 기록
- 다음 활동 추천

에 유용하다.

## 5. 발달영역을 넓게 본다

Pathways는 Feeding과 Sensory를 독립영역으로 둔다.

이는 Kinedu의 4영역보다 더 세밀하다.

특히 feeding을:
- 빨기
- 삼키기
- 질감
- finger feeding
- cup/utensil

같은 기술 발달로 본다.

통합 육아앱에서도 이유식과 발달 데이터를 완전히 분리하기보다 **feeding development** 관점으로 연결할 수 있다.

## 6. 특수 경로: Preemie / NICU

공식 IA에 Preemie와 NICU가 별도 진입점으로 존재한다.

이것은 매우 중요한 포용적 설계다.

```
Standard Age Path
≠
Preterm/NICU Path
```

동일한 월령표를 모두에게 강요하지 않는다.

## 7. Today Dashboard

Pathways Today에는:
- Tummy Time
- First Week Survival Guide
- Baby Progress
- 영역별 진도
- New This Week

등이 결합된다.

즉 사이트형 지식베이스를 **개인 홈**으로 변환하려는 구조다.

## 8. Activities와 Milestone 연결

공식 Activity library는 월령·영역별 활동을 제공한다.

이상적인 연결:

```
Milestone not started / making progress
→ Related Activities
→ Parent plays
→ Observation update
```

Kinedu와 같은 adaptive engine 수준은 아니어도 **knowledge graph의 기반**이 된다.

## 9. 의료적 안전 경계

공식 사이트는:
- 자료는 정보 목적
- 전문 의료조언 대체 아님
- therapy/diagnosis/treatment가 아님

을 명확히 한다.

또 milestone 누락이 있으면 의료진과 상의하도록 안내한다.

이런 명확한 boundary text는 발달 서비스에서 필수다.

## 10. 무료 전략

대부분의 자료가 무료다.

따라서 비즈니스 모델보다는:
- 공공적 신뢰
- 전문가 자료 확산
- 병원/전문가 활용

에 가깝다.

제품 설계 관점에서 이는 **신뢰를 monetization과 분리한 reference architecture**로 볼 수 있다.

## 11. 강점

- taxonomy가 정교함
- 행동 정의가 구체적
- 영상/활동 연결
- 조산/NICU 지원
- 무료 접근
- 의료 경계가 명확

## 12. 구조적 한계

- 개인화 추천 깊이는 제한적
- 정보량이 많아 초보 부모가 과도하게 탐색할 수 있음
- 영역별 percentage progress가 점수처럼 받아들여질 수 있음
- 한국 임상/검진체계와 직접 연결되지 않음

## 13. 가져올 패턴

1. **Age × Domain × Resource Taxonomy**
2. **Observable Behavior Specification**
3. **Three-state Development Status**
4. **Special Pathways for Preemie/NICU**
5. **Milestone ↔ Activity Graph**
6. **Explicit Medical Boundary**
7. **Video as Behavioral Exemplar**

## 14. 근거

- https://pathways.org/milestones
- https://pathways.org/activities
- https://pathways.org/today
- https://pathways.org/checklists/milestone-checklist/

## 결론

Pathways.org는 기능 UX보다 **발달 콘텐츠와 데이터 자체를 어떻게 구조화할지** 연구하기 가장 좋은 사례다.
