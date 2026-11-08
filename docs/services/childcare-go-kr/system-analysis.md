# 아이사랑 — 기술·정보구조·문제 해결 분석

## 1. 공개 기술 현황

내부 source/backend는 공개 분석하지 않았다. [U]

제품적으로 중요한 것은 **taxonomy와 행정 연결**이다.

## 2. 개념 데이터 구조

[C]

```
AgeStage
ParentingDomain
OfficialContent
├─ source
├─ reviewed_at
└─ age_range

ChildcareFacility
├─ location
├─ type
├─ capacity
├─ evaluation
└─ transport

Household / Support
Notice
Consultation
```

## 3. 얽힌 문제 — 월령마다 정보는 달라지지만 메뉴를 매번 바꾸면 학습비용 증가

해법:
```
Stable Categories
+
Changing Content
```

## 4. 얽힌 문제 — 육아정보에서 실제 행정으로 넘어감

민간 콘텐츠는 읽고 끝나는 경우가 많다.

아이사랑은:
`정보 → 기관검색 → 신청/결제/소통`

으로 실제 action까지 이어진다.

## 5. Provenance

공공정보는 source와 기준연도를 명시한다.

민간앱도 공식 건강정보를 재가공할 때:
- source URL
- last reviewed
- effective period

를 데이터 필드로 가져야 한다.

## 6. 우리 시스템에 일반화

아이사랑은 예쁜 UX 참고보다 **한국 육아 coverage taxonomy와 institution transition**을 설계 기준으로 쓰는 것이 더 가치가 크다.
