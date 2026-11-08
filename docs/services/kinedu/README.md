# Kinedu — 서비스 정본 분석

> 유형: 영유아 발달 평가 / 개인화 활동  
> 공개 제품코드: 확인 못함 [U]  
> 직접 검증: 공식 Home / Assessment / Science [A1]

## 1. 서비스 정의

Kinedu는 **부모의 일상 관찰을 발달 skill model로 바꾸고, 그 모델을 오늘 실행할 맞춤 활동과 장기 progress report로 변환하는 발달 개인화 플랫폼**이다.

## 2. 핵심 문제

부모 질문:
> 우리 아기가 다른 아이보다 빠른가?

보다 제품이 바꾸려는 질문은:
> 지금 우리 아기와 무엇을 해주면 되는가?

다.

## 3. 전체 구조

```
Baby Profile
├─ Assessment
│  ├─ age-adaptive questions
│  ├─ prematurity correction
│  └─ uncertainty answer
├─ Skill Model
│  ├─ 414 milestones
│  ├─ 46 skills
│  └─ 4 areas
├─ Daily Activities
├─ Progress Report
├─ Expert Content/Class
└─ Daily Baby Tracker
```

## 4. 공개 코드/폴더 구조

공식 모바일 제품의 공개 저장소는 확인하지 못했다.

Kinedu GitHub 조직에 다른 오픈소스 프로젝트가 존재해도 현재 앱의 제품코드라는 근거가 없으므로 분석에서 제외한다.

## 5. 핵심 데이터 흐름

```
Caregiver Observation
→ Age-aware Interpretation
→ Skill State
→ Recommended Activity
→ Parent/Baby Interaction
→ New Observation
```

## 6. activation 구조

```
웹 방문
→ 실제 3문항 preview
→ 5분 미만 assessment
→ 개인화 결과
→ 상세 profile/구독
```

기능 탐색보다 **자기 아이 결과**를 먼저 보여준다.

## 7. 가장 잘 푼 문제

- 발달 체크를 단순 yes/no에서 progression으로 확장
- 관찰을 행동 추천으로 연결
- 조산아 교정연령을 onboarding 단계에서 고려
- "진단 아님" boundary를 반복적으로 명시

## 8. 위험

- developmental age가 점수처럼 느껴질 수 있음
- caregiver report bias
- 문화/언어 차이
- 활동 추천이 "과제"가 될 위험

## 9. 참고할 패턴

- Assessment as Activation
- Uncertain Answer Option
- Skill Graph
- Multi-state Progress
- Observation → Recommendation
- Parent-mediated Activity
- Medical Boundary

## 10. 관련 문서

- [화면·UI·UX](surface-map.md)
- [기술·데이터·문제 해결](system-analysis.md)
- [직접 관찰](../../direct-inspection/apps/kinedu-site.md)
