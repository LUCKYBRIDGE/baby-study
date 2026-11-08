# CDC Milestone Tracker — 공식 사이트 직접 관찰

> 관찰일: 2026-11-08  
> 근거: CDC 공식 Milestone Tracker / Digital Checklist  
> 레벨: A1

## 1. 공식 범위

CDC는 Milestone Tracker를 **2개월~5세** 발달 모니터링 도구로 정의한다.

핵심 domain:
- plays
- learns
- speaks
- acts
- moves

## 2. 기능을 직접 확인

공식 페이지가 나열하는 기능:

- 여러 아이 등록
- interactive illustrated checklist
- prematurity corrected age
- milestone photos/videos
- tips/activities
- act-early guidance
- PDF/email milestone summary
- well-visit snapshot
- family resources
- doctor appointment tracking
- developmental screening reminders

여기서 중요한 건 단순 체크리스트보다 **clinical handoff 기능이 많다는 것**이다.

## 3. 온라인 checklist와 앱의 관계

CDC 웹에는 별도로:
- 2m
- 4m
- 6m
- 9m
- 1y
- 15m
- 18m
- 2y
- 30m
- 3y
- 4y
- 5y

연령별 digital checklist가 있다.

즉 콘텐츠 정의는 웹과 앱이 공유 가능한 구조이며, 앱은 여기에:
- child profile
- 저장
- reminder
- summary

를 붙인 product layer로 볼 수 있다.

## 4. "모니터링" 경계를 반복해서 명시

공식 페이지는 앱이 AAP가 권장하는 validated standardized developmental screening tool을 대체하지 않는다고 명시한다.

즉:
```
Milestone Monitoring
≠
Standardized Screening
≠
Diagnosis
```

을 제품 차원에서 명확히 분리한다.

한국에서는:
```
일상 milestone tracker
≠
K-DST
≠
전문의 평가
```
로 같은 원칙을 적용해야 한다.

## 5. PDF/email summary

CDC 앱의 특히 좋은 기능이다.

일상 관찰을:
```
App-only data
```
에 가두지 않고
```
Doctor-shareable summary
```
로 변환한다.

통합 육아앱에서는:
- 최근 milestone 관찰
- 우려사항
- 질문
- 성장/생활 요약

을 함께 묶는 방향이 더 강력하다.

## 6. Well Visit Snapshot

의사 방문에서 받은 정보를 앱에 다시 기록하는 기능도 있다.

따라서 데이터가 일방향이 아니다.

```
Home observation
→ Doctor visit
→ Visit information
→ Home follow-up
```

의 양방향 loop다.

## 7. 개인정보

CDC는 이 앱을 통해 사용자/아동을 식별할 수 있는 개인정보를 수집·공유하지 않는다고 공식 페이지에 명시한다.

공공 발달앱의 **data minimization reference**로 가치가 높다.

## 8. 공개 코드 현황

CDC GitHub 조직에서 Milestone Tracker의 현재 공식 제품 repository는 이번 조사에서 찾지 못했다.

공식 페이지는 Georgia Tech Computing for Good 학생들이 개발에 기여했다고 밝히지만, 이를 근거로 임의의 GitHub 저장소를 공식 소스로 간주하지 않았다.

## 9. 직접 관찰 결론

CDC Milestone Tracker의 가장 중요한 구조:

```
Observe
→ Illustrated checklist
→ Concern
→ Summary
→ Appointment/doctor
```

이다.

상업앱처럼 retention을 극대화하는 게 아니라 **부모 관찰의 질과 의료진 전달 품질을 높이는 것**이 목적이다.

## 10. 직접 확인

- https://www.cdc.gov/act-early/milestones-app/
- https://www.cdc.gov/act-early/digital-online-checklist/
