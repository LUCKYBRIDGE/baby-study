# Kinedu — 직접 사이트/Assessment 관찰

> 관찰일: 2026-11-08  
> 근거: 공식 홈, Science, Assessment  
> 레벨: A1

## 1. 실제 최상위 웹 동선

공식 사이트 상단에서 확인되는 핵심 경로:
- Classes
- Blog
- Science
- How's my baby?
- Try free

즉 단순 app landing이 아니라:
```
Education
+
Scientific credibility
+
Assessment acquisition funnel
```
을 함께 운영합니다.

## 2. Assessment를 직접 따라가며 확인한 구조

공식 Assessment 페이지 첫 CTA:

> Less than 5 minutes · Not a diagnosis · Born early? Ages corrected automatically

이 한 줄에 제품의 중요 특성이 거의 다 들어 있습니다.

- 짧은 시간
- 의료적 한계 표시
- 조산아 교정연령

## 3. 가입 전 미리보기

사이트는 가입 전 **실제 평가 형태의 3문항 preview**를 보여줍니다.

예시 질문:
- 일상에서 실제로 보이는 행동
- 답변:
  - I see this
  - Not yet
  - I'm not sure

이 구조가 좋습니다.

일반적인 Yes/No에 `I'm not sure`를 넣어 부모가 억지로 판단하지 않아도 됩니다.

## 4. 실제 평가 구조

공식 설명:
- 32문항
- 5분 미만
- 나이에 따라 완전히 다른 질문
- 중간 저장 가능
- 일부 문항은 reading에 포함되지 않음

즉 assessment가 고정 체크리스트가 아니라 **age-adaptive question set**입니다.

## 5. 결과 구조

무료 결과:
- overall picture
- developmental age
- strongest area

유료 full profile:
- 4개 영역 전체
- 해당 나이의 milestone 전체
- 반복 평가
- progress curve
- emerging skill
- pediatrician summary

즉 paywall도:
```
간단한 답
→ 해석의 근거
→ 장기 추적
```
으로 설계되어 있습니다.

## 6. "Developmental age"의 UX

사이트는 예를 들어:
> Showing the skills of a typical 8-month-old

처럼 결과를 표현합니다.

장점:
- 부모가 직관적으로 이해
- 의료진에게 설명 쉬움

위험:
- 한 숫자로 아이 전체를 규정하는 느낌
- 빠름/느림 비교 유발

Kinedu도 이를 보완하기 위해:
- strongest area
- skills opening up
- "not a score"
- "story, not a verdict"

문구를 반복합니다.

## 7. 교정연령

조산아는 2세까지 자동으로 corrected age를 적용한다고 명시합니다.

이는 단순 설정 옵션이 아니라 **assessment engine의 입력값**입니다.

## 8. 의료적 boundary를 UI 전반에 반복

사이트 여러 위치에서:
- not a diagnosis
- developmental surveillance
- pediatrician과 상담

을 반복합니다.

고위험 UX에서 한 번의 면책문구보다 **맥락마다 boundary를 반복 노출하는 방식**이 더 좋습니다.

## 9. Science 페이지에서 직접 확인한 모델

- 414 milestones
- 46 skills
- 4 areas
- 3.5M children
- 280M+ answers
- caregiver report

그리고 skill status:
- Upcoming
- Reinforce
- On track
- Mastered

즉 내부 모델은 milestone checklist가 아니라 **연결된 skill trajectory**로 설명됩니다.

## 10. 제품 퍼널

```
SEO / Science / Blog
→ Free 5-min assessment
→ Immediate personalized result
→ Full profile subscription
→ App daily activities
```

가입보다 **개인화 가치 체험을 먼저** 제공합니다.

## 11. 직접 관찰로 얻은 시사점

### 좋은 점
- onboarding 전에 실제 경험을 보여줌
- 불확실성 답변 허용
- 조산아 처리
- 평가 결과를 다음 행동과 연결
- 의료 경계가 명확

### 주의할 점
- developmental age는 매우 강한 숫자
- 사용자에게 "성적"처럼 느껴질 수 있음

## 12. 참고

- https://www.kinedu.com/
- https://www.kinedu.com/science
- https://www.kinedu.com/assessment
