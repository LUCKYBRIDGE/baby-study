# BabyTime — 서비스 정본 분석

> 유형: 육아 기록 / 공동양육 / 패턴 분석  
> 공개 제품코드: **확인하지 못함 [U]**  
> 직접 검증: 공식 홈페이지·FAQ [A1/A2]

## 1. 서비스 정의

BabyTime은 **수유·수면·기저귀 등 고빈도 사건을 최대한 빨리 기록하고, 동일 기록을 타임라인·간격·통계로 다시 읽게 하며, 여러 양육자가 같은 아기 상태를 공유하게 하는 이벤트 로그 중심 앱**이다.

## 2. 해결하는 핵심 문제

부모가 반복해서 겪는 문제는 다음이다.

- 마지막 수유가 언제였는지 기억하기 어렵다.
- 여러 사람이 돌보면 서로 인수인계해야 한다.
- 하루치 기록은 남지만 패턴은 눈으로 찾기 어렵다.
- 모든 기록 항목을 항상 쓰지는 않는다.
- 신생아 돌봄 중에는 긴 폼을 작성하기 어렵다.

BabyTime의 해결 방식은:

```
즉시 기록
→ 현재 상태 공유
→ 하루 일과
→ 이벤트 간격
→ 기간 통계
```

이다.

## 3. 전체 정보구조

[A1/A2]

```
Baby Context
├─ Activity
│  ├─ 수유
│  ├─ 수면
│  ├─ 기저귀
│  ├─ 유축
│  ├─ 목욕
│  ├─ 병원/기타
│  └─ 활동 아이콘 순서 조정
├─ Pattern
│  ├─ 일과표
│  └─ 이벤트 간격
├─ Stats
│  ├─ 일
│  ├─ 주
│  └─ 월
├─ Profile
│  ├─ 성장
│  ├─ 다이어리
│  └─ 사진
├─ Community
│  └─ D+day 기반 또래 다이어리
└─ Caregiver
   ├─ 엄마
   ├─ 아빠
   ├─ 베이비시터
   └─ 가족
```

## 4. 공개 파일·폴더 구조 현황

BabyTime 공식 앱/웹 제품의 공개 소스 저장소는 현재 분석 범위에서 확인하지 못했다.

따라서 다음과 같은 내부 구조는 **확정하지 않는다.**

- 프론트엔드 프레임워크
- 백엔드 언어
- DB 종류
- 내부 API route
- 앱 package 구조

대신 공식 UI/FAQ에서 관찰 가능한 **제품 구조**만 정리한다.

## 5. 핵심 데이터 흐름

[A2/C]

```
활동 아이콘 탭
→ 최소 Event 생성
→ 필요 시 상세 수정
→ 공유 Baby Timeline
→ Pattern/Interval projection
→ Day/Week/Month aggregation
```

여기서 중요한 점은 **상세 폼 완료보다 사건 포착을 먼저 성공시키는 것**이다.

## 6. 주요 반복 사용 루프

### 기록 루프
`사건 발생 → 탭 → 저장 → 마지막 상태 확인`

### 인수인계 루프
`양육자 A 기록 → 공유 상태 갱신 → 양육자 B 확인`

### 패턴 루프
`며칠 기록 → 일과/간격 확인 → 생활 패턴 이해`

### 추억 루프
`다이어리/사진 → 성장 기록 → 과거 회고`

## 7. 가장 잘 푼 문제

**기억 부담과 공동양육 인수인계 비용**을 가장 단순한 인터랙션으로 줄였다.

특히 Activity / Pattern / Stats를 분리하여 동일 데이터를 세 가지 질문에 답하게 한다.

- 무슨 일이 있었나?
- 어느 간격으로 반복되나?
- 기간 전체로 얼마나 했나?

## 8. 구조적 한계

- 예측/추천층은 Huckleberry/Napper보다 약하다.
- 의료/예방접종/검진까지 확장하려면 권한과 안전 경계가 더 정교해야 한다.
- 커뮤니티의 또래 비교는 불안 유발 가능성이 있다.
- 공개 코드가 없어 기술적 세부 동기화/오프라인 전략은 미확인이다.

## 9. 참고할 패턴

- Tap-first Event Creation
- Optional Detail After Capture
- Contextual Timer
- User-customizable Action Rail
- Timeline / Interval / Stats 분리
- Baby-centered Caregiver Invite
- Age-relative Community

## 10. 관련 문서

- [화면·UI·UX](surface-map.md)
- [기술·데이터·문제 해결](system-analysis.md)
- [직접 관찰 원문](../../direct-inspection/apps/babytime-site.md)
- [기존 Deep Dive](../../deep-dive/apps/babytime-deep-dive.md)
