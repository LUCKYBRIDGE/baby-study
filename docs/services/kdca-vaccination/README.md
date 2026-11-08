# 질병관리청 예방접종도우미 — 서비스 정본 분석

> 유형: 공식 예방접종 일정 / 개인 접종내역 / 알림 / 의료기관 탐색  
> 직접 검증: 질병관리청 공식 사이트 [A1/A2]

## 1. 서비스 정의

예방접종도우미는 **국가의 최신 예방접종 규칙과 개인 실제 접종내역, 사전알림, 위탁의료기관 탐색을 연결하는 authoritative vaccination system**이다.

## 2. 실제 상위 IA

[A1]

```
예방접종 관리
├─ 본인 예방접종
└─ 가족/자녀 예방접종

예방접종 정보
├─ 분류/방법
├─ 표준 일정
├─ 감염병
└─ 국가사업

예방접종 알림터
코로나19
엠폭스
NIP 아카이브
```

## 3. 핵심 구조

```
Official Rule
+
Child Actual Record
+
Reminder
+
Provider
```

## 4. 일정은 정적 데이터가 아님

[A1]

2026년에도 사업대상, 지원백신, 인플루엔자 사업기간 등이 갱신된다.

따라서 앱에 "한 번 넣고 끝"으로 하드코딩하면 안 된다.

## 5. 가장 잘 푼 문제

- 무엇을 언제 맞아야 하나?
- 이미 무엇을 맞았나?
- 어디서 맞나?
- 놓치지 않으려면?
- 국가 지원 대상인가?

를 하나의 공식 시스템에서 해결한다.

## 6. 구조적 한계

- 행정/전문 정보 밀도가 높음
- 예외 상황을 일반 부모가 해석하기 어려움
- user-friendly lifecycle dashboard는 약함

## 7. 참고할 패턴

- Versioned Official Schedule
- Schedule ≠ Actual Record
- Eligibility Window
- Reminder Consent
- Provider Search
- Exception → Clinician

## 8. 관련 문서

- [페이지·UI·UX](surface-map.md)
- [기술·규칙엔진·문제 해결](system-analysis.md)
- [공공 시스템 직접 관찰](../../direct-inspection/web/korea-public-systems.md)
