# Napper — 서비스 정본 분석

> 유형: 수면 전문화 육아 앱  
> 공개 제품코드: 확인 못함 [U]  
> 직접 검증: 공식 Home / Pricing / Privacy [A1/A2]

## 1. 서비스 정의

Napper는 **수면 기록을 wake window와 개인화된 낮잠·취침 예측으로 바꾸어 부모가 하루 일정을 미리 준비하게 하는 수면 vertical 앱**이다.

## 2. 해결하는 핵심 문제

부모의 실제 질문은:
- 오늘 얼마나 잤나?
보다
- **다음 잠은 언제 올까?**
- **언제부터 재울 준비를 해야 할까?**
- **오늘 낮잠이 꼬였을 때 이후 일정은 어떻게 바뀌나?**

에 가깝다.

## 3. 전체 제품 구조

[A1]

```
Baby Sleep Profile
├─ Daily Sleep Tracking
├─ Age-based Schedule
├─ Personalized Sleep Analysis
├─ Trends / Statistics
├─ Sleep Course
├─ Sleep Sounds
└─ Additional Baby Tracking
```

## 4. 공개 파일/폴더 구조

공식 제품의 공개 코드 저장소는 확인하지 못했다.

따라서 내부 framework, backend, DB를 단정하지 않는다.

## 5. 핵심 데이터 흐름

```
Sleep Event
→ Wake Window
→ Personal Pattern
→ Next Nap / Bedtime
→ Reminder / Preparation
→ Actual Sleep
→ Recalculation
```

## 6. Cold Start → Personalization

초기에는 개인 데이터가 적기 때문에:
`age-based schedule`

이 필요하다.

기록이 쌓이면:
`age baseline + actual rhythm`

으로 이동한다.

이 구조는 수면뿐 아니라 수유·배변·놀이 추천에도 일반화 가능하다.

## 7. 가장 잘 푼 문제

- 과거 기록을 미래 행동으로 전환
- sleep domain에 깊게 집중
- 월령 기본값을 개인 데이터로 보정
- 부모가 앱을 보며 "다음 행동"을 준비하게 함

## 8. 구조적 위험

- prediction이 아이의 실제 졸림 신호보다 권위적으로 보일 수 있음
- 기록 누락 시 모델 왜곡
- 여행/질병/시차/성장변화 같은 outlier
- AI가 아기 데이터를 처리할 경우 privacy 부담

## 9. 참고할 패턴

- Vertical Depth
- Future-facing Dashboard
- Age Baseline → Personalized Model
- Prediction Feedback
- Preparation Reminder
- AI Data Transparency

## 10. 관련 문서

- [화면·UI·UX](surface-map.md)
- [기술·데이터·문제 해결](system-analysis.md)
- [직접 관찰](../../direct-inspection/apps/napper-site.md)
