---
title: 스냅숏으로 구독 초기화 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 77a9ade2-cdc0-4ae9-a02d-6e29d7c2ada0
caps.latest.revision: 31
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 3149d667a2f84aa24bd5ecd061959144abc95968
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36182788"
---
# <a name="initialize-a-subscription-with-a-snapshot"></a>스냅숏으로 구독 초기화
  게시가 생성된 후 일반적으로 초기 스냅숏이 생성되어 스냅숏 폴더로 복사됩니다. 이 작업은 새 게시 마법사에서 만든 병합 게시에 대해 기본적으로 수행됩니다. 스냅숏은 그런 다음 구독의 초기 동기화 중 배포 에이전트(트랜잭션 및 스냅숏 게시의 경우) 또는 병합 에이전트(병합 게시의 경우)에 의해 구독자에 적용됩니다. 스냅숏 프로세스는 게시 유형에 따라 달라집니다.  
  
-   스냅숏이 스냅숏 게시, 트랜잭션 게시 또는 매개 변수가 있는 필터를 사용하지 않는 병합 게시용인 경우 스냅숏에는 제약 조건, 확장 속성, 인덱스, 트리거 및 복제에 필요한 시스템 테이블뿐만 아니라 스키마 및 데이터가 bcp(대량 복사 프로그램) 파일로 포함됩니다. 스냅숏을 만들고 적용하는 방법은 [스냅숏 만들기 및 적용](create-and-apply-the-snapshot.md)을 참조하세요.  
  
-   스냅숏이 매개 변수가 있는 필터를 사용하는 병합 게시용인 경우 2단계 프로세스를 통해 스냅숏이 생성됩니다. 먼저 게시된 개체의 데이터를 제외하고 복제 스크립트와 스키마를 포함하는 스키마 스냅숏이 생성됩니다. 그런 후 스키마 스냅숏에서 복사된 스크립트 및 스키마를 포함하는 스냅숏과 구독의 파티션에 속해 있는 데이터를 사용하여 구독이 초기화됩니다. 자세한 내용은 [Snapshots for Merge Publications with Parameterized Filters](snapshots-for-merge-publications-with-parameterized-filters.md)을 참조하세요.  
  
 스냅숏을 구성하는 파일은 복제 유형과 게시의 아티클에 따라 달라집니다. 이러한 파일은 배포자를 구성할 때 지정한 기본 스냅숏 폴더나 게시를 만들 때 지정한 대체 스냅숏 폴더에 복사됩니다.  
  
|복제 유형|일반 스냅숏 파일|  
|-------------------------|---------------------------|  
|스냅숏 복제 또는 트랜잭션 복제|스키마(.sch), 데이터(.bcp), 제약 조건 및 인덱스(.dri), 제약 조건(.idx), 트리거(.trg)(구독자 업데이트 전용), 압축 스냅숏 파일(.cab)|  
|병합 복제|스키마(.sch), 데이터(.bcp), 제약 조건 및 인덱스(.dri), 트리거(.trg), 시스템 테이블 데이터(.sys), 충돌 테이블(.cft), 압축 스냅숏 파일(.cab)|  
  
 특정 시점에서 중단된 스냅숏 전송은 자동으로 재개되며 전송이 이미 완료된 파일은 다시 보내지 않습니다. 스냅숏 에이전트의 배달 단위는 각 게시 아티클에 대한 bcp 파일이므로 부분적으로 배달된 파일은 완전히 다시 배달되어야 합니다. 그러나 스냅숏 배달을 재개하면 전송되는 데이터 양이 크게 줄어들 수 있으므로 연결이 불안한 경우에도 스냅숏이 늦지 않게 배달될 수 있습니다.  
  
## <a name="snapshot-options"></a>스냅숏 옵션  
 스냅숏으로 구독을 초기화할 때 사용할 수 있는 옵션에는 여러 가지가 있습니다. 다음 작업을 수행할 수 있습니다.  
  
-   기본 스냅숏 폴더 위치 대신 또는 기본 스냅숏 폴더 위치에 추가로 대체 스냅숏 폴더 위치를 지정합니다. 자세한 내용은 [Alternate Snapshot Folder Locations](alternate-snapshot-folder-locations.md)을 참조하세요.  
  
-   이동식 미디어에 저장하거나 느린 네트워크를 통해 전송하기 위해 스냅숏을 압축합니다. 자세한 내용은 [Compressed Snapshots](compressed-snapshots.md)을 참조하세요.  
  
-   스냅숏 적용 전후에 Transact-SQL 스크립트를 실행합니다. 자세한 내용은 [스냅숏 적용 전후에 스크립트 실행](execute-scripts-before-and-after-the-snapshot-is-applied.md)을 참조하세요.  
  
-   FTP(파일 전송 프로토콜)를 사용하여 스냅숏 파일을 전송합니다. 자세한 내용은 [FTP를 통해 스냅숏 전송](transfer-snapshots-through-ftp.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [구독 초기화](initialize-a-subscription.md)   
 [스냅숏 폴더 보안 설정](security/secure-the-snapshot-folder.md)  
  
  