# 임신육아종합포털 아이사랑 — 서비스 정본 분석

> 유형: 공공 육아정보 / 보육행정 / 어린이집 / 상담  
> 운영: 대한민국 공공서비스  
> 직접 검증: 공식 포털 월령별 육아 페이지 [A1]

## 1. 서비스 정의

아이사랑은 **월령별 육아정보와 어린이집 탐색·보육료·가정통신문·상담 같은 보육행정을 한 포털에서 제공하는 국가 육아 인프라**다.

## 2. 두 제품층

```
Parenting Knowledge
+
Childcare Administration
```

### Parenting Knowledge
- 성장발달
- 관계와 소통
- 행동
- 안전
- 수유
- 배설
- 수면
- 건강과 일상
- 놀이와 학습

### Administration
- 어린이집 검색
- 보육 관련 신청/지원
- 보육료
- 가정통신문
- 상담

## 3. 핵심 구조

월령이 바뀌어도 상위 taxonomy는 안정적으로 유지되고 콘텐츠만 교체된다.

```
Stable Domain Taxonomy
+
Age-specific Content
```

## 4. 공개 파일/폴더 구조

공공 포털의 내부 소스/서버 구조는 분석 대상 공개 저장소로 확인하지 않았다. [U]

대신 실제 URL/menu hierarchy를 제품 구조로 기록한다.

## 5. 가장 잘 푼 문제

민간 앱이 놓치기 쉬운 육아영역을 광범위하게 커버하고, 아이가 커진 뒤에는 **가정 돌봄 → 보육기관 이용**으로 사용자 과업이 전환되는 것까지 포함한다.

## 6. 구조적 한계

- 메뉴 규모가 크고 정보밀도가 높음
- 개인화된 daily action은 약함
- 생활기록과 직접 연결되지 않음
- 행정과 육아정보가 별도 제품처럼 느껴질 수 있음

## 7. 참고할 패턴

- Stable Age Taxonomy
- Official Provenance
- Institution Transition
- Public Transaction
- Broad Coverage Checklist

## 8. 관련 문서

- [페이지·UI·UX](surface-map.md)
- [기술·정보구조·문제 해결](system-analysis.md)
- [공공 시스템 직접 관찰](../../direct-inspection/web/korea-public-systems.md)
