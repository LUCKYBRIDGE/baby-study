# FamilyAlbum — 공식 도움말 직접 관찰

> 관찰일: 2026-11-08  
> 근거: FamilyAlbum 공식 도움말/프리미엄 안내  
> 레벨: A1/A2

## 1. 실제 서비스 구조

FamilyAlbum은 단순 사진 업로드 서비스가 아니라 다음 네 층으로 구성됩니다.

```
Baby Album
├─ Media archive
├─ Family permission
├─ Social interaction
└─ Memory generation
```

이 구조 위에 포토북·인화 등 실물 상품이 연결됩니다.

## 2. 실제 권한 모델

공식 도움말에서 실제 역할은 단순 "가족" 하나가 아닙니다.

- **Album Admin**
- **Member (앱 사용자)**
- **Member (브라우저 사용자)**

관리자는 다음과 같은 운영 권한을 가집니다.
- 가족 초대/연결 해제
- 공개 범위 설정
- 업로드/편집/삭제
- 댓글 제한
- 다운로드 제한
- 일부 프리미엄 관리

즉 FamilyAlbum의 핵심 엔터티는 특정 부모 계정이 아니라:

```
Album
├─ Admin
├─ Member
└─ Media
```

에 가깝습니다.

## 3. 콘텐츠별 공개 범위

기본적으로 미디어 공개범위가 존재하고, 관리자용/가족용 노출이 분리됩니다.

프리미엄에서는 더 세밀한 그룹별 공유가 가능합니다.

이 방식에서 배울 점:
- 가족 구성원이 모두 같은 권한일 필요 없음
- **사진 단위 visibility**가 존재해야 함
- 건강 기록과 가족 사진은 동일 permission group을 쓰면 안 됨

## 4. 생후 월령 자동 정리

공식 설명에서 촬영된 사진·영상은 아기 나이에 맞춰 월별로 자동 정리됩니다.

즉 사용자가 직접 폴더를 만들지 않아도:

```
captured_at
+
birth_date
→ age-relative bucket
```

으로 변환됩니다.

육아 서비스에서 절대 날짜보다 "생후 몇 개월"이 더 의미 있는 맥락이 될 수 있다는 좋은 사례입니다.

## 5. 1초 동영상 생성 방식

공식 도움말을 직접 보면 1초 동영상은 단순 랜덤 조합이 아닙니다.

선정 과정에서:
- 공개범위
- 사람/얼굴
- 댓글 등 반응
- 기간 전체의 균형

등을 고려한다고 설명합니다.

즉 자동 회고는:

```
Stored Media
→ Scoring/Selection
→ Balanced recap
```

형태의 recommendation system에 가깝습니다.

## 6. 매우 중요한 개인정보 관찰

공식 도움말상 **이미 생성된 1초 동영상은 원본 사진을 삭제하거나 공개범위를 변경해도 자동 삭제되지 않을 수 있습니다.**

이것은 중요한 설계 이슈입니다.

```
Source Asset
→ Derived Artifact
```

이 만들어졌다면, 원본의 권한 변경을 파생 결과물에 어떻게 전파할지 명시적으로 설계해야 합니다.

통합 육아앱에서는 다음 정책이 필요합니다.
- 원본 삭제 시 생성 영상 처리
- 권한 변경 시 기존 recap 재처리
- 다운로드된 복사본 통제 불가 안내
- derived asset provenance

## 7. Memories 탭

2026년 공식 도움말에서는 Memories 관련 경험이 별도 탭으로 확장되어:
- 과거의 오늘
- 1초 동영상
- 성장 회고 콘텐츠

를 묶습니다.

이것은 저장소와 회고를 다른 화면으로 분리한 좋은 구조입니다.

```
Archive = 찾기
Memories = 다시 느끼기
```

## 8. 무료/유료 경계

무료에서도 강한 core value를 제공합니다.
- 사진/영상 업로드
- 가족 공유
- 자동 정리
- 기본 1초 동영상

유료는:
- 더 긴 영상
- 더 자주 생성되는 회고
- 세밀한 공개범위
- 추가 편의

등 **권한/자동화/회고의 고급 기능**에 배치됩니다.

## 9. 직접 관찰로 얻은 핵심 시사점

FamilyAlbum에서 가장 참고할 부분은 UI가 아니라:

1. Baby-centered workspace
2. Role-based permission
3. Per-item visibility
4. Age-relative organization
5. Derived memory artifact
6. Derived artifact privacy policy

입니다.

특히 5~6번은 기존 분석에서 놓치기 쉬운 부분입니다.

## 10. 참고

- https://help.family-album.com/
- https://family-album.com/ko/premium
