# 아기 양육 기록 데이터 모델

> 제품 구현을 위한 스키마 확정본이 아니라, 앱 분석 때 어떤 데이터를 구분해서 볼지 정의하는 개념 모델이다.

# 1. 핵심 설계

아기 기록은 문서형 일기보다 **시간 기반 이벤트 스트림(event stream)**으로 보는 편이 자연스럽다.

```
Baby
 ├─ Care events
 │   ├─ Feeding
 │   ├─ Sleep
 │   ├─ Diaper
 │   ├─ Temperature/Symptom
 │   ├─ Medication
 │   └─ Activity
 ├─ Growth measurements
 ├─ Vaccinations
 ├─ Checkups
 ├─ Milestones
 ├─ Food exposures
 └─ Memories
```

홈 화면은 이 원자료를 다시 읽어 **현재 상태**를 만든다.

예:

```
마지막 수유  02:10 · 110ml · 2시간 14분 전
현재 수면    03:42부터 · 42분째
마지막 기저귀 03:30 · 소변
```

---

# 2. 공통 엔터티

## Baby

- id
- display_name
- birth_date
- due_date
- sex(optional)
- premature / gestational context(optional)
- timezone
- profile_photo(optional)
- archived_at

### 주의
발달 기능에서 조산 관련 교정연령이 필요한 경우 출생일 하나만으로 처리하면 안 된다.

---

## Caregiver

- id
- display_name
- relationship
- role
- permissions
- joined_at
- revoked_at

### 권한 예
- owner
- co_parent
- caregiver
- family_viewer

건강 기록 수정권과 사진 열람권은 분리 가능해야 한다.

---

# 3. 공통 이벤트 구조

모든 일상 이벤트가 가질 수 있는 공통 필드:

```json
{
  "id": "event_id",
  "baby_id": "baby_id",
  "type": "feeding",
  "started_at": "...",
  "ended_at": null,
  "created_by": "caregiver_id",
  "created_at": "...",
  "updated_at": "...",
  "source": "manual",
  "note": null
}
```

## source 예
- manual
- timer
- widget
- voice
- photo_ai
- imported
- device

자동 입력과 수동 입력은 구분해야 한다.

---

# 4. Feeding

## Breastfeeding
- side: left/right/both
- duration
- switched_side_at(optional)

## Bottle
- content: formula / expressed_milk / other
- offered_ml
- consumed_ml

## Pumping
- left_ml
- right_ml
- total_ml
- duration

## 파생
- feeds_24h
- total_bottle_ml_24h
- mean_interval
- longest_interval

### 주의
'먹인 양'과 '준비한 양'을 혼동하면 안 된다.

---

# 5. Sleep

- started_at
- ended_at
- sleep_kind: nap/night/unknown
- location(optional)
- note

## 파생
- duration
- total_sleep_24h
- daytime_sleep
- nighttime_sleep
- wake_window
- night_wakings

## 예측
- predicted_next_sleep_at
- confidence
- algorithm_version

예측값은 실제 기록과 별도 데이터로 유지해야 한다.

---

# 6. Diaper

- kind: wet / stool / both / dry
- stool_color(optional)
- stool_consistency(optional)
- amount(optional)

상세 필드는 기본 UI에서 숨기는 편이 적합하다.

---

# 7. Temperature & Symptom

## Temperature
- value
- unit
- measurement_site
- device(optional)

## Symptom
- symptom_code/text
- started_at
- ended_at
- severity: user-observed
- note

부모가 적은 '심함'은 의료진 진단의 중증도와 동일하지 않다.

---

# 8. Medication

## MedicationPlan
- name
- prescribed_by(optional)
- dose_instruction
- schedule
- start_date
- end_date

## MedicationAdministration
- plan_id
- actual_time
- actual_amount
- recorded_by

**알림 발생 ≠ 투여 완료**.

---

# 9. GrowthMeasurement

- measured_at
- weight
- length_or_height
- head_circumference
- source: home/clinic/checkup
- note

## 파생
- trend
- growth_chart_position
- interval_change

성장도표 기준 버전과 출처를 저장할 필요가 있다.

---

# 10. Vaccination

## VaccineScheduleItem
- vaccine_code
- recommended_window
- dose_number
- source_authority
- source_version

## VaccinationRecord
- vaccine_code
- dose_number
- administered_at
- institution(optional)
- product(optional)
- note

국가 기준이 바뀔 수 있으므로 schedule과 actual record를 분리한다.

---

# 11. HealthCheckup

- checkup_type
- eligibility_window
- appointment_at
- completed_at
- measurements
- clinician_notes_as_entered_by_parent
- follow_up_at
- attachments(optional)

진료 전 질문 목록을 별도 엔터티로 둘 가치가 있다.

---

# 12. Milestone

## MilestoneDefinition
- code
- domain
- description
- age_context
- source
- source_version

## BabyMilestoneObservation
- milestone_code
- status
- observed_at
- recorded_by
- note

status 예:
- not_observed
- emerging
- observed
- consistently_observed
- unsure

단순 boolean보다 발달의 진행성을 표현하기 쉽다.

---

# 13. FoodExposure

- food_id/name
- first_exposure_at
- preparation/form
- amount(optional)
- acceptance
- reaction
- note

## Reaction
- occurred_at
- symptoms
- severity_as_observed
- medical_care_sought
- note

음식 DB 자체 정보와 아기 개인 기록을 분리한다.

---

# 14. Activity / Play

- activity_type
- started_at
- duration
- child_response(optional)
- developmental_domains(optional)

매일 모든 활동을 기록하게 만들기보다 추천 품질 개선 등에 필요한 최소 피드백만 받는 것이 좋다.

---

# 15. Memory

- captured_at
- media
- caption
- milestone_link(optional)
- visibility
- uploaded_by

건강 기록과 가족 추억 미디어는 동일한 공유 정책을 사용하지 않는 것이 안전하다.

---

# 16. Schedule와 실제 기록 분리

반드시 두 개를 구분한다.

```
예방접종 예정  → VaccinationScheduleItem
예방접종 완료  → VaccinationRecord

약 먹을 시간   → MedicationPlan
실제로 먹임    → MedicationAdministration

예상 낮잠      → Prediction
실제로 잠듦    → SleepEvent
```

이를 섞으면 데이터 신뢰성이 무너진다.

---

# 17. 파생 데이터는 재계산 가능하게

가능하면 원자료를 보존하고 통계는 재계산한다.

예:
- 평균 수유 간격
- 하루 수면 총량
- 최근 7일 변화

통계 값을 사용자가 직접 수정하는 구조보다 원 이벤트를 고치는 구조가 낫다.

---

# 18. 시간 처리

육아 기록은 시간대가 중요하다.

- UTC 저장 + 사용자 timezone 표시
- 여행 시 timezone 변경
- 밤 12시 기준으로 하루를 자르면 야간 수면 분석이 왜곡될 수 있음
- '24시간 rolling window'와 'calendar day'를 구분

---

# 19. 수정 이력

공동양육에서는 최소한 다음이 유용하다.

- created_by
- updated_by
- updated_at
- deleted_at
- 필요 시 audit log

특히 약 복용 등은 누가 수정했는지 확인 가능해야 한다.

---

# 20. 데이터 내보내기

이상적인 export:

- CSV: 이벤트 분석용
- JSON: 전체 백업/이관
- PDF: 진료/검진용 요약
- media archive: 사진·영상

서비스 종속을 줄이려면 **원자료 내보내기**가 중요하다.

---

# 21. 최소 데이터 원칙

아기 데이터는 장기적으로 민감하다.

수집 전에 묻는다.

1. 이 데이터가 핵심 기능에 필요한가?
2. 부모에게 명확한 가치로 되돌아가는가?
3. 몇 년 후에도 보관해야 하는가?
4. 가족 구성원 모두에게 보여도 되는가?
5. 광고·AI 개인화에 사용되는가?

필요하지 않은 정보는 애초에 받지 않는 것이 가장 안전하다.

---

# 22. 분석 시 체크할 핵심

각 앱에서 다음을 찾아 기록한다.

- 실제 저장하는 원자료
- 사용자가 보는 파생 통계
- 앱이 생성하는 추론
- 원자료 수정 가능 여부
- 여러 양육자 충돌 처리
- 내보내기
- 삭제
- 의료진 공유
- 월령이 올라가면서 활성 데이터 타입이 변하는지
