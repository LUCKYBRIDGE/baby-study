# 질병관리청 예방접종도우미 Deep Dive — 구조·기능·문제 해결 방식

> 조사 기준일: 2026-11-08  
> 공식: https://nip.kdca.go.kr/

## 1. 서비스 한 문장

예방접종도우미는 **국가의 최신 예방접종 기준·지원사업·개인 접종내역·사전알림·위탁의료기관 탐색을 연결하는 authoritative vaccination system**이다.

## 2. 핵심 구조

```
Official Vaccine Knowledge
├─ National Program
├─ Vaccine Guidelines
├─ Seasonal Programs
└─ Vaccine Information

Personal Management
├─ Child Registration
├─ Vaccination History
└─ Notification Consent

Action
├─ Pre-notification
├─ Find Contracted Institution
└─ Consultation / vaccination
```

## 3. 이 시스템의 핵심은 '달력'이 아니다

예방접종 일정은 변한다.

2026년에도:
- 국가예방접종사업 기준
- 인플루엔자 대상 연령
- 사업기간
- 지침 문서

가 업데이트되고 있다.

따라서 민간 앱이 일정을 복사해 하드코딩하면 장기적으로 위험하다.

필요한 데이터 구조:

```
Schedule Definition
├─ authority
├─ version
├─ reviewed_at
├─ eligibility
├─ vaccine
├─ dose
└─ recommended window
```

## 4. 개인 접종기록과 공식 일정은 다른 데이터

```
Official Schedule
≠
Child Actual Record
```

예:
- "BCG 권장" = schedule
- "2026-12-20 접종" = actual

이 둘을 분리해야:
- 지연
- 누락
- 이미 접종
- 계절 캠페인

을 안전하게 처리할 수 있다.

## 5. 사전알림 시스템

공식 안내에서 자녀 예방접종관리 내:
- 아이 예방접종내역 조회
- 개인정보 수정
- 문자 알림 동의

구조를 확인할 수 있고, 국민비서 채널을 통한 필수예방접종 알림도 지원한다.

즉 알림은 단순 앱 push가 아니라 **국가 notification infrastructure**와 연결된다.

## 6. 계절성 프로그램

인플루엔자처럼:
- 매년 대상
- 시작/종료일
- 1회/2회 여부

가 달라지는 프로그램은 birth-based schedule과 별도 모델로 관리해야 한다.

```
Routine Vaccination
+
Seasonal Campaign
```

## 7. 의료기관 연결

국가사업은 위탁의료기관/보건소에서 지원된다.

따라서 complete user journey는:

```
Eligibility
→ Reminder
→ Find Institution
→ Confirm availability
→ Visit
→ Actual Record
```

이다.

## 8. 지연/예외의 안전 처리

공식 페이지는 일정·횟수에 대해 예진의사와 상담하도록 안내하는 경우가 있다.

민간 앱은 특수상황에서 자체 재계산을 확정적으로 제시하지 말고:
- 공식 기준 원문
- 의료기관
- 의료진 상담

으로 escalation해야 한다.

## 9. 강점

- authoritative source
- 최신성
- 실제 접종 기록과 연결
- 알림
- 의료기관 탐색
- 지침 원문 제공

## 10. 한계

- 일반 부모에게 정보가 복잡함
- 전문 행정/지침 구조가 깊음
- UX보다 정확성과 행정성이 우선됨

## 11. 민간 앱에 가져올 패턴

1. **Source-versioned schedule**
2. **Official schedule / actual record 분리**
3. **Routine / seasonal program 분리**
4. **Eligibility window**
5. **Reminder → provider search**
6. **Exception escalation**
7. **최종검토일 표시**

## 12. 근거

- https://nip.kdca.go.kr/irhp/infm/goVcntInfo.do?menuCd=131
- https://nip.kdca.go.kr/irhp/infm/goVcntInfo.do?menuCd=134
- https://nip.kdca.go.kr/irhp/infm/goVcntInfo.do?menuCd=138
- https://nip.kdca.go.kr/irhp/infm/goVcntInfo.do?menuCd=162

## 결론

예방접종 기능은 단순 체크리스트가 아니라 **버전 관리되는 규칙 엔진 + 실제 기록 + 알림 + 기관 연결**로 설계해야 한다.
