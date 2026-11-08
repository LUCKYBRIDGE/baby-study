# 육아 앱·웹 기능 비교 매트릭스

> 2026-11-08 1차 분석 기준.  
> ● 강한 핵심 기능 / ○ 제공 또는 보조 / △ 제한적·간접 / — 핵심 아님  
> 점수표가 아니라 **제품의 중심축을 비교하기 위한 표**다.

| 서비스 | 생활기록 | 수면예측 | 발달 | 이유식 | 성장 | 공동양육 | 추억 | 전문가정보 | 공공일정 | 커뮤니티 | 개인화 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| BabyTime | ● | △ | ○ | ○ | ● | ● | ○ | △ | △ | ○ | ○ |
| Huckleberry | ● | ● | ○ | ○ | ○ | ● | △ | ● | △ | — | ● |
| Kinedu | ○ | △ | ● | ○ | ○ | △ | △ | ● | — | — | ● |
| FamilyAlbum | — | — | — | — | — | ● | ● | — | — | — | ○ |
| Napper | △ | ● | — | — | — | ○ | — | ○ | — | — | ● |
| BabySparks | — | — | ● | △ | △ | ○ | — | ● | — | — | ● |
| Solid Starts | — | — | △ | ● | — | △ | — | ● | — | — | ● |
| 베이비빌리 | ○ | △ | ○ | ○ | ● | △ | ○ | ○ | △ | ● | ● |
| 마미톡 | ● | △ | ○ | ○ | ● | ○ | ○ | ● | ○ | ● | ● |
| CDC Milestone Tracker | — | — | ● | — | △ | △ | — | ● | ○ | — | ○ |
| 아이사랑 | — | — | ● | ○ | ○ | — | — | ● | ● | — | 월령 |
| 예방접종도우미 | — | — | — | — | — | — | — | ● | ● | — | 생년월일 |
| NHIS 영유아검진 | — | — | ● | — | ● | — | — | ● | ● | — | 검진시기 |

---

# 서비스별 핵심 한 줄

## BabyTime
**가장 빨리 기록하고 함께 확인한다.**

## Huckleberry
**기록을 다음 행동 예측으로 바꾼다.**

## Kinedu
**발달 관찰을 오늘의 놀이로 바꾼다.**

## FamilyAlbum
**쌓인 사진을 가족의 성장 기억으로 다시 만든다.**

## Napper
**수면 하나를 깊게 파고 하루 일정을 예측한다.**

## BabySparks
**발달이론을 일일 활동 프로그램으로 만든다.**

## Solid Starts
**음식 검색을 즉시 실행 가능한 이유식 방법으로 바꾼다.**

## 베이비빌리
**월령을 중심으로 정보·커뮤니티·커머스를 배치한다.**

## 마미톡
**임신기의 병원 접점을 출산 후 육아 플랫폼으로 연결한다.**

## CDC
**발달 관찰을 안전하게 의료진 대화로 연결한다.**

## 아이사랑
**국내 월령별 육아 정보의 범위를 제공한다.**

## 예방접종도우미
**예방접종에서 신뢰 가능한 최신 기준을 제공한다.**

## NHIS
**일상 육아와 국가 검진의 공식 접점을 만든다.**

---

# 하나의 서비스로 합친다면 필요한 모듈

```
CORE
├─ Baby Profile / Age Context
├─ Timeline
├─ Caregiver & Permission
├─ Notifications
└─ Export

DAILY
├─ Feeding
├─ Sleep
├─ Diaper
├─ Health
└─ Medication

HEALTH
├─ Growth
├─ Vaccination
├─ Checkup
└─ Doctor Summary

DEVELOPMENT
├─ Milestones
├─ Activities
└─ Concerns

FEEDING
├─ Foods DB
├─ Exposure
└─ Reaction

MEMORY
├─ Photos
├─ Milestones
└─ Auto recap

KNOWLEDGE
├─ Age-based content
├─ Official sources
└─ Expert content
```

중요: 이 모든 모듈을 동시에 홈에 보여주면 실패한다. **월령과 현재 상황에 따라 홈이 재구성되어야 한다.**
