---
title: 트랜잭션 게시 (SQL Server Management Studio)에 대 한 데이터 충돌 보기 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- queued updating subscriptions [SQL Server replication]
- viewing conflict information
ms.assetid: 9977dd75-b0de-4376-9c13-86d80567d8aa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e046351ca3dc7977691fc98e24453ccbf8e6af53
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63144414"
---
# <a name="view-data-conflicts-for-transactional-publications-sql-server-management-studio"></a>트랜잭션 게시의 데이터 충돌 확인(SQL Server Management Studio)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 복제 충돌 뷰어에서 피어 투 피어 트랜잭션 복제와 지연 업데이트 구독이 포함된 트랜잭션 복제의 충돌을 볼 수 있습니다. 충돌 감지 및 해결 방법은 [피어 투 피어 복제에서 충돌 검색](transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md) 및 [지연 업데이트 충돌 해결 옵션 설정&#40;SQL Server Management Studio&#41;](publish/create-an-updatable-subscription-to-a-transactional-publication.md)을 참조하세요.  
  
 충돌 데이터의 가용성은 복제 유형 및 충돌 보존 기간에 따라 달라집니다.  
  
-   피어 투 피어 복제의 경우 충돌이 감지되면 기본적으로 배포 에이전트가 실패합니다. 오류 로그에 충돌 오류가 기록되지만 충돌 테이블에는 충돌 데이터가 기록되지 않으므로 해당 데이터를 볼 수 없습니다. 배포 에이전트가 계속할 수 있으면 충돌이 감지된 각 노드에 로컬로 충돌이 기록됩니다. 자세한 내용은 [Conflict Detection in Peer-to-Peer Replication](transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)의 "충돌 처리"를 참조하십시오.  
  
-   지연 업데이트 구독의 경우 모든 충돌에 대한 데이터를 볼 수 있습니다. 지정된 충돌 보존 기간(기본값: 14일) 동안 복제 충돌 뷰어에서 충돌 데이터를 확인할 수 있습니다. 충돌 보존 기간을 설정하려면 다음 중 하나를 수행합니다.  
  
    -   @conflict_retention sp_addpublication [의](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)매개 변수에 보존 값을 지정합니다.  
  
    -   값을 지정 `'conflict_retention'` 에 대 한는 @property 매개 변수 및 보존 기간에 대 한 값을 @value 의 매개 변수 [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)합니다.  
  
### <a name="to-view-conflicts"></a>충돌을 보려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 해당 서버에 연결한 후 다음과 같은 서버 노드를 확장합니다.  
  
    -   피어 투 피어 복제의 경우 충돌이 발생한 노드입니다.  
  
    -   지연 업데이트 구독의 경우 게시자입니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  충돌을 확인할 게시를 마우스 오른쪽 단추로 클릭한 다음 **충돌 보기**를 클릭합니다.  
  
4.  **충돌 테이블 선택** 대화 상자에서 충돌을 확인하려는 데이터베이스, 게시 및 테이블을 선택합니다.  
  
5.  복제 충돌 뷰어에서 다음을 수행할 수 있습니다.  
  
    -   상단 표 오른쪽의 단추를 사용하여 행을 필터링합니다.  
  
    -   상단 표에서 행을 선택하여 해당 행에 대한 정보를 하단 표에 표시합니다.  
  
    -   상단 표에서 행을 하나 이상 선택한 다음 **제거**를 클릭하여 충돌 메타데이터 테이블에서 행을 제거합니다.  
  
    -   속성 단추(**...**)를 클릭하여 충돌과 관련된 열에 대한 자세한 정보를 확인합니다.  
  
    -   **이 충돌 정보 기록** 을 선택하여 충돌 데이터를 파일에 기록합니다. 파일의 위치를 지정하려면 **보기** 메뉴를 가리킨 다음 **옵션**을 클릭합니다. 값을 입력하거나 찾아보기 단추 (**...**)를 클릭한 다음 해당 파일을 검색합니다. **확인** 을 클릭하여 **옵션** 대화 상자를 닫습니다.  
  
6.  복제 충돌 뷰어를 닫습니다.  
  
## <a name="see-also"></a>관련 항목  
 [피어 투 피어 트랜잭션 복제](transactional/peer-to-peer-transactional-replication.md)   
 [Queued Updating Conflict Detection and Resolution](transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)  
  
  
