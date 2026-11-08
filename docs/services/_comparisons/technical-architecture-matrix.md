# 기술·데이터 아키텍처 비교

> 내부 기술스택이 공개되지 않은 서비스는 framework 이름을 추정하지 않고 **제품적으로 확인 가능한 데이터 구조**만 비교한다.

## 1. 아키텍처 유형

| 유형 | 서비스 | 핵심 구조 |
|---|---|---|
| Event Store | BabyTime | 사건 → 타임라인/통계 |
| Event + Projection | Huckleberry | history + current/last state |
| Predictive Model | Napper/Huckleberry | event → prediction |
| AI Capture Adapter | MOMI | natural language → candidate event |
| Skill Graph | Kinedu | observation → skill state |
| Knowledge Graph | Pathways | milestone ↔ activity ↔ resource |
| Object DB | Solid Starts | food definition + personal exposure |
| Workspace/Permission | FamilyAlbum | album + members + visibility |
| Lifecycle Orchestrator | 베이비빌리/마미톡 | stage → module priority |
| Versioned Rule System | KDCA | official schedule + eligibility |
| Clinical Workflow | NHIS/CDC | observation/screening → handoff |

## 2. Ground Truth

### Event Ground Truth
- 수유
- 수면
- 배변
- 체온
- 약 실제 복용
- 성장 측정

### Definition Ground Truth
- 공식 예방접종 기준
- milestone definition
- food guidance
- 검진 차수

### Derived
- 평균
- 총량
- interval
- progress
- prediction
- recommendation
- AI summary

Derived 값을 Raw처럼 저장하면 수정/재계산이 어려워진다.

## 3. 가장 좋은 공개 코드 사례 — Huckleberry ecosystem

비공식 공개 구현에서 관찰:

```
users/{uid}
childs/{child}

sleep/{child}
feed/{child}
diaper/{child}
health/{child}
pump/{child}
activities/{child}
```

반복 패턴:

```
domain root
├─ current timer
├─ prefs.last*
└─ history
```

이 구조는 홈 성능과 실시간 동기화에 적합하다.

## 4. 권한 모델

| 서비스 | 모델 |
|---|---|
| Huckleberry | shared account / multi-device |
| BabyTime | child-centered caregiver invite |
| FamilyAlbum | workspace + admin/member permission |
| 공공 시스템 | 법정대리인/인증 기반 |

권장:

```
Baby Workspace
├─ Owner/Parent
├─ Caregiver
├─ Family Viewer
└─ Clinical Share
```

데이터 종류별 permission이 추가되어야 한다.

## 5. Catalog + Personal History

반복되는 좋은 구조:

### Solid Starts
`Food Definition + Exposure History`

### KDCA
`Schedule Definition + Vaccination Record`

### Pathways
`Milestone Definition + Observation`

### Medication
`Medicine Definition + Administration Record`

즉 **Definition과 Child-specific Event를 분리**하는 것이 핵심이다.

## 6. Prediction 구조

```
Observed History
→ Feature/Pattern
→ Prediction
→ User Action
→ Actual Event
→ Feedback
```

Prediction은 ground truth가 아니다.

## 7. AI 구조

권장:

```
Input
→ Transcript
→ ParsedCandidate
→ Validation
→ User Confirmation
→ Ground-truth Event
```

AI가 DB write를 바로 확정하지 않는다.

## 8. Official Data 구조

공공 건강정보:

```
Authority
Version
Effective Period
Reviewed At
Definition
```

을 갖는 versioned source로 관리한다.

## 9. Derived Artifact

FamilyAlbum의 자동영상, MOMI의 AI 일기처럼:

```
Source
→ Derived Artifact
```

가 존재한다.

필요:
- lineage
- permission inheritance
- delete propagation
- regeneration

## 10. 권장 reference architecture

```
Identity / Baby Workspace
        ↓
Ground-truth Event Store
        ↓
Current-state Projection
        ↓
Domain Services
        ↓
Pattern / Prediction / Recommendation
        ↓
Age-adaptive Experience Layer

Official Source Layer
        ↕
Health / Schedule / Clinical Handoff

Media Store
        ↓
Memory / Derived Artifacts
```
