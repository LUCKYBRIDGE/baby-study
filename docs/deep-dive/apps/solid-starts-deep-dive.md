# Solid Starts Deep Dive — 구조·기능·문제 해결 방식

> 조사 기준일: 2026-11-08  
> 공식 근거: Solid Starts 공식 앱 소개

## 1. 서비스 한 문장

Solid Starts는 **음식이라는 객체를 중심으로 '어떻게 제공할지'에 대한 전문가 지식, 연령별 사진·영상, 알레르기 안내, 개인 섭취 기록, 식단 계획을 연결하는 이유식 전문 지식-행동 플랫폼**이다.

## 2. 핵심 문제 정의

부모의 실제 질문:
> "7개월 아기에게 망고를 어떻게 줘야 하지?"

이 질문은 긴 교육과정을 원하지 않는다.

필요한 것은:
```
음식 검색
→ 지금 월령에 맞는 형태
→ 사진/영상
→ 안전/알레르기 정보
→ 실제 제공
→ 먹인 기록
```

Solid Starts는 **검색 의도와 행동 사이 거리를 짧게** 만든다.

## 3. 전체 구조

```
Baby Age/Profile
├─ First Foods Database (500+)
│  ├─ Food Detail
│  ├─ How to Serve by Age
│  ├─ Photo/Video
│  ├─ Nutrition
│  ├─ Safety
│  └─ Allergen Information
├─ Food Log
│  ├─ Tried
│  ├─ Favorite
│  └─ Reaction
├─ Allergen Plan
├─ First 100 Foods
├─ Personalized Meal Plan
├─ Recipes (300+)
└─ Expert Library
```

## 4. Object-centered Information Architecture

일반 육아정보:
```
이유식 시작하기
├─ 초기 이유식
├─ 중기 이유식
└─ 후기 이유식
```

Solid Starts:
```
Mango
Egg
Peanut
Apple
...
```

즉 사용자가 실제로 손에 든 **음식 객체**가 진입점이다.

이 구조는 부모의 상황적 검색과 잘 맞는다.

## 5. 콘텐츠→행동 연결

Food detail은 읽고 끝나지 않는다.

```
General Food Knowledge
↓
Age-specific Serving
↓
Parent Serves Food
↓
Personal Food Log
```

일반 정보와 개인 기록이 같은 객체 ID를 공유하는 모델로 해석할 수 있다.

예:
```
Food: Egg
├─ Expert Content
└─ Baby Exposure History
   ├─ 1st exposure
   ├─ 2nd exposure
   └─ reaction
```

이 구조는 매우 강력하다.

## 6. 시각적 지시의 역할

먹이는 크기·형태는 텍스트보다 사진이 훨씬 빠르다.

Solid Starts는 연령별 제공형태를 시각적으로 보여주는 것을 핵심 가치로 둔다.

육아앱에서 **텍스트보다 이미지가 판단속도를 높이는 영역**을 구분해야 한다.

- 음식 크기
- 발달 행동
- 안전 환경
- 자세

등이 대표적이다.

## 7. First 100 Foods

개인화된 첫 100가지 음식 계획은 단순 콘텐츠가 아니라 **progress system**이다.

```
Not tried
→ Planned
→ Tried
→ Repeated
```

장점:
- 다음 음식 선택 부담 감소
- 다양성 증가
- 진행상황 가시화

위험:
- 100개 달성이 목적화될 수 있음
- 개인 의료상황보다 앱 진도를 우선할 위험

따라서 "목표"보다 "다양성을 돕는 가이드"로 표현하는 것이 적절하다.

## 8. 알레르기 기능

공식 소개는 주요 알레르겐에 대해:
- 단계별 계획
- 제공량
- 반응 모습
- 성공 후 지속 노출

등을 제공한다고 설명한다.

이 영역은 고위험이다.

따라서 데이터 구조도 일반 음식기록보다 정밀해야 한다.

```
Exposure
├─ Food
├─ Time
├─ Preparation
├─ Amount
└─ Reaction
   ├─ Symptom
   ├─ Onset
   └─ Medical care
```

제품은 진단보다 **정확한 기록 + 공식/전문가 안내 + 필요 시 진료 연결**에 집중해야 한다.

## 9. Personalized Meal Plan

음식 DB가 "무엇인지"를 설명한다면 meal plan은 "다음에 무엇을 할지"를 결정한다.

```
Baby Age
+
Foods Already Tried
+
Plan Goal
→ Next Meal Suggestions
```

즉 Solid Starts도 결국 **Data → Next Action** 구조를 갖는다.

## 10. 전문가 시스템

공식 페이지는 소아과, 알레르기, feeding therapy, 작업치료, 수유, 영양 전문가가 자료를 만든다고 설명한다.

이 구조의 핵심은 "전문가가 있다"가 아니라:
- 모든 정보가 전문가 검토 체계에 들어감
- 오픈 인터넷 대신 curated library
- 콘텐츠가 월령에 맞게 개인화

된다는 점이다.

## 11. 강점

- 부모의 순간적 질문과 정확히 맞는 검색 구조
- 객체 중심 데이터 모델
- 이미지/영상으로 판단시간 단축
- 일반 정보→개인 기록 연결
- 전문성이 제품 IA에 녹아 있음
- meal plan으로 다음 행동까지 연결

## 12. 구조적 위험

- 의료·알레르기 정보의 지역별 권고 차이
- 안전정보가 구독벽에 가려질 위험
- food count 게임화
- 일반 사용자에게 세부정보가 과다할 수 있음

## 13. 가져올 패턴

1. **Object-centered Search**
2. **Age-specific Object View**
3. **Visual Instruction**
4. **Knowledge ↔ Personal History**
5. **Progressive Exposure Log**
6. **Curated Expert Library**
7. **Database → Next-action Plan**

## 14. 근거

- https://solidstarts.com/app/

## 결론

Solid Starts의 가장 큰 교훈은 **일반 정보와 개인 행동 기록을 같은 '음식 객체' 중심으로 결합한 것**이다.
