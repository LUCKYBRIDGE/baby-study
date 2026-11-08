# 베이비빌리 — 서비스 정본 분석

> 유형: 임신·출산·육아 super-app / 콘텐츠 / 커뮤니티 / 건강 / 커머스  
> 공개 제품코드: 공식 확인 못함 [U]  
> 직접 검증: 공식 한국 사이트 [A1]

## 1. 서비스 정의

베이비빌리는 **임신 주수와 아기 월령을 전역 context로 사용해 콘텐츠·성장정보·커뮤니티·건강기록·쇼핑의 우선순위를 시기별로 바꾸는 생애주기형 super-app**이다.

## 2. 공식 상위 구조

[A1]

```
임신 준비
임신
육아
베동 모임
커머스/입점
```

앱에서는 여기에 건강기록과 stage-specific content가 결합된다.

## 3. 공개 코드/폴더 구조

공식 제품 repository는 확인하지 못했다.

검색되는 동명/clone 저장소는 ownership 근거가 부족해 기술분석에서 제외한다.

## 4. 핵심 시스템

```
Current Stage
├─ pregnancy week
└─ baby age
      ↓
Home priority
Content
Community cohort
Health reference
Commerce timing
```

즉 age가 filter가 아니라 **global router**다.

## 5. 주요 사용자 가치

- 지금 필요한 정보만 큐레이션
- 같은 시기 부모와 커뮤니티
- 아기/엄마 건강기록
- 시기별 구매 부담 완화
- 임신부터 육아까지 계정 관계 유지

## 6. 가장 잘 푼 문제

정보 과잉을 **시기 기반 relevance**로 줄인다.

## 7. 구조적 위험

- content/community/commerce/home 경쟁
- 의료정보와 상품 추천의 이해상충
- 같은 월령 커뮤니티의 잘못된 일반화
- daily tracker 전문성은 전용앱보다 낮을 수 있음

## 8. 참고할 패턴

- Age as Global Context
- Lifecycle State Machine
- Cohort Community
- Stage-curated Feed
- Commerce Timing
- Emotional Character Layer

## 9. 관련 문서

- [페이지·UI·UX](surface-map.md)
- [기술·데이터·문제 해결](system-analysis.md)
- [직접 관찰](../../direct-inspection/apps/babybilly-site.md)
