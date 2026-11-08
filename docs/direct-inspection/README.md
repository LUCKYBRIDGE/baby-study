# Direct Inspection Index

이 폴더는 **공식 사이트·공식 FAQ·공식 앱스토어 페이지를 직접 열어 확인한 내용**과, 공개 GitHub 저장소가 있는 경우 **실제 파일·코드 구조를 읽어 확인한 내용**을 정리합니다.

기존 `docs/deep-dive/`가 제품 구조를 해석한 문서라면, 이 폴더는 그 해석의 근거가 되는 **관찰 기록(evidence notes)**에 가깝습니다.

## 근거 레벨

- **A1 — 공식 제품 사이트에서 직접 확인**
- **A2 — 공식 FAQ/도움말에서 직접 확인**
- **A3 — 공식 앱스토어/Play Store에서 직접 확인**
- **B1 — 공개 GitHub 저장소 코드에서 확인**
- **B2 — 공개 서드파티 저장소에서 확인한 비공식 구현**
- **C — 제품적 추론**

B1/B2는 공식 앱 내부구조의 공식 문서가 아닙니다. 특히 Huckleberry 관련 공개 API 저장소는 **비공식 reverse-engineered client**이므로, 내부 구현을 확정적으로 단정하지 않고 "공개 코드상 관찰"로만 사용합니다.

## 앱/서비스

- [BabyTime](apps/babytime-site.md)
- [Huckleberry](apps/huckleberry-site-and-public-repos.md)
- [Kinedu](apps/kinedu-site.md)
- [Pathways.org](apps/pathways-site.md)
- [FamilyAlbum](apps/familyalbum-site.md)
- [Solid Starts](apps/solid-starts-site.md)
- [베이비빌리](apps/babybilly-site.md)
- [마미톡](apps/mommytalk-site.md)
- [MOMI](apps/momi-store.md)

## 공공 시스템

- [대한민국 공공 육아·건강 시스템](web/korea-public-systems.md)

## 공개 저장소

- [Huckleberry 공개 서드파티 생태계](repositories/huckleberry-public-ecosystem.md)
- [공개 저장소 확인 현황](repositories/repository-availability.md)

## 분석 방법

각 사이트에서 다음을 실제로 따라갑니다.

1. 최상위 내비게이션
2. 첫 화면이 무엇을 우선하는지
3. 기능이 어떤 탭/카테고리로 분리되는지
4. 기록이 생성되는 단계
5. 기록 후 어떤 화면으로 되돌아오는지
6. 다자녀/공동양육 구조
7. 통계/리포트의 시간 단위
8. 무료/유료 경계
9. 의료·발달 정보의 출처/면책
10. 공개 저장소가 있으면 실제 데이터 path와 type

## 현재 가장 중요한 직접 관찰 결론

### BabyTime
실제 FAQ 기준으로 **아이콘 1회 탭 시 기록이 즉시 생성**되고, 상세는 생성된 항목을 다시 열어 수정합니다. 기록 화면, 패턴, 통계, 커뮤니티, 프로필이 명확히 분리됩니다.

### Huckleberry
공식 사이트상 무료는 tracking/reporting, Plus는 prediction/AI logging/lock-screen, Premium은 Berry/개인화 수면계획으로 계층화됩니다. 비공식 공개 코드에서는 child별 Firestore collection 구조와 실시간 listener 패턴이 확인됩니다.

### Kinedu
실제 Assessment 웹페이지는 가입 전에 3문항 미리보기를 제공하고, 실제 평가가 32문항·5분 미만이며, 조산아 교정연령과 '진단 아님'을 UI에 반복 노출합니다.

### Pathways
실제 웹 IA가 `Today / Play / Track / Explore`로 구성되고 Track 아래에 Milestone, Tummy Timer, Diaper, Feeding을 함께 둡니다. 즉 콘텐츠 사이트라기보다 tracking + developmental guidance product에 가깝습니다.

### FamilyAlbum
권한 모델이 관리자/앱 멤버/웹 멤버로 실제 분리되어 있고, 1초 동영상 생성도 공개범위·인물·댓글 등 여러 요소를 반영합니다.

### Solid Starts
실제 제품 페이지에서 `0–4 / 5–6 / 7–9 / 10–12 / 12+` 월령 단계가 제품 레벨로 드러나며, 음식 DB→알레르기→첫 100 음식→개인화 meal plan이 하나의 흐름으로 배치됩니다.
