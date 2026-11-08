# 영유아 건강검진 / 국민건강보험 — 서비스 정본 분석

> 유형: 공식 영유아 건강검진 / K-DST / 건강교육 / 전문기관 의뢰  
> 직접 검증: 국민건강보험 공식 PDF 및 국가건강정보 [A1/A2]

## 1. 서비스 정의

국가 영유아 건강검진은 **영유아 성장·발달·생활습관·안전을 정기적으로 확인하고, 사전문진·발달선별·검진·결과·필요 시 전문기관 의뢰까지 연결하는 국가 건강관리 프로토콜**이다.

## 2. 공식 사용자 흐름

[A1]

```
검진기관 검색/예약
→ 웹 문진
→ 발달선별검사지(해당 차수)
→ 검진
→ 결과
→ 필요 시 전문기관
```

## 3. 핵심 검사 범위

- 문진/진찰
- 신체계측
- 발달평가/상담
- 건강교육

## 4. 공개 파일/폴더 구조

공공 시스템 내부 source repository는 분석하지 않았다. [U]

대신 공식 PDF와 웹 행정 흐름을 제품구조로 본다.

## 5. 가장 잘 푼 문제

일상적인 "잘 크고 있나?"를 정기적인 공공 health checkpoint로 만든다.

그리고 우려가 있으면:
`screening → referral`
로 연결한다.

## 6. 건강교육

검진 자체에:
- 안전
- 수면
- 구강
- 대소변
- 미디어
- 정서/사회성
- 개인위생
- 취학 준비

등 시기별 부모교육이 포함된다.

## 7. 참고할 패턴

- Eligibility Window
- Pre-visit Questionnaire
- Screening Boundary
- Doctor Question Inbox
- Result → Follow-up
- Clinical Handoff
- Age-specific Parent Education

## 8. 관련 문서

- [페이지·UI·UX](surface-map.md)
- [기술·의료경계·문제 해결](system-analysis.md)
- [공공 시스템 직접 관찰](../../direct-inspection/web/korea-public-systems.md)
