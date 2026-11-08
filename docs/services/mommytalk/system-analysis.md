# 마미톡 — 기술·데이터·문제 해결 분석

## 1. 공개 기술 현황

내부 제품코드는 공개 확인하지 못했다. [U]

서비스 경계상 최소 다음 시스템이 필요하다.

- hospital/ultrasound integration
- pregnancy profile
- baby profile
- daily event log
- statistics
- content CMS
- community
- commerce

## 2. 핵심 데이터 모델

[C]

```
User
PregnancyProfile
UltrasoundAsset
Baby

CareEvent
├─ feeding
├─ sleep
├─ elimination
├─ food
├─ temperature
├─ medication
└─ visit

Content
CommunityPost
```

## 3. 얽힌 문제 — 병원 데이터와 생활데이터의 신뢰도가 다름

초음파/병원 산출물과 사용자가 직접 입력한 육아기록을 같은 source로 보면 안 된다.

각 데이터에:
- source
- created_by
- verified_at

같은 provenance가 필요하다.

## 4. 얽힌 문제 — 임신앱은 출산 순간 churn 위험이 큼

해법:
```
Pregnancy Utility
→ Birth Transition
→ Baby Utility
```

출산 후 immediately useful한 tracker가 있어야 관계가 끊기지 않는다.

## 5. 얽힌 문제 — 건강정보와 커뮤니티

의료감수 콘텐츠와 사용자 경험담은 구조적으로 분리해야 한다.

```
Expert Knowledge
≠
Community Experience
```

검색 결과에서도 source badge가 필요하다.

## 6. 통계 구조

일/주 통계는 event log에서 파생되어야 한다.

사용자가 총량/평균을 다시 입력해서는 안 된다.

## 7. 우리 시스템에 일반화

실세계 기관에서 발생하는 결과물을 앱 activation에 쓰는 패턴은:
- 병원
- 어린이집
- 검진
- 예방접종

등에도 확장 가능하다.
