# MOMI(모미) Deep Dive — 구조·기능·문제 해결 방식

> 조사 기준일: 2026-11-08  
> 공식 근거: Google Play / App Store 공식 등록정보

## 1. 서비스 한 문장

MOMI는 **음성·자연어를 육아 이벤트로 구조화해 기록 부담을 줄이고, 임신기 기록·육아 타임라인·AI 일기·가족앨범·성장리포트·AI 대화까지 결합한 AI-first 육아 기록 앱**이다.

## 2. 전체 구조

```
Pregnancy / Baby Profile
├─ Voice / Text Capture
│  ├─ Feeding
│  ├─ Sleep
│  ├─ Diaper
│  ├─ Pumping
│  ├─ Temperature
│  └─ Growth etc.
├─ Direct Button Logging
├─ Timeline / Category Views
├─ Growth Report
├─ AI Diary
│  ├─ raw note
│  └─ polished diary
├─ AI Prenatal Talk
├─ Family Album
├─ MOMI AI
│  └─ chat over records/questions
├─ AI Studio
├─ Vaccination guidance
└─ Wishlist / gifting
```

공식 설명상 임신 중에는 태동, 혈당, 혈압, 헤모글로빈, 수면 등을, 출산 후에는 수유·유축·수면·기저귀·목욕·체온·성장·영양제·예방접종 등을 다룬다.

## 3. 핵심 문제: 기록할 손이 없다

육아기록의 마찰은 "입력폼이 어렵다" 이전에 **손이 자유롭지 않다**는 점이다.

MOMI의 핵심 흐름:

```
"분유 120ml 먹었어"
↓
Speech-to-text
↓
Intent / Entity / Time parsing
↓
Structured record candidate
↓
사용자 확인
↓
Save
```

이 방식은 AI를 육아상담보다 먼저 **input compiler**로 사용하는 좋은 사례다.

## 4. AI 기록 구조에서 중요한 점

공식 설명은 AI가 정리한 내용을 **저장 전에 확인**하라고 명시한다.

이것은 매우 중요하다.

AI output과 authoritative user record를 분리한다.

```
AI Parsed Candidate ≠ Saved Ground Truth
```

저장 전 확인을 거쳐야:
- 잘못된 시간
- 단위 오류
- 이벤트 종류 오류
- 여러 이벤트 혼동

을 줄일 수 있다.

## 5. Multi-event Parsing

육아에서는 자연어 한 문장에 사건 여러 개가 들어간다.

> "7시에 분유 100 먹고 기저귀 갈았고 8시 반부터 잤어."

좋은 parser는:
```
Feeding Event
Diaper Event
Sleep Event
```
로 나눈다.

이 방식은 버튼형 기록보다 catch-up 입력에 특히 강하다.

## 6. 임신→육아 데이터 연속성

MOMI는 임신 단계부터 시작한다.

```
Pregnancy
├─ 태동
├─ 혈압
├─ 혈당
└─ 태담/일기

Birth

Baby Care
├─ Feeding
├─ Sleep
├─ Diaper
├─ Growth
└─ Vaccination
```

즉 같은 사용자 관계가 출산을 경계로 **데이터 타입만 전환**된다.

## 7. 일기에서 원본과 AI 수정본을 함께 보관

공식 설명에서 AI가 다듬은 일기와 원본을 함께 보관한다고 한다.

이것은 생성형 AI UX에서 매우 좋은 패턴이다.

```
Original Memory
+
AI-polished Version
```

AI가 사용자의 실제 기억을 덮어쓰지 않는다.

향후 육아 기록에서도:
- 원 음성 transcript
- AI 요약
- 구조화 데이터

를 분리할 가치가 있다.

## 8. 리포트 구조

앱은:
- 타임라인
- 카테고리별 화면
- 월간 성장 리포트

를 제공한다.

즉:
```
Raw Event → Timeline → Category Summary → Monthly Report
```
구조다.

2026년 업데이트에서 생후 개월 수에 맞춘 성장 리포트, 월간 원형 그래프 등이 추가된 점은 **age context를 리포트에 반영하는 방향**을 보여준다.

## 9. AI 기능 확장 전략

MOMI는 AI를 기록에만 쓰지 않는다.

- AI 일기
- AI 태담
- AI chat
- AI studio

까지 확장한다.

이 전략의 장점:
- AI 구독 가치를 여러 순간에 제공
- 임신/출산 전후로 AI 기능 유지

위험:
- 핵심인 기록 기능보다 엔터테인먼트 AI가 홈을 복잡하게 만들 수 있음
- 의료/건강 질문에서 AI 권한 범위를 강하게 제한해야 함

## 10. 가족앨범과 위시리스트

MOMI는 기록 앱에서:
- 사진/영상 가족앨범
- 가족 댓글/반응
- wishlist
- gift funding
- 감사카드

로 확장한다.

이것은 흥미로운 구조다.

```
Care Data
→ Family Relationship
→ Memory
→ Gift Coordination
```

하지만 건강정보와 가족용 앨범의 권한은 분리되어야 한다.

## 11. 수익모델

App Store 기준 AI Pro / AI Max 월간·연간 플랜이 존재한다.

즉 과금 핵심은:
- AI 기능
- 일부 미디어/원본 다운로드
- 플랜별 제공 범위

다.

Huckleberry와 달리 **prediction intelligence**보다 생성형 AI 경험이 중심이다.

## 12. 개인정보·안전

공식 앱 설명은:
- 건강정보와 AI 응답은 기록/참고용
- 의료 진단·치료 대체 아님
- AI 결과 저장 전 확인

을 명시한다.

좋은 방향이지만 실제로는 추가 확인이 필요하다.
- 음성 원본 보관기간
- AI provider 전달 데이터
- 아동 이미지 처리
- 가족앨범 접근권한
- 삭제/export

## 13. 강점

- 실제 육아 상황에 적합한 음성 입력
- AI 결과를 ground truth로 자동 확정하지 않음
- 임신→육아 continuity
- 원본과 AI 수정본 분리
- 기록·일기·사진을 한 앱에 연결

## 14. 구조적 위험

- AI 기능 과다로 핵심 루프 희석
- 고위험 수치 parsing 오류
- 건강 질문에 대한 AI 과신
- 미디어/건강 데이터의 권한 경계
- 작은 서비스의 장기 데이터 보존 신뢰 문제

## 15. 가져올 패턴

1. **AI as Input Compiler**
2. **Candidate → Confirm → Save**
3. **Multi-event Natural Language Parsing**
4. **Original + AI-transformed Version**
5. **Lifecycle Data Type Switching**
6. **Voice-first Quick Capture**
7. **AI Feature Hub는 핵심 기록과 분리**

## 16. 근거

- https://play.google.com/store/apps/details?id=com.pew_pew.momi
- https://apps.apple.com/kr/app/%EB%AA%A8%EB%AF%B8-momi-ai-%EC%9C%A1%EC%95%84%EA%B8%B0%EB%A1%9D/id6761996467

## 결론

MOMI는 국내 앱 중 **AI를 육아 기록의 입력 마찰 해소에 가장 직접적으로 적용한 사례**다.

가장 중요한 설계는 AI 자체가 아니라:

**말하기 → 구조화 후보 → 확인 → 신뢰 가능한 기록**

이라는 safety-aware input pipeline이다.
