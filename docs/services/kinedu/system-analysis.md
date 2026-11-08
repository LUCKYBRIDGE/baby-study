# Kinedu — 기술·데이터·문제 해결 분석

## 1. 공개 기술 현황

제품 내부 framework/DB/API는 공개 확인하지 못했다. [U]

공식 Science 설명으로 확인되는 것은 **개념 모델**이다.

- 414 milestones
- 46 skills
- 4 developmental areas
- caregiver report
- 연령 패턴 비교
- progression state

## 2. 개념 데이터 모델

[C]

```
Baby
├─ birth_date
├─ due_date / corrected_age
└─ observations[]

MilestoneDefinition
├─ area
├─ skill
├─ expected_age_distribution
└─ observable_behavior

Observation
├─ milestone_id
├─ response
└─ observed_at

SkillState
├─ Upcoming
├─ Reinforce
├─ OnTrack
└─ Mastered

Activity
└─ target_skills[]
```

## 3. 얽힌 문제 — 발달은 binary가 아님

단순:
`했다 / 못했다`

로 저장하면 emerging skill을 표현할 수 없다.

Kinedu는 progression state로 문제를 푼다.

## 4. 얽힌 문제 — 결과만 보여주면 행동이 없음

발달평가만 하면 부모가:
> 그래서 뭘 해야 하지?

상태에 머문다.

해법:
```
assessment
→ skill state
→ today activity
```

## 5. 얽힌 문제 — 비교가 불안을 만듦

개인화는 또래 데이터가 필요하지만 결과를 percentile처럼 과도하게 보여주면 경쟁이 된다.

따라서:
- 다음 skill
- 강점
- 지원할 영역
- 활동

중심 표현이 더 안전하다.

## 6. corrected age

조산아의 calendar age와 발달 기대값을 동일하게 쓰지 않는다.

Profile에 due date/gestational context가 필요함을 보여준다.

## 7. Daily Utility + Long-term Value

발달 평가는 자주 하지 않는다.

그래서 daily activity/baby tracker가 retention을 만들고, assessment/profile이 장기 가치를 만든다.

```
Daily action
+
Periodic assessment
```

## 8. 우리 시스템에 일반화

발달 모듈은:
- 행동 정의: Pathways
- progression/recommendation: Kinedu
- 안전 경계: CDC

를 결합하는 것이 적절하다.
