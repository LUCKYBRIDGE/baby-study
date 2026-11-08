# Service Dossiers — 앱·웹별 정본 분석

이 폴더는 `baby-study`의 **서비스별 정본(canonical dossier)** 입니다.

기존 자료가 분석 단계에 따라 `apps/`, `deep-dive/`, `direct-inspection/`에 나뉘어 있었다면, 여기서는 **한 서비스를 하나의 폴더**로 모읍니다.

## 폴더 규격

각 서비스는 기본적으로 다음 3개 문서로 구성합니다.

```
docs/services/<service>/
├─ README.md          # 한눈에 보는 서비스 구조 + 파일/페이지 지도
├─ surface-map.md     # 실제 페이지·화면·UI·UX·버튼·사용자 흐름
└─ system-analysis.md # 기술·데이터·권한·알림·문제 해결 방식·한계
```

공개 코드가 존재하거나 분석 가치가 높은 경우에는 별도 repository 문서를 추가할 수 있습니다.

## 근거 표기

- **[A1]** 공식 제품 사이트 직접 확인
- **[A2]** 공식 도움말/FAQ/정책 직접 확인
- **[A3]** 공식 App Store/Google Play 직접 확인
- **[B1]** 공식 공개 소스코드 직접 확인
- **[B2]** 비공식 공개 구현/통합 저장소 직접 확인
- **[C]** 위 근거에 기반한 제품적 추론
- **[U]** 공개 자료로 확인 불가 / 미확인

내부 파일·폴더 구조가 공개되지 않은 상용 앱에 대해서는 **절대 추정으로 파일 트리를 만들지 않습니다.** 대신 공개 웹 경로, 화면 IA, 데이터 모델 추론, 공개 기술 단서만 기록합니다.

## 앱

| 서비스 | 핵심 분석 포인트 |
|---|---|
| [BabyTime](babytime/) | 초저마찰 기록, interval, 공동양육 |
| [Huckleberry](huckleberry/) | 이벤트 스토어, 실시간 상태, 수면예측, 공개 비공식 코드 |
| [Kinedu](kinedu/) | assessment → skill model → 활동 |
| [FamilyAlbum](familyalbum/) | 앨범 workspace, 권한, 자동 회고 |
| [Napper](napper/) | 수면 vertical, age baseline → personalized prediction |
| [BabySparks](babysparks/) | 일일 발달 커리큘럼, B2B 확장 |
| [Solid Starts](solid-starts/) | 음식 객체 중심 DB, 노출·반응 기록 |
| [베이비빌리](babybilly/) | 주수·월령 기반 super-app orchestration |
| [마미톡](mommytalk/) | 병원 초음파 진입점 → 육아 tracker |
| [MOMI](momi/) | 음성/자연어 → AI 구조화 → 확인 저장 |
| [Pathways.org](pathways/) | Today/Play/Track, observable milestone |
| [CDC Milestone Tracker](cdc-milestone/) | 모니터링 → concern → 의료진 인계 |

## 공공 웹·시스템

| 서비스 | 핵심 분석 포인트 |
|---|---|
| [아이사랑](childcare-go-kr/) | 월령 taxonomy + 보육행정 |
| [예방접종도우미](kdca-vaccination/) | 공식 일정 규칙 + 실제 접종 + 기관 |
| [영유아 건강검진](nhis-infant-checkups/) | 문진 → 선별 → 검진 → 결과 → 의뢰 |

## 이 폴더에서 우선 보는 순서

새 기능을 설계할 때는 각 서비스 폴더에서:

1. `README.md` — 전체 구조 파악
2. `surface-map.md` — 실제 화면·버튼·동선
3. `system-analysis.md` — 데이터/기술/문제 해결 원리

순으로 봅니다.

## 원자료와의 관계

- 1차 분석: `docs/apps/`, `docs/web/`
- 심층 해석: `docs/deep-dive/`
- 직접 검증 근거: `docs/direct-inspection/`
- 서비스별 정본: **`docs/services/`**

새로운 발견은 우선 직접 검증 문서에 근거를 남긴 뒤, 해당 서비스 dossier에 반영합니다.
