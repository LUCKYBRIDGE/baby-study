# 공개 저장소·파일구조 확인 매트릭스

> 서비스 폴더/파일 구조는 **공개 코드가 실제로 존재할 때만** 기록한다.

| 서비스 | 공식 제품 repo | 비공식/연관 repo | 실제 파일 구조 분석 |
|---|---|---|---|
| BabyTime | 미확인 | 뚜렷한 분석대상 없음 | 불가 |
| Huckleberry | 미확인 | py-huckleberry-api, HA, MCP, CLI, export dashboard | **완료** |
| Kinedu | 제품 repo 미확인 | 공식 org의 제품과 무관한 OSS 일부 | 제품 분석 제외 |
| FamilyAlbum | 제품 repo 미확인 | downloader/mirror 계열 | 제품 분석 제외 |
| Napper | 미확인 | 동명 프로젝트 | 제외 |
| BabySparks | 미확인 | 동명 개인 repo | 제외 |
| Solid Starts | 미확인 | 유사 food app | 제외 |
| 베이비빌리 | 공식 확인 못함 | clone/개인 repo | 제외 |
| 마미톡 | 미확인 | 확인 못함 | 불가 |
| MOMI | 미확인 | 확인 못함 | 불가 |
| Pathways | 미확인 | 확인 못함 | 불가 |
| CDC Milestone | 현재 공식 repo 미확인 | 개인 milestone apps | 제외 |
| 한국 공공시스템 | 별도 공개제품 repo 분석 안 함 | — | 웹/PDF IA 분석 |

## Huckleberry에서 실제 확인한 tree

### py-huckleberry-api

```
src/huckleberry_api/
├─ __init__.py
├─ api.py
├─ const.py
├─ firebase_types.py
├─ models.py
└─ py.typed

tests/
├─ test_activity.py
├─ test_activity_timer.py
├─ test_authentication.py
├─ test_bottle_feeding.py
├─ test_calendar.py
├─ test_diaper.py
├─ test_feeding.py
├─ test_growth.py
├─ test_listeners.py
├─ test_medicine.py
├─ test_pump.py
├─ test_sleep.py
├─ test_solids.py
├─ test_temperature.py
├─ test_timezone.py
└─ test_write_failures.py
```

### archiewood/baby-tracker

```
components/
├─ Timeline.svelte
└─ InternalTimeline.svelte

pages/
├─ index.md
├─ feeds.md
├─ diapers.md
├─ sleep.md
├─ growth.md
├─ tummy_time.md
└─ days/

queries/
├─ days.sql
└─ events.sql

scripts/
├─ update_csv.py
└─ generate_download.py

sources/huckleberry/
├─ events.csv
├─ targets.csv
└─ connection.yaml
```

## 왜 엄격하게 구분하는가

사이트 UI만 보고:

```
src/
components/
services/
firebase/
```

같은 가상의 내부 tree를 만드는 것은 분석이 아니라 추측이다.

따라서 상용 비공개 제품은:
- URL path
- screen IA
- public API/policy
- product flow

까지만 기록하고, 내부 파일 tree는 **미확인**으로 남긴다.
