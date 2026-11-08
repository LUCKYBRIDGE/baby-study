# FamilyAlbum — 기술·권한·문제 해결 분석

## 1. 공개 기술 현황

내부 framework/DB는 공개 확인하지 못했다. [U]

그러나 제품 기능상 필요한 시스템 경계는 명확하다.

- Media storage
- Album membership
- Per-item visibility
- Automated organization
- Derived recap artifact
- Comment/reaction
- Commerce

## 2. 핵심 데이터 모델

[C]

```
Album
Member
├─ role
└─ permissions

MediaAsset
├─ captured_at
├─ uploaded_by
├─ visibility
└─ child_age_at_capture

Comment
Reaction

DerivedMemory
├─ source_asset_ids[]
├─ generated_at
└─ visibility
```

## 3. 얽힌 문제 — 가족 전체에게 보여주되 사생활 보호

모든 가족이 같은 권한이면 안 된다.

해법:
- Admin/Member 분리
- 콘텐츠별 visibility
- 기능별 permission

## 4. 얽힌 문제 — 수천 장을 누가 정리하나

수동 폴더 대신:
```
birth_date + captured_at
→ month/age organization
```

으로 자동화한다.

## 5. 얽힌 문제 — 저장만 하면 시간이 지나며 가치가 낮아짐

자동 회고가 이를 해결한다.

```
Accumulation
→ Selection
→ Recap
→ Emotional reward
```

## 6. Derived Artifact 문제

가장 중요한 기술/정책 이슈다.

원본이:
- 삭제
- visibility 변경

되어도 파생 영상이 자동으로 동일 처리되지 않을 수 있다.

우리 시스템에서는 derived artifact에:
- source lineage
- permission inheritance
- delete propagation

을 명시적으로 설계해야 한다.

## 7. 의료/일상 데이터와 결합할 경우

같은 Baby workspace 안에서도 권한은 분리해야 한다.

```
Baby Workspace
├─ Medical: parents only
├─ Care Log: caregivers
└─ Memories: extended family
```

FamilyAlbum의 permission 모델을 그대로 건강 데이터에 쓰는 것은 부족하다.

## 8. 수익모델 구조

Core sharing/storage는 강하게 무료로 제공하고:
- 고급 permission
- 더 잦은 recap
- 편의
- physical goods

에서 monetization한다.

## 9. 우리 시스템에 일반화할 패턴

- Baby-centered workspace
- Role-based Permission
- Per-item Visibility
- Age-relative Timeline
- Derived Artifact Lineage
- Automatic Memory Reward
