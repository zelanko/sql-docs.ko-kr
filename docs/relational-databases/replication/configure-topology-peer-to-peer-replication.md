---
title: "토폴로지 구성(피어 투 피어 복제) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.p2pwizard.peers.f1
ms.assetid: 5377c59f-2e25-4852-a306-c87ae3dca9fd
caps.latest.revision: "29"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ba3f308aaa3e5eea99a7cae23630c8462414a1fb
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="configure-topology-peer-to-peer-replication"></a>토폴로지 구성(피어 투 피어 복제)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] **토폴로지 구성** 페이지를 사용하여 새 노드 추가, 노드 삭제, 기존 노드 간 새 연결 추가와 같은 일반적인 구성 태스크를 수행할 수 있습니다. 이 마법사의 **게시** 페이지에서 선택한 노드는 디자인 화면에 표시됩니다. 구성 옵션을 지정하려면 노드, 연결 또는 디자인 화면을 마우스 오른쪽 단추로 클릭합니다.  
  
> [!NOTE]  
>  피어 투 피어 토폴로지 구성 마법사는 닫힐 때 토폴로지 정보를 요청합니다. 모든 노드가 이 정보 요청에 응답하기 전에 마법사가 닫혔다가 다시 열리면 마법사에 부분 네트워크가 표시될 수 있습니다.  
  
## <a name="options"></a>변수  
 **토폴로지 구성** 페이지에는 여러 가지 인터페이스 요소와 요소를 마우스 오른쪽 단추로 클릭하면 사용할 수 있는 옵션이 포함되어 있습니다. 다음 표에서는 각 인터페이스 요소에 대해 설명합니다.  
  
|인터페이스 요소|Description|  
|-----------------------|-----------------|  
|디자인 화면|다른 인터페이스 요소가 표시됩니다. 요소를 추가하려면 디자인 화면을 마우스 오른쪽 단추로 클릭합니다.|  
|![토폴로지의 첫 번째 노드](../../relational-databases/replication/media/p2pwizard-firstnode.gif "토폴로지의 첫 번째 노드")|토폴로지의 원래 노드입니다. 새 노드는 원래 노드의 게시 데이터베이스 복사본을 사용하여 초기화됩니다.|  
|![완전한 정보가 있는 노드](../../relational-databases/replication/media/p2pwizard-complete.gif "완전한 정보가 있는 노드")|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전의 인스턴스를 실행하는 노드로서, 복제 기능에서는 이 노드에 대한 완전한 정보를 갖고 있습니다. 구성 옵션을 지정하려면 노드를 마우스 오른쪽 단추로 클릭합니다.|  
|![불완전한 정보가 있는 노드](../../relational-databases/replication/media/p2pwizard-incomplete.gif "불완전한 정보가 있는 노드")|복제 기능에서 완전하지 않은 정보를 갖고 있는 노드입니다. 구성 옵션을 지정하려면 노드를 마우스 오른쪽 단추로 클릭합니다.<br /><br /> 다음과 같은 경우 복제 기능에서 완전하지 않은 정보를 갖게 됩니다.<br /><br /> -노드에서 마법사에 필요한 메타데이터 중 일부를 저장하지 않는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]의 인스턴스를 실행하는 경우.<br /><br /> -노드에서 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하고 있지만 복제 기능에서 해당 노드의 구독 정보를 검색할 수 없는 경우. 이러한 상황에서 문제를 해결하려면 다음을 수행합니다.<br /><br /> 노드의 데이터베이스가 온라인 상태인지, 또한 노드에 연결된 배포 에이전트와 동일한 자격 증명을 사용하여 해당 데이터베이스에 연결할 수 있는지 확인합니다.<br /><br /> 노드에 연결된 로그 판독기 에이전트와 모든 배포 에이전트가 실행 중인지 확인합니다.<br /><br /> 새로 고침 제한 시간이 모든 토폴로지 정보를 수집할 수 있도록 충분히 높게 설정되어 있는지 확인합니다. 제한 시간을 설정하려면 디자인 화면을 마우스 오른쪽 단추로 클릭하고 **새로 고침 제한 시간 설정**을 클릭합니다.|  
|화살표가 있는 회색 선|두 노드 사이의 연결입니다. 연결을 추가하려면 연결할 노드 중 하나를 마우스 오른쪽 단추로 클릭합니다. 연결을 제거하려면 연결을 마우스 오른쪽 단추로 클릭합니다.<br /><br /> 선에 화살표가 하나만 있는 경우 복제 기능에서 노드 중 하나에 대해 완전하지 않은 정보를 갖고 있는 것입니다.|  
  
### <a name="options-for-the-design-surface"></a>디자인 화면에서 사용할 수 있는 옵션  
 **그래프 다시 그리기**  
 디자인 화면에서 토폴로지를 새로 고치지 않고 개체를 다시 그립니다. 개체를 다시 그리면 토폴로지가 보다 잘 표시될 수 있습니다.  
  
 **토폴로지 새로 고침**  
 토폴로지의 각 노드를 쿼리하고 각 노드에 대한 업데이트된 정보를 표시합니다. 노드가 여러 개인 경우 이 프로세스에는 몇 분 정도 소요될 수 있습니다.  
  
 마법사에서 토폴로지 정보를 요청하는 경우 모든 노드가 요청에 응답하기 전에 마법사를 닫았다가 다시 열면 이 페이지에 토폴로지의 노드가 모두 표시되지 않을 수 있습니다.  
  
 **새 피어 노드 추가**  
 피어 투 피어 토폴로지에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스를 추가합니다. 인스턴스를 노드로 추가하면 마법사가 완료된 후 해당 인스턴스에 게시가 만들어집니다. 노드를 추가한 후 해당 노드를 마우스 오른쪽 단추로 클릭하여 새 노드와 기존 노드 사이의 연결을 추가합니다.  
  
 피어 투 피어 토폴로지에 참가하려면 인스턴스가 다음 요구 사항을 충족해야 합니다.  
  
-   인스턴스가 이미 배포자로 구성되어 있거나 원격 배포자와 연결되어 있어야 합니다.  
  
-   인스턴스에 복제에 관련된 데이터베이스의 복사본이 들어 있어야 합니다. 이 복사본은 대개 원래 게시 데이터베이스의 복원된 백업입니다.  
  
 **표시할 노드 선택**  
 디자인 화면에 표시할 노드를 선택합니다. 이 옵션은 토폴로지에 많은 수의 노드가 있는 경우에 유용합니다. 디자인 화면에 표시되는 노드 사이에만 연결을 추가할 수 있습니다.  
  
 **새로 고침 제한 시간 설정**  
 작업 제한 시간이 초과될 때까지 새로 고침 프로세스를 실행할 수 있는 시간을 지정합니다.  
  
### <a name="options-for-each-node"></a>각 노드에 대해 사용할 수 있는 옵션  
 **새 피어 연결 추가**  
 두 노드 사이에 연결을 추가합니다. 예를 들어 노드 A와 노드 B 사이의 연결을 추가하는 경우 복제 과정에서 두 개의 구독이 추가되는데 첫 번째는 노드 A에서 노드 B의 게시 변경 내용을 받는 데 사용되는 구독이고, 두 번째는 노드 B에서 노드 A의 게시 변경 내용을 받는 데 사용되는 구독입니다.  
  
 **피어 노드 삭제**  
 토폴로지에서 노드를 제거합니다. 예를 들어 노드 C를 제거하면 해당 노드에 있는 게시도 제거됩니다. 이 경우 노드 A와 노드 C 간의 구독 및 노드 B와 노드 C 간의 구독도 제거됩니다. 노드 C의 데이터베이스는 삭제되지 않으며 게시 및 배포를 계속 사용할 수 있습니다.  
  
> [!NOTE]  
>  피어 투 피어 복제를 구성할 때는 각 노드에 대해 ID를 지정합니다. 이 ID는 토폴로지 내의 모든 노드에서 고유해야 하며 [MSpeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) 시스템 테이블의 originator_id 열에 저장됩니다. 노드가 토폴로지에서 제거되어도 ID는 기록 테이블에 계속 보관됩니다. ID를 보관하는 이유는 토폴로지에 있는 제거된 노드의 복제본이 변경될 경우 잘못된 충돌이 발생하는 것을 방지하기 위한 것입니다. 기존 ID를 새 노드에 다시 사용하려면 먼저 모든 노드의 MSpeer_originatorid_history 테이블에서 해당 ID를 수동으로 삭제해야 합니다. 노드의 ID를 제거하기 전에 [sp_requestpeerresponse](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) 를 실행하여 해당 노드에서 수행된 모든 변경 내용이 복제되었는지 확인하십시오.  
  
 **표시된 모든 노드에 연결**  
 선택한 노드와 다른 모든 노드 간의 연결을 추가합니다. 예를 들어 3개의 노드가 있는 토폴로지에서 노드 C에 대해 이 옵션을 선택한 경우 복제 과정에서 네 개의 구독이 추가됩니다. 두 개의 구독은 노드 A 및 노드 B에서 노드 C의 게시 변경 내용을 받는 데 사용되고, 다른 두 개의 구독은 노드 C에서 노드 A 및 노드 B의 게시 변경 내용을 받는 데 사용됩니다.  
  
 **표시할 노드 선택**  
 디자인 화면에 표시할 노드를 선택합니다. 이 옵션은 토폴로지에 많은 수의 노드가 있는 경우에 유용합니다. 디자인 화면에 표시되는 노드 사이에만 연결을 추가할 수 있습니다.  
  
### <a name="options-for-the-connection-arrows"></a>연결 화살표에 사용할 수 있는 옵션  
 **피어 연결 제거**  
 두 노드 사이의 연결을 제거합니다. 예를 들어 노드 A와 노드 B 사이의 연결을 제거하면 복제 과정에서 두 개의 구독이 삭제되는데 그 중 하나는 노드 A에서 노드 B의 게시 변경 내용을 받는 데 사용되는 구독이고, 다른 하나는 노드 B에서 노드 A의 게시 변경 내용을 받는 데 사용되는 구독입니다.  
  
## <a name="see-also"></a>참고 항목  
 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [피어 투 피어 토폴로지 관리&#40;복제 Transact-SQL 프로그래밍&#41;](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [@loopback_detection](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
