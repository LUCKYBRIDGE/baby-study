# BabySparks — 공식 사이트·가입·기관상품 직접 관찰

> 관찰일: 2026-11-08  
> 근거: 공식 Home / Register / Employers  
> 레벨: A1

## 1. 실제 사이트 구조

메인에서 큰 축은 세 가지다.

```
Online Parenting Classes
Parenting App
Parent Resources
```

즉 아기에게 해줄 활동과 부모가 배울 내용을 명확히 분리한다.

### Parenting App
- 0~3세
- personalized activities
- milestones
- 하루 20분

### Classes
- sleep
- nutrition
- discipline
- potty training 등
- on-demand
- live
- private coaching

## 2. "20분"이 제품 단위

BabySparks는 기능보다 **하루 20분**이라는 사용량을 메시지로 만든다.

이는 프로그램 자체를:
```
매일 약간씩 실행
→ 반복
→ progress
```
형태로 습관화한다.

좋은 점:
- 사용 기대치 명확
- 부모의 선택부담 감소

위험:
- 못한 날을 실패처럼 느낄 수 있음

따라서 통합 앱에서는 streak보다 "가능할 때 하나" 같은 유연한 디자인이 더 안전하다.

## 3. 가입 화면을 직접 보면 prematurity가 onboarding input

공식 Register 화면에서:
> 조산아는 실제 출생일보다 예정일 기준으로 발달할 수 있어 due date를 제공하면 추천 활동/마일스톤을 조정

한다고 직접 설명한다.

즉 corrected-age logic이 숨은 고급설정이 아니라 **가입 데이터**다.

필요 profile:

```
birth_date
due_date
prematurity_context
```

## 4. Premium에서 실제로 제공하는 것

등록/결제 화면에서 확인:
- 1,300+ development activities & milestones
- expert-created program
- weekly development reports
- 상황별 activity browse
- expert articles
- 최대 5 devices sync
- family/caregivers
- 최대 5 babies

즉 개인 B2C 상품에서도:
- multi-device
- caregiver
- multi-child

가 core premium value다.

## 5. B2B 구조가 매우 구체적

Childcare/organization 계열 상품에서 직접 확인되는 것:

- 가족을 home program으로 invite
- child progress 실시간 tracking
- 가족과 progress 공유
- unlimited children
- unlimited caregivers
- unlimited locations
- desktop dashboard

즉 데이터 계층을 다음처럼 볼 수 있다.

```
Organization
├─ Location
│  ├─ Caregiver
│  ├─ Child
│  └─ Progress
└─ Family connection
```

이건 어린이집/발달센터용 시스템 설계에도 바로 참고할 수 있다.

## 6. Employer 상품까지 확장

Employers 페이지에서는:
- working parents
- 600+ online courses
- 175+ experts
- 0~3 development program

을 employee benefit로 묶는다.

즉 같은 콘텐츠/프로그램을:

```
B2C parent
B2B childcare
B2B employer
```

세 채널로 재사용한다.

이는 콘텐츠 플랫폼의 확장성이 얼마나 중요한지 보여준다.

## 7. 제품 데이터 루프

```
Child profile
→ daily activity program
→ completion/observation
→ milestone progress
→ weekly report
→ next activity
```

단순 콘텐츠 library보다 **curriculum engine**에 가깝다.

## 8. 직접 관찰 결론

BabySparks의 강점은 activity 수가 많다는 데 있지 않다.

실제 구조의 핵심:

1. corrected age를 onboarding에서 처리
2. 하루 활동을 프로그램 단위로 큐레이션
3. progress를 가족과 공유
4. 동일 시스템을 개인/기관/기업으로 확장

이다.

## 9. 직접 확인한 페이지

- https://babysparks.com/
- https://babysparks.com/register/
- https://babysparks.com/employers/
