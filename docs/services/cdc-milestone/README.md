# CDC Milestone Tracker — 서비스 정본 분석

> 유형: 공공 발달 모니터링 앱  
> 운영: U.S. CDC  
> 공개 현재 제품코드: 확인 못함 [U]  
> 직접 검증: CDC 공식 사이트 [A1]

## 1. 서비스 정의

CDC Milestone Tracker는 **2개월~5세 아이의 발달 행동을 부모가 사진·영상 예시와 함께 관찰하고, 우려가 있을 때 의료진과 대화할 수 있는 요약과 진료 준비로 연결하는 공공 보건 도구**다.

## 2. 공식 기능

[A1]

- multiple children
- illustrated checklists
- corrected age
- photos/videos
- tips/activities
- act-early guidance
- PDF/email milestone summary
- well visit snapshot
- family resources
- appointment tracking
- screening reminders

## 3. 공개 코드/폴더 구조

현재 공식 앱 repository는 CDC GitHub에서 확인하지 못했다.

공식 페이지는 Georgia Tech Computing for Good의 개발 기여를 밝히지만, 임의의 GitHub 저장소를 공식코드로 간주하지 않는다.

## 4. 핵심 사용자 흐름

```
Observe
→ Checklist
→ Example
→ Concern
→ Summary
→ Doctor / Care Provider
```

## 5. 가장 중요한 경계

CDC가 직접:
`Milestone Tracker ≠ validated standardized developmental screening`

을 명시한다.

즉:
```
Monitoring
≠ Screening
≠ Diagnosis
```

## 6. 가장 잘 푼 문제

- 부모 관찰 기준의 모호함
- 의료진에게 설명하기 어려움
- 우려가 생겼을 때 다음 행동이 불명확함

## 7. 데이터 철학

CDC는 앱에서 사용자/아동을 식별 가능한 개인정보를 수집·공유하지 않는다고 안내한다.

공공형 privacy minimalism의 기준점이다.

## 8. 참고할 패턴

- Illustrated Checklist
- Corrected Age
- Concern Escalation
- Doctor-ready PDF
- Well Visit Snapshot
- Data Minimization

## 9. 관련 문서

- [페이지·UI·UX](surface-map.md)
- [기술·안전·문제 해결](system-analysis.md)
- [직접 관찰](../../direct-inspection/apps/cdc-milestone-site.md)
