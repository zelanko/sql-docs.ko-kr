---
title: "MSSQL_ENG018752 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG018752 오류"
ms.assetid: 405b2655-acb4-4e15-bcc6-b8f86bb22b37
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# MSSQL_ENG018752
    
## 메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|18752|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|한 번에 하나의 로그 판독기 에이전트 또는 로그 관련 프로시저(sp_repldone, sp_replcmds 및 sp_replshowcmds)만 데이터베이스에 연결할 수 있습니다. 로그 관련 프로시저를 실행한 경우 로그 판독기 에이전트를 시작하거나 다른 로그 관련 프로시저를 실행하기 전에 프로시저가 실행된 연결을 삭제하거나 해당 연결에 대해 sp_replflush를 실행하십시오.|  
  
## 설명  
 하나 이상의 현재 연결이 다음을 실행 하려고: **sp_repldone**, **sp_replcmds**, 또는 **sp_replshowcmds**합니다. 저장된 프로시저 [sp_repldone (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md) 및 [sp_replcmds (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) 저장된 프로시저는 로그 판독기 에이전트에서 검색 하 고 게시 된 데이터베이스에서 복제 된 트랜잭션에 대 한 정보를 업데이트 합니다. 저장된 프로시저 [sp_replshowcmds (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md) 특정 유형의 트랜잭션 복제와 관련 문제를 해결 하는 데 사용 됩니다.  
  
 이 오류는 다음과 같은 경우에 발생합니다.  
  
-   게시된 데이터베이스에 대해 로그 판독기 에이전트가 실행 중인데 두 번째 로그 판독기 에이전트가 같은 데이터베이스를 실행하려고 할 경우 두 번째 에이전트에 대해 오류가 발생하고 에이전트 기록에 표시됩니다.  
  
     에이전트가 여러 개인 것으로 표시되는 경우 해당 에이전트 중 하나는 분리된 프로세스의 결과일 수 있습니다.  
  
-   게시 된 데이터베이스에 대 한 로그 판독기 에이전트를 시작 하 고 사용자를 실행 하는 경우 **sp_repldone**, **sp_replcmds**, 또는 **sp_replshowcmds** 오류는 저장된 프로시저를 실행 하는 위치는 응용 프로그램에서 발생 하는 동일한 데이터베이스에 대해 (예: **sqlcmd**).  
  
-   게시 된 데이터베이스에 대 한 로그 판독기 에이전트가 없으며 실행 되 고 사용자를 실행 하는 경우 **sp_repldone**, **sp_replcmds**, 또는 **sp_replshowcmds** 및 다음 닫지 않을는 프로시저가 실행 된, 연결 오류는 로그 판독기 에이전트가 데이터베이스에 연결 하려고 할 때 발생 합니다.  
  
## 사용자 동작  
 다음 단계를 수행하면 문제를 해결하는 데 도움이 됩니다. 다음 단계를 수행하는 중 로그 판독기 에이전트가 오류 없이 시작되면 나머지 단계를 완료할 필요가 없습니다.  
  
-   로그 판독기 에이전트의 기록에서 이 오류의 원인이 될 수 있는 다른 오류가 있는지 확인합니다. 복제 모니터에서 에이전트 상태 및 오류 정보를 보는 방법에 대 한 정보를 참조 하십시오. [정보 보기 및 에이전트 관련 된는 게시 및 #40;에 대 한 작업 수행 복제 모니터 & #41;](../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md)합니다.  
  
-   출력을 확인 [sp_who (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) 특정 프로세스 id 번호 (Spid)에 대 한 게시 된 데이터베이스에 연결 된입니다. 실행 했을 가능성이 있는 연결을 닫습니다 **sp_repldone**, **sp_replcmds**, 또는 **sp_replshowcmds**합니다.  
  
-   로그 판독기 에이전트를 다시 시작합니다. 자세한 내용은 참조 [시작 및 중지 복제 에이전트 & #40; SQL Server Management Studio & #41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)합니다.  
  
-   배포자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스를 다시 시작(클러스터에서 오프라인 또는 온라인 상태로 만듦)합니다. 예약 된 작업을 실행할 수 있는 가능성이 있는 경우 **sp_repldone**, **sp_replcmds**, 또는 **sp_replshowcmds** 에서 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 다시 시작은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 해당 인스턴스에 대 한 에이전트입니다. 자세한 내용은 참조 [시작, 중지 또는 SQL Server 에이전트 서비스를 일시 중지](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)합니다.  
  
-   실행 [sp_replflush (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md) 게시자의 게시 데이터베이스를 다시 시작한 후 로그 판독기 에이전트에서.  
  
-   오류가 계속 발생하면 에이전트의 로깅을 늘리고 해당 로그의 출력 파일을 지정하십시오. 오류의 컨텍스트에 따라 이러한 작업을 수행하면 오류 및/또는 추가 오류 메시지가 발생할 수 있습니다.  
  
## 참고 항목  
 [오류 및 이벤트 참조 & #40입니다. 복제 및 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [복제 로그 판독기 에이전트](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
  