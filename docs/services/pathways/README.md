# Pathways.org — 서비스 정본 분석

> 유형: 발달 지식 / milestone tracking / 놀이 / 기본 생활기록  
> 공개 제품코드: 확인 못함 [U]  
> 직접 검증: Today / Play / Track / Activities [A1]

## 1. 서비스 정의

Pathways.org는 **발달을 추상 점수가 아니라 부모가 관찰할 수 있는 행동으로 정의하고, 이를 milestone tracking·놀이 활동·기본 생활 tracking과 연결하는 전문가 기반 발달 플랫폼**이다.

## 2. 실제 IA

[A1]

```
Today
Play
Track
│  ├─ Milestones
│  ├─ Tummy Timer
│  ├─ Diaper
│  └─ Feeding
└─ Explore
```

기존 "발달 콘텐츠 사이트"보다 훨씬 product-like하다.

## 3. 전체 taxonomy

연령:
- Baby on the Way
- Preemie
- NICU
- 0–2m
- 2–4m
- ...
- 6+ years

영역:
- Motor
- Sensory
- Communication
- Feeding
- Tummy Time
- Play
- Social Emotional
- Executive Function

## 4. 공개 코드/폴더 구조

공식 제품 repository는 확인하지 못했다.

## 5. 핵심 데이터 흐름

```
Age Context
→ Observable Milestones
→ Track State
→ Related Activities
→ Play
→ Re-observe
```

## 6. 가장 잘 푼 문제

- "발달이 좋다" 같은 추상판단을 구체 행동으로 바꿈
- 사진/영상 예시로 관찰 품질 개선
- 조산/NICU를 상위 경로로 분리
- 발달과 feeding/tummy time 같은 실제 일상을 연결

## 7. 위험

- progress percentage가 점수처럼 보일 수 있음
- 정보량 과다
- 개인화 깊이는 Kinedu보다 약함

## 8. 참고할 패턴

- Age × Domain × Resource taxonomy
- Observable Behavior
- Three-state Progress
- Special Pathway
- Milestone ↔ Activity Graph
- Progressive Personalization

## 9. 관련 문서

- [페이지·UI·UX](surface-map.md)
- [기술·데이터·문제 해결](system-analysis.md)
- [직접 관찰](../../direct-inspection/apps/pathways-site.md)
