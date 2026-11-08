# Huckleberry — 서비스 정본 분석

> 유형: 육아 기록 / 수면 예측 / AI 입력 / 분석  
> 공식 제품 소스코드: **공개 확인 못함 [U]**  
> 비공식 공개 구현: 다수 확인 [B2]

## 1. 서비스 정의

Huckleberry는 **일상 육아 기록을 ground-truth 데이터로 축적하고, 그 위에 수면 예측·일정계획·인사이트·AI 입력·전문가형 문제 해결을 단계적으로 쌓는 데이터 중심 육아 플랫폼**이다.

## 2. 제품 계층

[A1]

```
Free
├─ Sleep / Feed / Diaper / Pump / Solids / Health / Activity
├─ Timer / Reminder
├─ Reports
└─ Multi-device sync

Plus
├─ SweetSpot prediction
├─ Insights
├─ Schedule Creator
├─ AI logging
├─ Enhanced Reports
├─ Lock-screen
├─ Widget
└─ Watch

Premium
├─ Berry AI guidance
└─ Personalized sleep plan
```

## 3. 가장 중요한 제품 구조

```
Record
→ Current State
→ Report
→ Prediction
→ Plan
→ Action
→ New Record
```

BabyTime이 기억을 보조한다면 Huckleberry는 기록을 **다음 행동**으로 바꾼다.

## 4. 공개 저장소 현황

공식 Huckleberry 저장소는 확인하지 못했다.

다만 다음 비공식 공개 프로젝트를 직접 확인했다. [B2]

- `Woyken/py-huckleberry-api`
- `Woyken/huckleberry-homeassistant`
- `bckenstler/py-huckleberry-mcp`
- `jayhickey/huckleberry-cli`
- `archiewood/baby-tracker`

이들은 공식 API 계약이 아니며 reverse-engineered/외부 활용 프로젝트다.

## 5. 공개 코드에서 관찰되는 구조

[B2]

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

여러 domain이:

```
root
├─ timer
├─ prefs.last*
└─ intervals / data
```

패턴을 반복한다.

## 6. 핵심 사용 루프

### Tracking
`Event → current state → report`

### Sleep intelligence
`sleep history → SweetSpot → next nap → actual sleep → recalculation`

### AI capture
`voice/text/photo → parsed candidate → event`

### Planning
`age + wake time + nap count → Schedule Creator`

## 7. 가장 잘 푼 문제

- 기록의 "왜"를 prediction으로 연결
- 앱 밖 입력 surface 확장
- age/need에 따라 tracker category 숨김
- current state와 history를 분리한 구조가 공개 코드에서도 관찰됨

## 8. 구조적 한계

- 공식 caregiver 안내는 같은 계정의 다기기 사용이라 identity/role이 약하다.
- prediction이 부모 판단보다 권위적으로 보일 위험이 있다.
- AI/수면/활동/배변까지 확장하며 super-app 복잡도가 증가할 수 있다.
- 비공식 코드에 의존한 구현은 서비스 변경에 취약하다.

## 9. 참고할 패턴

- Ground-truth Free Layer
- Paid Intelligence Layer
- Current State + History
- Domain-specific Event Types
- Real-time Listener
- Prediction Feedback Loop
- Multiple Input Surfaces
- Command-style AI Tools

## 10. 관련 문서

- [화면·UI·UX](surface-map.md)
- [기술·데이터·공개 저장소](system-analysis.md)
- [직접 관찰](../../direct-inspection/apps/huckleberry-site-and-public-repos.md)
- [공개 저장소 생태계](../../direct-inspection/repositories/huckleberry-public-ecosystem.md)
