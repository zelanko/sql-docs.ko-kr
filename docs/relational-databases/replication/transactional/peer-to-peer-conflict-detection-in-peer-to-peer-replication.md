---
title: "피어 투 피어 복제에서 충돌 검색 | Microsoft 문서"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactional replication, peer-to-peer replication
- peer-to-peer transactional replication, conflict detection
ms.assetid: 754a1070-59bc-438d-998b-97fdd77d45ca
caps.latest.revision: "18"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0d27cca1b3e5a35dfcf405b8f10cd0e099e2a756
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="peer-to-peer---conflict-detection-in-peer-to-peer-replication"></a>피어 투 피어 - 피어 투 피어 복제에서 충돌 검색
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 피어 투 피어 트랜잭션 복제를 사용하면 토폴로지의 모든 노드에서 데이터를 삽입, 업데이트 및 삭제하고 데이터 변경 내용을 다른 노드로 전파할 수 있습니다. 모든 노드에서 데이터를 변경할 수 있으므로 각 노드에서의 변경이 서로 충돌할 수 있습니다. 두 개 이상의 노드에서 행이 수정되면 이 행이 다른 노드에 전파될 때 충돌이 발생하거나 업데이트가 손실될 수 있습니다.  
  
 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 이상 버전의 피어 투 피어 복제에서는 피어 투 피어 토폴로지에서 충돌을 검색할 수 있는 옵션을 제공합니다. 이 옵션을 사용하면 일관성 없는 응용 프로그램 동작, 업데이트 손실과 같은 검색되지 않는 충돌로 인해 발생하는 문제를 방지할 수 있습니다. 이 옵션을 설정하면 기본적으로 충돌을 일으키는 변경이 배포 에이전트 오류를 유발하는 치명적 오류로 취급됩니다. 충돌이 발생할 경우 충돌이 해결되고 데이터가 토폴로지 전체에서 일관성을 가질 때까지 토폴로지가 일관성 없는 상태로 유지됩니다.  
  
> [!NOTE]  
>  데이터 불일치의 가능성을 배제하려면 충돌 검색이 설정되어 있는 경우라도 피어 투 피어 토폴로지에서 충돌이 발생하지 않도록 해야 합니다. 특정 행에 대한 쓰기 작업이 하나의 노드에서만 수행되도록 하려면 데이터에 액세스하여 변경하는 응용 프로그램에서 삽입, 업데이트 및 삭제 작업을 분할해야 합니다. 이렇게 분할하면 한 노드에서 발생한 지정된 행에 대한 수정이 다른 노드에서 해당 행을 수정하기 전에 토폴로지의 모든 노드와 동기화됩니다. 응용 프로그램에 정교한 충돌 검색 및 해결 기능이 필요한 경우 병합 복제를 사용하세요. 자세한 내용은 [병합 복제](../../../relational-databases/replication/merge/merge-replication.md) 및 [병합 복제 충돌 감지 및 해결](../../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md)을 참조하세요.  
  
## <a name="understanding-conflicts-and-conflict-detection"></a>충돌 및 충돌 검색 이해  
 단일 데이터베이스에서는 서로 다른 응용 프로그램에 의해 수행된 동일한 행에 대한 변경이 충돌을 일으키지 않습니다. 트랜잭션이 직렬화되고, 동시 변경 처리를 위해 잠금이 사용되기 때문입니다. 피어 투 피어 복제와 같은 비동기 분산형 시스템에서는 트랜잭션이 각 노드에서 독립적으로 활동하며 여러 노드 간에 트랜잭션을 직렬화하는 메커니즘이 없습니다. 2단계 커밋과 같은 프로토콜을 사용할 수 있지만 이 경우 성능이 크게 저하됩니다.  
  
 피어 투 피어 복제와 같은 시스템에서는 개별 피어에서 변경 내용이 커밋될 때 충돌이 검색되지 않습니다. 대신 이러한 변경 내용이 복제되어 다른 피어에 적용될 때 충돌이 검색됩니다. 피어 투 피어 복제에서 충돌은 각 게시된 테이블의 숨겨진 열을 기반으로 각 노드에 변경 내용을 저장하는 저장 프로시저에 의해 검색됩니다. 이 숨겨진 열은 각 노드에 대해 지정되는 *송신자 ID* 와 행의 버전을 결합하는 ID를 저장합니다. 동기화 중에 배포 에이전트는 각 테이블에 대해 프로시저를 실행합니다. 이러한 프로시저는 다른 피어의 삽입, 업데이트 및 삭제 작업을 적용합니다. 숨겨진 열 값을 읽을 때 충돌을 검색하면 프로시저는 다음과 같은 심각도 수준 16의 오류 22815를 일으킵니다.  
  
 `A conflict of type '%s' was detected at peer %d between peer %d (incoming), transaction id %s  and peer %d (on disk), transaction id %s`  
  
 기본적으로 이 오류가 발생하면 배포 에이전트는 노드에 변경 내용을 적용하는 작업을 중지합니다. 검색된 충돌을 처리하는 방법은 이 항목의 뒷부분에 나오는 "충돌 처리"를 참조하세요.  
  
> [!NOTE]  
>  숨겨진 열에는 DAC(관리자 전용 연결)를 통해 로그인한 사용자만 액세스할 수 있습니다. DAC에 대한 자세한 내용은 [데이터베이스 관리자를 위한 진단 연결](../../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)을 참조하세요.  
  
 피어 투 피어 복제는 다음과 같은 충돌 유형을 검색합니다.  
  
-   삽입-삽입  
  
     피어 투 피어 복제에 참여하는 각 테이블의 모든 행은 기본 키 값을 사용하여 고유하게 식별됩니다. 삽입-삽입 충돌은 동일한 키 값을 가진 행이 둘 이상의 노드에 삽입될 때 발생합니다.  
  
-   업데이트-업데이트  
  
     동일한 행이 둘 이상의 노드에서 업데이트될 때 발생합니다.  
  
-   삽입-업데이트  
  
     하나의 노드에서 행이 업데이트되었지만 다른 노드에서 동일한 행이 삭제된 후 다시 삽입되는 경우 발생합니다.  
  
-   삽입-삭제  
  
     하나의 노드에서 행이 삭제되었지만 다른 노드에서 동일한 행이 삭제된 후 다시 삽입된 경우 발생합니다.  
  
-   업데이트-삭제  
  
     하나의 노드에서 행이 업데이트되었지만 다른 노드에서 동일한 행이 삭제된 경우 발생합니다.  
  
-   삭제-삭제  
  
     둘 이상의 노드에서 행이 삭제된 경우 발생합니다.  
  
## <a name="enabling-conflict-detection"></a>충돌 검색 사용  
 충돌 검색을 사용하려면 모든 노드에서 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 이상 버전이 실행되어야 하고 모든 노드에 대해 충돌 검색을 사용하도록 설정되어 있어야 합니다. [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 이상 버전에서는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 충돌 검색이 기본적으로 사용되도록 설정됩니다. 충돌 발생 가능성이 낮은 경우라도 충돌 검색을 사용하도록 설정하는 것이 좋습니다. 충돌 검색은 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 또는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 저장 프로시저를 사용하여 사용하거나 사용하지 않도록 설정할 수 있습니다.  
  
-   [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 게시 속성 **대화 상자의** 구독 옵션 **페이지를 사용하거나 피어 투 피어 토폴로지 구성 마법사의** 토폴로지 구성 **페이지를 사용하여** 에서 충돌 검색을 사용하거나 사용하지 않도록 설정할 수 있습니다. 자세한 내용은 [Conflict Detection in Peer-to-Peer Replication](../../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)을 참조하세요.  
  
     [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]를 사용하여 충돌 검색을 구성하면 충돌이 검색된 경우 변경 내용 적용을 중지하도록 배포 에이전트가 구성됩니다.  
  
-   또한 [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) 또는 [sp_configure_peerconflictdetection](../../../relational-databases/system-stored-procedures/sp-configure-peerconflictdetection-transact-sql.md)저장 프로시저를 이용하여 검색 활성화 및 비활성화도 실행할 수 있습니다.  
  
     저장 프로시저를 사용하여 충돌 검색을 구성하면 충돌이 검색된 경우 배포 에이전트가 변경 내용 적용을 중지할지 여부를 지정할 수 있습니다. 에이전트는 기본적으로 변경 내용 적용을 중지합니다. 기본 설정을 사용하는 것이 좋습니다.  
  
## <a name="handling-conflicts"></a>충돌 처리  
 피어 투 피어 복제에서 충돌이 일어나면 피어 투 피어 충돌 검색 경고가 발생됩니다. 충돌이 발생할 때 알 수 있도록 이 경고를 구성하는 것이 좋습니다. 경고에 대한 자세한 내용은 [복제 에이전트 이벤트에 대한 경고 사용](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)을 참조하세요.  
  
 배포 에이전트가 중단되고 경고가 발생된 후 다음 방법 중 하나를 사용하여 발생한 충돌을 처리하세요.  
  
-   충돌이 검색된 노드를 필요한 데이터가 포함된 노드의 백업에서 다시 초기화합니다(권장되는 방법). 이 방법을 사용하면 데이터 상태의 일관성을 확보할 수 있습니다.  
  
-   배포 에이전트에서 변경 내용 적용을 계속하도록 하여 노드를 다시 동기화합니다.  
  
    1.  @property 매개 변수에 'p2p_continue_onconflict', @value 매개 변수에 **true**를 지정하여 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)을 실행합니다.  
  
    2.  배포 에이전트를 시작합니다.  
  
    3.  충돌 뷰어를 사용하여 충돌이 검색되었는지 확인하고 충돌에 관련된 행, 충돌의 유형 및 충돌 시 우선 적용 사항을 확인합니다. 충돌은 구성 중에 지정된 송신자 ID 값을 기반으로 해결됩니다. 가장 높은 ID의 노드를 출처로 하는 행이 충돌에서 우선 적용됩니다. 자세한 내용은 [트랜잭션 게시의 데이터 충돌 확인&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)을 참조하세요.  
  
    4.  유효성 검사를 실행하여 충돌 행이 올바르게 일치되었는지 확인합니다. 자세한 내용은 [복제된 데이터의 유효성 검사](../../../relational-databases/replication/validate-replicated-data.md)를 참조하세요.  
  
        > [!NOTE]  
        >  이 단계를 수행한 이후에도 데이터에 일관성이 없는 경우에는 우선 순위가 가장 높은 노드의 행을 수동으로 업데이트한 후 이 노드에서 변경 내용이 전파되도록 해야 합니다. 토폴로지에 더 이상 충돌하는 변경 내용이 없으면 모든 노드가 일관적인 상태가 됩니다.  
  
    5.  @property 매개 변수에 'p2p_continue_onconflict', @value 매개 변수에 **false**를 지정하여 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)을 실행합니다.  
  
## <a name="see-also"></a>참고 항목  
 [@loopback_detection](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
