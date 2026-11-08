# FamilyAlbum — 페이지·UI·UX·버튼 지도

## 1. 핵심 화면군

공식 도움말로 확인 가능한 개념적 화면군:

```
Album
├─ Timeline / media
├─ Memories
├─ Family Members / Settings
├─ Upload
└─ Premium / Products
```

## 2. Upload

핵심 action:
- 사진 업로드
- 영상 업로드
- 공개범위 선택

공개범위가 업로드 후 사후설정이 아니라 **콘텐츠 생성 행위와 가까운 위치**에 있는 것이 중요하다.

## 3. Album timeline

자동으로 생후 월령 기준 정리된다.

사용자는:
- 폴더 만들기
- 월별 분류
- 날짜 순서 조정

같은 관리 작업을 덜 하게 된다.

## 4. Family Members

[A2]

역할:
- Album Admin
- App Member
- Browser Member

관리자가 조정하는 대표 행동:
- 초대/해제
- 멤버 upload 허용
- comment 허용
- download 허용

이 화면은 단순 연락처가 아니라 **permission console**이다.

## 5. Visibility

기본적으로:
- 가족 전체
- 관리자만

같은 공개범위가 존재한다.

유료에서는 더 세밀한 그룹이 가능하다.

## 6. Memories

Archive와 Memories는 목적이 다르다.

```
Archive
= 찾기/보관

Memories
= 다시 보기/감정적 보상
```

1초 동영상 같은 자동 생성 결과는 후자에 배치된다.

## 7. Product/Print

이미 쌓인 사진을 다시 고르는 수고를 줄여:
`stored media → physical product`

로 이어지는 자연스러운 commerce UX가 가능하다.

## 8. UX 강점

- 업로드 자체가 쉬움
- 가족에게 별도 재전송 불필요
- 월령 자동정리
- 자동 회고
- 역할별 기능 차등

## 9. UX에서 특히 주의할 점

파생영상의 source media가 나중에 삭제/비공개 처리될 때 사용자가 "당연히 같이 사라질 것"이라 예상할 수 있다.

따라서 파생 결과물에는:
- 생성 출처
- 권한
- 삭제정책

을 명확히 보여주는 것이 더 낫다.

## 10. 미확인

- 현재 최신 네이티브 tab exact 구조
- 대량 업로드 실패/재시도 UX
- offline upload queue
- 얼굴인식/선별 모델의 구체 UI
