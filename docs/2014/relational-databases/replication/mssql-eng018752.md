---
title: MSSQL_ENG018752 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG018752 error
ms.assetid: 405b2655-acb4-4e15-bcc6-b8f86bb22b37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0558ded6ed10284df39270ddeca9d92434daf40e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63057546"
---
# <a name="mssqleng018752"></a>MSSQL_ENG018752
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|18752|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|한 번에 하나의 로그 판독기 에이전트 또는 로그 관련 프로시저(sp_repldone, sp_replcmds 및 sp_replshowcmds)만 데이터베이스에 연결할 수 있습니다. 로그 관련 프로시저를 실행한 경우 로그 판독기 에이전트를 시작하거나 다른 로그 관련 프로시저를 실행하기 전에 프로시저가 실행된 연결을 삭제하거나 해당 연결에 대해 sp_replflush를 실행하십시오.|  
  
## <a name="explanation"></a>설명  
 현재 둘 이상의 연결에서 **sp_repldone**, **sp_replcmds**또는 **sp_replshowcmds**중 하나를 실행하려고 합니다. 저장 프로시저 [sp_repldone&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-repldone-transact-sql) 및 [sp_replcmds&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replcmds-transact-sql)는 게시된 데이터베이스에 복제된 트랜잭션에 대한 정보를 찾아 업데이트하기 위해 로그 판독기 에이전트에서 사용하는 저장 프로시저입니다. 저장 프로시저 [sp_replshowcmds&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql)는 트랜잭션 복제와 관련된 특정 문제를 해결하는 데 사용됩니다.  
  
 이 오류는 다음과 같은 경우에 발생합니다.  
  
-   게시된 데이터베이스에 대해 로그 판독기 에이전트가 실행 중인데 두 번째 로그 판독기 에이전트가 같은 데이터베이스를 실행하려고 할 경우 두 번째 에이전트에 대해 오류가 발생하고 에이전트 기록에 표시됩니다.  
  
     에이전트가 여러 개인 것으로 표시되는 경우 해당 에이전트 중 하나는 분리된 프로세스의 결과일 수 있습니다.  
  
-   게시된 데이터베이스에 대해 로그 판독기 에이전트가 시작되었는데 사용자가 같은 데이터베이스에 대해 **sp_repldone**, **sp_replcmds**또는 **sp_replshowcmds** 를 실행할 경우 저장 프로시저가 실행된 애플리케이션(예: **sqlcmd**)에서 오류가 발생합니다.  
  
-   게시된 데이터베이스에 대해 실행 중인 로그 판독기 에이전트가 없는 상태에서 사용자가 **sp_repldone**, **sp_replcmds**또는 **sp_replshowcmds** 를 실행한 다음 프로시저가 실행된 연결을 닫지 않을 경우 로그 판독기 에이전트가 데이터베이스에 연결을 시도하면 오류가 발생합니다.  
  
## <a name="user-action"></a>사용자 동작  
 다음 단계를 수행하면 문제를 해결하는 데 도움이 됩니다. 다음 단계를 수행하는 중 로그 판독기 에이전트가 오류 없이 시작되면 나머지 단계를 완료할 필요가 없습니다.  
  
-   로그 판독기 에이전트의 기록에서 이 오류의 원인이 될 수 있는 다른 오류가 있는지 확인합니다. 복제 모니터에서 에이전트 상태 및 오류 정보를 보는 방법에 대한 자세한 내용은 [복제 모니터를 사용하여 정보 보기 및 작업 수행](monitor/view-information-and-perform-tasks-replication-monitor.md)을 참조하세요.  
  
-   [sp_who&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-who-transact-sql)의 출력에서 게시된 데이터베이스에 연결된 특정 프로세스 ID 번호(SPID)를 확인합니다. **sp_repldone**, **sp_replcmds**또는 **sp_replshowcmds**를 실행했을 가능성이 있는 연결을 모두 닫습니다.  
  
-   로그 판독기 에이전트를 다시 시작합니다. 자세한 내용은 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)를 참조하세요.  
  
-   배포자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스를 다시 시작(클러스터에서 오프라인 또는 온라인 상태로 만듦)합니다. 예약된 작업이 다른 **인스턴스에서**sp_repldone **,** sp_replcmds **또는** sp_replshowcmds [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 실행했을 가능성이 있는 경우 해당 인스턴스에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트도 다시 시작합니다. 자세한 내용은 [SQL Server 에이전트 서비스 시작, 중지 또는 일시 중지](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)를 참조하세요.  
  
-   게시 데이터베이스의 게시자에서 [sp_replflush&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replflush-transact-sql)를 실행한 다음 로그 판독기 에이전트를 다시 시작합니다.  
  
-   오류가 계속 발생하면 에이전트의 로깅을 늘리고 해당 로그의 출력 파일을 지정하십시오. 오류의 컨텍스트에 따라 이러한 작업을 수행하면 오류 및/또는 추가 오류 메시지가 발생할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](errors-and-events-reference-replication.md)   
 [복제 로그 판독기 에이전트](agents/replication-log-reader-agent.md)  
  
  
