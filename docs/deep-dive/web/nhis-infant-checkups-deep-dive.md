# 영유아 건강검진 / NHIS Deep Dive — 구조·기능·문제 해결 방식

> 조사 기준일: 2026-11-08  
> 공식 근거: 국민건강보험공단, 국가건강정보포털

## 1. 서비스 한 문장

국가 영유아 건강검진은 **생후 14~71개월의 성장·발달·생활습관·안전을 정기적으로 평가하고, 온라인 문진·K-DST·검진기관·결과·전문진료 의뢰를 연결하는 국가 성장관리 프로토콜**이다.

## 2. 전체 사용자 여정

```
Eligibility
→ Find/Book Screening Institution
→ Pre-visit Questionnaire
→ K-DST (applicable ages)
→ Visit
→ Physical / Development Assessment
→ Health Education
→ Result
→ Follow-up / Specialist Referral
```

이 흐름은 민간 육아앱이 의료 영역과 연결할 때 따라야 할 좋은 기본 골격이다.

## 3. 검진 구조

공식 국가건강정보포털 기준:
- 생후 14~71개월
- 총 8회 건강검진
- 문진/진찰
- 신체계측
- 발달평가/상담
- 건강교육

발달평가는 K-DST를 사용한다.

## 4. 건강교육이 월령별 curriculum 역할

검진에는 단순 측정만 있는 것이 아니다.

시기별:
- 영양
- 안전
- 안전수면
- 구강
- 대소변 가리기
- 전자미디어
- 정서/사회성
- 개인위생
- 취학 전 준비

등의 교육이 포함된다.

이 목록은 **국가가 중요하다고 보는 부모교육 커리큘럼**으로 해석할 수 있다.

## 5. Pre-visit Questionnaire의 의미

공단은 검진 전 웹 문진표와 일부 차수부터 발달선별검사지 작성을 지원한다.

육아앱이 평소 데이터를 잘 가지고 있다면:
```
Daily Log
→ Pre-fill / Summary
→ Visit Preparation
```
로 발전할 수 있다.

단, 공식 문진을 민간 앱이 임의 대체해서는 안 된다.

## 6. Clinical Handoff

검진 결과 이상 시:
- 소아청소년과
- 안과
- 이비인후과
- 발달 전문기관

등으로 의뢰될 수 있다.

즉 검진 시스템은:

```
Monitoring
→ Screening
→ Referral
```

이라는 명확한 의료 escalation chain을 갖는다.

## 7. 민간 앱이 추가할 수 있는 가장 큰 가치

### 검진 전
- 검진 가능 기간 알림
- 병원 찾기
- 부모 질문 누적
- 최근 수유/수면/배변 요약
- 성장 측정값 정리
- 예방접종 기록 연결

### 검진 후
- 부모가 받은 설명 기록
- follow-up 일정
- 결과 PDF/사진 보관
- 다음 검진 시점

## 8. 중요한 데이터 구분

```
Parent observation
≠
K-DST screening result
≠
Doctor diagnosis
```

제품에서 동일한 "발달 상태" 필드로 합치면 안 된다.

## 9. 강점

- 생애주기 기반 공식 프로토콜
- 발달과 성장 통합
- 부모교육 포함
- 사전문진
- 의료기관 연결
- 결과 후 referral 구조

## 10. 한계

- 일상 기록과 직접 연결되지 않음
- 부모가 검진 사이 기간의 변화를 관리하기는 어려움
- 사용자 경험이 행정 중심
- 여러 서비스/화면을 이동해야 할 수 있음

## 11. 가져올 패턴

1. **Eligibility Window**
2. **Pre-visit Preparation**
3. **Official Screening Boundary**
4. **Doctor Question Inbox**
5. **Result → Follow-up Tasks**
6. **Clinical Handoff**
7. **Age-specific Parent Education**

## 12. 근거

- https://www.nhis.or.kr/static/html/wbma/c/wbhaca04800_2024.pdf
- https://health.kdca.go.kr/healthinfo/biz/health/gnrlzHealthInfo/gnrlzHealthInfo/gnrlzHealthInfoView.do?cntnts_sn=6671
- https://health.kdca.go.kr/healthinfo/biz/health/ntcnInfo/healthSourc/thtimtCntnts/thtimtCntntsView.do?thtimt_cntnts_sn=131

## 결론

영유아 검진은 육아앱의 별도 일정 기능이 아니라 **평소 기록을 공식 건강관리로 전달하는 핵심 clinical handoff point**로 설계할 가치가 있다.
