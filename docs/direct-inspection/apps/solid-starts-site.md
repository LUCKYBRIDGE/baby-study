# Solid Starts — 공식 사이트 직접 관찰

> 관찰일: 2026-11-08  
> 근거: Solid Starts 공식 앱/제품 페이지  
> 레벨: A1

## 1. 실제 월령 단계가 제품 IA에 들어가 있음

공식 페이지에서 다음 단계가 제품 레벨로 직접 드러납니다.

- 0–4 months
- 5–6 months
- 7–9 months
- 10–12 months
- 12+ months

즉 월령은 단순 글 태그가 아니라 **음식 제공방법과 기능 우선순위를 바꾸는 전역 context**입니다.

## 2. 음식 DB가 핵심 진입점

공식 제품은 500개 이상의 음식에 대해:
- 월령별 제공 형태
- 사진/영상
- 손과 비교한 크기
- 영양 정보
- 안전 정보
- 알레르기 관련 정보

를 제공합니다.

일반적인 기사형 구조가 아니라:

```
Food Object
→ Age-specific View
→ Serve
→ Log
```

구조입니다.

## 3. 정보와 기록이 같은 객체에 연결됨

음식을 본 뒤 개인 기록으로 이어집니다.

- 먹어봄
- 좋아함/싫어함
- 반응
- 첫 노출 이력

이 방식은 매우 중요합니다.

```
Global Food Knowledge
+
Baby-specific Food History
```

를 같은 food ID를 중심으로 결합할 수 있습니다.

## 4. 알레르기 기능

공식 페이지에서는 주요 알레르겐에 대해:
- 단계별 도입 가이드
- 제공량
- 반응이 어떻게 보일 수 있는지
- 성공 후 지속 노출

같은 정보를 제공합니다.

제품적으로는 알레르기 기능을 일반 recipe 기능과 동일 수준으로 취급하면 안 됩니다.

필요한 기록:
```
Food
Time
Serving form
Amount
Observed reaction
Reaction onset
Medical care
```

고위험 정보이므로 앱이 진단 대신 **관찰 기록 + 전문가/공식 안내** 역할을 해야 합니다.

## 5. First 100 Foods

공식 제품은 "첫 100가지 음식" 경로를 개인화합니다.

단순 checklist가 아니라 이미 먹어본 음식을 바탕으로 다음 계획을 제안합니다.

```
Tried foods
+
Age
+
Plan
→ Next foods / meal plan
```

이것은 database가 recommendation engine으로 확장된 사례입니다.

## 6. Meal Plan

개인화 meal plan은:
- 이미 노출된 음식
- 현재 단계
- 레시피

를 연결합니다.

즉 서비스 가치가:

```
검색
→ 정보
→ 기록
→ 개인화 계획
```

순으로 상승합니다.

## 7. 시각적 instruction의 중요성

이유식은 텍스트 설명보다:
- 실제 크기
- 모양
- 질감
- 잡는 방식

이 중요합니다.

Solid Starts는 이를 사진/영상 중심으로 풀어냅니다.

육아 앱 전체에서도 다음은 visual-first가 적합합니다.
- 음식 크기
- 발달 동작
- 안전 자세
- 수면환경
- 놀이 자세

## 8. 유료 구조

공식 페이지에서 2026-11-08 기준:
- 월간 플랜
- 연간 플랜
- 무료 체험

이 확인됩니다.

과금 가치는 단순 음식 검색보다:
- 개인화 meal plan
- 전문가 라이브러리
- 지속적인 계획

쪽에 배치됩니다.

가격은 변경될 수 있으므로 repository에는 절대값보다 **과금 경계**를 중심으로 기록합니다.

## 9. 구조적 위험

- "100 foods"가 성취 경쟁처럼 느껴질 수 있음
- 알레르기 안전정보가 과도하게 유료화되어서는 안 됨
- 국가별 권고 차이
- 부모가 앱 계획을 아이 반응보다 우선할 위험

## 10. 핵심 시사점

Solid Starts는 다음 구조를 참고할 가치가 큽니다.

```
Object-centered search
→ Age-specific instruction
→ Personal history
→ Next-action plan
```

이는 음식뿐 아니라:
- 예방접종
- 발달 기술
- 약
- 건강 증상

같은 다른 육아 도메인에도 응용 가능합니다.

## 11. 참고

- https://solidstarts.com/app/
