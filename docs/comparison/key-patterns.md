# 육아 서비스에서 반복적으로 발견되는 핵심 설계 패턴

# 1. One-tap Event Logging

대표: BabyTime

아기를 안고 있는 상황을 기본으로 본다.

```
탭 → 저장
```

상세정보는 나중에 선택적으로 추가한다.

---

# 2. Last Event First

통계보다 먼저:

- 마지막 수유
- 현재 수면
- 마지막 기저귀
- 마지막 약

을 보여준다.

부모가 가장 자주 묻는 것은 평균보다 **'마지막이 언제였지?'**다.

---

# 3. Caregiver Handoff

대표: BabyTime, Huckleberry

다른 양육자가 앱을 열었을 때 10초 안에 현재 상황을 이해하게 한다.

---

# 4. Age-Adaptive Home

대표: 베이비빌리, 마미톡, 아이사랑

```
출생 2주
→ 수유/수면 중심

6개월
→ 이유식/발달 중심

18개월
→ 언어/놀이/생활습관 중심
```

메뉴를 계속 추가하는 대신 **우선순위를 교체**한다.

---

# 5. Data → Prediction

대표: Huckleberry, Napper

```
실제 기록
→ 패턴
→ 다음 시점 예상
```

예측은 실제값과 명확히 구분한다.

---

# 6. Data → Action

대표: Kinedu

```
발달 관찰
→ 오늘 해볼 활동
```

리포트를 읽는 것보다 다음 행동이 중요하다.

---

# 7. Search → Action

대표: Solid Starts

```
사과 검색
→ 8개월 제공방법
→ 사진 확인
→ 오늘 먹임
→ 내 기록
```

검색결과를 정보에서 끝내지 않는다.

---

# 8. Evidence-linked Advice

대표: CDC, 공공 보건서비스

건강/발달 정보는:
- 출처
- 검토/업데이트일
- 적용 범위
- 한계

를 함께 보여준다.

---

# 9. Monitoring ≠ Screening ≠ Diagnosis

발달/건강 제품의 핵심 안전원칙.

```
일상 관찰
≠
표준화 선별검사
≠
의료진 진단
```

UI와 문구에서 세 단계를 섞지 않는다.

---

# 10. Clinical Handoff

대표: CDC, NHIS 관점

앱에서 기록만 하지 말고 병원 가기 전에:

```
최근 생활
+
성장
+
증상
+
부모 질문
```

을 한 장으로 만든다.

---

# 11. Planned ≠ Done

예방접종과 약에서 특히 중요하다.

- 알림 발생
- 예정
- 실제 완료

를 별개 상태로 저장한다.

---

# 12. Automatic Memory Reward

대표: FamilyAlbum

```
평소 사진 업로드
→ 몇 달 뒤 자동 성장영상
```

추가 입력 없이 큰 보상을 주는 구조.

---

# 13. Age-relative Time

육아에서는:
```
2027년 4월
```
보다
```
생후 4개월
```
이 더 중요한 경우가 많다.

둘 다 저장하되 UI에서 아기 나이를 적극 활용한다.

---

# 14. Progressive Detail

대표: 좋은 tracking UX 전반

```
[대변]
```
을 누르면 기본 기록 완료.

필요한 경우만:
- 색
- 양
- 상태
- 메모

를 펼친다.

---

# 15. AI First as Friction Reducer

대표: Huckleberry의 AI logging 방향

육아 AI의 첫 역할은 '의사처럼 답하기'보다:

> "분유 120 먹고 방금 잠들었어"

를 안전하게 구조화하는 것이다.

```
자연어/음성
→ 구조화 후보
→ 사용자 확인
→ 저장
```

이 구조가 위험은 낮고 사용가치는 높다.

---

# 16. Cohort Context

대표: 베이비빌리

같은 월령 부모의 질문은 맥락이 잘 맞는다.

커뮤니티뿐 아니라:
- FAQ
- 인기 질문
- 상품
- 활동

에도 cohort를 적용할 수 있다.

---

# 17. Domain Verticalization

대표: Napper, Solid Starts

'육아 전체'를 해결하지 않아도 하나의 고통이 충분히 크면 강력한 전문 앱이 된다.

- 잠
- 이유식
- 발달
- 사진

---

# 18. Official Source as Backend, not Copy

예방접종·검진처럼 변경될 수 있는 국가 기준은 앱에 복사해 방치하지 않는다.

```
공식 기준
→ 최신화
→ 사용자에게 필요한 부분만 표현
→ 원문 링크
```

---

# 우선순위

향후 하나의 육아 앱을 만든다고 가정하면 먼저 구현할 패턴:

## P0
1. Baby profile + age context
2. One-tap logging
3. Last event first
4. Caregiver sync
5. Planned vs Done
6. Official schedule links

## P1
7. Timeline + weekly patterns
8. Age-adaptive home
9. Doctor-ready summary
10. Growth/checkup/vaccine module

## P2
11. Sleep prediction
12. Development activity recommendation
13. Food database + exposure
14. Automatic memory recap

## P3
15. AI voice/text logging
16. Community
17. Commerce

AI·커뮤니티·커머스보다 **기록 신뢰성과 공동양육**이 먼저다.
