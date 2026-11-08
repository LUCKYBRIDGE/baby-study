# CDC Milestone Tracker Deep Dive — 구조·기능·문제 해결 방식

> 조사 기준일: 2026-11-08  
> 운영: U.S. CDC  
> 공식: https://www.cdc.gov/act-early/milestones-app/

## 1. 서비스 한 문장

CDC Milestone Tracker는 **2개월~5세의 발달 행동을 부모가 이해하고 체크하게 하되, 앱의 역할을 '모니터링과 의료진 대화 준비'로 제한하는 공공 보건형 발달 도구**다.

## 2. 전체 구조

```
Child Profile
├─ Age-based Checklist
│  ├─ Play
│  ├─ Learn
│  ├─ Speak
│  ├─ Act
│  └─ Move
├─ Photo / Video Examples
├─ Development Tips
├─ Concern Guidance
├─ Multiple Children
├─ Corrected Age
├─ Appointment Reminder
├─ Visit Notes
└─ Summary
   ├─ PDF
   └─ Email/share
```

## 3. 핵심 목표가 '점수'가 아니다

상업 발달앱은:
```
개인화 → 활동 추천 → retention
```

CDC:
```
관찰 → 이해 → 우려 인지 → 의료진과 대화
```

이다.

이 차이가 중요한 안전장치다.

## 4. 행동 예시를 이미지/영상으로 제공

발달 항목은 문장만으로 해석이 흔들릴 수 있다.

사진/영상 예시를 함께 제공하면:
- 부모의 관찰 기준 통일
- 잘못된 체크 감소
- 설명 비용 감소

효과가 있다.

발달 데이터에서 **input quality 개선 장치**인 셈이다.

## 5. Corrected Age

조산아를 고려한 corrected age 기능이 포함된다.

따라서 발달 시스템의 child profile에는 필요 시:
- birth date
- due date
- gestational context

가 들어가야 한다.

## 6. Concern Flow

좋은 발달앱은 "못함"에 빨간 경고만 띄우지 않는다.

CDC 모델:

```
Milestone Observation
→ Concern
→ What to do
→ Appointment
→ Notes/Summary
→ Healthcare Provider
```

즉 **clinical handoff**가 완성되어 있다.

## 7. PDF/Email Summary

데이터를 앱 내부에 가두지 않고 의료진에게 전달 가능한 형태로 변환한다.

이것은 매우 중요한 패턴이다.

진료 시 필요한 것은 모든 로그가 아니라:
- 체크 결과
- 부모 우려
- 질문
- 핵심 메모

의 간결한 요약이다.

## 8. Monitoring / Screening / Diagnosis 구분

CDC는 milestone checklist가 표준화된 발달 선별검사를 대체하지 않는다는 점을 명확히 한다.

제품에서 이 세 단계를 분리해야 한다.

```
Monitoring
≠ Screening
≠ Diagnosis
```

한국에서는 일반 milestone tracker와 K-DST도 반드시 별개로 다뤄야 한다.

## 9. 개인정보 철학

공식 설명상 CDC가 개인 식별정보를 수집/공유하지 않는다고 안내한다.

발달 데이터는 장기간 민감할 수 있으므로 공공형 제품의 **최소수집 원칙**이 좋은 기준이 된다.

## 10. 강점

- 목적이 안전하게 제한됨
- 행동 예시가 명확
- 조산아 고려
- 진료용 export
- concern → healthcare 흐름
- 상업적 불안 자극이 적음

## 11. 한계

- 개인화 활동 추천은 제한적
- 미국 체계라 한국 의료 연결에 그대로 쓸 수 없음
- 세밀한 생활기록과는 분리됨

## 12. 가져올 패턴

1. **Behavior Example**
2. **Corrected-age Support**
3. **Concern Escalation Path**
4. **Doctor-ready Summary**
5. **Monitoring ≠ Screening Label**
6. **Data Minimization**

## 13. 결론

CDC 앱은 "발달 기능을 얼마나 많이 넣을까"보다 **어디까지 앱이 말하고 어디서 전문가에게 넘길까**를 설계하는 기준점이다.
