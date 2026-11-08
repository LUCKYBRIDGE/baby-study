# BabyTime — 페이지·UI·UX·버튼 지도

## 1. 진입점과 전역 상태

[A2]

사용자는 현재 선택된 **아기 프로필**을 기준으로 모든 기록을 본다. 다자녀일 경우 프로필 사진 롱탭 또는 프로필 화면의 선택 UI로 아이를 전환한다.

즉 전역 context는:

```
Current Baby
+
Current Date
```

다.

## 2. 화면 트리

```
Main / Activity
├─ 빠른 활동 아이콘
├─ 오늘의 기록 목록
└─ 생성된 기록 상세 수정

Pattern
├─ 일과표
│  ├─ 날짜 이전/다음
│  └─ 활동별 표시 on/off
└─ Pattern
   └─ 선택 활동의 interval

Stats
├─ Day
├─ Week
├─ Month
├─ 그래프 추가/삭제
└─ 그래프 순서 변경

Profile
├─ Baby switch
├─ 성장곡선
├─ 다이어리
└─ 공동양육자 초대

Community
└─ D+day 이동/검색
```

## 3. Activity 화면의 핵심 UI

### 빠른 기록 버튼
[A2]

상단의 활동 아이콘은 단순 "폼 열기" 버튼이 아니라 **record creation trigger**다.

```
[수유] [수면] [기저귀] [유축] ...
   ↓
즉시 이벤트 생성
```

### 생성된 기록 row
기록 생성 후 목록 row 자체가 다시 편집 진입점이 된다.

이 방식은:
- capture와 edit를 분리
- 야간/한 손 사용에서 tap 수 감소
- 세부정보를 나중에 보완 가능

이라는 장점이 있다.

### 활동 아이콘 재정렬
사용 빈도에 따라 순서를 바꿀 수 있다. 사용자가 사실상 자신의 월령별 홈을 직접 조정하는 셈이다.

## 4. 시간형 기록 UI

수면·모유수유·목욕 등은 시작/종료/지속시간이 중요하다.

[A2]

공식 FAQ에서 시간 수정과 stopwatch 계열 동작이 확인된다.

좋은 UX 포인트:
- 모든 이벤트에 timer를 강요하지 않음
- 시간형 domain만 duration을 강조
- 기록 이후에도 시작/종료 시각 수정 가능

## 5. Pattern 화면

### 일과표
- 날짜 이동
- 활동별 toggle
- 같은 시간축에 여러 이벤트 배치

### Interval
특정 활동의 **다음 이벤트까지 걸린 시간**을 읽게 한다.

예:
```
수유 08:10
  ↓ 2h 47m
수유 10:57
```

이것은 육아에서 매우 유용한 데이터 projection이다.

## 6. Stats 화면

- Day / Week / Month
- 원하는 graph만 추가
- graph 삭제
- graph order 변경

즉 고정 dashboard보다 **사용자 조립형 dashboard**에 가깝다.

## 7. 공동양육 UI

[A2]

```
Profile
→ 공동양육자 초대
→ 관계 선택
→ 6자리 코드
→ 상대 입력
→ Baby workspace 연결
```

여기서 관계 label을 받는다는 점이 중요하다.

## 8. Community UI

또래 탐색이 달력 날짜가 아니라 `D+N`을 기준으로 한다.

버튼/행동:
- 이전 일령
- 다음 일령
- 특정 D+day 입력

일반 게시판보다 월령 맥락이 강하다.

## 9. UX 강점

- 기록 생성 우선
- 행동 버튼이 바로 눈에 보임
- 상세입력은 후순위
- 보여줄 활동을 줄일 수 있음
- 같은 데이터를 여러 projection으로 읽음

## 10. 미확인 네이티브 UX

[U]

공개 웹/FAQ만으로는 다음을 확정하지 않았다.

- 현재 최신 앱의 exact bottom navigation
- dark mode 품질
- widget
- lock-screen
- offline conflict resolution
- push permission flow
- 실제 haptic
- 기록 취소/undo UX
