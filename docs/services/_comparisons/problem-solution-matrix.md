# 복잡하게 얽힌 문제와 해결 방식 비교

## 1. 빠르게 기록해야 하지만 정확해야 한다

### 충돌
- 상세 필드가 많을수록 정확
- 입력이 길수록 누락 증가

### 사례
- BabyTime: event 먼저 생성
- MOMI: 음성 parse 후 확인
- Huckleberry: domain별 최소 필드

### 일반 해법
```
Minimal Capture
→ Optional Detail
→ Validation for High-risk Fields
```

---

## 2. 여러 양육자가 공유해야 하지만 개인정보도 지켜야 한다

### 사례
- BabyTime: child invite + role label
- Huckleberry: shared account
- FamilyAlbum: admin/member + item visibility

### 일반 해법
공동양육은 채팅이 아니라 **shared state + permission** 문제다.

```
Baby Workspace
+
Role
+
Data Scope
+
Audit
```

---

## 3. 기록이 많아질수록 오히려 읽기 어려워진다

### 사례
- BabyTime: Timeline / Interval / Stats 분리
- Huckleberry: current state + reports
- FamilyAlbum: archive / memories 분리

### 일반 해법
데이터를 삭제하기보다 **projection을 분리**한다.

---

## 4. 월령에 따라 필요한 기능이 바뀐다

### 사례
- 베이비빌리: global stage router
- Solid Starts: age-specific food view
- Pathways: age path
- 아이사랑: stable taxonomy + age content

### 일반 해법
```
Age/Stage
→ Module Priority
```

고정 홈에 기능을 계속 추가하지 않는다.

---

## 5. 발달을 알려주고 싶지만 부모를 불안하게 만들면 안 된다

### 사례
- Pathways: observable behavior + progress
- Kinedu: skill trajectory + next activity
- CDC: monitoring ≠ screening

### 일반 해법
- rank 금지
- 관찰 가능한 행동
- emerging state
- 다음 활동
- concern escalation

---

## 6. 개인화는 하고 싶지만 데이터가 처음엔 없다

### 사례
- Napper: age baseline → personalized sleep
- Pathways: age-based → progress-based activity
- Solid Starts: stage guidance → history-based meal plan

### 일반 해법
```
Cold Start Default
→ Observe User
→ Personalized Model
```

---

## 7. AI는 편하지만 틀릴 수 있다

### 사례
- MOMI: confirm before save
- Huckleberry: AI as logging surface

### 일반 해법
AI를 authority가 아니라 **adapter**로 둔다.

---

## 8. 건강정보는 유용해야 하지만 앱이 진단하면 위험하다

### 사례
- CDC: doctor handoff
- NHIS: screening/referral
- KDCA: exception → clinician
- Solid Starts: allergen expert guidance

### 일반 해법
```
Explain
→ Observe
→ Record
→ Official Source
→ Professional
```

---

## 9. 공식 일정은 최신이어야 한다

### 사례
KDCA는 실제 사업기간·대상·최종검토일이 갱신된다.

### 일반 해법
하드코딩이 아니라:

```
Versioned Definition
+
Effective Date
+
Source
```

---

## 10. 사진과 기록이 쌓여도 부모가 다시 보지 않는다

### 사례
FamilyAlbum:
`archive → automatic recap`

### 일반 해법
추가 입력 없이 **자동 보상**을 만든다.

---

## 11. 기능이 너무 많으면 super-app이 복잡해진다

### 사례
- 베이비빌리
- 마미톡
- MOMI

### 일반 해법
기능을 홈에 모두 배치하지 않는다.

```
Current Context
→ Top 3 Actions
→ Secondary Modules
```

---

# 최종 설계 질문

어떤 기능을 추가하기 전에 다음을 묻는다.

1. 부모의 어떤 반복 질문을 없애는가?
2. 입력은 몇 초 걸리는가?
3. 원자료인가, 파생값인가?
4. 다른 양육자가 알아야 하는가?
5. 월령이 지나면 사라져야 하는가?
6. 알림이 정말 필요한가?
7. 공식/의료 시스템으로 넘겨야 하는 지점은 어디인가?
8. AI 없이도 ground truth는 유지되는가?
9. export/delete가 가능한가?
10. 홈에 반드시 보여야 하는가?
