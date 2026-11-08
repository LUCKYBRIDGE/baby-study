# Pathways.org — 기술·데이터·문제 해결 분석

## 1. 공개 기술 현황

내부 product source는 공개 확인하지 못했다. [U]

강점은 기술스택보다 **content/data taxonomy**에 있다.

## 2. 개념 데이터 모델

[C]

```
AgeRange
DevelopmentDomain
MilestoneDefinition
AbilityDefinition
Activity
Resource
ChildObservation
TrackerEvent
```

## 3. Observable Behavior

추상적인:
`언어발달이 좋음`

대신:
`구체적으로 어떤 행동을 하는가`

를 데이터 단위로 삼는다.

이렇게 해야 caregiver report 품질이 높아진다.

## 4. 상태 모델

```
Not Started
Making Progress
Achieved
```

emerging skill을 표현할 수 있다.

## 5. Knowledge Graph

```
Milestone
↔ Skill/Domain
↔ Activity
↔ Video/Article
```

콘텐츠를 페이지 파일 목록으로 관리하는 것보다 relation graph로 보는 것이 적합하다.

## 6. 얽힌 문제 — 특수 발달경로

조산/NICU를 표준 age calculation과 분리한다.

일반 아이에게 최적화한 milestone timeline을 강제하지 않는다.

## 7. 얽힌 문제 — 정보와 행동의 거리

Article만 제공하면 실행으로 이어지지 않는다.

Today/Play를 두어:
`Knowledge → Action`

거리 자체를 줄인다.

## 8. 우리 시스템에 일반화

발달 콘텐츠는:
- 행동정의
- 예시 미디어
- 관련활동
- 부모관찰

을 하나의 graph로 구성하는 것이 좋다.
