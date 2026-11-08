# Deep Dive Index

> 육아·발달·건강 관련 앱/웹을 **기능 목록이 아니라 제품 구조와 문제 해결 메커니즘** 기준으로 분석한다.

## 분석 기준

각 문서는 가능한 한 다음 순서로 본다.

1. 서비스가 해결하는 핵심 불확실성
2. 전체 정보구조(IA)
3. 핵심 엔터티와 데이터 흐름
4. 온보딩/첫 가치 경험
5. 반복 사용 루프
6. 입력 방식
7. 기록 → 통계 → 예측/추천 변환
8. 공동양육/권한
9. 알림/일정
10. 생애주기 적응
11. 전문가·공공정보 연결
12. 수익모델
13. 개인정보/안전
14. 강점과 구조적 한계
15. 일반화 가능한 설계 패턴

> **확인된 사실과 제품적 추론을 가능한 한 분리한다.**  
> 공개 페이지로 확인하기 어려운 실제 앱 인터랙션은 향후 설치 테스트 대상으로 남긴다.

---

# 앱 Deep Dive

| 서비스 | 핵심 메커니즘 | 문서 |
|---|---|---|
| BabyTime | 최소 터치 이벤트 기록 → 패턴/통계 → 공동양육 | [babytime-deep-dive.md](apps/babytime-deep-dive.md) |
| Huckleberry | 기록 → 리포트 → 수면예측 → 계획/AI | [huckleberry-deep-dive.md](apps/huckleberry-deep-dive.md) |
| Kinedu | 발달관찰 → Skill Model → 오늘 활동 | [kinedu-deep-dive.md](apps/kinedu-deep-dive.md) |
| FamilyAlbum | 아이 중심 가족공간 → 권한 → 자동 회고 | [familyalbum-deep-dive.md](apps/familyalbum-deep-dive.md) |
| Napper | 수면로그 → wake window → 개인화 일정 | [napper-deep-dive.md](apps/napper-deep-dive.md) |
| BabySparks | 발달 지식 → 일일 활동 프로그램 → 진도 | [babysparks-deep-dive.md](apps/babysparks-deep-dive.md) |
| Solid Starts | 음식 검색 → 월령별 방법 → 개인 섭취이력 | [solid-starts-deep-dive.md](apps/solid-starts-deep-dive.md) |
| 베이비빌리 | 주수/월령을 전역 context로 사용 | [babybilly-deep-dive.md](apps/babybilly-deep-dive.md) |
| 마미톡 | 병원 초음파 접점 → 임신 → 육아 생애주기 | [mommytalk-deep-dive.md](apps/mommytalk-deep-dive.md) |
| MOMI | 음성 → AI 구조화 후보 → 사용자 확인 → 기록 | [momi-deep-dive.md](apps/momi-deep-dive.md) |
| Pathways.org | 관찰 가능한 발달행동 + 활동 + 특수경로 | [pathways-deep-dive.md](apps/pathways-deep-dive.md) |
| CDC Milestone Tracker | 발달 모니터링 → concern → 의료진 인계 | [cdc-milestone-tracker-deep-dive.md](apps/cdc-milestone-tracker-deep-dive.md) |

---

# 웹 / 공공 시스템 Deep Dive

| 서비스 | 핵심 메커니즘 | 문서 |
|---|---|---|
| 아이사랑 | 월령별 육아 taxonomy + 보육행정 | [childcare-go-kr-deep-dive.md](web/childcare-go-kr-deep-dive.md) |
| 예방접종도우미 | 버전 관리되는 공식 규칙 + 실제 접종기록 + 알림 | [kdca-vaccination-deep-dive.md](web/kdca-vaccination-deep-dive.md) |
| 영유아 건강검진 | 문진 → 선별 → 검진 → 결과 → 의뢰 | [nhis-infant-checkups-deep-dive.md](web/nhis-infant-checkups-deep-dive.md) |

---

# 어떤 기능을 만들 때 무엇을 볼까?

## 신생아 기록
1. BabyTime
2. Huckleberry
3. MOMI

## 수면
1. Napper
2. Huckleberry

## 발달
1. Pathways.org — 행동 정의
2. CDC — 안전/의료 경계
3. Kinedu — 개인화 추천
4. BabySparks — 활동 커리큘럼

## 이유식
1. Solid Starts
2. 아이사랑 공식 월령 정보

## 공동양육
1. FamilyAlbum — 권한
2. BabyTime — 실시간 상태 공유
3. Huckleberry — 다기기 sync

## 임신→출산→육아 생애주기
1. 마미톡
2. 베이비빌리
3. MOMI

## 공식 일정/의료 연결
1. 예방접종도우미
2. 영유아 건강검진
3. 아이사랑

---

# 가장 중요한 결합 가설

하나의 강한 육아 시스템은 한 서비스를 복제해서 만들기보다 다음을 결합하는 편이 낫다.

```
BabyTime
빠른 기록/공동양육
+
Huckleberry/Napper
패턴/예측
+
MOMI
음성 AI 입력
+
Pathways/Kinedu
발달 관찰/활동
+
Solid Starts
객체 중심 이유식
+
FamilyAlbum
가족 권한/추억
+
KDCA/NHIS/아이사랑
한국 공식 건강·보육 체계
```

단, 홈에 모든 기능을 동시에 노출하면 안 된다.  
**주수·월령·현재 상태에 따라 필요한 모듈의 우선순위를 교체하는 orchestration layer**가 필요하다.
