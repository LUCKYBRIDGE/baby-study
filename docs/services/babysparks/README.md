# BabySparks — 서비스 정본 분석

> 유형: 0~3세 발달 활동 / 부모교육 / 기관관리  
> 공개 제품코드: 확인 못함 [U]  
> 직접 검증: 공식 Home / Register / Employers [A1]

## 1. 서비스 정의

BabySparks는 **발달 지식을 매일 실행할 수 있는 짧은 활동 프로그램으로 바꾸고, milestone·주간 progress·부모교육·기관 dashboard까지 연결하는 커리큘럼 플랫폼**이다.

## 2. 제품 구조

```
Child Profile
├─ Daily Program
│  └─ Activities
├─ Milestones
├─ Weekly Progress
├─ Browse Activities
├─ Parent Classes
└─ Family / Organization
```

## 3. 공개 코드/폴더 구조

공식 제품 repository는 확인하지 못했다.

동명 GitHub 저장소는 공식 연결 근거가 없어 제외한다.

## 4. 핵심 가치

"1,000개 활동"보다 중요한 것은 **오늘 할 활동을 시스템이 골라주는 것**이다.

```
Child State
→ Daily Program
→ Activity
→ Observation/Completion
→ Weekly Progress
```

## 5. Onboarding

[A1]

조산아의 경우 due date를 받아 추천 활동과 milestone 기대값을 조정한다.

즉 corrected age가 onboarding data다.

## 6. 확장 구조

B2C:
- 한 가족
- 다자녀
- 여러 caregiver

B2B:
- organization
- location
- caregiver
- child
- family link

Employer:
- working parent benefit

하나의 curriculum/content engine을 여러 채널에 재사용한다.

## 7. 가장 잘 푼 문제

- 발달지식의 실행 전환
- 선택 과부하 감소
- 가정과 기관의 progress 공유
- 부모교육과 아이활동 분리

## 8. 위험

- 놀이를 숙제로 만들 수 있음
- progress가 성적처럼 보일 수 있음
- content 양이 많아도 추천 정확도가 낮으면 가치 감소

## 9. 참고할 패턴

- Daily Program
- Activity ↔ Milestone Link
- Corrected-age Onboarding
- Weekly Reflection
- B2C/B2B Shared Engine

## 10. 관련 문서

- [화면·UI·UX](surface-map.md)
- [기술·데이터·문제 해결](system-analysis.md)
- [직접 관찰](../../direct-inspection/apps/babysparks-site.md)
