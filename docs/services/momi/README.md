# MOMI(모미) — 서비스 정본 분석

> 유형: AI 육아기록 / 임신·육아 / 가족앨범  
> 공개 제품코드: 확인 못함 [U]  
> 직접 검증: Google Play / App Store [A3]

## 1. 서비스 정의

MOMI는 **음성·자연어를 육아 이벤트로 구조화하고 사용자가 확인한 뒤 저장하게 하여, 손이 부족한 육아 상황의 입력 마찰을 줄이는 AI-first 기록 앱**이다.

## 2. 핵심 흐름

[A3]

```
"분유 120ml 먹었어"
→ Speech/Text
→ AI Parse
→ 구조화 후보
→ 사용자 확인
→ 저장
→ Timeline / Summary
```

## 3. 공개 코드/폴더 구조

공식 repository는 확인하지 못했다.

따라서 AI provider, backend stack, DB를 앱 설명만으로 단정하지 않는다.

## 4. 범위

임신기:
- 태동
- 혈당
- 혈압
- 수면 등

출산 후:
- 수유
- 수면
- 기저귀
- 체온
- 성장
- 예방접종/영양제 등

추가:
- AI 일기
- 가족앨범
- AI 대화
- AI Studio
- 월간 리포트

## 5. 가장 중요한 안전구조

**AI Parsed Candidate ≠ Saved Record**

사용자가 확인해야만 ground truth가 된다.

## 6. 가장 잘 푼 문제

- 아이를 안고 있을 때 손을 쓰기 어려움
- 여러 이벤트를 나중에 한 번에 기록
- 자연어 시간을 구조화
- 원문 기억과 AI 정리본을 함께 유지

## 7. 위험

- 시간/단위 parsing 오류
- 의료·약·체온 같은 고위험 필드
- AI 기능 과다로 핵심 기록 UX가 묻힘
- 아기 사진/건강데이터의 AI 처리범위

## 8. 참고할 패턴

- AI as Input Compiler
- Candidate → Confirm → Save
- Multi-event Parsing
- Original + AI-transformed
- Lifecycle Data Switching

## 9. 관련 문서

- [페이지·UI·UX](surface-map.md)
- [기술·AI·문제 해결](system-analysis.md)
- [직접 관찰](../../direct-inspection/apps/momi-store.md)
