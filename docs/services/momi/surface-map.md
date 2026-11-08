# MOMI — 페이지·UI·UX·버튼 지도

## 1. 핵심 Home UX

공식 스토어 설명에서 두 가지 입력방식이 동시에 강조된다.

### Voice
`말하기 → AI 분석 → 확인`

### Direct Button
`기록 버튼 → 구조화 입력`

AI가 실패하거나 말하기 곤란한 상황을 버튼이 보완하는 **hybrid input**이다.

## 2. Voice Capture

좋은 화면 구조:

```
[마이크]
↓
transcript
↓
AI가 찾은 이벤트 카드들
├─ 분유 120ml
├─ 19:00
└─ ...
↓
[수정] [저장]
```

핵심 버튼은 "AI에게 물어보기"가 아니라 **확인/수정/저장**이다.

## 3. Multi-event 입력

예:
> 7시에 분유 먹이고 기저귀 갈고 8시 반부터 잤어.

UI는 한 문장을 세 개 카드로 분리해야 한다.

```
Feed card
Diaper card
Sleep card
```

각 카드별로 수정/제외가 가능해야 안전하다.

## 4. 빠른 기록

직접버튼 입력은 AI 의존성을 낮춘다.

필요한 상황:
- 야간
- 주변이 시끄러움
- 정확한 약/체온
- privacy가 필요한 장소

## 5. Timeline / Summary

공식 설명에서:
- 마지막 수유
- 오늘 수면
- 성장 리포트

같은 요약가치가 강조된다.

즉 기록 후 즉시 "현재 상태"를 보여준다.

## 6. AI Diary

원문과 AI 정리본을 함께 보관하는 점이 좋다.

버튼:
- 원문 보기
- AI 버전 보기
- 편집
- 보관

처럼 source와 transformation을 구분하는 것이 적합하다.

## 7. 가족앨범

건강/생활 기록과 media sharing이 같은 앱에 있지만 UI 권한은 분리하는 편이 좋다.

## 8. AI Chat

AI 질문 화면은 기록 조회형 질문과 의료상담형 질문을 구분해야 한다.

- "마지막 수유 언제?" → 기록 기반
- "이 열은 위험해?" → 고위험, 공식/의료 안내 우선

## 9. 미확인

- 음성 partial parse 실패 UI
- 위험 필드 confirmation 강도
- caregiver role
- offline voice queue
- AI source citation
