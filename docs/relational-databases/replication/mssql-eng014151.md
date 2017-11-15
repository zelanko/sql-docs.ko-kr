---
title: "MSSQL_ENG014151 | Microsoft 문서"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: MSSQL_ENG014151 error
ms.assetid: 54b45e70-46b3-4c7a-a5bf-06f6dd028ceb
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b6ff7b1cd07bfb91ab44ced875fc321c7b9ae34b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqleng014151"></a>MSSQL_ENG014151
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|14151|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|복제-%s: 에이전트 %s이(가) 실패했습니다. %s|  
  
## <a name="explanation"></a>설명  
 이 오류는 복제 에이전트 실패 시 발생합니다. 메시지 끝의 텍스트는 실패 컨텍스트에 따라 달라집니다.  
  
## <a name="user-action"></a>사용자 동작  
 여러 상황에서 이러한 오류가 발생할 수 있으므로 필요에 따라 다음 방법을 사용합니다.  
  
-   실패한 에이전트가 이제 실패 없이 실행되는지 알아보려면 해당 에이전트를 다시 시작합니다. 자세한 내용은 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 및 [복제 에이전트 실행 파일 개념](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)을 참조하세요.  
  
-   에이전트 기록과 작업 기록에서 같은 시간대에 발생한 다른 오류를 확인합니다. 복제 모니터에서 에이전트 상태 및 오류 정보를 보는 방법은 다음 항목을 참조하십시오.  
  
    -   스냅숏 에이전트, 로그 판독기 에이전트 및 큐 판독기 에이전트에 대해서는 [게시 관련 에이전트에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md)을 참조하세요.  
  
    -   배포 에이전트 및 병합 에이전트에 대해서는 [구독 관련 에이전트에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)을 참조하세요.  
  
-   에이전트에서 액세스하는 컴퓨터 사이에 기본 연결이 제대로 작동하는지 확인한 다음 [sqlcmd Utility](../../tools/sqlcmd-utility.md)와 같은 유틸리티를 사용하여 각 컴퓨터에 연결합니다. 각 컴퓨터에 연결할 때는 에이전트 연결 시 사용하는 계정과 같은 계정을 사용합니다. 각 에이전트 계정에 필요한 사용 권한에 대한 자세한 내용은 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하십시오.  
  
-   스냅숏을 만들거나 적용하는 동안 오류가 발생하면 스냅숏 디렉터리의 파일에서 오류를 확인합니다.  
  
-   오류가 계속 발생하면 에이전트의 로깅을 늘리고 해당 로그의 출력 파일을 지정하십시오. 오류의 컨텍스트에 따라 이러한 작업을 수행하면 오류 및/또는 추가 오류 메시지가 발생할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 에이전트 관리](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [오류 및 이벤트 참조&#40;복제&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [복제 배포 에이전트](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [복제 로그 판독기 에이전트](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [복제 병합 에이전트](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [복제 큐 판독기 에이전트](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  
