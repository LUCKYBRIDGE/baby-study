# Huckleberry 공개 서드파티 저장소 생태계 분석

> 관찰일: 2026-11-08  
> 주의: 아래 저장소들은 Huckleberry 공식 저장소가 아닙니다. 공개된 커뮤니티 구현을 통해 데이터 구조와 외부 활용 가능성을 연구하기 위한 자료입니다.

## 분석 저장소

1. https://github.com/Woyken/py-huckleberry-api
2. https://github.com/Woyken/huckleberry-homeassistant
3. https://github.com/bckenstler/py-huckleberry-mcp
4. https://github.com/jayhickey/huckleberry-cli
5. https://github.com/archiewood/baby-tracker

# 1. py-huckleberry-api

가장 구조적 정보가 많습니다.

## 저장소 구조

```
src/huckleberry_api/
├─ api.py
├─ firebase_types.py
├─ const.py
└─ models.py

tests/
├─ sleep
├─ feeding
├─ bottle
├─ diaper
├─ growth
├─ medicine
├─ temperature
├─ pump
├─ solids
├─ activity
├─ listeners
└─ firebase models
```

특히 `firebase_types.py`를 "canonical schema reference"로 명시하고 있습니다.

## 관찰되는 데이터 패턴

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

각 domain은 대체로:

```
root
├─ prefs.last*
├─ timer (해당되는 경우)
└─ history subcollection
```

을 공유합니다.

### 장점
- 현재 상태 읽기 빠름
- 마지막 기록 표시 빠름
- 이력은 append형으로 관리
- domain별 listener 구성 가능

## tests가 중요한 이유

단순 reverse engineering 코드가 아니라 실제 live payload와 write/read behavior를 검증하는 테스트가 다수 존재합니다.

예:
- listener refresh
- timer
- write failure
- timezone
- bottle/feed interval
- live Firebase models

따라서 README보다 **tests + schema comments**가 더 강한 근거가 됩니다.

# 2. huckleberry-homeassistant

Home Assistant 통합은 Huckleberry event를 다른 시스템에서 어떤 상태로 소비할 수 있는지 보여줍니다.

## child별 sensor

- sleep status
- nursing
- pumping
- growth
- medication
- bottle
- solids
- diaper
- activities

## current state와 history 분리

- sensor = 마지막/현재 상태
- calendar = 과거 events

이 역시:

```
Current Projection
+
Historical Projection
```

패턴을 확인시켜 줍니다.

## 자동화 가능성

예:
- 수면 시작 시 알림
- 수유 20분 지속 시 알림
- 특정 이벤트 기록

즉 육아 기록 데이터는 앱 화면 안에서만 가치 있는 것이 아니라 **home automation trigger**로도 사용할 수 있습니다.

# 3. py-huckleberry-mcp

MCP 서버는 자연어 agent가 육아 기록을 읽고 쓰는 interface 사례입니다.

22개 tool로:
- child
- sleep
- feeding
- diaper
- growth

를 다룹니다.

특히:
- start/pause/resume/complete/cancel
- direct retroactive logging
- history retrieval

을 분리합니다.

이는 AI 육아 비서의 tool schema를 설계할 때 참고 가치가 큽니다.

좋은 AI tool은:
```
log_sleep()
start_sleep()
complete_sleep()
get_sleep_history()
```
처럼 **명확한 domain command**를 가져야 합니다.

# 4. huckleberry-cli

CLI는 같은 API를 매우 단순한 명령으로 노출합니다.

예:
```
sleep start
sleep stop
feed start --side=left
feed switch
diaper poo
growth
```

이 구조는 좋은 앱의 빠른 UI와 비슷합니다.

즉 GUI가 없어도 **domain verb가 명확하면 기능 구조가 이해됩니다.**

# 5. archiewood/baby-tracker

이 저장소는 Huckleberry export를 외부 분석 대시보드로 변환합니다.

## 데이터 확보

`scripts/update_csv.py`를 직접 보면:
- 이메일 IMAP 접속
- 제목 "Your data export has been delivered" 검색
- 다운로드 링크 추출
- events.csv 저장

을 자동화합니다.

이는 Huckleberry CSV export가 실제 외부 분석 pipeline에 사용될 수 있음을 보여주는 사례입니다.

## 분석 구조

```
Huckleberry CSV
→ SQL normalization
→ Daily timeline
→ Sleep dashboard
→ Growth dashboard
→ Guideline comparison
```

## 좋은 아이디어

기록앱 내부 통계와 별개로:
- 원자료 export
- 외부 분석
- 의료/공식 기준과 비교

할 수 있습니다.

이는 사용자 데이터 portability의 실제 가치를 보여줍니다.

# 6. 공개 코드에서 특히 참고할 설계

## A. current state + history

```
prefs.last*
+
intervals
```

## B. timer와 completed event 분리

진행중 상태를 history event로 미리 저장하지 않습니다.

## C. polymorphic feed

```
feed
├─ breast
├─ bottle
└─ solids
```

공통 상위 domain 아래 mode별 payload.

## D. global catalog + personal custom type

solids는:
- curated food
- child custom food
- actual feed history

가 분리됩니다.

## E. reminder를 preference로 분리

event와 reminder 설정을 같은 record로 섞지 않습니다.

## F. AI/automation-friendly API

명령형 도구로 변환하기 좋은 구조입니다.

# 7. 그대로 가져오면 안 되는 것

이 공개 구현은 비공식 reverse engineering입니다.

따라서:
- endpoint/API를 서비스 의존 구현에 그대로 사용
- private backend와 결합
- 비공개 필드에 장기 의존

하는 것은 피해야 합니다.

우리가 가져올 것은 **구조적 패턴**입니다.

# 8. 결론

공개 생태계까지 보면 Huckleberry의 핵심은 화면보다 다음 데이터모델에 있습니다.

```
Child
├─ Current domain state
├─ Active timers
├─ Last-event summaries
├─ Historical events
├─ Reminders
└─ Derived intelligence
```

이 구조는 향후 독자적인 육아 기록 시스템의 좋은 reference architecture입니다.
