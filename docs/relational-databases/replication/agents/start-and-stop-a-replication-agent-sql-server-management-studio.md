---
title: 복제 에이전트 시작 및 중지(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], stopping
- agents [SQL Server replication], starting
ms.assetid: 97977c4a-8c7c-4a22-9480-69aa812bd1e5
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 339da4b5d9112aa10aa52e12c8a39f6a2adaa30b
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770699"
---
# <a name="start-and-stop-a-replication-agent-sql-server-management-studio"></a>복제 에이전트 시작 및 중지(SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]와 복제 모니터에 있는 **작업** 폴더 및 **복제** 폴더에서 에이전트를 시작하고 중지합니다. 다음 에이전트 및 작업을 시작하고 중지할 수 있습니다.  
  
-   스냅샷 에이전트 - 모든 게시에서 사용  
  
-   로그 판독기 에이전트 - 모든 트랜잭션 게시에서 사용  
  
-   큐 판독기 에이전트 - 지연 업데이트 구독이 활성화된 트랜잭션 게시에서 사용  
  
-   배포 에이전트 - 구독을 트랜잭션 및 스냅샷 게시와 동기화함  
  
-   병합 에이전트 - 구독을 병합 게시와 동기화함  
  
-   복제 유지 관리 작업  
  
 병합 에이전트 및 배포 에이전트를 시작하는 방법은 [밀어넣기 구독 동기화](../../../relational-databases/replication/synchronize-a-push-subscription.md) 및 [끌어오기 구독 동기화](../../../relational-databases/replication/synchronize-a-pull-subscription.md)를 참조하세요. 유지 관리 작업에 대한 자세한 내용은 [복제 유지 관리 작업 실행&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md)을 참조하세요.  
  
 복제 모니터를 시작하는 방법은 [복제 모니터 시작](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)을 참조하세요.  
  
### <a name="to-start-and-stop-a-snapshot-agent-or-log-reader-agent-from-management-studio"></a>Management Studio에서 스냅샷 에이전트 또는 로그 판독기 에이전트를 시작하고 중지하려면  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 게시자에 연결한 다음 해당 서버 노드 및 **복제** 폴더를 확장합니다.  
  
2.  **로컬 게시** 폴더를 확장한 다음 게시를 마우스 오른쪽 단추로 클릭합니다.  
  
3.  **스냅샷 에이전트 상태 보기** 또는 **로그 판독기 에이전트 상태 보기**를 클릭합니다.  
  
4.  **시작** 또는 **중지**를 클릭합니다.  
  
### <a name="to-start-and-stop-a-queue-reader-agent-from-management-studio"></a>Management Studio에서 큐 판독기 에이전트를 시작하고 중지하려면  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 배포자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **SQL Server 에이전트** 폴더를 확장한 다음 **작업** 폴더를 확장합니다.  
  
3.  에이전트에 대한 작업을 마우스 오른쪽 단추로 클릭한 다음 **작업 시작** 또는 **작업 중지**를 클릭합니다. 큐 판독기 에이전트에 대한 작업 이름의 형식은 **[\<배포자>].\<정수>** 입니다.  
  
### <a name="to-start-and-stop-a-snapshot-agent-log-reader-agent-or-queue-reader-agent-from-replication-monitor"></a>복제 모니터에서 스냅샷 에이전트, 로그 판독기 에이전트 또는 큐 판독기 에이전트를 시작하고 중지하려면  
  
1.  왼쪽 창에서 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  **에이전트** 탭을 클릭합니다.  
  
3.  에이전트를 마우스 오른쪽 단추로 클릭한 다음 **에이전트 시작** 또는 **에이전트 중지**를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 모니터링](../../../relational-databases/replication/monitor/monitoring-replication.md)   
 [복제 에이전트 실행 파일 개념](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [Replication Agents Overview](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
