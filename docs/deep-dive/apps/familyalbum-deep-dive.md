# FamilyAlbum Deep Dive — 구조·기능·문제 해결 방식

> 조사 기준일: 2026-11-08  
> 공식 근거: FamilyAlbum 공식 도움말, Premium 페이지

## 1. 서비스 한 문장

FamilyAlbum은 **아이 사진·영상을 가족 전용 공간에 모으고, 아기 연령 기반으로 자동 정리하며, 권한·회고영상·실물상품을 결합해 시간이 지날수록 가치가 커지게 만드는 성장 메모리 플랫폼**이다.

## 2. 핵심 문제

아이가 태어나면 미디어가 급증한다.

기존 방식:
```
부모 휴대폰
→ 카카오톡 전송
→ 조부모 저장
→ 다시 요청
→ 사진 중복/누락
```

FamilyAlbum:
```
Photo/Video Upload
→ Baby Album
→ Family Access
→ Automatic Age Organization
→ Comment/Reaction
→ Recap
→ Print/Product
```

핵심은 파일 저장이 아니라 **가족 단위의 아이 중심 workspace**다.

## 3. 전체 구조

```
Baby Album
├─ Media Timeline
│  ├─ Photos
│  └─ Videos
├─ Age/Month Auto Organization
├─ Visibility
│  ├─ Family
│  ├─ Admin only
│  └─ Premium custom groups
├─ Family Members
│  ├─ Admin
│  └─ Member
├─ Social Layer
│  ├─ Comments
│  ├─ Reactions
│  └─ View history
├─ Memory Automation
│  ├─ Seasonal 1-second movie
│  ├─ Monthly recap (premium)
│  └─ Annual recap (premium)
└─ Commerce
   ├─ Photo books
   ├─ Prints
   └─ DVDs etc.
```

## 4. 핵심 엔터티가 Account가 아니라 Album

일반 클라우드:
```
User
└─ Files
```

FamilyAlbum:
```
Album
├─ Admin A
├─ Admin B
├─ Member C
└─ Media
```

이 구조는 육아 앱에 매우 중요하다.

아이의 데이터가 특정 부모 한 명에게 종속되지 않고 **아이 단위 공간**에 묶인다.

## 5. 권한 시스템

공식 도움말에서 관리자와 멤버가 분리된다.

관리자:
- 가족 초대/해제
- 공개범위
- 업로드
- 편집/삭제
- 댓글 허용 제한
- 다운로드 허용 제한
- 프리미엄 관리

멤버:
- 관리자 설정 범위 내 열람
- 조건부 업로드/댓글/다운로드

웹 멤버는 권한이 더 제한적이다.

이것은 매우 좋은 **role + surface 기반 permission** 사례다.

## 6. 공개 범위 설계

무료:
- 가족 전원
- 관리자 한정

Premium:
- 친가/외가 등 더 세분화된 공개범위

이 설계는 중요한 제품적 통찰을 준다.

사진은 모두 같은 민감도가 아니다.

예:
- 일반 사진 → 전체 가족
- 산후/병원 사진 → 부모만
- 특정 친족 행사 → 선택 그룹

따라서 데이터 개체별 visibility를 지원해야 한다.

## 7. 연령 기반 자동 정리

[확인] 업로드된 사진·영상은 아기 연령에 맞춰 월별 자동 정리된다.

이것이 일반 사진앱과 큰 차이다.

```
촬영일
+
출생일
=
생후 N개월
```

육아 서비스에서 날짜는 두 좌표를 가진다.

- 절대시간: 2027-06-03
- 상대시간: 생후 5개월 12일

FamilyAlbum은 후자를 제품의 핵심 맥락으로 활용한다.

## 8. Memory Automation

1초 동영상은 업로드된 사진·영상 일부를 자동으로 연결해 생성된다.

무료:
- 계절 단위

Premium:
- 월간
- 연간

여기서 중요한 것은 영상편집 기능 자체가 아니다.

사용자가 추가 작업을 하지 않아도:
```
Accumulated Data
→ Automated Emotional Reward
```

가 발생한다.

기록 서비스의 가장 강력한 장기 리텐션 패턴 중 하나다.

## 9. 입력과 보상의 시간차

일반 tracking:
```
지금 입력
→ 지금 통계
```

FamilyAlbum:
```
매일 업로드
→ 몇 달 후 큰 감정적 보상
```

이 긴 시간차 때문에 데이터가 쌓일수록 서비스 전환비용과 애착이 커진다.

## 10. 무료와 유료의 경계

무료에서도:
- 무제한 업로드
- 기본 공개범위
- 계절 1초 동영상
- 댓글
- 포토북 제안

을 제공한다.

유료는:
- 긴 영상
- 공개범위 세분화
- 더 잦은 자동 회고
- 추가 편의

를 제공한다.

즉 core storage를 강하게 무료로 제공하고, **조직·권한·회고의 고급층**에서 과금한다.

## 11. Commerce 연결

FamilyAlbum의 커머스는 광고형 배너보다 구조적으로 자연스럽다.

```
이미 쌓인 미디어
→ 자동 선택/제안
→ 포토북/인화
```

사용자가 이미 가진 데이터를 물리적 결과물로 바꾸므로 전환 맥락이 좋다.

## 12. 강점

- 아이 중심 workspace
- 세밀한 가족 권한
- 자동 연령 정리
- 시간이 지날수록 가치 증가
- 자동 회고로 감정적 보상
- 자연스러운 실물 상품 연결

## 13. 구조적 한계

### 건강 데이터와는 분리
메모리 시스템으로는 강하지만 일상돌봄 상태 인계에는 적합하지 않다.

### 가족관계 변화
한 번 다운로드된 미디어는 권한 회수만으로 되돌릴 수 없다.

### 장기 개인정보
아동 사진이 수년간 축적되는 만큼 export/delete 정책이 매우 중요하다.

### 과도한 업로드 유도
자동 회고 품질이 업로드량에 비례하면 사용자가 모든 순간을 기록해야 한다는 압박을 느낄 수 있다.

## 14. 가져올 패턴

1. **Baby-centered Workspace**
2. **Role-based Family Permission**
3. **Per-item Visibility**
4. **Age-relative Media Timeline**
5. **Automatic Memory Reward**
6. **Data-to-Physical Product**
7. **Family-wide Subscription Benefit**

## 15. 통합 육아앱에 적용한다면

생활기록과 사진을 동일 권한으로 묶지 않는 것이 좋다.

```
Baby Workspace
├─ Care Data
│  └─ Parents/Caregivers
├─ Medical Data
│  └─ Parents only
└─ Memories
   └─ Extended Family
```

FamilyAlbum은 특히 이 **권한 모델**을 참고할 가치가 높다.

## 16. 근거

- https://help.family-album.com/hc/ko/articles/360038267214
- https://help.family-album.com/hc/ko/articles/4404247061529
- https://help.family-album.com/hc/ko/articles/360038852333
- https://family-album.com/ko/premium
- https://help.family-album.com/hc/ko/articles/4404344217113

## 결론

FamilyAlbum은 사진앱이 아니라 **가족 권한 + 연령 기반 정리 + 자동 회고**의 결합체다.

가장 배울 만한 구조는:

**Baby Workspace → Permission → Age Timeline → Automatic Memory Reward**

다.
