# Napper Deep Dive — 구조·기능·문제 해결 방식

> 조사 기준일: 2026-11-08  
> 공식 근거: Napper 공식 제품/가격/개인정보/수면 가이드

## 1. 서비스 한 문장

Napper는 **수면 로그를 다음 낮잠·취침 시간 예측과 하루 일정으로 변환하는 수면 전문화(vertical) 육아 앱**이다.

## 2. 전체 제품 구조

```
Baby Sleep Profile
├─ Daily Sleep Tracking
├─ Age-based Sleep Schedule
├─ Personalized Sleep Analysis
├─ Trends & Statistics
├─ Sleep Course
├─ Sleep Sounds
├─ Other Baby Tracking
│  ├─ Feeding
│  ├─ Diaper
│  └─ Pumping etc.
└─ AI-based personalized insights
```

공식 가격 페이지상 무료/Unlimited 구조로 나뉘며, Unlimited는 수면 분석·개인화, 수면 코스, 수면음, 통계, 무제한 tracking category를 포함한다.

## 3. 문제 정의

수면앱이 풀어야 할 진짜 질문은:
- 오늘 총 몇 시간 잤나?
보다
- **다음 잠은 언제 준비해야 하나?**
- **외출은 언제 잡아야 하나?**
- **오늘 낮잠이 짧았는데 뒤 일정은 어떻게 바뀌나?**

다.

Napper는 로그를 미래 계획에 쓰는 방향으로 설계되어 있다.

## 4. 핵심 데이터 루프

```
Sleep Event
→ Wake Window
→ Pattern
→ Personalized Schedule
→ Nap/Bedtime Prediction
→ Reminder
→ Actual Sleep Event
→ Schedule Recalibration
```

이 구조는 기록 서비스가 예측 서비스로 발전하는 전형적인 형태다.

## 5. 정적 기준과 개인화의 층

Napper는 age-based schedule과 personalized schedule을 모두 둔다.

### Cold Start
개인 데이터가 없을 때:
```
Age-based Default
```

### Warm State
며칠 기록 후:
```
Age Default
+
Baby's Actual Rhythm
→ Personalized Schedule
```

공식 수면가이드도 며칠간 수면을 기록하면 자연스러운 리듬에 적응한 개인 일정이 생성된다고 설명한다.

이 패턴은 수면뿐 아니라 수유·배변·놀이 추천에도 적용 가능하다.

## 6. 홈에서 가장 중요한 정보

수면 전문 앱의 홈은 통계보다 **다음 예정 상태**가 중요하다.

이상적인 정보 우선순위:

```
Next Nap
├─ 예상 시간
├─ 준비 시작 시간
├─ 현재 깨어있는 시간
└─ 오늘 실제 수면 흐름

Then
└─ Daily totals / trend
```

즉 future-facing dashboard다.

## 7. 예측의 UX 원칙

수면은 확률적이다.

따라서:
- "14:31에 재우세요" 같은 단일 확정값보다
- 시간 범위
- 아이 신호 우선 안내
- 최근 데이터 근거
- 예측이 틀렸을 때 빠른 수정

이 적절하다.

예:
```
다음 낮잠 예상 14:20~14:45
최근 3일 기록을 기준으로 계산됨
[잠들었어요] [아직 안 졸려요]
```

## 8. 콘텐츠와 제품 기능의 연결

Napper 공식 블로그는 월령별 수면 스케줄을 제시하되:
- 건강한 만삭아 기준
- 개인차
- 의료진 조언 우선

을 명시한다.

이는 좋은 콘텐츠 구조다.

```
Generic Education
→ App personalization
```

웹 콘텐츠는 검색 유입과 신뢰를 만들고, 앱은 개인 데이터를 사용해 다음 단계로 간다.

## 9. 개인정보 구조에서 볼 점

공식 privacy policy는 다음을 수집한다고 밝힌다.
- 계정
- 아기 수면 데이터
- 기타 feeding/diaper/pumping 데이터
- 기기/사용 정보
- IP 기반 대략 위치

또한 AI assistant 개인화를 위해 아기 나이, 수면·수유·기저귀·체온, 이름 등 일부 데이터를 모델 기술 파트너에게 전송할 수 있다고 설명한다.

이 점은 AI 육아앱 설계에서 매우 중요하다.

AI 사용 시:
1. 어떤 데이터가 외부 모델로 가는가
2. 왜 필요한가
3. 저장/학습 여부
4. 최소화 가능한가

를 명확히 해야 한다.

## 10. 강점

- 하나의 고통점에 깊게 집중
- 수면 데이터를 행동/일정으로 변환
- 월령 기본값 + 개인 데이터라는 합리적 cold-start
- 전문 콘텐츠와 앱 기능이 연결
- 일상 기록보다 미래 계획을 전면화

## 11. 한계와 위험

### 예측이 부모 판단을 대체할 위험
아이의 졸림 신호가 앱보다 우선이어야 한다.

### 데이터 누락 민감성
로그를 빠뜨리면 모델이 잘못된 패턴을 학습할 수 있다.

### 특수상황
질병, 여행, 시간대 변경, 성장 급등기 등은 정상 패턴을 깨뜨린다.

### AI 개인정보
아기 건강·행동 데이터의 외부 모델 처리 범위를 특히 투명하게 보여야 한다.

## 12. 가져올 패턴

1. **Vertical Depth**
2. **Cold-start Default → Personalized Model**
3. **Future-facing Dashboard**
4. **Prediction Feedback**
5. **Preparation Reminder**
6. **Content → Personalized Tool Funnel**
7. **AI Data Transparency**

## 13. 근거

- https://napper.app/en/pricing/
- https://napper.app/privacy/
- https://napper.app/en/blog/baby-sleep/6-month-old-sleep-schedule-and-daily-routine/

## 결론

Napper에서 가장 배울 것은 "수면을 기록한다"가 아니라 **수면 데이터를 하루 계획 엔진으로 만드는 방식**이다.
