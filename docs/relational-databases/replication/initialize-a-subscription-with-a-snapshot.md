---
description: 새 게시를 위해 스냅샷으로 구독 초기화
title: 스냅샷으로 구독 초기화
ms.custom: ''
ms.date: 03/23/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 77a9ade2-cdc0-4ae9-a02d-6e29d7c2ada0
author: MashaMSFT
ms.author: mathoma
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 2936d9c53f3dd99bcd112de3743107128da25fc2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479924"
---
# <a name="initialize-a-subscription-with-a-snapshot-for-a-new-publication"></a>새 게시를 위해 스냅샷으로 구독 초기화

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

이 문서는 복제 게시가 초기화될 때 진행되는 프로세스에 대해 설명합니다. 초기 스냅샷이 구독자에 적용됩니다.

## <a name="snapshot-for-a-new-publication"></a>새 게시에 대한 스냅샷

기본적으로 스냅샷은 게시가 만들어진 후에 캡처됩니다.
스냅샷은 스냅샷 폴더로 복사됩니다. 이 기본 동작은 새 게시 마법사를 사용하여 생성된 병합 게시에 대해 이루어집니다.

### <a name="snapshot-is-applied-to-subscriber"></a>스냅샷이 구독자에 적용됨

새 스냅샷이 에이전트에 의해 구독자에 적용됩니다. 적용은 구독의 초기 동기화 중에 진행됩니다. 적용을 진행하는 에이전트는 게시 유형에 따라 달라집니다.

- ‘트랜잭션’ 및 ‘스냅샷’ 게시의 경우:
  - 배포 에이전트

- ‘병합’ 게시의 경우:
  - 병합 에이전트

### <a name="type-of-publication"></a>게시 유형

다음 표에서는 각 게시 유형에 대한 스냅샷의 내용을 보여 줍니다.

&nbsp;

| 스냅샷의 게시 유형 | 스냅샷의 내용 |
| :---------------------------------------- | :----------------------- |
| <ul> <li>스냅샷 게시</li> <li>트랜잭션 게시</li> <li>매개 변수가 있는 필터를 사용하지 않는 병합 게시</li> </ul> | <ul> <li>스키마</li> <li>BCP(대량 복사 프로그램)를 위한 파일에 있는 데이터</li> <li>제약 조건</li> <li>확장 속성</li> <li>인덱스</li> <li>트리거</li> <li>복제에 필요한 시스템 테이블</li> </ul> <br/>[스냅샷 만들기 및 적용](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하세요. |
| <ul> <li>매개 변수가 있는 필터를 사용하는 병합 게시</li> </ul> | <ul> <li>스키마 스냅샷(복제 스크립트, 게시된 개체, 단 데이터는 없음)</li> <li>구독의 파티션에 속하는 데이터</li> </ul> <br/>[매개 변수가 있는 필터를 사용하는 병합 게시의 스냅샷](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)을 참조하세요. |
| | |

#### <a name="two-part-process-with-merge-publication-that-uses-parameterized-filters"></a>매개 변수가 있는 필터를 사용하는 병합 게시의 2단계 프로세스

매개 변수가 있는 필터를 사용하는 병합 게시의 경우 스냅샷은 다음과 같은 2단계 프로세스를 통해 생성됩니다.

1. 다음 항목을 포함하는 스키마 스냅샷이 생성됩니다.
   - 복제 스크립트.
   - 게시된 개체의 스키마.
   - (단, 데이터는 없음)

2. 그런 다음, 각 구독이 스냅샷을 사용하여 초기화됩니다. 스냅샷에는 다음 항목이 포함됩니다.
   - 스키마 스냅샷에서 복사된 스키마 및 스크립트.
   - 구독의 파티션에 속하는 데이터.

## <a name="type-of-replication"></a>복제 유형

스냅샷에 포함되는 파일 형식은 복제 유형과 게시에 포함된 아티클에 따라 달라집니다.

&nbsp;

| 복제 유형 | 일반 스냅샷 파일 |
| :------------------ | :-------------------- |
| 스냅샷 복제 또는<br/>트랜잭션 복제 | &bullet; 스키마(.sch) <br/>&bullet; 데이터(.bcp) <br/>&bullet; 제약 조건 및 인덱스(.dri) <br/>&bullet; 압축된 스냅샷 파일(.cab) <br/>&bullet; 트리거(. 태그), 구독자 업데이트 전용 <br/><br/>&bullet; 제약 조건(idx). |
| 병합 복제                                      | &bullet; 스키마(.sch) <br/>&bullet; 데이터(.bcp) <br/>&bullet; 제약 조건 및 인덱스(.dri) <br/>&bullet; 압축된 스냅샷 파일(.cab) <br/>&bullet; 트리거(.trg) <br/><br/>&bullet; 시스템 테이블 데이터(.sys) <br/>&bullet; 충돌 테이블(.cft) |
| | |

### <a name="snapshot-folder"></a>스냅샷 폴더

파일은 기본 ‘스냅샷 폴더’에 복사되거나 스냅샷을 위한 ‘대체 폴더’에 복사됨으로써 전송됩니다.

스냅샷 폴더는 배포자가 구성될 때 지정됩니다. 대체 폴더는 게시가 생성될 때 지정됩니다.

### <a name="resume-transfer-after-interruption"></a>중단 후 전송 재개

불안정한 연결에 의해 스냅샷 폴더로의 파일 전송이 중단된 경우 자동으로 재개됩니다.

효율성을 높이기 위해, 재개 과정에서는 중단 전에 완전히 전송된 파일이 다시 전송되지 않습니다.

## <a name="snapshot-options"></a>Snapshot Options

스냅샷으로 구독을 초기화할 때 사용할 수 있는 몇 가지 옵션이 있습니다. 다음을 수행할 수 있습니다.

- 기본 스냅샷 폴더 위치 대신 또는 기본 스냅샷 폴더 위치에 추가로 대체 스냅샷 폴더 위치를 지정합니다. 자세한 내용은 [스냅샷 옵션 수정](../../relational-databases/replication/snapshot-options.md)을 참조하세요.

- 이동식 미디어에 스토리지하거나 느린 네트워크를 통해 전송하기 위해 스냅샷을 압축합니다. 자세한 내용은 [Compressed Snapshots](../../relational-databases/replication/snapshot-options.md#compressed-snapshots)을 참조하세요.

- 스냅샷 적용 전후에 Transact-SQL 스크립트를 실행합니다. 자세한 내용은 [스냅샷 적용 전후에 스크립트 실행](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)을 참조하세요.

- FTP(파일 전송 프로토콜)를 사용하여 스냅샷 파일을 전송합니다. 자세한 내용은 [FTP를 통해 스냅샷 전송](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)을 참조하세요.

## <a name="see-also"></a>참고 항목

[구독 초기화](../../relational-databases/replication/initialize-a-subscription.md)

[스냅샷 폴더 보안 설정](../../relational-databases/replication/security/secure-the-snapshot-folder.md)
