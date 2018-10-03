---
title: 지연 업데이트 충돌 감지 및 해결 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- viewing queued updating conflicts
- conflict resolution [SQL Server replication]
- queued updating subscriptions [SQL Server replication]
- articles [SQL Server replication], conflict resolution
ms.assetid: 084ac587-25e7-4bd0-a385-556bbe07d02f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 46d54056a60b2059bed038ddb8de3c83941ff38c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48085644"
---
# <a name="queued-updating-conflict-detection-and-resolution"></a>Queued Updating Conflict Detection and Resolution
  지연 업데이트 구독으로 여러 위치에서 같은 데이터를 수정할 수 있기 때문에 데이터를 게시자에 동기화할 때 충돌이 발생할 수 있습니다. 복제는 변경 내용이 게시자와 동기화될 때 충돌을 감지하고 게시를 만들 때 선택한 해결 정책을 사용하여 이러한 충돌을 해결합니다. 다음과 같은 두 가지 충돌이 일어날 수 있습니다.  
  
-   업데이트 및 삽입 충돌. 이러한 충돌은 같은 데이터를 두 위치에서 변경할 때 발생합니다. 이 경우 한 가지 변경 내용만 적용됩니다.  
  
-   삭제 충돌. 삭제 충돌은 한 위치에서 행을 삭제하고 다른 위치에서 같은 행을 변경할 때 발생합니다.  
  
 충돌 감지와 해결에는 많은 시간과 리소스가 필요하기 때문에 각 구독자가 서로 다른 데이터 하위 집합을 수정하도록 데이터 파티션을 만들어 응용 프로그램에서 충돌을 최소화하는 것이 좋습니다.  
  
## <a name="detecting-conflicts"></a>충돌 감지  
 게시를 만들고 지연 업데이트를 설정하면 복제는 기본 테이블에 기본값이 **newid()** 인**uniqueidentifier**열( **msrepl_tran_version** )을 추가합니다. 게시자 또는 구독자에서 게시된 데이터가 변경되면 행은 새로운 GUID(Globally Unique Identifier)를 받아 새로운 행 버전이 있음을 표시합니다. 큐 판독기 에이전트는 충돌이 있는지 확인하기 위해 동기화 중 이 열을 사용합니다.  
  
 큐에서 트랜잭션은 이전 행 버전 값과 새로운 행 버전 값을 유지합니다. 게시자에서 트랜잭션이 적용되면 트랜잭션에서의 GUID와 게시에 있는 GUID가 비교됩니다. 트랜잭션에 저장된 이전 GUID가 게시에 있는 GUID와 일치하면 게시는 업데이트되고 구독자가 생성한 새 GUID를 행에 할당합니다. 트랜잭션에서 GUID와 함께 게시를 업데이트하면 게시 및 트랜잭션에 일치하는 행 버전을 갖게 됩니다.  
  
 트랜잭션에 저장된 이전 GUID가 게시에 있는 GUID와 일치하지 않으면 충돌이 감지됩니다. 게시에 있는 새 GUID는 두 개의 다른 행 버전이 있음을 표시하는데 이 중 하나는 구독자가 제출하는 트랜잭션에 있고 최근의 다른 하나는 게시자에 존재합니다. 이 경우 구독자 트랜잭션을 동기화하기 전 다른 구독자 또는 게시자가 게시에서 같은 행을 업데이트한 것입니다.  
  
 병합 복제와 달리 GUID는 행 자체를 식별하는 데 사용되지 않고 행이 변경되었는지를 검사하는 데 사용됩니다.  
  
## <a name="resolving-conflicts"></a>충돌 해결  
 지연 업데이트를 사용하여 게시를 만드는 경우 충돌이 감지되면 사용할 충돌 해결 프로그램을 선택합니다. 충돌 해결 프로그램은 큐 판독기 에이전트에서 동기화 중에 발생한 동일한 행의 여러 버전을 처리하는 방법을 제어합니다. 게시에 대한 구독이 없을 경우에 한해서 게시를 만든 후 충돌 해결 정책을 변경할 수 있습니다. 다음의 충돌 해결 프로그램을 선택할 수 있습니다.  
  
-   게시자 내용 적용(기본값)  
  
-   게시자 내용을 적용하고 구독을 다시 초기화  
  
-   구독자 내용 적용  
  
 충돌을 기록하고 충돌 뷰어를 사용해서 볼 수 있습니다.  
  
 **지연 업데이트 충돌 해결 정책을 설정하려면**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [지연 업데이트 충돌 해결 옵션 설정&#40;SQL Server Management Studio&#41;](../publish/set-queued-updating-conflict-resolution-options-sql-server-management-studio.md)  
  
-   복제 Transact-SQL 프로그래밍: [트랜잭션 게시에 대해 업데이트할 수 있는 구독 설정](../publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
 **데이터 충돌을 보려면**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [트랜잭션 게시의 데이터 충돌 확인&#40;SQL Server Management Studio&#41;](../view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
### <a name="publisher-wins"></a>게시자 내용 적용  
 충돌 해결 시 게시자 내용이 적용되도록 설정하면 게시자에 있는 데이터를 기준으로 트랜잭션 일관성을 유지 관리합니다. 충돌 트랜잭션은 트랜잭션을 처음에 초기화한 구독자로 롤백됩니다.  
  
 큐 판독기 에이전트가 충돌을 감지하고 보상 명령이 생성되며 배포 데이터베이스에서 게시함으로써 생성된 보상 명령을 구독자로 전파합니다. 그 다음 배포 에이전트는 보상 명령을 충돌 트랜잭션이 시작된 구독자에 적용합니다. 보정 동작은 게시자에 있는 행과 일치하도록 구독자에서 행을 업데이트합니다.  
  
 보상 명령이 적용될 때까지 실행하여 구독자에서 롤백할 트랜잭션 결과를 읽을 수 있습니다. 이는 커밋되지 않은 데이터 읽기(커밋되지 않은 격리 수준 읽기)에 해당합니다. 발생할 수 있는 후속 종속 트랜잭션에 대해서는 보상이 없습니다. 그러나 트랜잭션 경계는 유지되고 트랜잭션의 모든 동작은 커밋되거나 충돌이 있을 경우 롤백됩니다.  
  
### <a name="publisher-wins-and-the-subscription-is-reinitialized"></a>게시자 내용을 적용하고 구독을 다시 초기화  
 구독자를 다시 초기화하여 충돌을 해결하면 구독자에서 엄격한 트랜잭션 일관성이 유지되지만 게시에 많은 양의 데이터가 포함되어 있을 경우 시간이 오래 걸릴 수 있습니다.  
  
 큐 판독기 에이전트가 충돌을 감지하면 큐에 남은 모든 트랜잭션(충돌한 트랜잭션을 포함)은 거부되고 구독자는 다시 초기화하도록 표시됩니다. 배포 에이전트는 게시에 대해 생성된 다음 스냅숏을 구독자에 적용합니다.  
  
### <a name="subscriber-wins"></a>구독자 내용 적용  
 구독자 변경 내용 적용 정책에서 충돌 감지는 게시자 변경 내용 적용 항목을 업데이트하는 마지막 구독자 트랜잭션을 의미합니다. 이 경우 충돌이 감지되면 구독자가 보낸 트랜잭션이 계속 사용되고 게시자가 업데이트됩니다. 이 정책은 이러한 변경 내용이 데이터 무결성을 손상하지 않은 응용 프로그램에 적합합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Updatable Subscriptions for Transactional Replication](updatable-subscriptions-for-transactional-replication.md)  
  
  
