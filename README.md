# baby-study

아기를 키우는 과정에서 필요한 **정보, 기록, 판단, 알림, 가족 협업, 발달 지원 시스템**을 체계적으로 연구하는 저장소입니다.

이 저장소의 목적은 특정 앱을 추천하는 데 그치지 않습니다. 국내외 육아·발달·건강·가족공유 서비스가 부모의 문제를 어떻게 정의하고, 어떤 데이터를 기록하며, 그 데이터를 어떻게 정보·추천·행동으로 바꾸는지를 분석합니다.

> 분석 기준일: 2026-11-08  
> 주의: 이 저장소는 제품·UX·정보구조 연구용입니다. 의료 진단이나 개인별 치료 지침을 제공하지 않습니다. 건강 관련 판단은 소아청소년과 등 의료전문가 및 대한민국의 공식 보건 지침을 우선합니다.

## 바로 보기

- **직접 사이트·저장소 검증 기록:** [docs/direct-inspection/README.md](docs/direct-inspection/README.md)
- **직접 확인한 Source Map:** [docs/direct-inspection/source-map.md](docs/direct-inspection/source-map.md)
- **Craft Anything 기반 분석 방법:** [docs/direct-inspection/methodology-craft-anything.md](docs/direct-inspection/methodology-craft-anything.md)
- **직접 관찰 후 핵심 비교:** [docs/direct-inspection/cross-findings.md](docs/direct-inspection/cross-findings.md)
- **앱·웹 구조 심층분석 인덱스:** [docs/deep-dive/README.md](docs/deep-dive/README.md)
- **서비스 아키텍처 비교 지도:** [docs/deep-dive/architecture-comparison.md](docs/deep-dive/architecture-comparison.md)
- **아기 양육 요구 전체 지도:** [docs/00-framework/parenting-needs-map.md](docs/00-framework/parenting-needs-map.md)
- **육아 기록 데이터 모델:** [docs/00-framework/record-data-model.md](docs/00-framework/record-data-model.md)
- **기능 비교 매트릭스:** [docs/comparison/feature-matrix.md](docs/comparison/feature-matrix.md)
- **공통 디자인 패턴:** [docs/comparison/key-patterns.md](docs/comparison/key-patterns.md)

## 연구 질문

1. 출생 직후부터 영유아기까지 부모가 실제로 반복해서 확인해야 하는 정보는 무엇인가?
2. 어떤 기록은 반드시 남길 가치가 있고, 어떤 기록은 과도한 입력 부담만 만드는가?
3. 기록을 어떻게 패턴, 알림, 다음 행동, 진료 준비로 전환할 수 있는가?
4. 엄마·아빠·조부모·베이비시터 등 여러 양육자가 같은 상태를 어떻게 공유해야 하는가?
5. 수면·수유·배변·성장·발달처럼 서로 연결된 데이터를 하나의 맥락으로 볼 수 있는가?
6. 안전·건강처럼 고위험 정보에서 앱은 어디까지 안내하고 어디서 의료기관 연결로 넘겨야 하는가?
7. 발달 지원은 '또래 비교'와 불안을 키우지 않으면서 어떻게 유용하게 제공할 수 있는가?
8. 부모가 피곤한 상황에서도 1~3초 안에 기록할 수 있는 인터랙션은 무엇인가?
9. 아이가 성장하면서 신생아용 기록 UI를 어떻게 이유식·발달·놀이·교육 중심으로 자연스럽게 전환할 수 있는가?
10. 유료화가 부모에게 실질적인 가치를 주는 지점은 어디인가?

## 디렉터리

- `docs/00-framework/` — 육아 요구 지도, 공통 분석틀, 데이터 모델
- `docs/apps/` — 1차 앱별 분석
- `docs/web/` — 1차 공공·전문 웹서비스 분석
- `docs/deep-dive/apps/` — 앱별 구조·IA·데이터흐름·루프 심층분석
- `docs/deep-dive/web/` — 공공 웹/시스템 심층분석
- `docs/direct-inspection/` — 공식 사이트·FAQ·앱스토어·공개 저장소를 직접 확인한 근거 기록
- `docs/comparison/` — 기능 비교표와 공통 디자인 패턴
- `docs/ideas/` — 향후 제품 아이디어와 설계 가설

## 현재 Deep Dive 완료 대상

### 앱
- BabyTime
- Huckleberry
- Kinedu
- FamilyAlbum
- Napper
- BabySparks
- Solid Starts
- 베이비빌리
- 마미톡
- MOMI
- Pathways.org
- CDC Milestone Tracker

### 공공 웹/시스템
- 임신육아종합포털 아이사랑
- 질병관리청 예방접종도우미
- 영유아 건강검진 / 국민건강보험

## 분석 원칙

### 1. 기능보다 사용자 문제를 먼저 본다
'수면 타이머가 있다'보다 '마지막 수면 시간을 기억하지 않아도 되게 한다'를 분석합니다.

### 2. 화면보다 시스템을 본다
메뉴 이름만 정리하지 않고 다음을 추적합니다.

```
입력
→ 원자료
→ 파생데이터
→ 패턴/해석
→ 예측/추천
→ 다음 행동
→ 결과
```

### 3. 확인된 사실과 추론을 분리한다
공식 웹·FAQ·앱스토어·공공기관 자료에서 확인되는 기능을 우선 사용하고, 내부 구조는 공개된 사용자 흐름을 바탕으로 제품적 추론임을 구분합니다.

### 4. 부모의 인지부하를 핵심 지표로 본다
신생아기에는 한 손 조작, 야간 사용, 잠금화면, 위젯, 음성 입력, 기본값, 자동완성 등의 가치가 일반 앱보다 훨씬 큽니다.

### 5. 고위험 영역과 저위험 영역을 분리한다
- 저위험: 사진, 놀이, 추억, 일상 기록
- 중위험: 수면 패턴, 식사 패턴, 발달 활동 추천
- 고위험: 발열, 약 복용, 호흡 이상, 탈수 의심, 알레르기 반응, 발달 우려

고위험 기능에서는 앱의 자신감 있는 진단보다 **명확한 한계 표시 + 공식 정보 + 의료전문가 연결**이 더 중요합니다.

### 6. 월령에 따라 홈 화면 자체가 바뀌어야 한다
0~3개월과 18개월 부모의 핵심 과업은 다릅니다. 고정 메뉴를 계속 추가하는 방식보다 생애주기별 정보구조가 적합한지 봅니다.

## 1차 분석 대상과 핵심 연구 주제

| 유형 | 서비스 | 핵심 연구 주제 |
|---|---|---|
| 앱 | BabyTime | 초저마찰 기록, 공동양육, 생활패턴 시각화 |
| 앱 | Huckleberry | 기록 → 예측 → 개인화 조언 |
| 앱 | Kinedu | 발달평가 → 오늘의 활동 추천 |
| 앱 | FamilyAlbum | 아이 중심 가족 공유와 추억 자동화 |
| 앱 | Napper | 수면 전문화와 개인화 일정 |
| 앱 | BabySparks | 발달 활동 콘텐츠와 진도 추적 |
| 앱/웹 | Solid Starts | 이유식·알레르기·음식 데이터베이스 |
| 앱 | 베이비빌리 | 시기별 정보·커뮤니티·기록·커머스 |
| 앱 | 마미톡 | 임신→출산→육아로 이어지는 장기 사용자 여정 |
| 앱 | MOMI | 음성/자연어 AI 기록과 확인 기반 저장 |
| 앱/웹 | Pathways.org | 행동 단위 발달 정의와 활동 연결 |
| 앱/웹 | CDC Milestone Tracker | 공공기관 기반 발달 모니터링 |
| 웹/앱 | 임신육아종합포털 아이사랑 | 국내 공식 육아정보와 보육 서비스 |
| 웹 | 예방접종도우미 | 예방접종 일정·기록·기관 연결 |
| 웹/앱 | 영유아 건강검진 | 문진·K-DST·검진·결과·의뢰 |

## 핵심 산출물

- 아기 양육 전체 정보구조
- 꼭 기록할 데이터와 선택적으로 기록할 데이터 구분
- 월령별 홈 화면 모델
- 공동양육 권한 모델
- 진료 전 요약 리포트 모델
- 수유·수면·배변·성장·발달 통합 타임라인
- 예방접종·검진·약·병원 일정 시스템
- 이유식 및 알레르기 노출 기록 모델
- 발달 마일스톤과 놀이 추천 시스템
- 가족 사진·영상 성장 타임라인
- 부모의 기록 피로도를 낮추는 입력 UX 패턴
- 안전·의료 정보 가드레일

## 주요 공식 참고원

- 대한민국 임신육아종합포털 아이사랑: https://www.childcare.go.kr/
- 질병관리청 예방접종도우미: https://nip.kdca.go.kr/
- 질병관리청 국가건강정보포털: https://health.kdca.go.kr/
- 국민건강보험공단: https://www.nhis.or.kr/
- CDC Learn the Signs. Act Early.: https://www.cdc.gov/act-early/
- WHO Infant and young child feeding: https://www.who.int/news-room/fact-sheets/detail/infant-and-young-child-feeding
- HealthyChildren.org (American Academy of Pediatrics): https://www.healthychildren.org/

## 분석 방법 메모

소프트웨어 분석은 `storytold/craft-anything`의 **Study → Check → evidence 중심 접근**을 참고합니다. 화면을 흉내 내는 데 목적을 두지 않고, 관찰 가능한 사용자 흐름과 공개 자료를 근거로 기능의 목적·구조·한계를 분리해서 기록합니다.

- Craft Anything: https://github.com/storytold/craft-anything
