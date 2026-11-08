# Solid Starts — 페이지·UI·UX·버튼 지도

## 1. 제품 진입점

공식 app page에서 주요 action은:
- stage 선택
- food search
- allergen guidance
- meal plan
- food log

으로 이어진다.

## 2. Stage selector

[A1]

```
[0–4] [5–6] [7–9] [10–12] [12+]
```

stage가 바뀌면 동일 음식도 제공형태가 달라진다.

즉 age는 단순 filter가 아니라 **object rendering context**다.

## 3. Food Search

핵심 검색 UX:
- 음식명 검색
- 음식 카드
- 상세 진입

부모는 긴 article navigation을 거치지 않고 손에 든 음식 이름으로 바로 들어간다.

## 4. Food Detail

필요 UI:
- 음식명
- 월령별 serving
- 손과 크기 비교
- 사진
- 영상
- nutrition
- choking/safety
- allergen
- log action

"읽기"와 "먹이고 기록하기"가 같은 페이지 안에서 연결된다.

## 5. Food Log

공식 제품 설명에서:
- tried
- favorite
- reaction

등 개인 history를 남길 수 있다.

즉 object detail에서 바로 personal state가 보이는 것이 적합하다.

## 6. Allergen Flow

좋은 UX는:
```
Allergen
→ step
→ serving amount
→ reaction signs
→ actual exposure record
→ repeat guidance
```

로 이어져야 한다.

고위험이므로 단순 체크 애니메이션보다 경고/의료 연결이 중요하다.

## 7. First 100 Foods

진행률을 제공하더라도 "100개 달성" 경쟁으로 보이지 않도록:
- 다양성
- 다음 추천
- 이미 먹은 음식

중심이 더 적합하다.

## 8. Meal Plan

Food database의 검색모드에서 **시스템 추천모드**로 전환하는 화면이다.

```
History
+
Age
→ planned meals
```

## 9. Visual-first UX

다음 정보는 텍스트보다 이미지가 우선이다.
- 크기
- 모양
- 잡는 방식
- 제공 형태

Solid Starts의 강한 UX 포인트다.

## 10. 미확인

- 네이티브 exact navigation
- reaction emergency UX
- offline food DB
- caregiver sync
- 한국 로컬라이제이션 방식
