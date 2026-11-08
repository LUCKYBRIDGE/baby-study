# Napper — 공식 사이트·가격·개인정보정책 직접 관찰

> 관찰일: 2026-11-08  
> 근거: 공식 Home / Pricing / Privacy  
> 레벨: A1/A2

## 1. 실제 웹 IA

공식 상단 내비게이션:

```
Home
App Features & Pricing
Our story
Blog
Gift
Support
Download app
```

즉 웹은 앱 자체보다:
- 기능/가격
- 수면 콘텐츠
- 신뢰
- acquisition

에 최적화되어 있다.

## 2. Hero에서 실제로 약속하는 것

첫 메시지는 "sleep logging"이 아니라 **Make bedtime easier**다.

그리고 바로:
- personalized sleep plans
- soothing sounds
- 오늘 밤 적용 가능한 tips

를 묶는다.

즉 제품 정체성은 tracker가 아니라 **sleep decision assistant**에 가깝다.

## 3. 실제 기능 표현

공식 가격 페이지에서 무료/Unlimited 비교로 확인되는 핵심 기능:

- Daily sleep tracking
- Sleep schedule based on age
- Personalized sleep analysis
- Educational sleep courses
- Custom baby sleep sounds
- Trends and statistics
- Track everything

이 구조에서 중요한 점:

```
Free
= 기록 + 기본 월령 schedule

Unlimited
= 개인화 분석 + 교육 + 확장 tracking
```

따라서 cold-start 시에는 age-based schedule을 제공하고, 기록이 쌓이면 personalized layer를 얹는 구조로 해석할 수 있다.

## 4. 실제 사용자 가치가 future-facing

공식 홈페이지 후기와 제품 설명에서 반복적으로 등장하는 가치:
- 다음 nap/bedtime을 알 수 있음
- wake window를 확인
- 미리 준비
- 하루 일정을 수면에 맞춰 조직

즉 dashboard의 중심은 과거 집계보다:

```
What happened?
→ What happens next?
```

이다.

## 5. 공유 구조

공식 홈페이지 사용자 후기에는 profile을 다른 부모/양육자와 공유해 함께 기록한다는 사용 사례가 직접 노출된다.

다만 공식 help 문서 수준에서 role/permission 구조까지는 이번 조사에서 확인하지 못했다.

따라서:
- caregiver collaboration 존재 가능성: 높음
- 상세 permission model: 미확인

으로 둔다.

## 6. 개인정보정책에서 실제 확인된 수집항목

2026-04-21 업데이트 정책에서:

### Account
- 이메일
- 사용자명
- 비밀번호

### Baby data
- sleep duration
- wake time
- nap
- breastfeeding
- diaper
- pumping 등

### Device/usage
- 기기
- OS
- 앱 사용정보
- IP 기반 대략적 위치

를 수집한다고 명시한다.

## 7. AI assistant 데이터

정책상 AI personalized insight를 위해 일부 데이터를 사용한다.

명시된 예:
- 아기 나이
- sleep
- feeding
- diaper
- temperature
- 아기/부모의 first name

또 underlying language-model technology를 제공하는 기술 파트너 예시로 **OpenAI 또는 Anthropic**을 명시한다.

이건 매우 중요한 직접 근거다.

육아 AI에서 사용자에게 최소 다음을 보여줄 필요가 있다.

```
AI에 전달되는 데이터
AI에 전달되지 않는 데이터
목적
보관
삭제
```

## 8. AI에서 얻는 설계 교훈

Napper는 AI 자체보다 **민감데이터 governance** 분석에 좋은 사례다.

좋은 점:
- AI로 쓰이는 데이터 범위를 policy에 설명
- 제3자 기술 제공자 가능성을 공개
- portability/erasure 권리 설명

추가 검증 필요:
- 앱 화면에서 실제 AI consent를 얼마나 잘 안내하는지
- AI 기능 opt-out
- provider별 retention

## 9. 데이터 portability

정책에서 사용자는:
- access
- rectification
- erasure
- restriction
- portability
- objection

권리를 요청할 수 있다고 설명한다.

육아 기록처럼 수년 쌓이는 데이터에서 **machine-readable portability**는 중요한 제품 요구사항이다.

## 10. 직접 관찰 결론

Napper의 실제 제품 구조는:

```
Age baseline
+
Daily sleep events
→ Personalized model
→ Next nap/bedtime
→ Preparation
→ Actual event
→ Recalculate
```

이다.

그리고 Privacy 관점에서는 **AI assistant가 아기 일상 데이터를 외부 언어모델 기술 파트너와 처리할 수 있다는 점**이 육아 AI 설계 시 반드시 참고해야 할 사례다.

## 11. 직접 확인한 페이지

- https://napper.app/en/
- https://napper.app/en/pricing/
- https://napper.app/privacy/
