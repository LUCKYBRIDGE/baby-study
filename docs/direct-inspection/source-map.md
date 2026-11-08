# 직접 확인한 사이트·저장소 Source Map

> 2026-11-08 현재

이 문서는 각 서비스에 대해 **실제로 어느 페이지/저장소까지 확인했는지**를 기록한다.

| 서비스 | Home | Feature/Core | FAQ/Help | Pricing | Privacy | 공개 repo | 상태 |
|---|---:|---:|---:|---:|---:|---:|---|
| BabyTime | ✓ | ✓ | ✓ | — | 일부 | 공식 없음 | 직접검증 |
| Huckleberry | ✓ | ✓ | ✓ | ✓ | ✓ | 비공식 생태계 다수 | 직접검증+코드 |
| Kinedu | ✓ | ✓ Assessment/Science | ✓ | 일부 | 일부 | 공식 앱 repo 없음 | 직접검증 |
| Pathways | ✓ | ✓ Today/Play/Track | ✓ | 무료 | ✓ | 공식 repo 없음 | 직접검증 |
| FamilyAlbum | ✓ | ✓ Memories/Album | ✓ | ✓ | 일부 | 공식 앱 repo 없음 | 직접검증 |
| Napper | ✓ | ✓ | Support | ✓ | ✓ | 공식 repo 없음 | 직접검증 |
| BabySparks | ✓ | ✓ Register/B2B | FAQ | ✓ | ✓ 링크 | 공식 앱 repo 없음 | 직접검증 |
| Solid Starts | ✓ | ✓ App/Foods DB | FAQ 일부 | ✓ | 일부 | 공식 repo 없음 | 직접검증 |
| 베이비빌리 | ✓ | ✓ | 콘텐츠 | 커머스 | 정책 링크 | 공식 repo 확인 안 됨 | 직접검증 |
| 마미톡 | ✓ | ✓ | 커뮤니티 기능안내 | 커머스 | ✓ | 공식 repo 없음 | 직접검증 |
| MOMI | Store | Store 기능 | — | IAP | Play Data Safety | 공식 repo 없음 | 스토어검증 |
| CDC Milestone | ✓ | ✓ checklist | ✓ | 무료 | 공식 정책 | 공식 repo 미확인 | 직접검증 |
| 아이사랑 | ✓ | ✓ 월령/행정 | ✓ | 공공 | 공공정책 | — | 직접검증 |
| 예방접종도우미 | ✓ | ✓ 일정/기관 | ✓ | 공공 | 공공정책 | — | 직접검증 |
| NHIS 영유아검진 | ✓ | ✓ PDF/웹 | ✓ | 공공 | 공공정책 | — | PDF 직접검증 |

## Huckleberry 코드에서 실제 확인한 저장소

### Woyken/py-huckleberry-api
확인:
- 전체 tree
- README
- `firebase_types.py`
- test directory
- changelog/search excerpts

직접 확인된 주요 domain:
- user
- child
- sleep
- feed
- diaper
- health
- pump
- activities
- reminders
- solids catalog

### Woyken/huckleberry-homeassistant
확인:
- README
- child sensor
- calendar history
- automation service
- realtime sync 설명

### bckenstler/py-huckleberry-mcp
확인:
- README
- 22 tool 구조
- child/sleep/feeding/diaper/growth commands

### jayhickey/huckleberry-cli
확인:
- README
- command taxonomy

### archiewood/baby-tracker
확인:
- 전체 tree
- CSV email import script
- SQL normalization
- sleep/growth dashboards

## 공식 repo가 없을 때의 원칙

코드가 공개되지 않은 제품은 '내부 기술구조'를 확정하지 않는다.

대신:
```
Visible IA
+
Official Help
+
Policy
+
App Store
+
Network/API public documentation if available
```
까지만 근거로 사용한다.

클론 repository나 이름만 같은 개인 repository는 분석 근거에서 제외한다.
