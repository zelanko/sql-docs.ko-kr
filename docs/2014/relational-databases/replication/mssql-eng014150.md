---
title: MSSQL_ENG014150 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014150 error
ms.assetid: c3dd3109-abf3-4b38-a4e9-ef48d0235656
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 032651d75eb4210005765f82adbb4d504ee2a316
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48136823"
---
# <a name="mssqleng014150"></a>MSSQL_ENG014150
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|14150|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|복제-%s: 에이전트 %s이(가) 성공했습니다. %s|  
  
## <a name="explanation"></a>설명  
 이 메시지는 복제 에이전트가 성공적으로 실행되었음을 나타냅니다. 복제는 다음 에이전트를 사용합니다.  
  
-   스냅숏 에이전트 이 에이전트는 모든 게시에서 사용합니다.  
  
-   로그 판독기 에이전트 이 에이전트는 모든 트랜잭션 게시에서 사용합니다.  
  
-   큐 판독기 에이전트 이 에이전트는 지연 업데이트 구독이 활성화된 트랜잭션 게시에서 사용합니다.  
  
-   배포 에이전트 이 에이전트는 구독을 트랜잭션 및 스냅숏 게시와 동기화합니다.  
  
-   병합 에이전트 이 에이전트는 구독을 병합 게시와 동기화합니다.  
  
-   복제 유지 관리 작업  
  
## <a name="user-action"></a>사용자 동작  
 다른 에이전트가 요청 시 또는 예약 시에 실행되는 반면 로그 판독기 에이전트, 큐 판독기 에이전트 및 배포 에이전트는 일반적으로 계속 실행됩니다. 에이전트의 실행을 완료하지 않도록 하려면 에이전트의 상태를 확인하십시오. 자세한 내용은 [Monitor Replication Agents](agents/replication-agents.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [복제 에이전트 관리](agents/replication-agent-administration.md)   
 [오류 및 이벤트 참조&#40;복제&#41;](errors-and-events-reference-replication.md)   
 [복제 배포 에이전트](agents/replication-distribution-agent.md)   
 [복제 로그 판독기 에이전트](agents/replication-log-reader-agent.md)   
 [복제 병합 에이전트](agents/replication-merge-agent.md)   
 [복제 큐 판독기 에이전트](agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](agents/replication-snapshot-agent.md)  
  
  
