# Craft Anything 기반 직접 분석 방법

> 기준 저장소: https://github.com/storytold/craft-anything  
> 확인일: 2026-11-08

## 1. 실제 Craft Anything 저장소에서 확인한 핵심

Craft Anything의 공식 README는 분석·재구현 워크플로를 다음 네 단계로 설명한다.

```
Study
→ Build
→ Check
→ Ready
```

이 중 `baby-study`에서 사용하는 것은 주로 **Study + Check의 사고방식**이다.

Craft Anything은 직접 다음을 강조한다.

- 원본을 실제로 관찰
- 화면 너비별 페이지
- 코드/파일/실행방식 확인
- 모든 답에 근거를 남김
- "추측이 아닌 검증"
- Clean room과 Deep 모드를 구분
- 결과에 confidence, coverage, limitations를 포함

또 `AGENTS.md`에는 다음 원칙이 명시되어 있다.

> Evidence is the result.

즉 분석 결과보다 **무엇을 근거로 그렇게 판단했는가**가 핵심이다.

## 2. baby-study에서 적용하는 방식

우리는 각 육아 서비스를 다음 세 층으로 분리한다.

### A. Observed
실제 공식 사이트/FAQ/앱스토어에서 직접 확인한 것.

예:
- 실제 메뉴명
- 탭 구조
- 입력 순서
- 가격
- 권한 설명
- 공식 데이터 정책

### B. Code-observed
공개 저장소 코드에서 확인한 것.

예:
- 디렉터리 구조
- API client
- 데이터 type
- event schema
- test
- realtime listener

### C. Inferred
A/B를 바탕으로 한 제품적 해석.

예:
- 왜 root에 last-state를 두었는지
- 어떤 사용자 문제를 줄이려 한 것인지
- 우리 시스템에 어떻게 적용할 수 있는지

문서에서는 세 층을 혼동하지 않는다.

---

# 3. 사이트 분석 절차

각 사이트마다 최소 다음 페이지를 실제로 확인한다.

## 3.1 Entry
- 홈페이지
- hero
- 주요 CTA
- 상단/하단 navigation

## 3.2 Core product
- 기능 소개
- 실제 웹 도구
- tracker
- assessment
- search/database

## 3.3 Monetization
- pricing
- free trial
- paid feature boundary

## 3.4 Trust
- science
- experts
- source
- medical disclaimer

## 3.5 Support
- FAQ
- help center
- error/edge-case 설명

## 3.6 Privacy
- 어떤 아기 데이터를 수집하는지
- AI provider 전달 여부
- retention
- deletion/export
- family sharing

그 후 아래 구조로 정리한다.

```
Navigation
→ User Flow
→ Data Input
→ Derived Output
→ Repeat Loop
→ Permission
→ Safety
→ Monetization
```

---

# 4. 저장소 분석 절차

공개 repository를 발견하면 이름만 보고 공식이라고 간주하지 않는다.

## 공식 여부
1. 회사/기관 GitHub 조직인가?
2. 공식 사이트가 repository로 연결되는가?
3. README에 공식 제품과의 관계가 명시되는가?
4. 실제 배포 앱과 연결되는가?

확인되지 않으면 **비공식 저장소**로 표시한다.

## 코드에서 보는 순서

```
README
→ tree
→ package/build config
→ core models
→ API/data access
→ tests
→ migration/changelog
→ integrations
```

특히 README보다 다음을 더 중요하게 본다.

- type/schema
- test fixtures
- actual write/read code
- migration
- changelog

왜냐하면 기능 소개보다 실제 데이터 제약을 더 정확하게 보여주기 때문이다.

---

# 5. Evidence Card

향후 각 핵심 발견은 다음 형식으로 남긴다.

```
Finding:
Source:
Evidence type: A1 / A2 / A3 / B1 / B2
Observed:
Inference:
Confidence:
Limitations:
```

근거 레벨:
- A1 공식 제품사이트
- A2 공식 도움말/FAQ/정책
- A3 공식 앱스토어
- B1 공식 공개 소스코드
- B2 비공식 공개 구현
- C 제품적 추론

---

# 6. 직접 설치가 필요한 영역

웹으로 확인할 수 없는 것:
- 네이티브 onboarding animation
- 실제 tab transition
- haptic
- keyboard behavior
- offline
- push notification permission
- native widget
- lock-screen live activity
- exact tap count
- loading/error state

이런 항목은 **미확인으로 표시**하고 추측하지 않는다.

---

# 7. 분석의 목표

목표는 특정 앱의 디자인을 복제하는 것이 아니다.

```
관찰 가능한 구조
→ 일반화 가능한 원리
→ 독자적인 육아 시스템 설계
```

로 변환하는 것이다.

특히 다음 질문에 답할 수 있어야 한다.

- 어떤 데이터가 ground truth인가?
- 어떤 값이 파생값인가?
- 사용자에게 왜 이 화면이 필요한가?
- 어떤 데이터가 다음 행동으로 연결되는가?
- 어느 순간 의료진/공식 시스템으로 넘겨야 하는가?
- 아이가 성장하면 이 기능은 사라지는가, 변하는가?
