# FamilyAlbum — 서비스 정본 분석

> 유형: 가족 사진·영상 공유 / 성장 아카이브 / 자동 회고  
> 공개 제품코드: 확인 못함 [U]  
> 직접 검증: 공식 도움말·Premium [A1/A2]

## 1. 서비스 정의

FamilyAlbum은 **아이를 중심으로 가족 멤버를 연결하고, 사진·영상을 생후 월령 기준으로 자동 정리하며, 권한과 자동 회고를 붙여 시간이 지날수록 가치가 커지는 가족 메모리 플랫폼**이다.

## 2. 핵심 구조

```
Album / Child Space
├─ Media
├─ Admin / Member
├─ Visibility
├─ Comment / Reaction
├─ Memories
│  ├─ 1s Movie
│  └─ recap
└─ Physical Products
```

## 3. 공개 파일/폴더 구조

공식 제품 소스코드는 확인하지 못했다.

동명/관련 downloader·mirror 저장소는 제품 공식 코드로 간주하지 않는다.

## 4. 핵심 엔터티

가장 중요한 엔터티는 User보다 Album이다.

```
Album
├─ Admin
├─ App Member
├─ Browser Member
└─ Media
```

## 5. 권한

[A2]

관리자와 멤버는:
- 초대
- 업로드
- 삭제/수정
- 댓글
- 다운로드
- 공개범위
- 1초 동영상

권한이 다르다.

## 6. 핵심 데이터 흐름

```
Media Upload
→ captured_at + birth_date
→ age-relative organization
→ family interaction
→ automated recap
→ optional print/product
```

## 7. 가장 잘 푼 문제

- 가족 단톡방의 중복/누락
- 부모 한 명에게 사진이 종속되는 문제
- 수천 장의 사진 정리 문제
- 시간이 지나면 기록의 감정가치가 떨어지는 문제

## 8. 구조적 핵심

**Automatic Memory Reward**

사용자가 추가 입력을 하지 않아도 쌓인 데이터가 나중에 회고영상으로 돌아온다.

## 9. 위험

- 아동 사진의 장기 개인정보
- 이미 다운로드된 파일은 권한회수 불가
- 파생영상과 원본 권한의 불일치
- 가족관계 변화

## 10. 관련 문서

- [화면·UI·UX](surface-map.md)
- [기술·권한·파생데이터](system-analysis.md)
- [직접 관찰](../../direct-inspection/apps/familyalbum-site.md)
